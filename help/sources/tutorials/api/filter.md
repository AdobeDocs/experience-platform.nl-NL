---
keywords: Experience Platform;huis;populaire onderwerpen;de stroomdienst;De Dienst API van de stroom;bronnen;Bronnen
title: Gegevens op rijniveau voor een bron filteren met behulp van de Flow Service API
description: Deze zelfstudie behandelt de stappen voor het filteren van gegevens op bronniveau met behulp van de Flow Service API
source-git-commit: 122f6bda2fbcf72bf098b972ff7b081f4c5e3388
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 1%

---

# Gegevens op rijniveau filteren voor een bron die de [!DNL Flow Service] API

>[!IMPORTANT]
>
>De steun voor het filtreren van rij-vlakke gegevens voor een bron is momenteel slechts beschikbaar voor [[!DNL Google BigQuery]](../../connectors/databases/bigquery.md) en [[!DNL Snowflake]](../../connectors/databases/snowflake.md) bronnen.

Deze zelfstudie bevat stappen voor het filteren van gegevens op rijniveau voor een bron met behulp van de [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Aan de slag

Voor deze zelfstudie hebt u een goed inzicht nodig in de volgende onderdelen van Adobe Experience Platform:

* [Bronnen](../../home.md): [!DNL Experience Platform] staat gegevens toe om uit diverse bronnen worden opgenomen terwijl het voorzien van de capaciteit om, inkomende gegevens te structureren te etiketteren en te verbeteren gebruikend [!DNL Platform] diensten.
* [Sandboxen](../../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

### Platform-API&#39;s gebruiken

Zie de handleiding voor informatie over hoe u aanroepen naar Platform-API&#39;s kunt uitvoeren [aan de slag met Platform-API&#39;s](../../../landing/api-guide.md).

## Brongegevens filteren

De volgende schetsen stappen om rij-vlakke gegevens voor uw bron te filtreren.

### Verbindingsspecificaties opzoeken

Voordat u de API kunt gebruiken voor het filteren van gegevens op rijniveau voor een bron, moet u eerst de verbindingsspecificatie van uw bron details ophalen om te bepalen welke operatoren en taal door een specifieke bron worden ondersteund.

Om de verbindingsspecificatie van een bepaalde bron terug te winnen, doe een verzoek van de GET aan `/connectionSpecs` van het [!DNL Flow Service] API terwijl het verstrekken van de bezitsnaam van uw bron als deel van uw vraagparameters.

**API-indeling**

```http
GET /connectionSpecs/{QUERY_PARAMS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{QUERY_PARAMS}` | De optionele queryparameters waarmee u resultaten wilt filteren. U kunt de [!DNL Google BigQuery] verbindingsspecificatie toepassen `name` eigenschap en specificeren `"google-big-query"` in uw zoekopdracht. |

**Verzoek**

Met het volgende verzoek worden verbindingsspecificaties opgehaald voor [!DNL Google BigQuery].

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=name=="google-big-query"' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol antwoord keert de verbindingsspecificaties voor terug [!DNL Google BigQuery], inclusief informatie over de ondersteunde querytaal en logische operatoren.

>[!NOTE]
>
>De API-respons hieronder is afgebroken voor de beknoptheid.

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

{style=&quot;table-layout:auto&quot;}

#### Vergelijkingsoperatoren

| Operator | Beschrijving |
| --- | --- |
| `==` | Filtert op of de eigenschap gelijk is aan de opgegeven waarde. |
| `!=` | Filtert op of de eigenschap niet gelijk is aan de opgegeven waarde. |
| `<` | Filtert op of de eigenschap kleiner is dan de opgegeven waarde. |
| `>` | Filtert op of de eigenschap groter is dan de opgegeven waarde. |
| `<=` | Filtert op of de eigenschap kleiner dan of gelijk is aan de opgegeven waarde. |
| `>=` | Filtert op of de eigenschap groter dan of gelijk is aan de opgegeven waarde. |
| `like` | Filters die worden gebruikt in een `WHERE` naar een opgegeven patroon te zoeken. |
| `in` | Filtert op of het bezit binnen een gespecificeerde waaier is. |

{style=&quot;table-layout:auto&quot;}

### Filtervoorwaarden voor inname opgeven

Nadat u de logische operatoren en de querytaal hebt geïdentificeerd die door uw bron wordt ondersteund, kunt u PQL (Profile Query Language) gebruiken om de filtervoorwaarden op te geven die u op de brongegevens wilt toepassen.

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

### Een voorbeeld van uw gegevens bekijken

U kunt een voorvertoning van uw gegevens weergeven door een verzoek in te dienen bij de GET `/explore` van het [!DNL Flow Service] API tijdens `filters` als onderdeel van uw queryparameters en het opgeven van uw PQL-invoervoorwaarden in [!DNL Base64].

**API-indeling**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}&preview=true&filters={FILTERS}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BASE_CONNECTION_ID}` | De basis verbindings-id van uw bron. |
| `{TABLE_PATH}` | De eigenschap path van de tabel die u wilt inspecteren. |
| `{FILTERS}` | Uw PQL-filtervoorwaarden gecodeerd in [!DNL Base64]. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/89d1459e-3cd0-4069-acb3-68f240db4eeb/explore?objectType=table&object=TESTFAS.FASTABLE&preview=true&filters=ewogICJ0eXBlIjogIlBRTCIsCiAgImZvcm1hdCI6ICJwcWwvanNvbiIsCiAgInZhbHVlIjogewogICAgIm5vZGVUeXBlIjogImZuQXBwbHkiLAogICAgImZuTmFtZSI6ICJhbmQiLAogICAgInBhcmFtcyI6IFsKICAgICAgewogICAgICAgICJub2RlVHlwZSI6ICJmbkFwcGx5IiwKICAgICAgICAiZm5OYW1lIjogImxpa2UiLAogICAgICAgICJwYXJhbXMiOiBbCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJmaWVsZExvb2t1cCIsCiAgICAgICAgICAgICJmaWVsZE5hbWUiOiAiY2l0eSIKICAgICAgICAgIH0sCiAgICAgICAgICB7CiAgICAgICAgICAgICJub2RlVHlwZSI6ICJsaXRlcmFsIiwKICAgICAgICAgICAgInZhbHVlIjogIk0lIgogICAgICAgICAgfQogICAgICAgIF0KICAgICAgfQogICAgXQogIH0KfQ==\' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvol verzoek retourneert de volgende reactie.

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

### Een bronverbinding maken voor gefilterde gegevens

Om een bronverbinding tot stand te brengen en gefilterde gegevens in te voeren, doe een verzoek van de POST aan `/sourceConnections` eindpunt terwijl het verstrekken van uw het filtreren voorwaarden als deel van uw lichaamsparameters.

**API-indeling**

```http
POST /sourceConnections
```

**Verzoek**

Met de volgende aanvraag wordt een bronverbinding gemaakt voor het invoeren van gegevens van `test1.fasTestTable` waar `city` = `DDN`.

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

**Antwoord**

Een geslaagde reactie retourneert de unieke id (`id`) van de nieuwe bronverbinding.

```json
{
    "id": "b7581b59-c603-4df1-a689-d23d7ac440f3",
    "etag": "\"ef05d265-0000-0200-0000-6019e0080000\""
}
```

## Aanhangsel

Deze sectie verstrekt verdere voorbeelden van verschillende ladingen voor het filtreren.

### Enkelvoudige omstandigheden

U kunt de eerste `fnApply` voor scenario&#39;s die slechts één voorwaarde vereisen.

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

### Met de `in` operator

Zie de voorbeeldlading hieronder voor een voorbeeld van de exploitant `in`.

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

### Met de `isNull` operator

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

### Met de `NOT` operator

Zie de voorbeeldlading hieronder voor een voorbeeld van de exploitant `NOT`.

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

### Voorbeeld met geneste voorwaarden

Zie de voorbeeldlading hieronder voor een voorbeeld van complexe genestelde voorwaarden.

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
