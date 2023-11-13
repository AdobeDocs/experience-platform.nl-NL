---
keywords: Experience Platform;doel-API;ad-hocactivering;publiek ad-hoc activeren
solution: Experience Platform
title: Het publiek activeren naar batchbestemmingen via de API voor ad-hocactivering
description: Dit artikel illustreert de end-to-end workflow voor het activeren van het publiek via de API voor ad-hocactivering, inclusief de segmentatietaken die plaatsvinden vóór activering.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: 6304dabb6125b7eddcac16bcbf8abcc36a4c9dc2
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 0%

---

# Het publiek op aanvraag activeren naar batchbestemmingen via de API voor ad-hocactivering

>[!IMPORTANT]
>
>Na voltooiing van de bètafase [!DNL ad-hoc activation API] is nu algemeen beschikbaar voor alle klanten in de Experience Platform. In de GA-versie is de API bijgewerkt naar versie 2. Stap 4 ([De meest recente gebruikers-id voor exporttaken ophalen](#segment-export-id)) is niet meer vereist, omdat de API de export-id niet meer vereist.
>
>Zie [De ad-hocactiveringstaak uitvoeren](#activation-job) in deze zelfstudie vindt u meer informatie .

## Overzicht {#overview}

Met de API voor ad-hocactivering kunnen marketers het publiek programmatisch naar bestemmingen activeren, op een snelle en efficiënte manier, in situaties waarin onmiddellijke activering vereist is.

Gebruik de API voor ad-hocactivering om volledige bestanden te exporteren naar het gewenste systeem voor het ontvangen van bestanden. Activering van ad-hocgroepen wordt alleen ondersteund door [batchbestandsgebaseerde doelen](../destination-types.md#file-based).

In het onderstaande diagram ziet u de end-to-end workflow voor het activeren van het publiek via de API voor ad-hocactivering, inclusief de segmentatietaken die elke 24 uur in Platform plaatsvinden.

![ad-hocactivering](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)



## Gebruiksscenario’s {#use-cases}

### Verkoop of promoties van Flash

Een online detailhandelaar bereidt een beperkte flitsverkoop voor en wil klanten op korte termijn op de hoogte brengen. Via de API voor ad-hocactivering van Experience Platforms kan het marketingteam op aanvraag soorten publiek exporteren en snel e-mails met speciale acties naar de klantenbasis sturen.

### Actuele gebeurtenissen of het doorbreken van nieuws

Een hotel verwacht het hoogteweer in de komende dagen en het team wil de aankomende gasten snel informeren, zodat ze dienovereenkomstig kunnen plannen. Het marketingteam kan de API voor ad-hocactivering van het Experience Platform gebruiken om het publiek op aanvraag te exporteren en de gasten op de hoogte te stellen.

### Integratie testen

IT-beheerders kunnen de API voor ad-hocactivering van Experience Platforms gebruiken om doelgroepen op aanvraag te exporteren, zodat ze hun aangepaste integratie met Adobe Experience Platform kunnen testen en kunnen controleren of alles correct werkt.

## Guardrails {#guardrails}

Houd rekening met de volgende instructies wanneer u de API voor ad-hocactivering gebruikt.

* Op dit moment kan elke ad-hocactiveringstaak maximaal 80 soorten publiek activeren. Als u probeert meer dan 80 soorten publiek per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd.
* Ad-hocactiveringstaken kunnen niet gelijktijdig met de geplande [doelgroepen exporttaken](../../segmentation/api/export-jobs.md). Voordat u een ad-hocactiveringstaak uitvoert, moet u controleren of de geplande doelexporttaak is voltooid. Zie [doelgegevensstroom controleren](../../dataflows/ui/monitor-destinations.md) voor informatie over hoe de status van activeringsstromen moet worden gecontroleerd. Als uw activeringsgegevensstroom bijvoorbeeld een **[!UICONTROL Processing]** status, wacht tot de bewerking is voltooid voordat de ad-hocactiveringstaak wordt uitgevoerd.
* Voer niet meer dan één gelijktijdige ad-hocactiveringstaak per publiek uit.

## Segmenteringsoverwegingen {#segmentation-considerations}

Adobe Experience Platform voert elke 24 uur een geplande segmentatietaak uit. De API voor ad-hocactivering wordt uitgevoerd op basis van de meest recente segmentatieresultaten.

## Stap 1: Voorwaarden {#prerequisites}

Voordat u aanroepen kunt uitvoeren naar de Adobe Experience Platform API&#39;s, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een organisatie-account met toegang tot Adobe Experience Platform.
* Je Experience Platform account heeft de `developer` en `user` rollen ingeschakeld voor het Adobe Experience Platform API-productprofiel. Neem contact op met uw [Admin Console](../../access-control/home.md) beheerder om deze rollen voor uw rekening toe te laten.
* Je hebt een Adobe ID. Als je geen Adobe ID hebt, ga dan naar de [Adobe Developer Console](https://developer.adobe.com/console) en maak een nieuwe account.

## Stap 2: Referenties verzamelen {#credentials}

Als u aanroepen wilt uitvoeren naar platform-API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Toestemming: houder `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor platform-API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Zie voor meer informatie over sandboxen in Experience Platform de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Stap 3: De activeringsstroom maken in de gebruikersinterface van het platform {#activation-flow}

Voordat u het publiek kunt activeren via de API voor ad-hocactivering, moet u eerst een activeringsstroom hebben geconfigureerd in de interface van het platform, voor de gekozen bestemming.

Dit omvat het ingaan van in het activeringswerkschema, het selecteren van uw publiek, het vormen van een programma, en het activeren van hen. U kunt de UI of API gebruiken om een activeringsstroom tot stand te brengen:

* [Gebruik Platform UI om een activeringsstroom tot stand te brengen aan de uitvoerbestemmingen van het partijprofiel](../ui/activate-batch-profile-destinations.md)
* [Gebruik de Flow Service API om verbinding te maken met exportdoelen voor batchprofielen en gegevens te activeren](../api/connect-activate-batch-destinations.md)

## Stap 4: Vraag de meest recente uitvoertaak-id voor het publiek aan (niet vereist in v2) {#segment-export-id}

>[!IMPORTANT]
>
>In versie 2 van de API voor ad-hocactivering hoeft u de meest recente uitvoertaak-id voor het publiek niet te verkrijgen. U kunt deze stap overslaan en naar de volgende stap gaan.

Nadat u een activeringsstroom voor uw partijbestemming vormt, beginnen de geplande segmentatietaken automatisch om de 24 uur lopend.

Voordat u de ad-hocactiveringstaak kunt uitvoeren, moet u de id van de laatste doelexporttaak opvragen. U moet deze id doorgeven in de aanvraag voor een ad-hocactiveringstaak.

Volg de beschreven instructies [hier](../../segmentation/api/export-jobs.md#retrieve-list) om een lijst op te halen van alle doelexporttaken.

In de reactie, zoek het eerste verslag dat het schemabezit hieronder omvat.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

De id van de doelexporttaak bevindt zich in de `id` eigenschap, zoals hieronder weergegeven.

![doelgroep, taak-id exporteren](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Stap 5: De ad-hocactiveringstaak uitvoeren {#activation-job}

Adobe Experience Platform voert elke 24 uur een geplande segmentatietaak uit. De API voor ad-hocactivering wordt uitgevoerd op basis van de meest recente segmentatieresultaten.

>[!IMPORTANT]
>
>Let op de volgende eenmalige beperking: voordat u een ad-hocactiveringstaak uitvoert, moet u ervoor zorgen dat er ten minste 20 minuten zijn verstreken vanaf het moment dat het publiek voor het eerst werd geactiveerd volgens het schema dat u instelt in [Stap 3 - de activeringsstroom van het Platform UI creëren](#activation-flow).

Voordat u een ad-hocactiveringstaak uitvoert, moet u controleren of de geplande doeluitvoertaak voor uw publiek is voltooid. Zie [doelgegevensstroom controleren](../../dataflows/ui/monitor-destinations.md) voor informatie over hoe de status van activeringsstromen moet worden gecontroleerd. Als uw activeringsgegevensstroom bijvoorbeeld een **[!UICONTROL Processing]** status, wacht tot de bewerking is voltooid voordat de ad-hocactiveringstaak wordt uitgevoerd om een volledig bestand te exporteren.

Nadat de doelexporttaak is voltooid, kunt u de activering activeren.

>[!NOTE]
>
>Op dit moment kan elke ad-hocactiveringstaak maximaal 80 soorten publiek activeren. Als u probeert meer dan 80 soorten publiek per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u het publiek wilt activeren. U kunt deze id&#39;s ophalen vanuit de interface van het platform door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en klik op de gewenste doelrij om de doel-id in de rechtertrack te verhogen. Lees voor meer informatie de [documentatie van de werkruimte van doelen](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van het publiek dat u wilt activeren naar het geselecteerde doel. |

{style="table-layout:auto"}

### Verzoek met export-id&#39;s (af te gekeurd) {#request-deprecated}

>[!IMPORTANT]
>
>**Vervangen aanvraagtype**. Dit voorbeeldtype beschrijft het aanvraagtype voor API versie 1. In versie 2 van de API voor ad-hocactivering hoeft u niet de meest recente uitvoertaak-id voor het publiek op te nemen.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u het publiek wilt activeren. U kunt deze id&#39;s ophalen vanuit de interface van het platform door naar **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** en klik op de gewenste doelrij om de doel-id in de rechtertrack te verhogen. Lees voor meer informatie de [documentatie van de werkruimte van doelen](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van het publiek dat u wilt activeren naar het geselecteerde doel. |
| <ul><li>`exportId1`</li></ul> | De id die wordt geretourneerd in het antwoord van de [doelgroep exporteren](../../segmentation/api/export-jobs.md#retrieve-list) taak. Zie [Stap 4: Vraag de nieuwste id voor het exporteren van de doeltaak aan](#segment-export-id) voor instructies over hoe u deze id kunt vinden. |

{style="table-layout:auto"}

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
| `segment` | De id van het geactiveerde publiek. |
| `order` | De id van het doel waarop het publiek is geactiveerd. |
| `statusURL` | De status-URL van de activeringsstroom. U kunt de voortgang van de flow volgen met de [Flow Service-API](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

### API-foutcodes en specifieke berichten voor de API voor ad-hocactivering {#specific-error-messages}

Wanneer u de API voor ad-hocactivering gebruikt, kunt u foutberichten tegenkomen die specifiek zijn voor dit API-eindpunt. Bekijk de tabel om te begrijpen hoe u deze kunt aanpakken wanneer ze worden weergegeven.

| Foutbericht | Resolutie |
|---------|----------|
| Uitvoeren is al gestart voor publiek `segment ID` voor bestelling `dataflow ID` met run-id `flow run ID` | Dit foutbericht geeft aan dat er momenteel een ad-hocactiveringsstroom actief is voor een publiek. Wacht tot de taak is voltooid voordat u de activeringstaak opnieuw start. |
| Segmenten `<segment name>` maakt geen deel uit van deze gegevensstroom of van het planningsbereik! | Dit foutbericht geeft aan dat het publiek dat u hebt geselecteerd om te activeren, niet is toegewezen aan de gegevensstroom of dat het activeringsschema dat voor het publiek is ingesteld, is verlopen of nog niet is gestart. Controleer of het publiek inderdaad is toegewezen aan de dataflow en controleer of het activeringsschema voor het publiek de huidige datum overlapt. |

## Verwante informatie {#related-information}

* [Verbinden met batchbestemmingen en gegevens activeren met de Flow Service API](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Bèta) de dossiers van de uitvoer op bestelling aan partijbestemmingen gebruikend Experience Platform UI](/help/destinations/ui/export-file-now.md)