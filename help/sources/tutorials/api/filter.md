---
title: Gegevens op rijniveau voor een Source filteren met behulp van de Flow Service API
description: Deze zelfstudie behandelt de stappen voor het filteren van gegevens op bronniveau met behulp van de Flow Service API
exl-id: 224b454e-a079-4df3-a8b2-1bebfb37d11f
source-git-commit: 67abd5cda9cff1da8757ef691ebbf27e9a5550c5
workflow-type: tm+mt
source-wordcount: '1822'
ht-degree: 2%

---

# Gegevens op rijniveau voor een bron filteren met de API [!DNL Flow Service]

>[!AVAILABILITY]
>
>De steun voor het filtreren van rij-vlakke gegevens is momenteel slechts beschikbaar aan de volgende bronnen:
>
>* [ [Amazon Redshift] ](../../connectors/databases/redshift.md)
>* [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md)
>* [[!DNL Marketo Engage]  standaardactiviteiten ](../../connectors/adobe-applications/marketo/marketo.md)
>* [[!DNL Microsoft Dynamics]](../../connectors/crm/ms-dynamics.md)
>* [[!DNL Salesforce]](../../connectors/crm/salesforce.md)
>* [[!DNL Snowflake]](../../connectors/databases/snowflake.md)

Lees deze gids voor stappen op hoe te om rij-vlakke gegevens voor een bron te filtreren gebruikend [[!DNL Flow Service]  API ](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [ Bronnen ](../../home.md): [!DNL Experience Platform] staat gegevens toe om van diverse bronnen worden opgenomen terwijl het voorzien van u van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Experience Platform] diensten.
* [ Sandboxen ](../../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

### Experience Platform API&#39;s gebruiken

Voor informatie over hoe te om vraag aan Experience Platform APIs met succes te maken, zie de gids op [ begonnen wordt met Experience Platform APIs ](../../../landing/api-guide.md).

## Brongegevens filteren {#filter-source-data}

De volgende schetsen stappen om rij-vlakke gegevens voor uw bron te filtreren.

### Haal uw verbindingsspecificaties op {#retrieve-your-connection-specs}

De eerste stap bij het filtreren van rij-vlakke gegevens voor uw bron is de verbindingsspecificaties van uw bron terug te winnen en de exploitanten en de taal te bepalen die uw bron steunt.

Als u de verbindingsspecificatie van een bepaalde bron wilt ophalen, vraagt u GET het `/connectionSpecs` -eindpunt van de [!DNL Flow Service] API aan en geeft u de eigenschapnaam van de bron op als onderdeel van de queryparameters.

**API formaat**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMS}` | De optionele queryparameters waarmee u resultaten wilt filteren. U kunt de verbindingsspecificatie [!DNL Google BigQuery] ophalen door de eigenschap `name` toe te passen en `"google-big-query"` op te geven in de zoekopdracht. |

+++verzoek

Met de volgende aanvraag worden de verbindingsspecificaties voor [!DNL Google BigQuery] opgehaald.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

Een geslaagde reactie retourneert de statuscode 200 en de verbindingsspecificaties voor [!DNL Google BigQuery] , inclusief informatie over de ondersteunde querytaal en logische operatoren.

```json
"attributes": {
  "filterAtSource": {
    "enabled": true,
    "queryLanguage": "SQL",
    "logicalOperators": [
      "and",
      "or",
      "not"
    ],
    "comparisonOperators": [
      "=",
      "!=",
      "<",
      "<=",
      ">",
      ">=",
      "like",
      "in"
    ],
    "columnNameEscapeChar": "`",
    "valueEscapeChar": "'"
  }
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes.filterAtSource.enabled` | Bepaalt of de gevraagde bron het filtreren voor rij-vlakke gegevens steunt. |
| `attributes.filterAtSource.queryLanguage` | Bepaalt de vraagtaal die de gevraagde bron steunt. |
| `attributes.filterAtSource.logicalOperators` | Bepaalt de logische operatoren die u kunt gebruiken om gegevens op rijniveau voor uw bron te filteren. |
| `attributes.filterAtSource.comparisonOperators` | Bepaalt vergelijkingsexploitanten die u kunt gebruiken om rij-vlakke gegevens voor uw bron te filtreren. Zie de onderstaande tabel voor meer informatie over vergelijkingsoperatoren. |
| `attributes.filterAtSource.columnNameEscapeChar` | Bepaalt het teken dat moet worden gebruikt om kolommen te laten ontsnappen. |
| `attributes.filterAtSource.valueEscapeChar` | Bepaalt hoe waarden worden omringd wanneer het schrijven van een SQL vraag. |

{style="table-layout:auto"}

+++

#### Vergelijkingsoperatoren {#comparison-operators}

| Operator | Beschrijving |
| --- | --- |
| `==` | Filtert op of de eigenschap gelijk is aan de opgegeven waarde. |
| `!=` | Filtert op of de eigenschap niet gelijk is aan de opgegeven waarde. |
| `<` | Filtert op of de eigenschap kleiner is dan de opgegeven waarde. |
| `>` | Filtert op of de eigenschap groter is dan de opgegeven waarde. |
| `<=` | Filtert op of de eigenschap kleiner dan of gelijk is aan de opgegeven waarde. |
| `>=` | Filtert op of de eigenschap groter dan of gelijk is aan de opgegeven waarde. |
| `like` | Filters door in een `WHERE` -component te worden gebruikt om naar een opgegeven patroon te zoeken. |
| `in` | Filtert op of het bezit binnen een gespecificeerde waaier is. |

{style="table-layout:auto"}

### Filtervoorwaarden voor inname opgeven {#specify-filtering-conditions-for-ingestion}

Nadat u de logische operatoren en de querytaal hebt geïdentificeerd die door uw bron worden ondersteund, kunt u Profile Query Language (PQL) gebruiken om de filtervoorwaarden op te geven die u op de brongegevens wilt toepassen.

In het onderstaande voorbeeld worden voorwaarden alleen toegepast op geselecteerde gegevens die overeenkomen met de opgegeven waarden voor de knooppunttypen die als parameters worden vermeld.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "=",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "city"
      },
      {
        "nodeType": "literal",
        "value": "DDN"
      }
    ]
  }
}
```

### Een voorbeeld van uw gegevens bekijken {#preview-your-data}

U kunt een voorbeeld van uw gegevens bekijken door een GET-aanvraag in te dienen bij het `/explore` -eindpunt van de [!DNL Flow Service] API. U kunt `filters` echter opgeven als onderdeel van de queryparameters en de invoervoorwaarden voor PQL in [!DNL Base64] opgeven.

**API formaat**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van uw bron. |
| `{TABLE_PATH}` | De eigenschap path van de tabel die u wilt inspecteren. |
| `{FILTERS}` | Uw PQL-filtervoorwaarden zijn gecodeerd in [!DNL Base64] . |

+++verzoek

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

Een geslaagde reactie retourneert de inhoud en structuur van de gegevens.

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "FIRSTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "LASTNAME",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "CITY",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "AGE",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "HEIGHT",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "ISEMPLOYED",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "POSTG",
        "type": "boolean",
        "xdm": {
          "type": "boolean"
        }
      },
      {
        "name": "LATITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "LONGITUDE",
        "type": "double",
        "xdm": {
          "type": "number"
        }
      },
      {
        "name": "JOINEDDATE",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDAT",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "CREATEDATTS",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  },
 "data": [
    {
        "CITY": "MZN",
        "LASTNAME": "Jain",
        "JOINEDDATE": "2022-06-22T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-06-22T17:19:33",
        "FIRSTNAME": "Shivam",
        "POSTG": true,
        "HEIGHT": "169",
        "CREATEDATTS": "2022-06-22T17:19:33",
        "ISEMPLOYED": true,
        "LATITUDE": 2000.89,
        "AGE": "25"
    },
    {
        "CITY": "MUM",
        "LASTNAME": "Kreet",
        "JOINEDDATE": "2022-09-07T00:00:00",
        "LONGITUDE": 10500.01,
        "CREATEDAT": "2022-09-07T17:19:33",
        "FIRSTNAME": "Rakul",
        "POSTG": true,
        "HEIGHT": "155",
        "CREATEDATTS": "2022-09-07T17:19:33",
        "ISEMPLOYED": false,
        "LATITUDE": 2500.89,
        "AGE": "42"
    },
    {
        "CITY": "MAN",
        "LASTNAME": "Lee",
        "JOINEDDATE": "2022-09-14T00:00:00",
        "LONGITUDE": 1000.222,
        "CREATEDAT": "2022-09-14T05:02:33",
        "FIRSTNAME": "Denzel",
        "POSTG": true,
        "HEIGHT": "185",
        "CREATEDATTS": "2022-09-14T05:02:33",
        "ISEMPLOYED": true,
        "LATITUDE": 123.89,
        "AGE": "16"
    }
  ]
}
```

+++

### Een bronverbinding maken voor gefilterde gegevens

Om een bronverbinding tot stand te brengen en gefilterde gegevens in te voeren, doe een POST- verzoek aan het `/sourceConnections` eindpunt en verstrek uw het filtreren voorwaarden in de parameters van het verzoeklichaam.

**API formaat**

```http
POST /sourceConnections
```

+++verzoek

Met de volgende aanvraag wordt een bronverbinding gemaakt voor het invoeren van gegevens van `test1.fasTestTable` waarbij `city` = `DDN` .

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "BigQuery Source Connection",
      "description": "Source Connection for Filter test",
      "baseConnectionId": "89d1459e-3cd0-4069-acb3-68f240db4eeb",
      "data": {
        "format": "tabular"
      },
      "params": {
        "tableName": "test1.fasTestTable",
        "filters": {
          "type": "PQL",
          "format": "pql/json",
          "value": {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "DDN"
              }
            ]
          }
        }
      },
      "connectionSpec": {
        "id": "3c9b37f8-13a6-43d8-bad3-b863b941fedd",
        "version": "1.0"
      }
    }'
```

+++

+++Response

Een succesvolle reactie keert het unieke herkenningsteken (`id`) van de pas gecreëerde bronverbinding terug.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

+++

## Activiteitenentiteiten filteren voor [!DNL Marketo Engage] {#filter-for-marketo}

U kunt rij-niveau het filtreren gebruiken om voor activiteitenentiteiten te filtreren wanneer het gebruiken van de [[!DNL Marketo Engage]  bronschakelaar ](../../connectors/adobe-applications/marketo/marketo.md). Momenteel kunt u alleen filteren op activiteitentiteiten en standaardtypen. De activiteiten van de douane blijven onder [[!DNL Marketo]  gebiedsafbeeldingen ](../../connectors/adobe-applications/mapping/marketo.md) worden geregeerd.

### [!DNL Marketo] standaardactiviteitstypen {#marketo-standard-activity-types}

In de volgende tabel worden de standaardactiviteitstypen voor [!DNL Marketo] beschreven. Gebruik deze lijst als verwijzing voor uw het filtreren criteria.

| Type activiteit-id | Naam van type activiteit |
| --- | --- |
| 1 | Webpagina bezoeken |
| 2 | Formulier invullen |
| 3 | Klik op Koppeling |
| 6 | E-mail verzenden |
| 7 | E-mail bezorgd |
| 8 | E-mail verzonden |
| 9 | E-mailadres opzeggen |
| 10 | E-mail openen |
| 11 | Klik op E-mail |
| 12 | Nieuwe lead |
| 21 | Regelafstand omzetten |
| 22 | Score wijzigen |
| 24 | Toevoegen aan lijst |
| 25 | Verwijderen uit lijst |
| 27 | Door e-mail teruggekaatst |
| 32 | Leads samenvoegen |
| 34 | Toevoegen aan opportunity |
| 35 | Verwijderen uit opportunity |
| 36 | Opportunity bijwerken |
| 46 | Interessant moment |
| 101 | Opbrengstfase wijzigen |
| 104 | Status wijzigen in Progressie |
| 110 | Bellen Webhaak |
| 113 | Toevoegen aan cursus |
| 114 | Cursustrack wijzigen |
| 115 | Aanwezigheid van loop wijzigen |

{style="table-layout:auto"}

Voer de onderstaande stappen uit om de entiteiten met de standaardactiviteit te filteren wanneer u de [!DNL Marketo] bronconnector gebruikt.

### Concepten van gegevensstroom maken

Eerst, creeer a [[!DNL Marketo]  dataflow ](../ui/create/adobe-applications/marketo.md) en bewaar het als ontwerp. Raadpleeg de volgende documentatie voor gedetailleerde stappen voor het maken van een concept-gegevensstroom:

* [Een gegevensstroom opslaan als concept met de gebruikersinterface](../ui/draft.md)
* [Een gegevensstroom opslaan als concept met de API](../api/draft.md)

### Uw gegevensstroom-id ophalen

Zodra u een geschreven gegevensstroom hebt, moet u zijn overeenkomstige identiteitskaart dan terugwinnen.

Navigeer in de gebruikersinterface naar de broncatalogus en selecteer vervolgens **[!UICONTROL Dataflows]** in de bovenste koptekst. Gebruik de statuskolom om alle gegevens te identificeren die in ontwerp wijze werden bewaard, en dan de naam van uw gegevensstroom te selecteren. Gebruik vervolgens het deelvenster **[!UICONTROL Properties]** aan de rechterkant om de gegevensstroom-id te zoeken.

### Gegevens over gegevensstroom ophalen

Vervolgens moet u de gegevens over de gegevensstroom ophalen, met name de id van de bronverbinding die aan uw gegevensstroom is gekoppeld. Als u de gegevens over de gegevensstroom wilt ophalen, vraagt u GET het `/flows` -eindpunt aan en geeft u uw gegevensstroom-id op als padparameter.

**API formaat**

```http
GET /flows/{FLOW_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{FLOW_ID}` | De id van de gegevensstroom die u wilt ophalen. |

+++verzoek

Met de volgende aanvraag wordt informatie over de gegevensstroom-id opgehaald: `a7e88a01-40f9-4ebf-80b2-0fc838ff82ef` .

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

Een succesvolle reactie keert uw gegevens van de gegevensstroom, met inbegrip van informatie over zijn overeenkomstige bron en doelverbindingen terug. U moet nota nemen van uw bron en doel verbindings IDs, aangezien deze waarden later worden vereist, om uw gegevensstroom te publiceren.

```json {line-numbers="true" start-line="1" highlight="23, 26"}
{
    "items": [
        {
            "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "createdAt": 1728592929650,
            "updatedAt": 1728597187444,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "Marketo Engage Standard Activities ACME",
            "description": "",
            "flowSpec": {
                "id": "15f8402c-ba66-4626-b54c-9f8e54244d61",
                "version": "1.0"
            },
            "state": "enabled",
            "version": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "etag": "\"600290fc-0000-0200-0000-67084cc30000\"",
            "sourceConnectionIds": [
                "56f7eb3a-b544-4eaa-b167-ef1711044c7a"
            ],
            "targetConnectionIds": [
                "7e53e6e8-b432-4134-bb29-21fc6e8532e5"
            ],
            "inheritedAttributes": {
                "properties": {
                    "isSourceFlow": true
                },
                "sourceConnections": [
                    {
                        "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
                        "connectionSpec": {
                            "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                            "version": "1.0"
                        },
                        "baseConnection": {
                            "id": "0137118b-373a-4c4e-847c-13a0abf73b33",
                            "connectionSpec": {
                                "id": "bf1f4218-73ce-4ff0-b744-48d78ffae2e4",
                                "version": "1.0"
                            }
                        }
                    }
                ],
                "targetConnections": [
                    {
                        "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
                        "connectionSpec": {
                            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
                            "version": "1.0"
                        }
                    }
                ]
            },
            "options": {
                "isSampleDataflow": false,
                "errorDiagnosticsEnabled": true
            },
            "transformations": [
                {
                    "name": "Mapping",
                    "params": {
                        "mappingVersion": 0,
                        "mappingId": "f6447514ef95482889fac1818972e285"
                    }
                }
            ],
            "runs": "/runs?property=flowId==a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
            "lastOperation": {
                "started": 1728592929650,
                "updated": 0,
                "operation": "create"
            },
            "lastRunDetails": {
                "id": "2d7863d5-ca4d-4313-ac52-2603eaf2cdbe",
                "state": "success",
                "startedAtUTC": 1728594713537,
                "completedAtUTC": 1728597183080
            },
            "labels": [],
            "recordTypes": [
                {
                    "type": "experienceevent",
                    "extensions": {}
                }
            ]
        }
    ]
}
```

+++

### De verbindingsgegevens van de bron ophalen

Gebruik vervolgens de bron-verbindings-id en doe een GET-aanvraag aan het `/sourceConnections` -eindpunt om uw bronverbindingsgegevens op te halen.

**API formaat**

```http
GET /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | De id van de bronverbinding die u wilt ophalen. |

+++verzoek

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

+++Response

Een succesvolle reactie keert de details van uw bronverbinding terug. Noteer de versie omdat u deze waarde in de volgende stap nodig hebt om uw bronverbinding bij te werken.

```json {line-numbers="true" start-line="1" highlight="30"}
{
    "items": [
        {
            "id": "b85b895f-a289-42e9-8fe1-ae448ccc7e53",
            "createdAt": 1729634331185,
            "updatedAt": 1729634331185,
            "createdBy": "acme@AdobeID",
            "updatedBy": "acme@AdobeID",
            "createdClient": "exc_app",
            "updatedClient": "acme",
            "sandboxId": "7f3419ce-53e2-476b-b419-ce53e2376b02",
            "sandboxName": "prod",
            "imsOrgId": "acme@AdobeOrg",
            "name": "New Source Connection - 2024-10-23T03:28:50+05:30",
            "description": "Source connection created from the workflow",
            "baseConnectionId": "fd9f7455-1e23-4831-9283-7717e20bee40",
            "state": "draft",
            "data": {
                "format": "tabular",
                "schema": null,
                "properties": null
            },
            "connectionSpec": {
                "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                "version": "1.0"
            },
            "params": {
                "columns": [],
                "tableName": "Activity"
            },
            "version": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "etag": "\"210068a6-0000-0200-0000-6718201b0000\"",
            "inheritedAttributes": {
                "baseConnection": {
                    "id": "fd9f7455-1e23-4831-9283-7717e20bee40",
                    "connectionSpec": {
                        "id": "2d31dfd1-df1a-456b-948f-226e040ba102",
                        "version": "1.0"
                    }
                }
            },
            "lastOperation": {
                "started": 1729634331185,
                "updated": 0,
                "operation": "draft_create"
            }
        }
    ]
}
```

+++

### De bronverbinding bijwerken met filtervoorwaarden

Nu u uw bron-verbindings-id en de bijbehorende versie hebt, kunt u nu een PATCH-aanvraag indienen met de filtervoorwaarden die uw standaardactiviteitstypen opgeven.

Als u de bronverbinding wilt bijwerken, vraagt u PATCH het `/sourceConnections` -eindpunt aan en geeft u uw bron-verbindings-id op als een queryparameter. Daarnaast moet u een headerparameter `If-Match` opgeven met de bijbehorende versie van uw bronverbinding.

>[!TIP]
>
>De header `If-Match` is vereist wanneer een PATCH-aanvraag wordt ingediend. De waarde voor deze header is de unieke versie/tag van de gegevensstroom die u wilt bijwerken. De versie-/tijdlabelwaarde wordt bijgewerkt bij elke geslaagde update van een gegevensstroom.

**API formaat**

```http
PATCH /sourceConnections/{SOURCE_CONNECTION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | De id van de bronverbinding die u wilt bijwerken |

+++verzoek

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'If-Match: {VERSION_HERE}'
  -d '
      {
        "op": "add",
        "path": "/params/filters",
        "value": {
            "type": "PQL",
            "format": "pql/json",
            "value": {
                "nodeType": "fnApply",
                "fnName": "in",
                "params": [
                    {
                        "nodeType": "fieldLookup",
                        "fieldName": "activityType"
                    },
                    {
                        "nodeType": "literal",
                        "value": [
                            "Change Status in Progression",
                            "Fill Out Form"
                        ]
                    }
                ]
            }
        }
    }'
```

+++

+++Response

Een geslaagde reactie retourneert uw bron-verbindings-id en -tag (versie).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"210068a6-0000-0200-0000-6718201b0000\""
}
```

+++

### De bronverbinding publiceren

Wanneer de bronverbinding is bijgewerkt met de filtervoorwaarden, kunt u nu verder gaan van de conceptstatus en uw bronverbinding publiceren. Hiertoe dient u een POST-verzoek in bij het `/sourceConnections` -eindpunt en verstrekt u de id van de conceptbronverbinding en een handeling voor publicatie.

**API formaat**

```http
POST /sourceConnections/{SOURCE_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `{SOURCE_CONNECTION_ID}` | De id van de bronverbinding die u wilt publiceren. |
| `op` | Een handelingsverrichting die de staat van de gevraagde bronverbinding bijwerkt. Als u een conceptbronverbinding wilt publiceren, stelt u `op` in op `publish` . |

+++verzoek

Het volgende verzoek publiceert een opgestelde bronverbinding.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections/56f7eb3a-b544-4eaa-b167-ef1711044c7a/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een geslaagde reactie retourneert uw bron-verbindings-id en -tag (versie).

```json
{
    "id": "56f7eb3a-b544-4eaa-b167-ef1711044c7a",
    "etag": "\"9f007f7b-0000-0200-0000-670ef1150000\""
}
```

+++

### Doelverbinding publiceren

Net als bij de vorige stap moet u ook de doelverbinding publiceren om door te gaan en uw conceptgegevensstroom te publiceren. Maak een POST- verzoek aan het `/targetConnections` eindpunt en verstrek identiteitskaart van de ontwerp doelverbinding die u, evenals een actieverrichting voor het publiceren wilt publiceren.

**API formaat**

```http
POST /targetConnections/{TARGET_CONNECTION_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `{TARGET_CONNECTION_ID}` | De id van de doelverbinding die u wilt publiceren. |
| `op` | Een handelingsverrichting die de staat van de gevraagde doelverbinding bijwerkt. Als u een conceptdoelverbinding wilt publiceren, stelt u `op` in op `publish` . |

+++verzoek

In het volgende verzoek wordt de doelverbinding met de id gepubliceerd: `7e53e6e8-b432-4134-bb29-21fc6e8532e5` .

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections/7e53e6e8-b432-4134-bb29-21fc6e8532e5/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een succesvolle reactie keert identiteitskaart en het overeenkomstige etiket voor uw gepubliceerde doelverbinding terug.

```json
{
    "id": "7e53e6e8-b432-4134-bb29-21fc6e8532e5",
    "etag": "\"8e000533-0000-0200-0000-5f3c40fd0000\""
}
```

+++


### Uw gegevensstroom publiceren

Met uw bron- en doelverbindingen beide gepubliceerd, kunt u nu verdergaan met de laatste stap en uw gegevensstroom publiceren. Als u de gegevensstroom wilt publiceren, vraagt u een POST-aanvraag naar het `/flows` -eindpunt en geeft u uw gegevensstroom-id en een handeling op voor publicatie.

**API formaat**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| Parameter | Beschrijving |
| --- | --- |
| `{FLOW_ID}` | De id van de gegevensstroom die u wilt publiceren. |
| `op` | Een handelingsverrichting die de staat van de gevraagde dataflow bijwerkt. Als u een conceptgegevensstroom wilt publiceren, stelt u `op` in op `publish` . |

+++verzoek

Met het volgende verzoek wordt uw conceptgegevensstroom gepubliceerd.

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/a7e88a01-40f9-4ebf-80b2-0fc838ff82ef/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Response

Een geslaagde reactie retourneert de id en de bijbehorende `etag` gegevensstroom.

```json
{
  "id": "a7e88a01-40f9-4ebf-80b2-0fc838ff82ef",
  "etag": "\"4b0354b7-0000-0200-0000-6716ce1f0000\""
}
```

+++

Met de gebruikersinterface van Experience Platform kunt u controleren of uw conceptgegevensstroom is gepubliceerd. Navigeer naar de pagina met gegevensstromen in de broncatalogus en verwijs naar **[!UICONTROL Status]** van de gegevensstroom. Als succesvol, zou de status aan **Toegelaten** nu moeten worden geplaatst.

>[!TIP]
>
>* Een dataflow met toegelaten filtreren zal slechts eenmaal worden teruggevuld. Wijzigingen in de filtercriteria die u aanbrengt (of het nu een toevoeging of een verwijdering is), kunnen alleen van kracht worden voor incrementele gegevens.
>* Als u historische gegevens voor om het even welk nieuw type(n) activiteit moet innemen, wordt u geadviseerd om een nieuw dataflow tot stand te brengen en de het filtreren criteria met de aangewezen activiteitstypes in de filtervoorwaarde te bepalen.
>* U kunt geen aangepaste activiteitstypen filteren.
>* U kunt gefilterde gegevens niet voorvertonen.

## Bijlage

Deze sectie verstrekt verdere voorbeelden van verschillende ladingen voor het filtreren.

### Enkelvoudige omstandigheden

U kunt het eerste `fnApply` weglaten voor scenario&#39;s die slechts één voorwaarde vereisen.

+++Selecteren om voorbeeld weer te geven

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "like",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "firstname"
      },
      {
        "nodeType": "literal",
        "value": "%s"
      }
    ]
  }
}
```

+++

### De operator `in` gebruiken

Zie de voorbeeldlading hieronder voor een voorbeeld van de exploitant `in`.

+++Selecteren om voorbeeld weer te geven

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "in",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "firstname"
          },
          {
            "nodeType": "literal",
            "value": [
              "Ramen",
              "John"
            ]
          }
        ]
      }
    ]
  }
}
```

+++

### De operator `isNull` gebruiken

+++Selecteren om voorbeeld weer te geven

Zie de voorbeeldlading hieronder voor een voorbeeld van de exploitant `isNull`.

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "isNull",
    "params": [
      {
        "nodeType": "fieldLookup",
        "fieldName": "complaint_type"
      }
    ]
  }
}
```

+++

### De operator `NOT` gebruiken

Zie de voorbeeldlading hieronder voor een voorbeeld van de exploitant `NOT`.


+++Selecteren om voorbeeld weer te geven

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "NOT",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": "isNull",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "complaint_type"
          }
        ]
      }
    ]
  }
}
```

+++

### Voorbeeld met geneste voorwaarden

Zie de voorbeeldlading hieronder voor een voorbeeld van complexe genestelde voorwaarden.

+++Selecteren om voorbeeld weer te geven

```json
{
  "type": "PQL",
  "format": "pql/json",
  "value": {
    "nodeType": "fnApply",
    "fnName": "and",
    "params": [
      {
        "nodeType": "fnApply",
        "fnName": ">=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 20
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "<=",
        "params": [
          {
            "nodeType": "fieldLookup",
            "fieldName": "age"
          },
          {
            "nodeType": "literal",
            "value": 30
          }
        ]
      },
      {
        "nodeType": "fnApply",
        "fnName": "or",
        "params": [
          {
            "nodeType": "fnApply",
            "fnName": "!=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "city"
              },
              {
                "nodeType": "literal",
                "value": "PUD"
              }
            ]
          },
          {
            "nodeType": "fnApply",
            "fnName": "=",
            "params": [
              {
                "nodeType": "fieldLookup",
                "fieldName": "joinedDate"
              },
              {
                "nodeType": "literal",
                "value": "2020-04-22"
              }
            ]
          }
        ]
      }
    ]
  }
}
```

+++