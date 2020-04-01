---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: De verzoekverwerking van de privacy in Real-time Profiel van de Klant
topic: overview
translation-type: tm+mt
source-git-commit: 5f0e0deb4a2fae636ac4d2313a6541c25309c294

---


# De verzoekverwerking van de privacy in Real-time Profiel van de Klant

De privacydienst van het Platform van de Privacy van Adobe verwerkt klantenverzoeken om tot toegang te hebben, uit verkoop te kiezen, of hun persoonlijke gegevens te schrappen zoals die door privacyverordeningen zoals de Algemene Verordening van de Bescherming van Gegevens (GDPR) en de Wet van de Consumeprivacydienst van Californië (CCPA) worden afgebakend.

Dit document behandelt essentiële concepten met betrekking tot de verwerking van privacyverzoeken voor Real-time Klantprofiel.

## Aan de slag

U wordt aangeraden een goed begrip te hebben van de volgende services van het Experience Platform voordat u deze handleiding leest:

* [Privacy-service](home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, niet te verkopen of te verwijderen.
* [Identiteitsservice](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [Klantprofiel](../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform Identity Service biedt een brug tussen identiteitsgegevens van klanten op verschillende systemen en apparaten. De Dienst van de identiteit gebruikt **identiteitsnaamruimten** om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;E-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over identiteitsnaamruimten in het Platform van de Ervaring, zie het overzicht [van](../identity-service/namespaces.md)identiteitsnamespace.

## Verzoeken indienen {#submit}

>[!NOTE] Deze sectie behandelt hoe te om privacyverzoeken voor het meer van Gegevens te formatteren. Het wordt ten zeerste aanbevolen dat u de API [-documentatie](../privacy-service/api/getting-started.md) van de [privacyservice of de gebruikersinterface](../privacy-service/ui/overview.md) van deprivacyservice controleert voor volledige stappen over het verzenden van een privacytaak, waaronder het correct indelen van verzonden identiteitsgegevens van gebruikers in aanvragen.

In de volgende sectie wordt beschreven hoe u privacyverzoeken voor Real-time klantprofiel en het Data Lake kunt indienen met behulp van de Privacy Service API of UI.

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle beschikbare bestanden een specifieke `userIDs` en `namespace` `type` afhankelijk van de gegevensopslag gebruiken waarop ze van toepassing zijn. Id&#39;s voor het profielarchief moeten &#39;standard&#39; of &#39;custom&#39; gebruiken voor hun `type` waarde en een geldige [naamruimte](#namespaces) voor identiteit die door Identity Service wordt herkend voor hun `namespace` waarde.


Bovendien moet de `include` array van de aanvraaglading de productwaarden voor de verschillende gegevensopslag bevatten het verzoek wordt ingediend. Bij het indienen van aanvragen voor het Data Lake moet de array de waarde &quot;ProfileService&quot; bevatten.

Met de volgende aanvraag wordt een nieuwe privacytaak gemaakt voor zowel Real-time klantprofiel, waarbij de standaardnaamruimte &quot;E-mail&quot; wordt gebruikt. Het omvat ook de productwaarde voor Profiel in de `include` serie:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
    "companyContexts": [
      {
        "namespace": "imsOrgID",
        "value": "{IMS_ORG}"
      }
    ],
    "users": [
      {
        "key": "user12345",
        "action": ["access","delete"],
        "userIDs": [
          {
            "namespace": "Email",
            "value": "ajones@acme.com",
            "type": "standard"
          },
          {
            "namespace": "email_label",
            "value": "ajones@acme.com",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService", "aepDataLake"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### De gebruikersinterface gebruiken

Wanneer het creëren van baanverzoeken in UI, ben zeker om **AEP Gegevensmeer** en/of **Profiel** onder _Producten_ te selecteren om banen voor gegevens te verwerken die in het meer van Gegevens of in real time het Profiel van de Klant worden opgeslagen.

<img src="images/privacy/product-value.png" width="450"><br>

## Verzoek om verwerking verwijderen

Wanneer het Platform van de Ervaring een schrappingsverzoek van de Dienst van de Privacy ontvangt, verzendt het Platform bevestiging aan de Dienst van de Privacy dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn gemaakt. De records worden vervolgens binnen zeven dagen uit het Data Lake- of Profile-archief verwijderd. Tijdens dat venster van zeven dagen, worden de gegevens zachte geschrapt en daarom niet toegankelijk door om het even welke dienst van het Platform.

In toekomstige releases zal Platform een bevestiging sturen naar de Privacy Service nadat de gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijke concepten betrokken bij de verwerking van privacyverzoeken in het Platform van de Ervaring. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Zie het document over de verwerking van [privacyverzoeken in het Datameer](../catalog/privacy.md)voor informatie over het verwerken van privacyverzoeken voor platformbronnen die niet worden gebruikt door het profiel.