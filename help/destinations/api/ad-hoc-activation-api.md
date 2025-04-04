---
keywords: Experience Platform;doel-API;ad-hocactivering;publiek ad-hoc activeren
solution: Experience Platform
title: Het publiek activeren naar batchbestemmingen via de API voor ad-hocactivering
description: Dit artikel illustreert de end-to-end workflow voor het activeren van het publiek via de API voor ad-hocactivering, inclusief de segmentatietaken die plaatsvinden vóór activering.
type: Tutorial
exl-id: 1a09f5ff-0b04-413d-a9f6-57911a92b4e4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 0%

---

# Het publiek op aanvraag activeren naar batchbestemmingen via de API voor ad-hocactivering

>[!IMPORTANT]
>
>Na de Beta-fase is de [!DNL ad-hoc activation API] nu algemeen beschikbaar voor alle Experience Platform-klanten. In de GA-versie is de API bijgewerkt naar versie 2. Stap 4 ([ verkrijgt de recentste identiteitskaart van de publiekuitvoer ](#segment-export-id)) wordt niet meer vereist, aangezien API niet uitvoeridentiteitskaart meer vereist.
>
>Zie [ in werking stellen de ad-hoc activeringsbaan ](#activation-job) verder hieronder in dit leerprogramma voor meer informatie.

## Overzicht {#overview}

Met de API voor ad-hocactivering kunnen marketers het publiek programmatisch naar bestemmingen activeren, op een snelle en efficiënte manier, in situaties waarin onmiddellijke activering vereist is.

Gebruik de API voor ad-hocactivering om volledige bestanden te exporteren naar het gewenste systeem voor het ontvangen van bestanden. Ad-hoc publieksactivering wordt slechts gesteund door [ op dossier-gebaseerde bestemmingen ](../destination-types.md#file-based).

In het onderstaande diagram ziet u de end-to-end workflow voor het activeren van het publiek via de API voor ad-hocactivering, inclusief de segmentatietaken die elke 24 uur in Experience Platform plaatsvinden.

![ ad-hoc-activering ](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

## Gebruiksscenario’s {#use-cases}

### Flash-verkoop of -promoties

Een online retailer bereidt een beperkte flash-verkoop voor en wil klanten op korte termijn op de hoogte stellen. Via de API voor ad-hocactivering van Experience Platform kan het marketingteam soorten publiek op aanvraag exporteren en snel e-mails met speciale acties naar de klantenbasis sturen.

### Actuele gebeurtenissen of het doorbreken van nieuws

Een hotel verwacht het hoogteweer in de komende dagen en het team wil de aankomende gasten snel informeren, zodat ze dienovereenkomstig kunnen plannen. Het marketingteam kan de API voor ad-hocactivering van Experience Platform gebruiken om een publiek op aanvraag te exporteren en de gasten op de hoogte te stellen.

### Integratie testen

IT-managers kunnen de API voor ad-hocactivering van Experience Platform gebruiken om soorten publiek op aanvraag te exporteren, zodat ze hun aangepaste integratie met Adobe Experience Platform kunnen testen en kunnen controleren of alles correct werkt.

## Guardrails {#guardrails}

Houd rekening met de volgende instructies wanneer u de API voor ad-hocactivering gebruikt.

* Op dit moment kan elke ad-hocactiveringstaak maximaal 80 soorten publiek activeren. Als u probeert meer dan 80 soorten publiek per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd.
* De ad-hoc activeringsbanen kunnen niet gelijktijdig met geplande [ publiek uitvoeren banen ](../../segmentation/api/export-jobs.md). Voordat u een ad-hocactiveringstaak uitvoert, moet u controleren of de geplande doelexporttaak is voltooid. Zie [ bestemmingdataflow controle ](../../dataflows/ui/monitor-destinations.md) voor informatie over hoe te om het statuut van activeringsstromen te controleren. Als in uw activeringsgegevens bijvoorbeeld de status **[!UICONTROL Processing]** wordt weergegeven, wacht u tot deze is voltooid voordat u de ad-hocactiveringstaak uitvoert.
* Voer niet meer dan één gelijktijdige ad-hocactiveringstaak per publiek uit.

## Segmenteringsoverwegingen {#segmentation-considerations}

Adobe Experience Platform voert elke 24 uur een geplande segmentatietaak uit. De API voor ad-hocactivering wordt uitgevoerd op basis van de meest recente segmentatieresultaten.

## Stap 1: Voorwaarden {#prerequisites}

Voordat u aanroepen kunt uitvoeren naar de Adobe Experience Platform API&#39;s, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een organisatie-account met toegang tot Adobe Experience Platform.
* Voor uw Experience Platform-account zijn de rollen `developer` en `user` ingeschakeld voor het Adobe Experience Platform API-productprofiel. Contacteer uw [ Admin Console ](../../access-control/home.md) beheerder om deze rollen voor uw rekening toe te laten.
* Je hebt een Adobe ID. Als u geen Adobe ID hebt, ga naar [ Adobe Developer Console ](https://developer.adobe.com/console) en creeer een nieuwe rekening.

## Stap 2: Referenties verzamelen {#credentials}

Om vraag aan Experience Platform APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle Experience Platform API-aanroepen, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor Experience Platform API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in Experience Platform, zie de [ documentatie van het zandbakoverzicht ](../../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra media typekopbal:

* Inhoudstype: `application/json`

## Stap 3: De activeringsstroom maken in de gebruikersinterface van Experience Platform {#activation-flow}

Voordat u het publiek kunt activeren via de API voor ad-hocactivering, moet u eerst een activeringsstroom hebben geconfigureerd in de gebruikersinterface van Experience Platform voor het gekozen doel.

Dit omvat het ingaan van in het activeringswerkschema, het selecteren van uw publiek, het vormen van een programma, en het activeren van hen. U kunt de UI of API gebruiken om een activeringsstroom tot stand te brengen:

* [De gebruikersinterface van Experience Platform gebruiken om een activeringsstroom te maken voor exportdoelen met batchprofielen](../ui/activate-batch-profile-destinations.md)
* [Gebruik de Flow Service API om verbinding te maken met exportdoelen voor batchprofielen en gegevens te activeren](../api/connect-activate-batch-destinations.md)

## Stap 4: Vraag de meest recente uitvoertaak-id voor het publiek aan (niet vereist in v2) {#segment-export-id}

>[!IMPORTANT]
>
>In versie 2 van de API voor ad-hocactivering hoeft u de meest recente uitvoertaak-id voor het publiek niet te verkrijgen. U kunt deze stap overslaan en naar de volgende stap gaan.

Nadat u een activeringsstroom voor uw partijbestemming vormt, beginnen de geplande segmentatietaken automatisch om de 24 uur lopend.

Voordat u de ad-hocactiveringstaak kunt uitvoeren, moet u de id van de laatste doelexporttaak opvragen. U moet deze id doorgeven in de aanvraag voor een ad-hocactiveringstaak.

Volg de hier beschreven instructies [ ](../../segmentation/api/export-jobs.md#retrieve-list) om een lijst van alle banen van de publieksuitvoer terug te winnen.

In de reactie, zoek het eerste verslag dat het schemabezit hieronder omvat.

```
"schema":{
   "name":"_xdm.context.profile"
}
```

De gebruikers voeren baan ID uit is in het `id` bezit, zoals hieronder getoond.

![ identiteitskaart van de publiek de baanuitvoer ](../assets/api/ad-hoc-activation/segment-export-job-id.png)


## Stap 5: De ad-hocactiveringstaak uitvoeren {#activation-job}

Adobe Experience Platform voert elke 24 uur een geplande segmentatietaak uit. De API voor ad-hocactivering wordt uitgevoerd op basis van de meest recente segmentatieresultaten.

>[!IMPORTANT]
>
>Noteer de volgende eenmalige beperking: Alvorens een ad-hoc activeringsbaan in werking te stellen, zorg ervoor dat minstens één uur van het moment is overgegaan dat het publiek eerst volgens het programma werd geactiveerd u in [ Stap 3 - creeer activeringsstroom in Experience Platform UI ](#activation-flow) plaatste.

Voordat u een ad-hocactiveringstaak uitvoert, moet u controleren of de geplande doeluitvoertaak voor uw publiek is voltooid. Zie [ bestemmingdataflow controle ](../../dataflows/ui/monitor-destinations.md) voor informatie over hoe te om het statuut van activeringsstromen te controleren. Als in uw activeringsgegevens bijvoorbeeld de status **[!UICONTROL Processing]** wordt weergegeven, wacht u tot deze is voltooid voordat de ad-hocactiveringstaak wordt uitgevoerd om een volledig bestand te exporteren.

Nadat de doelexporttaak is voltooid, kunt u de activering activeren.

>[!NOTE]
>
>Op dit moment kan elke ad-hocactiveringstaak maximaal 80 soorten publiek activeren. Als u probeert meer dan 80 soorten publiek per taak te activeren, mislukt de taak. Dit gedrag kan in toekomstige versies worden gewijzigd.

### Verzoek {#request}

>[!IMPORTANT]
>
>Het is verplicht de header `Accept: application/vnd.adobe.adhoc.activation+json; version=2` op te nemen in uw aanvraag om versie 2 van de API voor ad-hocactivering te gebruiken.

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u het publiek wilt activeren. U kunt deze id&#39;s ophalen vanuit de gebruikersinterface van Experience Platform door naar het tabblad **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** te navigeren en op de gewenste doelrij te klikken om de doel-id op te halen in de rechtertrack. Voor meer informatie, lees de [ documentatie van de bestemmingswerkruimte ](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van het publiek dat u wilt activeren naar het geselecteerde doel. U kunt de API voor ad-hoc gebruiken om door Experience Platform gegenereerde soorten publiek en externe (aangepaste upload) soorten publiek te exporteren. Wanneer u een extern publiek activeert, gebruikt u de door het systeem gegenereerde id in plaats van de gebruikers-id. U vindt de door het systeem gegenereerde id in de overzichtsweergave voor het publiek in de gebruikersinterface. <br> ![ Mening van publiekidentiteitskaart die niet zou moeten worden geselecteerd.](/help/destinations/assets/api/ad-hoc-activation/audience-id-do-not-use.png " Mening van publiekidentiteitskaart die niet zou moeten worden geselecteerd."){width="100" zoomable="yes"} <br> ![ Mening van systeem-geproduceerde publiekidentiteitskaart die zou moeten worden gebruikt.](/help/destinations/assets/api/ad-hoc-activation/system-generated-id-to-use.png " Mening van systeem-geproduceerde publiekidentiteitskaart die zou moeten worden gebruikt."){width="100" zoomable="yes"} |

{style="table-layout:auto"}

### Aanvragen met export-id&#39;s {#request-export-ids}

<!--

>[!IMPORTANT]
>
>**Deprecated request type**. This example type describes the request type for the API version 1. In the v2 of the ad-hoc activation API, you do not need to include the latest audience export job ID.

-->

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
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u het publiek wilt activeren. U kunt deze id&#39;s ophalen vanuit de gebruikersinterface van Experience Platform door naar het tabblad **[!UICONTROL Destinations]** > **[!UICONTROL Browse]** te navigeren en op de gewenste doelrij te klikken om de doel-id op te halen in de rechtertrack. Voor meer informatie, lees de [ documentatie van de bestemmingswerkruimte ](/help/destinations/ui/destinations-workspace.md#browse). |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van het publiek dat u wilt activeren naar het geselecteerde doel. |
| <ul><li>`exportId1`</li></ul> | Identiteitskaart die in de reactie van de [ publiek is teruggekeerd voert ](../../segmentation/api/export-jobs.md#retrieve-list) baan uit. Zie [ Stap 4: verkrijg de recentste identiteitskaart van de publiekuitvoer baan ](#segment-export-id) voor instructies op hoe te om deze identiteitskaart te vinden. |

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
| `statusURL` | De status-URL van de activeringsstroom. U kunt de stroomvooruitgang volgen gebruikend de [ Dienst API van de Stroom ](../../sources/tutorials/api/monitor.md). |

{style="table-layout:auto"}

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

### API-foutcodes en specifieke berichten voor de API voor ad-hocactivering {#specific-error-messages}

Wanneer u de API voor ad-hocactivering gebruikt, kunt u foutberichten tegenkomen die specifiek zijn voor dit API-eindpunt. Bekijk de tabel om te begrijpen hoe u deze kunt aanpakken wanneer ze worden weergegeven.

| Foutbericht | Resolutie |
|---------|----------|
| Uitvoeren wordt al uitgevoerd voor publiek `segment ID` voor bestelling `dataflow ID` met run-id `flow run ID` | Dit foutbericht geeft aan dat er momenteel een ad-hocactiveringsstroom actief is voor een publiek. Wacht tot de taak is voltooid voordat u de activeringstaak opnieuw start. |
| Segmenten `<segment name>` maken geen deel uit van deze gegevensstroom of van het planningsbereik! | Dit foutbericht geeft aan dat het publiek dat u hebt geselecteerd om te activeren, niet is toegewezen aan de gegevensstroom of dat het activeringsschema dat voor het publiek is ingesteld, is verlopen of nog niet is gestart. Controleer of het publiek inderdaad is toegewezen aan de dataflow en controleer of het activeringsschema voor het publiek de huidige datum overlapt. |

## Verwante informatie {#related-information}

* [Verbinden met batchbestemmingen en gegevens activeren met de Flow Service API](/help/destinations/api/connect-activate-batch-destinations.md)
* [(Beta) Bestanden op aanvraag exporteren naar batchbestemmingen met behulp van de interface van Experience Platform](/help/destinations/ui/export-file-now.md)