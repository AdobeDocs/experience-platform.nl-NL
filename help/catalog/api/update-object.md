---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;api;een object bijwerken
solution: Experience Platform
title: Een catalogusobject bijwerken
description: U kunt een deel van een object Catalog bijwerken door de id ervan op te nemen in het pad van een PATCH-aanvraag. Dit document behandelt het gebruik van velden en het gebruik van JSON Patch-notatie voor het uitvoeren van PATCH-bewerkingen op Catalog-objecten.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 0%

---

# Een catalogusobject bijwerken

U kunt een deel van een [!DNL Catalog] -object bijwerken door de id ervan op te nemen in het pad van een PATCH-aanvraag. In dit document worden de twee methoden beschreven voor het uitvoeren van PATCH-bewerkingen op Catalog-objecten:

* Velden gebruiken
* JSON-patchnotatie gebruiken

>[!NOTE]
>
>PATCH-bewerkingen op een object kunnen de uitbreidbare velden, die onderling verwante objecten vertegenwoordigen, niet wijzigen. Wijzigingen in onderling verwante objecten moeten rechtstreeks worden aangebracht.

## Bijwerken met velden

In het volgende voorbeeld wordt getoond hoe u een object kunt bijwerken met behulp van velden en waarden.

**API formaat**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden bijgewerkt. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

In het volgende verzoek worden de velden `name` en `description` van een gegevensset bijgewerkt naar de waarden die in de laadbewerking zijn opgegeven. Objectvelden die niet moeten worden bijgewerkt, kunnen worden uitgesloten van de laadbewerking.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Reactie**

Een succesvolle reactie keert een serie terug die identiteitskaart van de bijgewerkte dataset bevat. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. Wanneer u een GET-aanvraag voor deze gegevensset uitvoert, tonen nu dat alleen de `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Bijwerken met JSON Patch-notatie {#patch-notation}

De volgende voorbeeldvraag toont aan hoe te om een voorwerp bij te werken gebruikend Reparatie JSON, zoals die in [&#x200B; wordt geschetst rFC-6902 &#x200B;](https://tools.ietf.org/html/rfc6902).

Voor meer informatie over de syntaxis van het Reparatie JSON, zie de [&#x200B; API grondbeginselen gids &#x200B;](../../landing/api-fundamentals.md#json-patch).

**API formaat**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden bijgewerkt. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Met de volgende aanvraag worden de velden `name` en `description` van een gegevensset bijgewerkt naar de waarden in elk JSON-object Patch. Wanneer u JSON Patch gebruikt, moet u ook de header Content-Type instellen op `application/json-patch+json` .

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Reactie**

Een geslaagde reactie retourneert een array met de id van het bijgewerkte object. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. Wanneer u een GET-aanvraag voor dit object uitvoert, tonen nu dat alleen de waarden `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Bijwerken met PATCH v2-notatie {#patch-v2-notation}

Het `/v2/dataSets/{DATASET_ID}` eindpunt verstrekt een flexibelere manier om complexe of diep genestelde datasetattributen bij te werken.

Wanneer u een diep genest veld bijwerkt (zoals `a.b.c.d` ), moet elk niveau in het pad al bestaan. Als een niveau ontbreekt, moet u elk niveau manueel creëren alvorens de definitieve waarde te plaatsen. Dit vereist vaak veelvoudige verrichtingen, die ingewikkeldheid toevoegen en de kans van fouten verhogen.

Het eindpunt `/v2/dataSets/{DATASET_ID}` leidt automatisch tot om het even welke ontbrekende niveaus in de weg. In plaats van `b` en `c` vóór het instellen `d` handmatig te controleren en toe te voegen, doet de PATCH `v2` -bewerking dit voor u.

Wanneer u een PATCH-aanvraag naar het `/v2/dataSets/{DATASET_ID}` -eindpunt verzendt, hoeft u alleen de uiteindelijke structuur te verzenden en vult het systeem de ontbrekende onderdelen in voordat u de update toepast.

>[!NOTE]
>
>`If-Match` en `If-None-Match` headers zijn optioneel voor het eindpunt `/v2/dataSets/{id}` . PATCH-verzoeken aan dit eindpunt voegen updates dynamisch samen, waarbij wijzigingen worden toegestaan zonder de meest recente gegevenssetversie op te halen. Hoewel dit het risico op gegevensverlies door gelijktijdige updates vermindert, kunt u `If-Match` met de nieuwste `etag` gebruiken om ervoor te zorgen dat wijzigingen alleen op een specifieke versie van toepassing zijn. `If-None-Match` voorkomt ook updates als de gegevensset niet is gewijzigd sinds de laatst bekende versie.

**API formaat**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{DATASET_ID}` | The identifier of the dataset to update. |

**Verzoek**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**Reactie**

Een geslaagde reactie retourneert een array met de id van de bijgewerkte gegevensset, die moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. Wanneer u een GET-aanvraag voor dit object uitvoert, wordt nu getoond dat het `extensions.adobe_lakeHouse.rowExpiration` -object is gemaakt zonder dat u daarvoor handmatig stappen hoeft te maken.

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### Een voorbeelddataset voor en na de update

Het voorbeeld JSON illustreert hieronder de datasetstructuur **vóór** het verzoek van PATCH, waar het `extensions.adobe_lakeHouse.rowExpiration` voorwerp niet in de dataset aanwezig is.

+++Selecteren om voorbeeld weer te geven

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

Het volgende JSON toont de datasetstructuur **na** het verzoek van PATCH. De update maakt automatisch het ontbrekende `extensions.adobe_lakeHouse.rowExpiration` -object zonder voorafgaande handmatige aanmaakstappen. In dit voorbeeld wordt getoond hoe de `/v2/` PATCH-aanvraag meerdere bewerkingen overbodig maakt, waardoor updates eenvoudiger en efficiënter worden.


+++Selecteren om voorbeeld weer te geven

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
