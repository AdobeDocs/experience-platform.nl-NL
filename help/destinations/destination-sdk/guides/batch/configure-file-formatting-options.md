---
description: Opties voor bestandsindeling configureren voor op bestanden gebaseerde doelen
title: Leer hoe u Destination SDK gebruikt om opties voor bestandsindeling voor op bestanden gebaseerde doelen te configureren.
exl-id: e61c7989-1123-4b3b-9781-a6097cd0e2b4
source-git-commit: d47c82339afa602a9d6914c1dd36a4fc9528ea32
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Opties voor bestandsindeling configureren voor op bestanden gebaseerde doelen

## Overzicht {#overview}

Met Destination SDK kunt u de opties voor opmaak en compressie van geëxporteerde bestanden uitgebreid aanpassen aan de vereisten in de opslagruimte.

Deze pagina beschrijft hoe te om Destination SDK te gebruiken om dossier het formatteren opties voor op dossier-gebaseerde bestemmingen te vormen.

## Vereisten {#prerequisites}

Alvorens aan de hieronder geschetste stappen vooruit te gaan, te lezen gelieve de [ Destination SDK begonnen ](../../getting-started.md) pagina voor informatie over het verkrijgen van de noodzakelijke de authentificatiegeloofsbrieven van de Adobe I/O en andere eerste vereisten om met Destination SDK APIs te werken.

Adobe raadt u ook aan de volgende documentatie te lezen en bekend te maken voordat u verdergaat:

* Elke beschikbare dossier het formatteren optie wordt gedocumenteerd bij lengte in de [ dossier het formatteren configuratie ](../../functionality/destination-server/file-formatting.md) sectie.
* Voltooi stappen om [ een op dossier-gebaseerde bestemming ](../../guides/configure-file-based-destination-instructions.md) te vormen gebruikend Destination SDK.

## Een server- en bestandsconfiguratie maken {#create-server-file-configuration}

Begin door het `/destination-server` eindpunt te gebruiken om te bepalen welke dossier het formatteren configuratieopties u opstelling voor de uitgevoerde dossiers wilt.

Hieronder ziet u een voorbeeld van een doelserverconfiguratie voor een [!DNL Amazon S3] -doel, met verschillende opties voor bestandsindeling geselecteerd.

**API formaat**

```http
POST platform.adobe.io/data/core/activation/authoring/destination-servers
```

**Verzoek**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/destination-server \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
{
  "name": "Amazon S3 Server with several CSV Options",
  "destinationServerType": "FILE_BASED_S3",
  "fileBasedS3Destination": {
    "bucket": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.bucket}}"
    },
    "path": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.path}}"
    }
  },
  "fileConfigurations": {
    "compression": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{% if customerData contains 'compression' and customerData.compression is not empty %}{{customerData.compression}}{% else %}NONE{% endif %}"
    },
    "fileType": {
      "templatingStrategy": "PEBBLE_V1",
      "value": "{{customerData.fileType}}"
    },
    "csvOptions": {
      "sep": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'delimiter' %}{{customerData.csvOptions.delimiter}}{% else %},{% endif %}"
      },
      "quote": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'quote' %}{{customerData.csvOptions.quote}}{% else %}\"{% endif %}"
      },
      "escape": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'escape' %}{{customerData.csvOptions.escape}}{% else %}\\{% endif %}"
      },
      "nullValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'nullValue' %}{{customerData.csvOptions.nullValue}}{% else %}null{% endif %}"
      },
      "emptyValue": {
        "templatingStrategy": "PEBBLE_V1",
        "value": "{% if customerData contains 'csvOptions' and customerData.csvOptions contains 'emptyValue' %}{{customerData.csvOptions.emptyValue}}{% else %}{% endif %}"
      }
    }
  }
}
}'
```

## De opties voor bestandsindeling toevoegen aan de doelconfiguratie {#create-destination-configuration}

>[!TIP]
>
>**verifieer het Experience Platform UI**. Als u de opties voor bestandsindeling configureert met de configuraties die in de onderstaande secties worden getoond, moet u de interface van het Experience Platform controleren op de manier waarop deze opties worden weergegeven.

Nadat u de gewenste opties voor bestandsindeling in de vorige stap hebt toegevoegd aan de configuratie voor de doelserver en bestandsindeling, kunt u nu het API-eindpunt `/destinations` gebruiken om de gewenste velden als gegevensvelden van de klant toe te voegen aan de doelconfiguratie.

>[!IMPORTANT]
>
>Deze stap is optioneel en bepaalt alleen welke opties voor bestandsindeling gebruikers in de gebruikersinterface van het Experience Platform moeten krijgen. Als u opstellings dossier formatterende opties niet als gebieden van klantengegevens formatteert, zal de dossieruitvoer met de standaardwaarden te werk gaan die in de [ worden gevormd server en dossierconfiguratie ](#create-server-file-configuration).

In deze stap kunt u de weergegeven opties groeperen in elke gewenste volgorde, u kunt aangepaste groepen, vervolgkeuzelijsten en voorwaardelijke groepen maken op basis van de geselecteerde bestandstypen. Al deze instellingen worden weergegeven in de opname en in de volgende secties.

![ het registreren van het scherm die diverse dossier het formatteren opties voor partijdossiers tonen.](../../assets/guides/batch/file-formatting-options.gif)

### De opties voor de bestandsindeling bepalen {#ordering}

De volgorde waarin u de opmaakopties voor bestanden toevoegt als gegevensvelden van klanten in de doelconfiguratie, wordt weerspiegeld in de gebruikersinterface. De onderstaande configuratie wordt bijvoorbeeld dienovereenkomstig weergegeven in de gebruikersinterface, waarbij de opties worden weergegeven in de volgorde **[!UICONTROL Delimiter]**, **[!UICONTROL Quote Character]**, **[!UICONTROL Escape Character]**, **[!UICONTROL Empty Value]**, **[!UICONTROL Null Value]** .

![ Beeld dat de orde van dossier het formatteren opties in Experience Platform UI toont.](../../assets/guides/batch/file-formatting-order.png)

```json
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\u0000",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": ""
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
```

### Groepeer de opties voor bestandsindeling {#grouping}

U kunt meerdere opmaakopties voor bestanden groeperen in één sectie. Wanneer u de verbinding met het doel instelt in de gebruikersinterface, kan de gebruiker een visuele groepering van vergelijkbare velden zien en hiervan profiteren.

Hiertoe maakt u met `"type": "object"` de groep en verzamelt u de gewenste opties voor bestandsindeling in een `properties` -parameter, zoals in het onderstaande voorbeeld wordt getoond, waar de groepering **[!UICONTROL CSV Options]** wordt gemarkeerd.

```json {line-numbers="true" start-number="100" highlight="106-128"}
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![ Beeld die de opties tonen CSV groeperen in UI.](../../assets/guides/batch/file-formatting-grouping.png)

### Vervolgkeuzekiezers maken voor de opties voor de bestandsindeling {#dropdown-selectors}

In situaties waarin u gebruikers de keuze wilt laten tussen verschillende opties, bijvoorbeeld met welk teken de velden in CSV-bestanden worden afgebakend, kunt u vervolgkeuzelijsten toevoegen aan de gebruikersinterface.

Hiervoor gebruikt u het `namedEnum` -object zoals hieronder wordt weergegeven en configureert u een `default` -waarde voor de opties die de gebruiker kan selecteren.

```json {line-numbers="true" start-number="100" highlight="114-124"}
[...]
"customerDataFields":[
[...]
{
   "name":"csvOptions",
   "title":"CSV Options",
   "description":"Select your CSV options",
   "type":"object",
   "properties":[
      {
         "name":"delimiter",
         "title":"Delimiter",
         "description":"Select your Delimiter",
         "type":"string",
         "isRequired":false,
         "default":",",
         "namedEnum":[
            {
               "name":"Comma (,)",
               "value":","
            },
            {
               "name":"Tab (\\t)",
               "value":"\t"
            }
         ],
         "readOnly":false,
         "hidden":false
      },
      [...]
   ]
}
[...]
]
```

![ het registreren van het Scherm die een voorbeeld van dropdown selecteurs tonen die met de hierboven getoonde configuratie worden gecreeerd.](../../assets/guides/batch/dropdown-options-file-formatting.gif)

### Voorwaardelijke opties voor bestandsindeling maken {#conditional-options}

U kunt opties voor voorwaardelijke bestandsindeling maken, die alleen in de activeringsworkflow worden weergegeven wanneer de gebruiker een bepaald bestandstype selecteert om te exporteren. In de onderstaande configuratie wordt bijvoorbeeld een voorwaardelijke groepering gemaakt voor CSV-bestandsopties. De CSV-bestandsopties worden alleen weergegeven wanneer de gebruiker CSV selecteert als het gewenste bestandstype voor exporteren.

Als u een veld als voorwaardelijk wilt instellen, gebruikt u de parameter `conditional` zoals hieronder wordt weergegeven:

```json
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            }
```

In een bredere context ziet u het veld `conditional` dat wordt gebruikt in de doelconfiguratie hieronder, naast de `fileType` tekenreeks en het object `csvOptions` waarin deze is gedefinieerd.

```json
        {
            "name": "fileType",
            "title": "File Type",
            "description": "Select your file type",
            "type": "string",
            "isRequired": true,
            "enum": [
                "PARQUET",
                "CSV",
                "JSON"
            ],
            "readOnly": false,
            "hidden": false
        },
        {
            "name": "csvOptions",
            "title": "CSV Options",
            "description": "Select your CSV options",
            "type": "object",
            "conditional": {
                "field": "fileType",
                "operator": "EQUALS",
                "value": "CSV"
            },            
            "properties": [
                {
                    "name": "delimiter",
                    "title": "Delimiter",
                    "description": "Select your Delimiter",
                    "type": "string",
                    "isRequired": false,
                    "default": ",",
                    "namedEnum": [
                        {
                            "name": "Comma (,)",
                            "value": ","
                        },
                        {
                            "name": "Tab (\\t)",
                            "value": "\t"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "quote",
                    "title": "Quote Character",
                    "description": "Select your Quote character",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Double Quotes (\")",
                            "value": "\""
                        },
                        {
                            "name":"Null Character (\u0000)",
                            "value": "\u0000"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "escape",
                    "title": "Escape Character",
                    "description": "Select your Escape character",
                    "type": "string",
                    "isRequired": false,
                    "default": "\\",
                    "namedEnum": [
                        {
                            "name": "Back Slash (\\)",
                            "value": "\\"
                        },
                        {
                            "name": "Single Quote (')",
                            "value": "'"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "emptyValue",
                    "title": "Empty Value",
                    "description": "Select the output value of blank fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                },
                {
                    "name": "nullValue",
                    "title": "Null Value",
                    "description": "Select the output value of 'null' fields",
                    "type": "string",
                    "isRequired": false,
                    "default": "null",
                    "namedEnum": [
                        {
                            "name": "Empty String",
                            "value": ""
                        },
                        {
                            "name": "\"\"",
                            "value": "\"\""
                        },
                        {
                            "name": "null",
                            "value": "null"
                        }
                    ],
                    "readOnly": false,
                    "hidden": false
                }
            ],
            "isRequired": false,
            "readOnly": false,
            "hidden": false
        }
```

Hieronder ziet u het resulterende UI-scherm op basis van de bovenstaande configuratie. Wanneer de gebruiker het bestandstype CSV selecteert, worden aanvullende opties voor bestandsindeling die verwijzen naar het CSV-bestandstype weergegeven in de gebruikersinterface.

![ het registreren van het scherm die de voorwaardelijke dossier het formatteren optie voor Csv- dossiers tonen.](../../assets/guides/batch/conditional-file-formatting.gif)

### Volledige API-aanvraag die alle hierboven weergegeven opties bevat

De API-aanvraag hieronder combineert in één configuratie alle opties die in de bovenstaande secties worden beschreven.

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
  "name": "My S3 Destination",
  "description": "Test destination",
  "status": "TEST",
  "sources": [
    "UNIFIED_PROFILE"
  ],
  "customerAuthenticationConfigurations": [
    {
      "authType": "S3"
    }
  ],
  "customerDataFields": [
    {
      "name": "bucket",
      "type": "string",
      "title": "Bucket",
      "description": "Enter your S3 Bucket",
      "isRequired": true
    },
    {
      "name": "path",
      "type": "string",
      "title": "Path",
      "description": "Enter your S3 Path",
      "isRequired": true
    },
    {
      "name": "fileType",
      "type": "string",
      "enum": [
        "CSV",
        "JSON",
        "PARQUET"
      ],
      "title": "File Type",
      "description": "Select your file type",
      "isRequired": true
    },
    {
      "name": "csvOptions",
      "type": "object",
      "title": "CSV Options",
      "description": "Select your CSV options",
      "conditional": {
        "field": "fileType",
        "operator": "EQUALS",
        "value": "CSV"
      },
      "properties": [
        {
          "name": "delimiter",
          "type": "string",
          "title": "Delimiter",
          "description": "Select your Delimiter",
          "namedEnum": [
            {
              "name": "Comma (,)",
              "value": ","
            },
            {
              "name": "Tab (\\t)",
              "value": "\t"
            }
          ],
          "default": ","
        },
        {
          "name": "quote",
          "type": "string",
          "title": "Quote Character",
          "description": "Select your Quote character",
          "namedEnum": [
            {
              "name": "Double Quotes (\")",
              "value": "\""
            },
            {
              "name": "Null Character (\\u0000)",
              "value": "\u0000"
            }
          ],
          "default": "\u0000"
        },
        {
          "name": "escape",
          "type": "string",
          "title": "Escape Character",
          "description": "Select your Escape character",
          "namedEnum": [
            {
              "name": "Back Slash (\\)",
              "value": "\\"
            },
            {
              "name": "Single Quote (')",
              "value": "'"
            }
          ],
          "default": "\\"
        },
        {
          "name": "emptyValue",
          "type": "string",
          "title": "Empty Value",
          "description": "Select the output value of blank fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": ""
        },
        {
          "name": "nullValue",
          "type": "string",
          "title": "Null Value",
          "description": "Select the output value of 'null' fields",
          "namedEnum": [
            {
              "name": "null",
              "value": "null"
            },
            {
              "name": "Empty String",
              "value": ""
            },
            {
              "name": "\"\"",
              "value": "\"\""
            }
          ],
          "default": "null"
        }
      ]
    }
  ],
  "uiAttributes": {
    "documentationLink": "https://www.adobe.com/go/aep",
    "category": "cloudStorage",
    "connectionType": "Server-to-server",
    "frequency": "Batch",
    "monitoringSupported": true,
    "flowRunsSupported": true
  },
  "schemaConfig": {
    "profileRequired": true,
    "segmentRequired": true,
    "identityRequired": true
  },
  "batchConfig": {
    "allowMandatoryFieldSelection": true,
    "allowDedupeKeyFieldSelection": true,
    "defaultExportMode": "DAILY_FULL_EXPORT",
    "allowedExportMode": [
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
    ],
    "allowedScheduleFrequency": [
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
    ],
    "defaultFrequency": "DAILY",
    "defaultStartTime": "00:00",
    "filenameConfig": {
      "allowedFilenameAppendOptions": [
        "SEGMENT_NAME",
        "DESTINATION_INSTANCE_ID",
        "DESTINATION_INSTANCE_NAME",
        "ORGANIZATION_NAME",
        "SANDBOX_NAME",
        "DATETIME",
        "CUSTOM_TEXT"
      ],
      "defaultFilenameAppendOptions": [
        "DATETIME"
      ],
      "defaultFilename": "%DESTINATION%_%SEGMENT_ID%"
    }
  },
  "destinationDelivery": [
    {
      "deliveryMatchers": [
        {
          "type": "SOURCE",
          "value": [
            "batch"
          ]
        }
      ],
      "authenticationRule": "CUSTOMER_AUTHENTICATION",
      "destinationServerId": "<server-id>"
    }
  ]
}'
```

Een succesvolle reactie keert de bestemmingsconfiguratie, met inbegrip van het unieke herkenningsteken (`instanceId`) van de configuratie terug.

## Bekende beperkingen {#known-limitations}

Een bepaalde combinatie van opties voor bestandsindeling kan tot ongewenste resultaten bij het exporteren van bestanden leiden.
Adobe raadt u aan de volgende combinatie van CSV-opties niet te selecteren:

```
nullValue -> ""
quote -> "
emptyValue -> ""
```

Als u de beperking wilt verduidelijken, kunt u overwegen een bestand met de volgende waarden te exporteren:

| firstname | lastname | land | state |
|---------|----------|---------|--------|
| Michael | Roze | VS | NY |
| James | Smith |  | null |

{style="table-layout:auto"}

Dit zou resulteren in een uitvoer zoals hieronder wordt getoond. U ziet hoe de null-waarde uit de tabel onjuist wordt geëxporteerd als een escape-aanhalingsteken.

```csv
Michael,Rose,USA,NY 
James,Smith,"","\"\""
```

## Volgende stappen {#next-steps}

Door dit artikel te lezen, weet u nu hoe u aangepaste opmaakopties voor bestanden voor geëxporteerde bestanden kunt instellen met behulp van Destination SDK. Daarna, kan uw team het [ activeringswerkschema voor op dossier-gebaseerde bestemmingen ](../../../ui/activate-batch-profile-destinations.md) gebruiken om gegevens naar de bestemming uit te voeren.
