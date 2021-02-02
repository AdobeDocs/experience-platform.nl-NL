---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Privacy-aanvraagverwerking in realtime-klantprofiel
topic: overview
type: Documentation
description: Adobe Experience Platform Privacy Service verwerkt verzoeken van klanten om toegang te krijgen, te weigeren of hun persoonlijke gegevens te verwijderen, zoals gedefinieerd in een groot aantal privacyregels. Dit document behandelt essentiële concepten met betrekking tot de verwerking van privacyverzoeken voor Real-time Klantprofiel.
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 0%

---


# De verzoekverwerking van de privacy in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang tot hun persoonsgegevens, om te weigeren deze te verkopen of om hun persoonsgegevens te verwijderen, zoals gedefinieerd in privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR) en [!DNL California Consumer Privacy Act] (CCPA).

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor [!DNL Real-time Customer Profile].

## Aan de slag

U wordt aangeraden de volgende [!DNL Experience Platform]-services goed te begrijpen voordat u deze handleiding leest:

* [[!DNL Privacy Service]](home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op verschillende systemen en apparaten. [!DNL Identity Service] gebruikt  **identity** namespacesto om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Voor meer informatie over identiteitsnaamruimten in [!DNL Experience Platform], zie [identity namespace overzicht](../identity-service/namespaces.md).

## Verzoeken {#submit} verzenden

In de onderstaande secties wordt beschreven hoe u met de API of UI van [!DNL Privacy Service] privacyverzoeken voor [!DNL Real-time Customer Profile] kunt indienen. Voordat u deze secties leest, wordt u ten zeerste aangeraden de [Privacy Service-API](../privacy-service/api/getting-started.md) of [Privacy Service-UI](../privacy-service/ui/overview.md) documentatie te controleren voor volledige stappen voor het verzenden van een privacytaak, waaronder het correct indelen van verzonden identiteitsgegevens van gebruikers in aanvraagladingen.

>[!IMPORTANT]
>
>Privacy Service kan alleen [!DNL Profile] gegevens verwerken met behulp van een samenvoegbeleid dat geen identiteitsstitching uitvoert. Als u UI gebruikt om te bevestigen of uw privacyverzoeken worden verwerkt, zorg ervoor dat u een beleid met &quot;[!DNL None]&quot;als zijn [!UICONTROL ID stitching] type gebruikt. Met andere woorden, u kunt geen samenvoegbeleid gebruiken waarbij [!UICONTROL ID stitching] aan &quot;[!UICONTROL Private graph]&quot;wordt geplaatst.
>
>![](./images/privacy/no-id-stitch.png)
>
>Het is ook belangrijk om op te merken dat de hoeveelheid tijd die een privacyverzoek kan duren om te voltooien niet kan worden gewaarborgd. Als er wijzigingen optreden in uw [!DNL Profile]-gegevens terwijl een aanvraag nog wordt verwerkt, kan niet worden gegarandeerd of deze records al dan niet worden verwerkt.

### De API gebruiken

Bij het maken van taakaanvragen in de API moeten alle id&#39;s in `userIDs` een specifieke `namespace` en `type` gebruiken. Een geldige [identity namespace](#namespaces) die door [!DNL Identity Service] wordt erkend moet voor de `namespace` waarde worden verstrekt, terwijl `type` of `unregistered` (voor standaard en douanenamespaces, respectievelijk) moet zijn.`standard`

>[!NOTE]
>
>Afhankelijk van de identiteitsgrafiek en de manier waarop uw profielfragmenten in gegevenssets van Platforms worden gedistribueerd, moet u mogelijk meer dan één id opgeven voor elke klant. Zie de volgende sectie [profielfragmenten](#fragments) voor meer informatie.

Daarnaast moet de `include`-array van de payload van het verzoek de productwaarden voor de verschillende gegevensopslagruimten bevatten waarop het verzoek wordt uitgevoerd. Bij het indienen van aanvragen bij de [!DNL Data Lake] moet de array de waarde &quot;ProfileService&quot; bevatten.

Het volgende verzoek leidt tot een nieuwe privacybaan voor de gegevens van één enkele klant in [!DNL Profile] opslag. Voor de klant worden twee identiteitswaarden opgegeven in de `userIDs`-array. een met de standaardnaamruimte `Email` en de andere met een aangepaste naamruimte `Customer_ID`. Het omvat ook de productwaarde voor [!DNL Profile] (`ProfileService`) in `include` serie:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/privacy/jobs \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
            "namespace": "Customer_ID",
            "value": "12345678",
            "type": "unregistered"
          }
        ]
      }
    ],
    "include": ["ProfileService"],
    "expandIds": false,
    "priority": "normal",
    "analyticsDeleteMethod": "anonymize",
    "regulation": "ccpa"
}'
```

### De gebruikersinterface gebruiken

Als u taakaanvragen maakt in de gebruikersinterface, moet u **[!UICONTROL AEP-gegevensmeer]** en/of **[!UICONTROL Profiel]** selecteren onder **[!UICONTROL Producten]** om taken te verwerken voor gegevens die zijn opgeslagen in respectievelijk [!DNL Data Lake] of [!DNL Real-time Customer Profile].

<img src="images/privacy/product-value.png" width="450"><br>

## Profielfragmenten in privacyverzoeken {#fragments}

In de [!DNL Profile] gegevensopslag, zullen de persoonlijke gegevens voor een individuele klant vaak van veelvoudige profielfragmenten bestaan, die met de persoon door de identiteitsgrafiek worden geassocieerd. Wanneer u een privacyverzoek indient bij de [!DNL Profile]-winkel, is het belangrijk om te weten dat aanvragen alleen op profielfragmentniveau worden verwerkt in plaats van op het volledige profiel.

Bijvoorbeeld, overweeg een situatie waar u de gegevens van de klantenattributen in drie afzonderlijke datasets opslaat, die verschillende herkenningstekens gebruiken om die gegevens met individuele klanten te associëren:

| Naam gegevensset | Primair identiteitsveld | Opgeslagen kenmerken |
| --- | --- | --- |
| Dataset 1 | `customer_id` | `address` |
| Gegevensset 2 | `email_id` | `firstName`, `lastName` |
| Gegevensset 3 | `email_id` | `mlScore` |

Een van de gegevenssets gebruikt `customer_id` als primaire id, terwijl de andere twee `email_id` gebruiken. Als u een privacyverzoek (toegang of schrapping) zou verzenden gebruikend slechts `email_id` als gebruiker - identiteitskaart waarde, slechts zouden `firstName`, `lastName`, en `mlScore` attributen worden verwerkt, terwijl `address` niet zou worden beïnvloed.

Om ervoor te zorgen dat uw privacyverzoeken alle relevante klantenattributen verwerken, moet u de primaire identiteitswaarden voor alle toepasselijke datasets verstrekken waar die attributen (tot een maximum van negen IDs per klant) kunnen worden opgeslagen. Zie de sectie over identiteitsgebieden in [grondbeginselen van schemacompositie](../xdm/schema/composition.md#identity) voor meer informatie over gebieden die algemeen als identiteiten worden gemerkt.

>[!NOTE]
>
>Als u verschillende [sandboxen](../sandboxes/home.md) gebruikt om uw [!DNL Profile]-gegevens op te slaan, moet u een afzonderlijke privacyaanvraag voor elke sandbox indienen en de juiste naam van de sandbox opgeven in de `x-sandbox-name`-header.

## Verzoek om verwerking verwijderen

Wanneer [!DNL Experience Platform] een verwijderingsverzoek van [!DNL Privacy Service] ontvangt, verzendt [!DNL Platform] bevestiging aan [!DNL Privacy Service] dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping zijn duidelijk gemaakt. De records worden vervolgens verwijderd uit de [!DNL Data Lake]- of [!DNL Profile]-winkel nadat de privacytaak is voltooid. Hoewel de verwijdertaak nog steeds wordt verwerkt, worden de gegevens via de elektronische weg verwijderd en zijn ze daarom niet toegankelijk voor een [!DNL Platform]-service. Raadpleeg de [[!DNL Privacy Service] documentatie](../privacy-service/home.md#monitor) voor meer informatie over het bijhouden van taakstatussen.

>[!IMPORTANT]
>
>Terwijl een succesvol schrappingsverzoek de verzamelde kenmerkgegevens voor een klant (of reeks klanten) verwijdert, verwijdert het verzoek niet de verenigingen die in de identiteitsgrafiek worden gevestigd.
>
>Een verwijderingsaanvraag die `email_id` en `customer_id` van een klant gebruikt, verwijdert bijvoorbeeld alle kenmerkgegevens die onder die id&#39;s zijn opgeslagen. Eventuele gegevens die vervolgens onder dezelfde `customer_id` worden ingevoerd, worden echter nog steeds gekoppeld aan de juiste `email_id`, aangezien de koppeling nog steeds bestaat.

In toekomstige releases zal [!DNL Platform] een bevestiging sturen naar [!DNL Privacy Service] nadat gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd aan de belangrijke concepten betrokken bij de verwerking van privacyverzoeken in [!DNL Experience Platform]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Voor informatie over het verwerken van privacyverzoeken voor [!DNL Platform] middelen niet die door [!DNL Profile] worden gebruikt, zie het document over [privacyverzoekverwerking in het meer van Gegevens](../catalog/privacy.md).