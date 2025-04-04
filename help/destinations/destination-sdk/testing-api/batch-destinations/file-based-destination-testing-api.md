---
description: Deze pagina verklaart hoe te om het /testing/destinationInstance API eindpunt te gebruiken om te testen als uw op dossier-gebaseerde bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.
title: Bestandsgebaseerde bestemming testen met voorbeeldprofielen
exl-id: 75f76aec-245b-4f07-8871-c64a710db9f6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# Bestandsgebaseerde bestemming testen met voorbeeldprofielen

## Overzicht {#overview}

Deze pagina verklaart hoe te om het `/testing/destinationInstance` API eindpunt te gebruiken om te testen als uw op dossier-gebaseerde bestemming correct wordt gevormd en om de integriteit van gegevensstromen aan uw gevormde bestemming te verifiëren.

U kunt verzoeken aan het het testen eindpunt met of zonder [ steekproefprofielen ](file-based-sample-profile-generation-api.md) aan de vraag toe te voegen. Als u geen profielen verzendt op de aanvraag, genereert de API automatisch een voorbeeldprofiel en voegt deze toe aan de aanvraag.

De automatisch gegenereerde voorbeeldprofielen bevatten algemene gegevens. Als u uw bestemming met douane, intuïtievere profielgegevens wilt testen, gebruik [ de generatie API van het steekproefprofiel ](file-based-sample-profile-generation-api.md) om een steekproefprofiel te produceren, dan zijn reactie aan te passen en het te omvatten in het verzoek aan het `/testing/destinationInstance` eindpunt.

## Aan de slag {#getting-started}

Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](../../getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan API met succes te maken, met inbegrip van hoe te om de vereiste toestemming van de bestemmings authoring en vereiste kopballen te verkrijgen.

## Vereisten {#prerequisites}

Voordat u het eindpunt `/testing/destinationInstance` kunt gebruiken, moet u controleren of aan de volgende voorwaarden is voldaan:

* U hebt een bestaande op dossier-gebaseerde bestemming die door Destination SDK wordt gecreeerd en u kunt het in uw [ doelcatalogus ](../../../ui/destinations-workspace.md) zien.
* U hebt ten minste één activeringsstroom voor uw doel gemaakt in de gebruikersinterface van Experience Platform.
* Als u de API-aanvraag met succes wilt uitvoeren, hebt u de id van de doelinstantie nodig die overeenkomt met de doelinstantie die u wilt testen. Krijg bestemmingsidentiteitskaart die u in de API vraag, van URL zou moeten gebruiken, wanneer het doorbladeren van een verbinding met uw bestemming in Experience Platform UI.

  ![ beeld UI die hoe te om bestemmingsidentiteitskaart van URL te krijgen toont.](../../assets/testing-api/get-destination-instance-id.png)
* *Facultatief*: Als u uw bestemmingsconfiguratie met een steekproefprofiel wilt testen dat aan de API vraag wordt toegevoegd, gebruik het [ /sample-profiles ](file-based-sample-profile-generation-api.md) eindpunt om een steekproefprofiel te produceren dat op uw bestaand bronschema wordt gebaseerd. Als u geen voorbeeldprofiel opgeeft, genereert de API er een en retourneert deze in de reactie.

## Test uw bestemmingsconfiguratie zonder profielen aan de vraag toe te voegen {#test-without-adding-profiles}

**API formaat**

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
| `{DESTINATION_INSTANCE_ID}` | De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [ eerste vereisten ](#prerequisites) sectie voor details op hoe te om deze identiteitskaart te verkrijgen. |

**Reactie**

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
| `activations` | Retourneert de gebruikers-id en de flow-run-id voor elk geactiveerd publiek. Het aantal activeringsitems (en de bijbehorende gegenereerde bestanden) is gelijk aan het aantal soorten publiek dat is toegewezen aan de doelinstantie. <br><br> Voorbeeld: als u twee soorten publiek aan de doelinstantie toewijst, bevat de `activations` -array twee items. Elk geactiveerd publiek komt overeen met één geëxporteerd bestand. |
| `results` | Keert bestemmingsidentiteitskaart en de stroom in werking gestelde IDs terug die u kunt gebruiken om [ resultaten API ](file-based-destination-results-api.md) te roepen, om de integratie verder te testen. |
| `inputProfiles` | Retourneert de voorbeeldprofielen die automatisch door de API worden gegenereerd. |

{style="table-layout:auto"}

## Test uw bestemmingsconfiguratie met profielen die aan de vraag worden toegevoegd {#test-with-added-profiles}

Om uw bestemming met douane, meer intuïtieve profielgegevens te testen, kunt u de reactie aanpassen die van het [ wordt verkregen/steekproef-profielen ](file-based-sample-profile-generation-api.md) eindpunt met waarden van uw keus, en het douaneprofiel in het verzoek aan het `/testing/destinationInstance` eindpunt omvatten.

**API formaat**

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
| `{DESTINATION_INSTANCE_ID}` | De doel-instantie-id van het doel dat u test.  De id van de doelinstantie waarvoor u voorbeeldprofielen genereert. Zie de [ eerste vereisten ](#prerequisites) sectie voor details op hoe te om deze identiteitskaart te verkrijgen. |
| `profiles` | Array die een of meerdere profielen kan bevatten. Gebruik het [ eindpunt van steekproefAPI van het profiel ](file-based-sample-profile-generation-api.md) om profielen te produceren in deze API vraag te gebruiken. |

**Reactie**

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
| `activations` | Retourneert de gebruikers-id en de flow-run-id voor elk geactiveerd publiek. Het aantal activeringsitems (en de bijbehorende gegenereerde bestanden) is gelijk aan het aantal soorten publiek dat is toegewezen aan de doelinstantie. <br><br> Voorbeeld: als u twee soorten publiek aan de doelinstantie toewijst, bevat de `activations` -array twee items. Elk geactiveerd publiek komt overeen met één geëxporteerd bestand. |
| `results` | Keert bestemmingsidentiteitskaart en de stroom in werking gestelde IDs terug die u kunt gebruiken om [ resultaten API ](file-based-destination-results-api.md) te roepen, om de integratie verder te testen. |
| `inputProfiles` | Retourneert de aangepaste voorbeeldprofielen die u hebt doorgegeven in de API-aanvraag. |

## API-foutafhandeling {#api-error-handling}

Destination SDK API-eindpunten volgen de algemene beginselen van Experience Platform API-foutberichten. Verwijs naar [ API statuscodes ](../../../../landing/troubleshooting.md#api-status-codes) en [ de fouten van de verzoekkopbal ](../../../../landing/troubleshooting.md#request-header-errors) in de het oplossen van problemengids van Experience Platform.

## Volgende stappen

Na het lezen van dit document, weet u nu hoe te om uw op dossier-gebaseerde bestemmingsconfiguratie te testen.

Als u een geldige API-reactie hebt ontvangen, werkt de bestemming correct. Als u meer gedetailleerde informatie over uw activeringsstroom wilt zien, kunt u het `results` bezit van de reactie op [ mening gedetailleerde activeringsresultaten ](file-based-destination-results-api.md) gebruiken.

Als u een openbare bestemming bouwt, kunt u [ uw bestemmingsconfiguratie ](../../guides/submit-destination.md) aan Adobe voor overzicht nu voorleggen.
