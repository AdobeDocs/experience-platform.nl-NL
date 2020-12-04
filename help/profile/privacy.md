---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: De verzoekverwerking van de privacy in Real-time Profiel van de Klant
topic: overview
translation-type: tm+mt
source-git-commit: 066337419431db24bde0a8d0d30b85132d08f43c
workflow-type: tm+mt
source-wordcount: '1058'
ht-degree: 0%

---


# Behandeling van privacyverzoek in [!DNL Real-time Customer Profile]

Adobe Experience Platform [!DNL Privacy Service] verwerkt verzoeken van klanten om toegang, om te weigeren of om hun persoonsgegevens te verwijderen zoals die zijn omschreven in privacyregels zoals de algemene gegevensbeschermingsverordening (GDPR) en [!DNL California Consumer Privacy Act] (CCPA).

Dit document behandelt essentiële concepten met betrekking tot het verwerken van privacyverzoeken voor [!DNL Real-time Customer Profile].

## Aan de slag

U wordt aangeraden de volgende [!DNL Experience Platform] services goed te begrijpen voordat u deze handleiding leest:

* [[!DNL Privacy Service]](home.md): Beheert verzoeken van klanten om hun persoonlijke gegevens in Adobe Experience Cloud-toepassingen te openen, uit de handel te nemen of te verwijderen.
* [[!DNL Identity Service]](../identity-service/home.md): Oplost de fundamentele uitdaging die door de fragmentatie van de gegevens van de klantenervaring wordt gesteld door identiteiten over apparaten en systemen te overbruggen.
* [[!DNL Real-time Customer Profile]](../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.

## Naamruimten voor identiteiten {#namespaces}

Adobe Experience Platform [!DNL Identity Service] biedt een brug tussen identiteitsgegevens van klanten op systemen en apparaten. [!DNL Identity Service] gebruikt **naamruimten** om context aan identiteitswaarden te verstrekken door hen met hun systeem van oorsprong te verbinden. Een naamruimte kan een algemeen concept vertegenwoordigen, zoals een e-mailadres (&quot;e-mail&quot;) of de identiteit koppelen aan een specifieke toepassing, zoals een Adobe Advertising Cloud-id (&quot;AdCloud&quot;) of een Adobe Target-id (&quot;TNTID&quot;).

De Dienst van de identiteit handhaaft een opslag van globaal bepaalde (standaard) en user-defined (douane) identiteitsnamespaces. Standaard naamruimten zijn beschikbaar voor alle organisaties (bijvoorbeeld E-mail en ECID), terwijl uw organisatie aangepaste naamruimten kan maken die aan de specifieke behoeften voldoen.

Zie het overzicht [!DNL Experience Platform]van naamruimte voor [identiteiten in voor meer informatie over naamruimten in naamruimten](../identity-service/namespaces.md).

## Verzoeken indienen {#submit}

In de volgende secties wordt beschreven hoe u privacyverzoeken kunt indienen voor het [!DNL Real-time Customer Profile] gebruik van de [!DNL Privacy Service] API of UI. Voordat u deze secties leest, wordt u ten zeerste aangeraden de API [-](../privacy-service/api/getting-started.md) Privacy Service of de [Privacy Service-UI](../privacy-service/ui/overview.md) -documentatie te raadplegen voor de volledige stappen voor het verzenden van een privacytaak, waaronder het correct opmaken van verzonden identiteitsgegevens van gebruikers in de payloads voor aanvragen.

>[!IMPORTANT]
>
>Privacy Service kan alleen [!DNL Profile] gegevens verwerken met een samenvoegbeleid dat geen identiteitsstitching uitvoert. Als u de UI gebruikt om te bevestigen of uw privacyverzoeken worden verwerkt, zorg ervoor dat u een beleid met &quot;[!DNL None]&quot;als zijn [!UICONTROL identiteitskaart het stitching] type gebruikt. Met andere woorden, u kunt geen samenvoegbeleid gebruiken waarbij [!UICONTROL id-stitching] is ingesteld op &#39;[!UICONTROL Privégrafiek]&#39;.
>
>![](./images/privacy/no-id-stitch.png)
>
>Het is ook belangrijk om op te merken dat de hoeveelheid tijd die een privacyverzoek kan duren om te voltooien niet kan worden gewaarborgd. Als er wijzigingen optreden in uw [!DNL Profile] gegevens terwijl een aanvraag nog wordt verwerkt, kan niet worden gegarandeerd of deze records al dan niet worden verwerkt.

### De API gebruiken

Bij het maken van taakaanvragen in de API `userIDs` moeten alle id&#39;s in de API een specifieke `namespace` en `type`specifieke id gebruiken. Voor de [waarde](#namespaces) moet een geldige naamruimte [!DNL Identity Service] voor de `namespace` identiteit worden opgegeven, terwijl de naam `type` of `standard` `unregistered` (voor respectievelijk standaard- en aangepaste naamruimten) moet zijn.

>[!NOTE]
>
>Afhankelijk van de identiteitsgrafiek en de manier waarop uw profielfragmenten in gegevenssets van Platforms worden gedistribueerd, moet u mogelijk meer dan één id opgeven voor elke klant. Zie de volgende sectie [profielfragmenten](#fragments) voor meer informatie.

Bovendien moet de `include` array van de aanvraaglading de productwaarden voor de verschillende gegevensopslag bevatten het verzoek wordt ingediend. Wanneer u een aanvraag naar de array indient, moet de array de waarde &quot;ProfileService&quot; bevatten. [!DNL Data Lake]

Met de volgende aanvraag wordt een nieuwe privacytaak gemaakt voor de gegevens van één klant in de [!DNL Profile] winkel. Er worden twee identiteitswaarden opgegeven voor de klant in de `userIDs` array. de ene met de standaardnaamruimte voor `Email` identiteit en de andere met een aangepaste `Customer_ID` naamruimte. Het omvat ook de productwaarde voor [!DNL Profile] (`ProfileService`) in de `include` serie:

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

Wanneer het creëren van baanverzoeken in UI, ben zeker om **[!UICONTROL AEP Gegevensmeer]** en/of **[!UICONTROL Profiel]** onder **[!UICONTROL Producten]** te selecteren om banen voor gegevens te verwerken die in [!DNL Data Lake] of [!DNL Real-time Customer Profile], respectievelijk worden opgeslagen.

<img src="images/privacy/product-value.png" width="450"><br>

## Profielfragmenten in privacyverzoeken {#fragments}

In de [!DNL Profile] gegevensopslag, zullen de persoonlijke gegevens voor een individuele klant vaak van veelvoudige profielfragmenten bestaan, die met de persoon door de identiteitsgrafiek worden geassocieerd. Wanneer u een privacyaanvraag naar de [!DNL Profile] winkel verzendt, is het belangrijk om te weten dat aanvragen alleen op profielfragmentniveau worden verwerkt in plaats van op het volledige profiel.

Bijvoorbeeld, overweeg een situatie waar u de gegevens van de klantenattributen in drie afzonderlijke datasets opslaat, die verschillende herkenningstekens gebruiken om die gegevens met individuele klanten te associëren:

| Naam gegevensset | Primair identiteitsveld | Opgeslagen kenmerken |
| --- | --- | --- |
| Dataset 1 | `customer_id` | `address` |
| Gegevensset 2 | `email_id` | `firstName`, `lastName` |
| Gegevensset 3 | `email_id` | `mlScore` |

Één van de datasets gebruikt `customer_id` als zijn primaire herkenningsteken, terwijl de andere twee gebruiken `email_id`. Als u een privacyverzoek (toegang of schrapping) zou verzenden gebruikend slechts `email_id` als de waarde van identiteitskaart van de gebruiker, slechts zouden `firstName`, `lastName`, en de `mlScore` attributen worden verwerkt, terwijl `address` niet zou worden beïnvloed.

Om ervoor te zorgen dat uw privacyverzoeken alle relevante klantenattributen verwerken, moet u de primaire identiteitswaarden voor alle toepasselijke datasets verstrekken waar die attributen (tot een maximum van negen IDs per klant) kunnen worden opgeslagen. Zie de sectie over identiteitsgebieden in de [grondbeginselen van schemacompositie](../xdm/schema/composition.md#identity) voor meer informatie over gebieden die algemeen als identiteiten worden gemerkt.

>[!NOTE]
>
>Als u verschillende [sandboxen](../sandboxes/home.md) gebruikt om uw [!DNL Profile] gegevens op te slaan, moet u voor elke sandbox een afzonderlijke privacyaanvraag indienen die de juiste naam van de sandbox in de `x-sandbox-name` header aangeeft.

## Verzoek om verwerking verwijderen

Wanneer [!DNL Experience Platform] een verwijderingsverzoek van [!DNL Privacy Service]ontvangt, [!DNL Platform] verzendt bevestiging aan [!DNL Privacy Service] dat het verzoek is ontvangen en de beïnvloede gegevens voor schrapping duidelijk zijn. De records worden vervolgens uit de [!DNL Data Lake] of [!DNL Profile] winkel verwijderd als de privacytaak is voltooid. Hoewel de verwijdertaak nog steeds wordt verwerkt, worden de gegevens via de elektronische weg verwijderd en zijn ze daarom niet toegankelijk voor enige [!DNL Platform] service. Raadpleeg de [[!DNL Privacy Service] documentatie](../privacy-service/home.md#monitor) voor meer informatie over het bijhouden van de taakstatus.

>[!IMPORTANT]
>
>Terwijl een succesvol schrappingsverzoek de verzamelde kenmerkgegevens voor een klant (of reeks klanten) verwijdert, verwijdert het verzoek niet de verenigingen die in de identiteitsgrafiek worden gevestigd.
>
>Bijvoorbeeld, verwijdert een schrappingsverzoek dat klant gebruikt `email_id` `customer_id` en alle kenmerkgegevens verwijdert die onder die IDs worden opgeslagen. Eventuele gegevens die daarna onder dezelfde regel worden opgenomen, `customer_id` zullen echter nog steeds in verband worden gebracht met het passende `email_id`, aangezien de koppeling nog steeds bestaat.

In toekomstige versies [!DNL Platform] wordt een bevestiging verzonden naar [!DNL Privacy Service] nadat gegevens fysiek zijn verwijderd.

## Volgende stappen

Door dit document te lezen, bent u geïntroduceerd in de belangrijke concepten betrokken bij de verwerking van privacyverzoeken in [!DNL Experience Platform]. U wordt aangeraden de documentatie in deze handleiding te blijven lezen om meer inzicht te krijgen in de manier waarop u identiteitsgegevens kunt beheren en privacytaken kunt maken.

Voor informatie over het verwerken van privacyverzoeken voor [!DNL Platform] middelen die niet door worden gebruikt, zie het document over [!DNL Profile]privacyaanvraagverwerking in het meer [](../catalog/privacy.md)van Gegevens.