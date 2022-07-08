---
description: Deze pagina verklaart hoe te om het /testing/destinationInstance API eindpunt te gebruiken om te testen als uw op dossier-gebaseerde bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.
title: Bestandsgebaseerde bestemming testen met voorbeeldprofielen
source-git-commit: fa092e4d1828d9ecd5bc98e3f225fa377f38065f
workflow-type: tm+mt
source-wordcount: '830'
ht-degree: 1%

---


# Bestandsgebaseerde bestemming testen met voorbeeldprofielen

## Overzicht {#overview}

Op deze pagina wordt uitgelegd hoe u de `/testing/destinationInstance` API eindpunt om te testen als uw op dossier-gebaseerde bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.

U kunt verzoeken aan het testende eindpunt met of zonder het toevoegen van [voorbeeldprofielen](file-based-sample-profile-generation-api.md) aan de vraag. Als u geen profielen verzendt op de aanvraag, genereert de API automatisch een voorbeeldprofiel en voegt deze toe aan de aanvraag.

De automatisch gegenereerde voorbeeldprofielen bevatten algemene gegevens. Als u uw doel wilt testen met aangepaste, intuïtievere profielgegevens, gebruikt u de opdracht [API voor genereren van voorbeeldprofiel](file-based-sample-profile-generation-api.md) om een steekproefprofiel te produceren, dan zijn reactie aan te passen en het op te nemen in het verzoek aan `/testing/destinationInstance` eindpunt.

## Aan de slag {#getting-started}

Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan API te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings creatie en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u de `/testing/destinationInstance` aan, zorg ervoor u aan de volgende voorwaarden voldoet:

* U hebt een bestaande op dossier-gebaseerde bestemming die door de Destination SDK wordt gecreeerd en u kunt het in uw zien [doelcatalogus](../ui/destinations-workspace.md).
* U hebt minstens één activeringsstroom voor uw bestemming in de gebruikersinterface van het Experience Platform gemaakt.
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Platform UI.

   ![UI-afbeelding die laat zien hoe u de id van de doelinstantie opgehaald kunt krijgen via de URL.](assets/get-destination-instance-id.png)
* *Optioneel*: Als u uw bestemmingsconfiguratie met een steekproefprofiel wilt testen dat aan de API vraag wordt toegevoegd, gebruik [/sample-profiles](file-based-sample-profile-generation-api.md) eindpunt om een steekproefprofiel te produceren dat op uw bestaand bronschema wordt gebaseerd. Als u geen voorbeeldprofiel opgeeft, genereert de API er een en retourneert deze in de reactie.

## Test uw bestemmingsconfiguratie zonder profielen aan de vraag toe te voegen {#test-without-adding-profiles}

**API-indeling**

```http
POST /authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Verzoek**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

| Padparameters | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [voorwaarden](#prerequisites) voor meer informatie over het verkrijgen van deze id. |

**Antwoord**

Een succesvolle reactie keert HTTP status 200 samen met de antwoordlading terug.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"john.smith@abc.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"crmid-P1A7l"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"string",
               "lastName":"string"
            }
         }
      }
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `activations` | Retourneert de segment-id en de flow-run-id voor elk geactiveerd segment. Het aantal activeringsitems (en de bijbehorende gegenereerde bestanden) is gelijk aan het aantal segmenten dat is toegewezen aan de doelinstantie. <br><br> Voorbeeld: Als u twee segmenten aan de bestemmingsinstantie in kaart bracht, `activations` array bevat twee items. Elk geactiveerd segment komt overeen met één geëxporteerd bestand. |
| `results` | Retourneert de ID van de doelinstantie en de ID&#39;s van de flowuitvoering die u kunt gebruiken om de [resultatenAPI](file-based-destination-results-api.md)om de integratie verder te testen. |
| `inputProfiles` | Retourneert de voorbeeldprofielen die automatisch door de API worden gegenereerd. |

{style=&quot;table-layout:auto&quot;}

## Test uw bestemmingsconfiguratie met profielen die aan de vraag worden toegevoegd {#test-with-added-profiles}

Als u uw bestemming wilt testen met aangepaste, intuïtievere profielgegevens, kunt u de reactie aanpassen die wordt verkregen via het dialoogvenster [/sample-profiles](file-based-sample-profile-generation-api.md) eindpunt met waarden van uw keus, en omvat het douaneprofiel in het verzoek aan `/testing/destinationInstance` eindpunt.

**API-indeling**

```http
POST  /testing/destinationInstance/{DESTINATION_INSTANCE_ID}
```

**Verzoek**

```shell
curl -X POST 'https://platform.adobe.io/data/core/activation/authoring/testing/destinationInstance/{DESTINATION_INSTANCE_ID}' 
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
 {
   "profiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}'
```

| Parameter | Beschrijving |
| -------- | ----------- |
| `{DESTINATION_INSTANCE_ID}` | De doel-instantie-id van het doel dat u test.  De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [voorwaarden](#prerequisites) voor meer informatie over het verkrijgen van deze id. |
| `profiles` | Array die een of meerdere profielen kan bevatten. Gebruik de [API-eindpunt van voorbeeldprofiel](file-based-sample-profile-generation-api.md) om profielen te genereren voor gebruik in deze API-aanroep. |

**Antwoord**

Een succesvolle reactie keert HTTP status 200 samen met de antwoordlading terug.

```json
{
   "activations":[
      {
         "segment":"6fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"81150d76-7909-46b6-83f4-fc855a92de07"
      },
      {
         "segment":"5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b",
         "flowRun":"4706780a-2ab3-4d33-8c76-7c87fd318cd8"
      }
   ],
   "results":"/authoring/testing/destinationInstance/fd3449fb-b929-45c8-9f3d-06b9d6aac328/results?flowRunIds=4706780a-2ab3-4d33-8c76-7c87fd318cd8,81150d76-7909-46b6-83f4-fc855a92de07",
   "inputProfiles":[
      {
         "segmentMembership":{
            "ups":{
               "fea8d394-5a8c-4cea-bebc-df020ce37f5c":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211895Z",
                  "status":"realized"
               },
               "5fa55d3a-18e1-4f65-95ed-ac8fdb03b45b":{
                  "lastQualificationTime":"2022-01-13T11:33:28.211893Z",
                  "status":"realized"
               }
            }
         },
         "personalEmail":{
            "address":"michaelsmith@example.com"
         },
         "identityMap":{
            "crmid":[
               {
                  "id":"Custom CRM ID"
               }
            ]
         },
         "person":{
            "name":{
               "firstName":"Michael",
               "lastName":"Smith"
            }
         }
      }
   ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `activations` | Retourneert de segment-id en de flow-run-id voor elk geactiveerd segment. Het aantal activeringsitems (en de bijbehorende gegenereerde bestanden) is gelijk aan het aantal segmenten dat is toegewezen aan de doelinstantie. <br><br> Voorbeeld: Als u twee segmenten aan de bestemmingsinstantie in kaart bracht, `activations` array bevat twee items. Elk geactiveerd segment komt overeen met één geëxporteerd bestand. |
| `results` | Retourneert de ID van de doelinstantie en de ID&#39;s van de flowuitvoering die u kunt gebruiken om de [resultatenAPI](file-based-destination-results-api.md)om de integratie verder te testen. |
| `inputProfiles` | Retourneert de aangepaste voorbeeldprofielen die u hebt doorgegeven in de API-aanvraag. |

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene API-foutberichtbeginselen voor Experience Platforms. Zie [API-statuscodes](../../landing/troubleshooting.md#api-status-codes) en [aanvragen, koptekstfouten](../../landing/troubleshooting.md#request-header-errors) in de gids voor het oplossen van problemen met Platforms.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om uw op dossier-gebaseerde bestemmingsconfiguratie te testen.

Als u een geldige API-reactie hebt ontvangen, werkt de bestemming correct. Als u meer gedetailleerde informatie over uw activeringsstroom wilt zien, kunt u de `results` eigenschap van het antwoord op [gedetailleerde activeringsresultaten weergeven](file-based-destination-results-api.md).

Als u een openbare bestemming bouwt, kunt u nu [Verzend uw doelconfiguratie](../destination-sdk/submit-destination.md) naar Adobe ter controle.