---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: De verzoekverwerking van de privacy in Real-time Profiel van de Klant
topic: overview
translation-type: tm+mt
source-git-commit: 397f08efa276f7885e099a0a8d9dc6d23fe0e8cc
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# Behandeling van privacyverzoek in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang, om te weigeren of om hun persoonsgegevens te verwijderen zoals die zijn omschreven in privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR) en [!DNL California Consumer Privacy Act] (CCPA).

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor [!DNL Real-time Customer Profile].

## Aan de slag

U wordt aangeraden de volgende [!DNL Experience Platform] services goed te begrijpen voordat u deze handleiding leest:

* [[!DNL-Privacy Service]](home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-time klantprofiel]](../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op systemen en apparaten. [!DNL Identity Service] gebruikt **naamruimten** om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Zie het overzicht [!DNL Experience Platform]van naamruimte voor [identiteiten in voor meer informatie over naamruimten in naamruimten](../identity-service/namespaces.md).

## Verzoeken indienen {#submit}

>[!NOTE]
>
>In deze sectie wordt beschreven hoe u privacyverzoeken voor de [!DNL Profile] gegevensopslag kunt maken. Het wordt ten zeerste aanbevolen de API [-](../privacy-service/api/getting-started.md) Privacy Service of de [Privacy Service-UI](../privacy-service/ui/overview.md) -documentatie te raadplegen voor volledige stappen over het verzenden van een privacytaak, waaronder het correct indelen van verzonden identiteitsgegevens van gebruikers in aanvragen.

In de volgende sectie wordt beschreven hoe u privacyaanvragen kunt indienen voor [!DNL Real-time Customer Profile] en de API of UI [!DNL Data Lake] [!DNL Privacy Service] kunt gebruiken.

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle beschikbare bestanden een specifieke `userIDs` en `namespace` `type` afhankelijk van de gegevensopslag gebruiken waarop ze van toepassing zijn. Id&#39;s voor de [!DNL Profile] winkel moeten &#39;standard&#39; of &#39;custom&#39; gebruiken voor hun `type` waarde, en een geldige [naamruimte](#namespaces) voor identiteit wordt door [!DNL Identity Service] herkend voor hun `namespace` waarde.


Bovendien moet de `include` array van de aanvraaglading de productwaarden voor de verschillende gegevensopslag bevatten het verzoek wordt ingediend. Wanneer u een aanvraag naar de array indient, moet de array de waarde &quot;ProfileService&quot; bevatten. [!DNL Data Lake]

Met de volgende aanvraag wordt een nieuwe privacytaak voor beide gemaakt [!DNL Real-time Customer Profile], waarbij de standaardnaamruimte E-mail wordt gebruikt. Het omvat ook de productwaarde voor [!DNL Profile] in de `include` serie:

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

Wanneer het creëren van baanverzoeken in UI, ben zeker om **[!UICONTROL AEP Gegevensmeer]** en/of **[!UICONTROL Profiel]** onder **[!UICONTROL Producten]** te selecteren om banen voor gegevens te verwerken die in [!DNL Data Lake] of [!DNL Real-time Customer Profile], respectievelijk worden opgeslagen.

<img src="images/privacy/product-value.png" width="450"><br>

## Verzoek om verwerking verwijderen

Wanneer [!DNL Experience Platform] een verwijderingsverzoek van [!DNL Privacy Service]ontvangt, [!DNL Platform] verzendt bevestiging aan [!DNL Privacy Service] dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn. De records worden vervolgens binnen zeven dagen uit de [!DNL Data Lake] winkel of de [!DNL Profile] opslagplaats verwijderd. Tijdens dat venster van zeven dagen, worden de gegevens zachte geschrapt en daarom niet toegankelijk door om het even welke [!DNL Platform] dienst.

In toekomstige versies [!DNL Platform] wordt een bevestiging verzonden naar [!DNL Privacy Service] nadat gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijke concepten betrokken bij de verwerking van privacyverzoeken in [!DNL Experience Platform]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Voor informatie over het verwerken van privacyverzoeken voor [!DNL Platform] middelen die niet door worden gebruikt, zie het document over [!DNL Profile]privacyaanvraagverwerking in het meer [](../catalog/privacy.md)van Gegevens.