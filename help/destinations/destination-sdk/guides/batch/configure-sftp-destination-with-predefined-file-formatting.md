---
description: Leer hoe u Destination SDK gebruikt om een SFTP-bestemming te configureren met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnamen.
title: Configureer een SFTP-bestemming met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnamen.
exl-id: 6e0fe019-7fbb-48e4-9469-6cc7fc3cb6e4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '713'
ht-degree: 0%

---

# Een SFTP-bestemming configureren met vooraf gedefinieerde opties voor bestandsindeling en aangepaste configuratie van bestandsnaam

## Overzicht {#overview}

Deze pagina beschrijft hoe te om Destination SDK te gebruiken om een bestemming van SFTP met vooraf bepaalde, standaard [&#x200B; dossier het formatteren opties &#x200B;](configure-file-formatting-options.md) en een douane [&#x200B; dossier te vormen - noem configuratie &#x200B;](../../functionality/destination-configuration/batch-configuration.md#file-name-configuration).

Deze pagina toont alle configuratieopties beschikbaar voor bestemmingen SFTP. U kunt de configuraties bewerken die in de onderstaande stappen worden weergegeven, of u kunt desgewenst bepaalde onderdelen van de configuraties verwijderen.

Voor gedetailleerde beschrijvingen van de hieronder gebruikte parameters, zie [&#x200B; configuratieopties in Doelen SDK &#x200B;](../../functionality/configuration-options.md).

## Vereisten {#prerequisites}

Alvorens aan de hieronder geschetste stappen vooruit te gaan, te lezen gelieve de [&#x200B; Destination SDK begonnen &#x200B;](../../getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke de authentificatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

## Stap 1: Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Begin door het `/destination-server` eindpunt te gebruiken [&#x200B; creeer een server en dossierconfiguratie &#x200B;](../../authoring-api/destination-server/create-destination-server.md).

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe configuratie van de bestemmingsserver, die door de parameters wordt gevormd die in de lading worden verstrekt.
De nuttige lading omvat hieronder een generische configuratie SFTP, met vooraf bepaalde, standaard [&#x200B; CSV dossier het formatteren &#x200B;](../../functionality/destination-server/file-formatting.md) configuratieparameters die de gebruikers in het Experience Platform UI kunnen bepalen.

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "name": "SFTP destination with predefined CSV formatting options",
    "destinationServerType": "FILE_BASED_SFTP",
    "fileBasedSFTPDestination": {
        "hostname": {
            "templatingStrategy": "NONE",
            "value": "{{customerData.hostname}}"
        },
        "rootDirectory": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.remotePath}}"
        },
        "port": 22
    },
    "fileConfigurations": {
        "compression": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.compression}}"
        },
        "fileType": {
            "templatingStrategy": "PEBBLE_V1",
            "value": "{{customerData.fileType}}"
        },
        "csvOptions": {
            "quote": {
                "templatingStrategy": "NONE",
                "value": "\""
            },
            "quoteAll": {
                "templatingStrategy": "NONE",
                "value": "false"
            },
            "escape": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "escapeQuotes": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "header": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreLeadingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "ignoreTrailingWhiteSpace": {
                "templatingStrategy": "NONE",
                "value": "true"
            },
            "nullValue": {
                "templatingStrategy": "NONE",
                "value": ""
            },
            "dateFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd"
            },
            "timestampFormat": {
                "templatingStrategy": "NONE",
                "value": "yyyy-MM-dd'T':mm:ss[.SSS][XXX]"
            },
            "charToEscapeQuoteEscaping": {
                "templatingStrategy": "NONE",
                "value": "\\"
            },
            "emptyValue": {
                "templatingStrategy": "NONE",
                "value": ""
            }
        }
    }
}'
```

Een succesvolle reactie keert de nieuwe configuratie van de bestemmingsserver, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug. Sla deze waarde op zoals deze in de volgende stap wordt vereist.

## Stap 2: Doelconfiguratie maken {#create-destination-configuration}

Na het creëren van de bestemmingsserver en de dossier het formatteren configuratie in de vorige stap, kunt u het `/destinations` API eindpunt nu gebruiken om een bestemmingsconfiguratie tot stand te brengen.

Om de serverconfiguratie in [&#x200B; stap 1 &#x200B;](#create-server-file-configuration) aan deze bestemmingsconfiguratie aan te sluiten, vervang de `destinationServerId` waarde in het API verzoek hieronder met de waarde die wordt verkregen wanneer het creëren van uw bestemmingsserver in [&#x200B; stap 1 &#x200B;](#create-server-file-configuration).

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destinations
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destinations \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "name":"SFTP destination with predefined CSV formatting options",
   "description":"SFTP destination with predefined CSV formatting options",
   "status":"TEST",
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      },
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ],
   "customerEncryptionConfigurations":[
       
   ],
   "customerDataFields":[
      {
         "name":"remotePath",
         "title":"Root directory",
         "description":"Enter root directory",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      },
      {
         "name":"hostname",
         "title":"Hostname",
         "description":"Enter hostname",
         "type":"string",
         "isRequired":true,
         "readOnly":false,
         "hidden":false
      }
   ],
   "uiAttributes":{
      "documentationLink":"https://www.adobe.com/go/destinations-sftp-en",
      "category":"SFTP",
      "connectionType":"SFTP",
      "monitoringSupported":true,
      "flowRunsSupported":true,
      "frequency":"Batch"
   },
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{instanceID of your destination server}}"
      }
   ],
   "schemaConfig":{
      "profileRequired":true,
      "segmentRequired":true,
      "identityRequired":true
   },
   "batchConfig":{
      "allowMandatoryFieldSelection":true,
      "allowDedupeKeyFieldSelection":true,
      "defaultExportMode":"DAILY_FULL_EXPORT",
      "allowedExportMode":[
         "DAILY_FULL_EXPORT",
         "FIRST_FULL_THEN_INCREMENTAL"
      ],
      "allowedScheduleFrequency":[
         "DAILY",
         "EVERY_3_HOURS",
         "EVERY_6_HOURS",
         "EVERY_8_HOURS",
         "EVERY_12_HOURS",
         "ONCE"
      ],
      "defaultFrequency":"DAILY",
      "defaultStartTime":"00:00",
      "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
      "backfillHistoricalProfileData":true
   }
}'
```

Een succesvolle reactie keert de nieuwe bestemmingsconfiguratie, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug. Sla deze waarde op zoals nodig is als u meer HTTP-aanvragen moet indienen om de doelconfiguratie bij te werken.

## Stap 3: Verifieer de gebruikersinterface van het Experience Platform {#verify-ui}

Op basis van de bovenstaande configuraties wordt in de catalogus met Experience Platforms nu een nieuwe persoonlijke doelkaart weergegeven die u kunt gebruiken.

![&#x200B; opname die van het Scherm de pagina van de bestemmingscatalogus met een geselecteerde bestemmingskaart toont.](../../assets/guides/batch/destination-card.gif)

In de beelden en de opnamen hieronder, neem nota hoe de opties in het [&#x200B; activeringswerkschema voor op dossier-gebaseerde bestemmingen &#x200B;](/help/destinations/ui/activate-batch-profile-destinations.md) de opties aanpassen die u in de bestemmingsconfiguratie selecteerde.

Wanneer u details over de bestemming invult, ziet u hoe de velden omringd zijn de aangepaste gegevensvelden die u instelt in de configuratie.

>[!TIP]
>
>De orde waarin u de gebieden van douanegegevens aan de bestemmingsconfiguratie toevoegt wordt niet weerspiegeld in UI. De aangepaste gegevensvelden worden altijd weergegeven in de volgorde die wordt weergegeven in de onderstaande schermopname.

![&#x200B; vul bestemmingsdetails &#x200B;](../../assets/guides/batch/file-configuration-options.gif) in

Wanneer u exportintervallen wilt plannen, ziet u hoe de velden die u opgeeft, de velden zijn die u instelt in de `batchConfig` -configuratie.
![&#x200B; de uitvoer die opties plannen &#x200B;](../../assets/guides/batch/file-export-scheduling.png)

Wanneer u de opties voor de configuratie van bestandsnamen weergeeft, ziet u hoe de weergegeven velden de `filenameConfig` -opties vertegenwoordigen die u instelt in de configuratie.
![&#x200B; filename configuratieopties &#x200B;](../../assets/guides/batch/file-naming-options.gif)

Als u om het even welke hierboven vermelde gebieden wilt aanpassen, herhaal [&#x200B; stappen één &#x200B;](#create-server-file-configuration) en [&#x200B; twee &#x200B;](#create-destination-configuration) om de configuraties volgens uw behoeften te wijzigen.

## Stap 4: (Optioneel) Publish uw bestemming {#publish-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Na het vormen van uw bestemming, gebruik [&#x200B; bestemmings het publiceren API &#x200B;](../../publishing-api/create-publishing-request.md) om uw configuratie voor overzicht voor te leggen aan Adobe.

## Stap 5: (Optioneel) Documenteer uw bestemming {#document-destination}

>[!NOTE]
>
>Deze stap wordt niet vereist als u een privé bestemming voor uw eigen gebruik creeert, en kijkt niet om het in de catalogus van bestemmingen voor andere te gebruiken klanten te publiceren.

Als u een Onafhankelijke Verkoper van de Software (ISV) of Integrator van het Systeem (SI) creërend a [&#x200B; geproduceerde integratie &#x200B;](../../overview.md#productized-custom-integrations) bent, gebruik het [&#x200B; zelfbedienings documentatieproces &#x200B;](../../docs-framework/documentation-instructions.md) om een pagina van de productdocumentatie voor uw bestemming in de [&#x200B; catalogus van de bestemmingen van het Experience Platform &#x200B;](../../../catalog/overview.md) tot stand te brengen.

## Volgende stappen {#next-steps}

Door dit artikel te lezen, weet u nu hoe te om een bestemming van douaneSFTP te schrijven door Destination SDK te gebruiken. Daarna, kan uw team het [&#x200B; activeringswerkschema voor op dossier-gebaseerde bestemmingen &#x200B;](../../../ui/activate-batch-profile-destinations.md) gebruiken om gegevens naar de bestemming uit te voeren.
