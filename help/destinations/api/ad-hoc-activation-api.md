---
keywords: Experience Platform;doel-API;ad-hocactivering;segmenten ad-hoc activeren
solution: Experience Platform
title: Doelsegmenten activeren naar batchbestemmingen via de API voor ad-hocactivering
description: Dit artikel illustreert de end-to-end workflow voor het activeren van publiekssegmenten via de API voor ad-hocactivering, inclusief de segmentatietaken die vóór activering plaatsvinden.
topic-legacy: tutorial
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 9e191d52d8385d716ed312725f72bd85c1e4b72d
workflow-type: tm+mt
source-wordcount: '1482'
ht-degree: 0%

---

# Activeer publiekssegmenten op aanvraag naar batchbestemmingen via de API voor ad-hocactivering

>[!IMPORTANT]
>
>Na voltooiing van de bètafase [!DNL ad-hoc activation API] is nu algemeen beschikbaar voor alle klanten in de Experience Platform. In de GA-versie is de API bijgewerkt naar versie 2. Stap 4 ([Vraag de meest recente segment-exporttaak-id aan](#segment-export-id)) is niet meer vereist, omdat de API de export-id niet meer vereist.
>
>Zie [De ad-hocactiveringstaak uitvoeren](#activation-job) in deze zelfstudie vindt u meer informatie .

## Overzicht {#overview}

Met de API voor ad-hocactivering kunnen marketers publiekssegmenten programmatisch op een snelle en efficiënte manier naar doelen activeren voor situaties waarin onmiddellijke activering vereist is.

In het onderstaande diagram ziet u de end-to-end workflow voor het activeren van segmenten via de API voor ad-hocactivering, inclusief de segmentatietaken die elke 24 uur in Platform plaatsvinden.

![ad-hocactivering](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Activering van ad-hocgroepen wordt alleen ondersteund door [batchbestandsgebaseerde doelen](../destination-types.md#file-based).

## Gebruiksscenario’s {#use-cases}

### Flash verkopen of promoties

Een online detailhandelaar bereidt een beperkte flitsverkoop voor en wil klanten op korte termijn op de hoogte brengen. Via de API voor ad-hocactivering van Experience Platforms kan het marketingteam segmenten op aanvraag exporteren en snel promotiemails sturen naar de klantenbasis.

### Actuele gebeurtenissen of het doorbreken van nieuws

Een hotel verwacht het hoogteweer in de komende dagen en het team wil de aankomende gasten snel informeren, zodat ze dienovereenkomstig kunnen plannen. Het marketingteam kan de API voor ad-hocactivering van Experience Platforms gebruiken om segmenten op aanvraag te exporteren en de gasten op de hoogte te stellen.

### Integratie testen

IT-beheerders kunnen de API voor ad-hocactivering van Experience Platforms gebruiken om segmenten op aanvraag te exporteren, zodat ze hun aangepaste integratie met Adobe Experience Platform kunnen testen en kunnen controleren of alles correct werkt.

## Guardrails {#guardrails}

Houd rekening met de volgende instructies wanneer u de API voor ad-hocactivering gebruikt.

* Momenteel kan elke ad-hocactiveringstaak maximaal 80 segmenten activeren. Als u probeert meer dan 80 segmenten per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd.
* Ad-hocactiveringstaken kunnen niet gelijktijdig met de geplande [segmentexporttaken](../../segmentation/api/export-jobs.md). Voordat u een ad-hocactiveringstaak uitvoert, moet u controleren of de geplande segmentexporttaak is voltooid. Zie [doelgegevensbeheer](../../dataflows/ui/monitor-destinations.md) voor informatie over hoe de status van activeringsstromen moet worden gecontroleerd. Als uw activeringsgegevens bijvoorbeeld een **[!UICONTROL Processing]** status, wacht tot de bewerking is voltooid voordat de ad-hocactiveringstaak wordt uitgevoerd.
* Voer niet meer dan één gelijktijdige ad-hocactiveringstaak per segment uit.

## Segmenteringsoverwegingen {#segmentation-considerations}

Adobe Experience Platform voert elke 24 uur een geplande segmentatietaak uit. De API voor ad-hocactivering wordt uitgevoerd op basis van de meest recente segmentatieresultaten.

## Stap 1: Vereisten {#prerequisites}

Voordat u aanroepen kunt uitvoeren naar de Adobe Experience Platform API&#39;s, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een IMS-organisatie-account met toegang tot Adobe Experience Platform.
* Je Experience Platform account heeft de `developer` en `user` rollen die zijn ingeschakeld voor het Adobe Experience Platform API-productprofiel. Neem contact op met uw [Admin Console](../../access-control/home.md) beheerder om deze rollen voor uw rekening toe te laten.
* Je hebt een Adobe ID. Als je geen Adobe ID hebt, ga dan naar de [Adobe Developer Console](https://developer.adobe.com/console) en maak een nieuwe account.

## Stap 2: Referenties verzamelen {#credentials}

Als u aanroepen wilt uitvoeren naar Platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor Platform-API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in Experience Platform raadpleegt u de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Stap 3: Activeringsstroom maken in de gebruikersinterface van het Platform {#activation-flow}

Voordat u segmenten kunt activeren via de API voor ad-hocactivering, moet u eerst een activeringsstroom hebben geconfigureerd in de gebruikersinterface van het Platform voor het gekozen doel.

Dit omvat het ingaan van in het activeringswerkschema, het selecteren van uw segmenten, het vormen van een programma, en het activeren van hen. U kunt de UI of API gebruiken om een activeringsstroom tot stand te brengen:

* [Gebruik de interface van het Platform om een activeringsstroom te creëren aan de uitvoerbestemmingen van het partijprofiel](../ui/activate-batch-profile-destinations.md)
* [Gebruik de Flow Service API om verbinding te maken met exportdoelen voor batchprofielen en gegevens te activeren](../api/connect-activate-batch-destinations.md)

## Stap 4: Vraag de meest recente segment-exporttaak-id aan (niet vereist in v2) {#segment-export-id}

>[!IMPORTANT]
>
>In versie 2 van de API voor ad-hocactivering hoeft u de meest recente segment-exporttaak-id niet te verkrijgen. U kunt deze stap overslaan en naar de volgende stap gaan.

Nadat u een activeringsstroom voor uw partijbestemming vormt, beginnen de geplande segmentatietaken automatisch om de 24 uur lopend.

Voordat u de ad-hocactiveringstaak kunt uitvoeren, moet u de id van de laatste segmentexporttaak opvragen. U moet deze id doorgeven in de aanvraag voor een ad-hocactiveringstaak.

Volg de beschreven instructies [hier](../../segmentation/api/export-jobs.md#retrieve-list) om een lijst van alle banen van de segmentuitvoer terug te winnen.

In de reactie, zoek het eerste verslag dat het schemabezit hieronder omvat.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

De id van de segmentexporttaak bevindt zich in `id` eigenschap, zoals hieronder weergegeven.

![uitvoertaak-id segment](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Stap 5: De ad-hocactiveringstaak uitvoeren {#activation-job}

Adobe Experience Platform voert elke 24 uur een geplande segmentatietaak uit. De API voor ad-hocactivering wordt uitgevoerd op basis van de meest recente segmentatieresultaten.

Voordat u een ad-hocactiveringstaak uitvoert, moet u controleren of de geplande segmentexporttaak voor uw segmenten is voltooid. Zie [doelgegevensbeheer](../../dataflows/ui/monitor-destinations.md) voor informatie over hoe de status van activeringsstromen moet worden gecontroleerd. Als uw activeringsgegevens bijvoorbeeld een **[!UICONTROL Processing]** status, wacht tot de bewerking is voltooid voordat de ad-hocactiveringstaak wordt uitgevoerd.

Nadat de segmentexporttaak is voltooid, kunt u de activering activeren.

>[!NOTE]
>
>Momenteel kan elke ad-hocactiveringstaak maximaal 80 segmenten activeren. Als u probeert meer dan 80 segmenten per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd.

### Verzoek {#request}

>[!IMPORTANT]
>
>Het is verplicht de `Accept: application/vnd.adobe.adhoc.activation+json; version=2` in uw verzoek om versie 2 van de API voor ad-hocactivering te gebruiken.

```shell
curl --location --request POST 'https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun' \
--header 'x-gw-ims-org-id: 5555467B5D8013E50A494220@AdobeOrg' \
--header 'Authorization: Bearer {{token}}' \
--header 'x-sandbox-id: 6ef74723-3ee7-46a4-b747-233ee7a6a41a' \
--header 'x-sandbox-name: {sandbox-id}' \
--header 'Accept: application/vnd.adobe.adhoc.activation+json; version=2' \
--header 'Content-Type: application/json' \
--data-raw '{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   }
}'
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u segmenten wilt activeren. U kunt deze id&#39;s ophalen vanuit de gebruikersinterface van het Platform door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en klik op de gewenste doelrij om de doel-id in de rechtertrack te verhogen. Lees voor meer informatie de [documentatie van de werkruimte van doelen](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van de segmenten die u wilt activeren voor het geselecteerde doel. |

{style=&quot;table-layout:auto&quot;}

### Verzoek met export-id&#39;s (af te gekeurd) {#request-deprecated}

>[!IMPORTANT]
>
>**Vervangen aanvraagtype**. Dit voorbeeldtype beschrijft het aanvraagtype voor API versie 1. In versie 2 van de API voor ad-hocactivering hoeft u de meest recente id voor de exporttaak van segmenten niet op te nemen.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -d '
{
   "activationInfo":{
      "destinationId1":[
         "segmentId1",
         "segmentId2"
      ],
      "destinationId2":[
         "segmentId2",
         "segmentId3"
      ]
   },
   "exportIds":[
      "exportId1"
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u segmenten wilt activeren. U kunt deze id&#39;s ophalen vanuit de gebruikersinterface van het Platform door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en klik op de gewenste doelrij om de doel-id in de rechtertrack te verhogen. Lees voor meer informatie de [documentatie van de werkruimte van doelen](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van de segmenten die u wilt activeren voor het geselecteerde doel. |
| <ul><li>`exportId1`</li></ul> | De id die wordt geretourneerd in het antwoord van de [segmentexport](../../segmentation/api/export-jobs.md#retrieve-list) taak. Zie [Stap 4: Vraag de meest recente segment-exporttaak-id aan](#segment-export-id) voor instructies over hoe u deze id kunt vinden. |

{style=&quot;table-layout:auto&quot;}

### Antwoord {#response}

Een geslaagde reactie retourneert HTTP-status 200.

```shell
{
   "order":[
      {
         "segment":"db8961e9-d52f-45bc-b3fb-76d0382a6851",
         "order":"ef2dcbd6-36fc-49a3-afed-d7b8e8f724eb",
         "statusURL":"https://platform.adobe.io/data/foundation/flowservice/runs/88d6da63-dc97-460e-b781-fc795a7386d9"
      }
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `segment` | De id van het geactiveerde segment. |
| `order` | De id van het doel waarop het segment is geactiveerd. |
| `statusURL` | De status-URL van de activeringsstroom. U kunt de voortgang van de flow volgen met de [Flow Service-API](../../sources/tutorials/api/monitor.md). |

{style=&quot;table-layout:auto&quot;}

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

### API-foutcodes en berichten die specifiek zijn voor de API voor ad-hocactivering {#specific-error-messages}

Wanneer u de API voor ad-hocactivering gebruikt, kunt u foutberichten tegenkomen die specifiek zijn voor dit API-eindpunt. Bekijk de tabel om te begrijpen hoe u deze kunt aanpakken wanneer ze worden weergegeven.

| Foutbericht | Resolutie |
|---------|----------|
| Reeds lopend voor segment `segment ID` voor bestelling `dataflow ID` met run-id `flow run ID` | Dit foutbericht geeft aan dat momenteel een ad-hocactiveringsstroom wordt uitgevoerd voor een segment. Wacht tot de taak is voltooid voordat u de activeringstaak opnieuw start. |
| Segmenten `<segment name>` maakt geen deel uit van deze gegevensstroom of van het planningsbereik! | Dit foutbericht geeft aan dat de segmenten die u hebt geselecteerd om te activeren, niet zijn toegewezen aan de gegevensstroom of dat het activeringsschema voor de segmenten is verlopen of nog niet is gestart. Controleer of het segment inderdaad is toegewezen aan de dataflow en controleer of het schema voor segmentactivering overlapt met de huidige datum. |

## Verwante informatie {#related-information}

* [Verbinden met batchbestemmingen en gegevens activeren met de Flow Service API](/help/destinations/api/connect-activate-batch-destinations.md)