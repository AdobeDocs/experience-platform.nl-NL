---
keywords: Experience Platform;doel-API;ad-hocactivering;segmenten ad-hoc activeren
solution: Experience Platform
title: (Bèta) Activeer publiekssegmenten via de API voor ad-hocactivering van het Experience Platform
description: Dit artikel illustreert de end-to-end workflow voor het activeren van segmenten via de API voor ad-hocactivering, inclusief de segmentatietaken die vóór activering plaatsvinden.
topic-legacy: tutorial
type: Tutorial
source-git-commit: 0c8fbaec9a592c9d5c20c077f31279f732ec2a0d
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 0%

---


# (Bèta) Activeer publiekssegmenten via de API voor ad-hocactivering van het Experience Platform

>[!IMPORTANT]
>
>De [!DNL ad-hoc activation API] in Platform wordt momenteel bèta gebruikt. De documentatie en de functionaliteit kunnen worden gewijzigd.

## Overzicht {#overview}

Met de API voor ad-hocactivering kunnen marketers publiekssegmenten programmatisch op een snelle en efficiënte manier naar doelen activeren voor situaties waarin onmiddellijke activering vereist is.

In het onderstaande diagram ziet u de end-to-end workflow voor het activeren van segmenten via de API voor ad-hocactivering, inclusief de segmentatietaken die elke 24 uur in Platform plaatsvinden.

![ad-hocactivering](../assets/api/ad-hoc-activation/ad-hoc-activation-overview.png)

>[!NOTE]
>
>Activering van ad-hocgroepen wordt alleen ondersteund door [batchbestandsgebaseerde doelen](../destination-types.md#file-based).

## Gebruiksscenario’s {#use-cases}

### Flash verkopen of promoties

Een online detailhandelaar bereidt een beperkte flitsverkoop voor en wil klanten op korte termijn op de hoogte brengen. Via de API voor ad-hocactivering van Experience Platforms kan het marketingteam publiekssegmenten op aanvraag exporteren en snel e-mails met speciale acties naar de klantenbasis verzenden.


### Actuele gebeurtenissen of het doorbreken van nieuws

Een hotel verwacht het hoogteweer in de komende dagen en het team wil de aankomende gasten snel informeren, zodat ze dienovereenkomstig kunnen plannen. Het marketingteam kan de API voor ad-hocactivering van Experience Platforms gebruiken om doelsegmenten op aanvraag te exporteren en de gasten op de hoogte te stellen.

### Integratie testen

IT-managers kunnen de API voor ad-hocactivering van Experience Platforms gebruiken om doelsegmenten op aanvraag te exporteren, zodat ze hun aangepaste integratie met Adobe Experience Platform kunnen testen en kunnen controleren of alles correct werkt.


## Guardrails {#guardrails}

Houd rekening met de volgende instructies wanneer u de API voor ad-hocactivering gebruikt.

* Elke ad-hocactiveringstaak kan maximaal 20 segmenten activeren. Als u probeert meer dan 20 segmenten per taak te activeren, mislukt de taak.
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
* x-gw-ims-org-id: `{IMS_ORG}`

De middelen in Experience Platform kunnen aan specifieke virtuele zandbakken worden geïsoleerd. In aanvragen voor Platform-API&#39;s kunt u de naam en id opgeven van de sandbox waarin de bewerking plaatsvindt. Dit zijn optionele parameters.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in Experience Platform raadpleegt u de [overzichtsdocumentatie van sandbox](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra media type kopbal:

* Inhoudstype: `application/json`

## Stap 3: Activeringsstroom maken in de gebruikersinterface van het Platform {#activation-flow}

Voordat u segmenten kunt activeren via de API voor ad-hocactivering, moet u eerst een activeringsstroom hebben geconfigureerd in de gebruikersinterface van het Platform voor het gekozen doel.

Dit omvat het ingaan van in het activeringswerkschema, het selecteren van uw segmenten, het vormen van een programma, en het activeren van hen.

Zie de volgende zelfstudie voor gedetailleerde instructies op hoe te om een activeringsstroom voor uw partijbestemmingen te vormen: [Gebruikersgegevens activeren om exportdoelen voor batchprofielen te maken](../ui/activate-batch-profile-destinations.md).

## Stap 4: Vraag de meest recente segment-exporttaak-id aan {#segment-export-id}

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
>U kunt maximaal 20 segmenten per ad-hocactiveringstaak activeren. Als u probeert meer segmenten te activeren, mislukt de taak.

### Verzoek

```shell
curl -X POST https://platform.adobe.io/data/core/activation/disflowprovider/adhocrun \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
   "exportId":[
      "exportId1"
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| <ul><li>`destinationId1`</li><li>`destinationId2`</li></ul> | De id&#39;s van de doelinstanties waarop u publiekssegmenten wilt activeren. |
| <ul><li>`segmentId1`</li><li>`segmentId2`</li><li>`segmentId3`</li></ul> | De id&#39;s van de publiekssegmenten die u wilt activeren voor de geselecteerde bestemming. |
| <ul><li>`exportId1`</li></ul> | De id die wordt geretourneerd in het antwoord van de [segmentexport](../../segmentation/api/export-jobs.md#retrieve-list) taak. Zie [Stap 4: Vraag de meest recente segment-exporttaak-id aan](#segment-export-id) voor instructies over hoe u deze id kunt vinden. |

### Antwoord

Een geslaagde reactie retourneert HTTP-status 200.

```shell
{
   "code":"DEST-ADH-200",
   "message":"Adhoc run triggered successfully",
   "statusURLs":[
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-1",
      "https://platform.adobe.io/data/core/activation/flowservice/runs?properties=providerRefId=ADH:segment-id-2"
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `code` | De API-antwoordcode. De succesvolle vraagwinst `DEST-ADH-200` (statuscode 200), terwijl een verkeerd opgemaakte code een waarde retourneert `DEST-ADH-400` (statuscode 400). |
| `message` | Het succes- of foutbericht dat door de API wordt geretourneerd. |
| `statusURLs` | De status-URL van de activeringsstroom. U kunt de voortgang van de flow volgen met de [Flow Service-API](../../sources/tutorials/api/monitor.md). |


## API-foutafhandeling

De eindpunten van SDK API van de bestemming volgen de algemene API van het Experience Platform foutenmeldingsbeginselen. Zie [API-statuscodes](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes) en [aanvragen, koptekstfouten](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors) in de gids voor het oplossen van problemen met Platforms.
