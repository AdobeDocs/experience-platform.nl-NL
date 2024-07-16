---
description: Deze pagina verklaart hoe te om het /testing/destinationInstance API eindpunt te gebruiken om de volledige details van uw testende resultaten te bekijken. Dit API eindpunt keert het zelfde resultaat terug zoals u zou verkrijgen wanneer het gebruiken van de Dienst API van de Stroom om dataflows te controleren.
title: Gedetailleerde activeringsresultaten weergeven
exl-id: a7b27beb-825e-47fd-8939-f499c3298f68
source-git-commit: 9ac6b075af3805da4dad0dd6442d026ae96ab5c7
workflow-type: tm+mt
source-wordcount: '545'
ht-degree: 1%

---

# Gedetailleerde activeringsresultaten weergeven {#view-test-results}

## Overzicht {#overview}

Op deze pagina wordt uitgelegd hoe u het API-eindpunt van `/testing/destinationInstance` gebruikt om de volledige details van de testresultaten voor bestandsgebaseerde doelen weer te geven.

Als u reeds [ uw bestemming ](file-based-destination-testing-api.md) hebt getest en een geldige API reactie hebt ontvangen, werkt uw bestemming correct.

Als u meer gedetailleerde informatie over uw activeringsstroom wilt zien, kunt u het `results` bezit van de [ bestemming gebruiken testende ](file-based-destination-testing-api.md) eindpuntreactie, zoals hieronder verder beschreven.

>[!NOTE]
>
>Dit API eindpunt keert het zelfde resultaat terug zoals u wanneer het gebruiken van de [ Dienst API van de Stroom ](../../../api/update-destination-dataflows.md) zou verkrijgen om dataflows te controleren.

## Aan de slag {#getting-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u het eindpunt `/testing/destinationInstance` kunt gebruiken, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een bestaande op dossier-gebaseerde bestemming die door de Destination SDK wordt gecreeerd en u kunt het in uw [ catalogus van bestemmingen ](../../../ui/destinations-workspace.md) zien.
* U hebt minstens één activeringsstroom voor uw bestemming in de gebruikersinterface van het Experience Platform gemaakt.
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Platform UI.

  ![ beeld UI die hoe te om bestemmingsidentiteitskaart van URL te krijgen toont.](../../assets/testing-api/get-destination-instance-id.png)
* U hebt eerder [ uw bestemmingsconfiguratie ](file-based-destination-testing-api.md) getest, en een geldige API reactie ontvangen, die a `results` bezit omvat. U gebruikt deze `results` -waarde om de bestemming verder te testen.

## Gedetailleerde resultaten voor doeltests weergeven {#test-activation-results}

Zodra u [ uw bestemmingsconfiguratie ](file-based-destination-testing-api.md) hebt bevestigd, kunt u gedetailleerde activeringsresultaten bekijken door een verzoek van de GET tot het `authoring/testing/destinationInstance/` eindpunt te richten en bestemmingsidentiteitskaart van de bestemming te verstrekken die u, en de stroom in werking stelt IDs van het geactiveerde publiek test.

U kunt volledige API URL vinden die u in het `results` bezit moet gebruiken dat in de [ reactie van de bestemmings testende vraag ](file-based-destination-testing-api.md) is teruggekeerd.

**API formaat**

```http
GET /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}/results?flowRunIds=id1,id2
```

| Padparameters | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [ eerste vereisten ](#prerequisites) sectie voor details op hoe te om deze identiteitskaart te verkrijgen. |

| Parameters van queryreeks | Beschrijving |
| -------- | ----------- |
| `flowRunIds` | De flow-id&#39;s die overeenkomen met het geactiveerde publiek. U kunt de stroom in werking stellen IDs in het `results` bezit vinden dat in de [ reactie van de bestemmings testende vraag ](file-based-destination-testing-api.md) is teruggekeerd. |

**Verzoek**

```shell
curl -X GET 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=30d34875-e7ba-4520-ab6e-5705e01dfb16,86c00ad7-443c-459a-855d-0e8cbee43c4f,12305c58-42a9-4230-8fad-1661ee49cb70' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Het antwoord bevat de volledige details van de activeringsstroom. U kunt de zelfde reactie verkrijgen door de [ Dienst API van de Stroom ](../../../api/update-destination-dataflows.md) te roepen om dataflows te controleren.

```json
{
   "items":[
      {
         "id":"18efd5d2-40ae-4f5c-afd1-37a39a45183a",
         "flowId":"a02071ad-f3a4-496c-a2b1-468812301d5d",
         "flowSpec":{
            "id":"25473b67-0801-418a-ab49-ed74ebf88137",
            "version":"1.0"
         },
         "metrics":{
            "durationSummary":{
               "startedAtUTC":1646652235124,
               "completedAtUTC":1646652270439
            },
            "latencySummary":null,
            "sizeSummary":{
               "inputBytes":122,
               "outputBytes":122
            },
            "recordSummary":{
               "inputRecordCount":1,
               "outputRecordCount":1,
               "createdRecordCount":1,
               "skippedRecordCount":0,
               "sourceSummaries":[
                  {
                     "id":"76e4b969-9700-4557-8330-0a8390afbdde",
                     "entitySummaries":[
                        {
                           "inputRecordCount":1,
                           "skippedRecordCount":0,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ],
               "targetSummaries":[
                  {
                     "id":"b43607b6-0dca-43b3-a0bc-ecdea4fa6aa9",
                     "entitySummaries":[
                        {
                           "outputRecordCount":1,
                           "createdRecordCount":1,
                           "id":"segment:4326c566-f81c-4ab0-8a80-9e741a5d0b1f"
                        }
                     ]
                  }
               ]
            },
            "fileSummary":{
               "inputFileCount":1,
               "outputFileCount":1
            },
            "statusSummary":{
               "status":"success"
            }
         },
         "activities":[
            {
               "id":"c4f238e3-7334-4933-8b56-64d7ea43ea54",
               "name":"Activation Batch XdmProcessor Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652235124,
                  "completedAtUTC":1646652255157
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "inputBytes":122,
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "inputFileCount":1,
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     "incremental.batchId":"",
                     "snapshot.batchId":"",
                     "snapshot.datasetId":"",
                     "incremental.datasetId":""
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            },
            {
               "id":"51d82b36-6b8f-11eb-9439-0242ac130002",
               "name":"Activation Batch Publisher Activity",
               "updatedAtUTC":0,
               "durationSummary":{
                  "startedAtUTC":1646652270326,
                  "completedAtUTC":1646652270439
               },
               "latencySummary":{
                  
               },
               "sizeSummary":{
                  "outputBytes":122
               },
               "recordSummary":{
                  "inputRecordCount":1,
                  "outputRecordCount":1,
                  "createdRecordCount":1,
                  "skippedRecordCount":0
               },
               "fileSummary":{
                  "outputFileCount":1
               },
               "statusSummary":{
                  "status":"success",
                  "extensions":{
                     
                  }
               },
               "sourceInfo":null,
               "targetInfo":null
            }
         ],
         "predecessors":null
      }
   ],
   "_links":{
      
   }
}
```

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van het Platform.

## Volgende stappen

Nadat u dit document hebt gelezen, weet u nu hoe u de doelconfiguratie op basis van een bestand kunt testen en alle details van de activeringsresultaten kunt bekijken.

Als u een openbare bestemming bouwt, kunt u [ uw bestemmingsconfiguratie ](../../guides/submit-destination.md) aan Adobe voor overzicht nu voorleggen.
