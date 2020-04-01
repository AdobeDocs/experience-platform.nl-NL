---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een object bijwerken
topic: developer guide
translation-type: tm+mt
source-git-commit: 4361032b419622d7decc02194d38885b114749e4

---


# Een object bijwerken

U kunt een deel van een object Catalog bijwerken door de id ervan op te nemen in het pad van een PATCH-aanvraag. In dit document worden de twee methoden beschreven voor het uitvoeren van PATCH-bewerkingen op catalogusobjecten:

* Velden gebruiken
* JSON-patchnotatie gebruiken

>[!NOTE] Met PATCH-bewerkingen op een object kunnen de uitbreidbare velden, die onderling verwante objecten vertegenwoordigen, niet worden gewijzigd.  Wijzigingen in onderling verwante objecten moeten rechtstreeks worden aangebracht.

## Bijwerken met velden

In het volgende voorbeeld wordt getoond hoe u een object kunt bijwerken met behulp van velden en waarden.

**API-indeling**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden bijgewerkt. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Het volgende verzoek werkt de `name` en `description` gebieden van een dataset aan de waarden bij die in de lading worden verstrekt. Objectvelden die niet moeten worden bijgewerkt, kunnen worden uitgesloten van de laadbewerking.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**Antwoord**

Een succesvolle reactie keert een serie terug die identiteitskaart van de bijgewerkte dataset bevat. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. Het uitvoeren van een GET verzoek voor deze dataset toont nu dat slechts `name` en `description` zijn bijgewerkt terwijl alle andere waarden onveranderd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Bijwerken met JSON Patch-notatie

De volgende voorbeeldvraag toont aan hoe te om een voorwerp bij te werken gebruikend Reparatie JSON, zoals geschetst in [RFC-6902](https://tools.ietf.org/html/rfc6902).

<!-- (Include once API fundamentals guide is published) 

For more information on JSON Patch syntax, see the [API fundamentals guide](). 

-->

**API-indeling**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden bijgewerkt. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

Met het volgende verzoek worden de `name` en `description` velden van een gegevensset bijgewerkt naar de waarden die in elk JSON-object Patch worden opgegeven. Wanneer u JSON Patch gebruikt, moet u ook de header Content-Type instellen op `application/json-patch+json`.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**Antwoord**

Een geslaagde reactie retourneert een array met de id van het bijgewerkte object. Deze id moet overeenkomen met de id die in de PATCH-aanvraag is verzonden. Wanneer u een GET-aanvraag voor dit object uitvoert, geeft dit nu aan dat alleen de aanvraag `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
