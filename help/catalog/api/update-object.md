---
keywords: Experience Platform;home;populaire onderwerpen;catalogus;api;een object bijwerken
solution: Experience Platform
title: Een catalogusobject bijwerken
description: U kunt een deel van een object Catalog bijwerken door de id ervan op te nemen in het pad van een PATCH-aanvraag. Dit document behandelt het gebruik van velden en het gebruik van JSON Patch-notatie voor het uitvoeren van PATCH-bewerkingen op Catalog-objecten.
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 296a988a67871933723ad0474c113cb93fdbf255
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---

# Een catalogusobject bijwerken

U kunt een deel van een [!DNL Catalog] -object door de id ervan op te nemen in het pad van een PATCH-aanvraag. In dit document worden de twee methoden beschreven voor het uitvoeren van PATCH-bewerkingen op Catalog-objecten:

* Velden gebruiken
* JSON-patchnotatie gebruiken

>[!NOTE]
>
>PATCH-bewerkingen op een object kunnen de uitbreidbare velden van het object, die onderling verwante objecten vertegenwoordigen, niet wijzigen. Wijzigingen in onderling verwante objecten moeten rechtstreeks worden aangebracht.

## Bijwerken met velden

In het volgende voorbeeld wordt getoond hoe u een object kunt bijwerken met behulp van velden en waarden.

**API-indeling**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type van [!DNL Catalog] te bijwerken object. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

De volgende aanvraag werkt de `name` en `description` velden van een gegevensset naar de waarden in de lading. Objectvelden die niet moeten worden bijgewerkt, kunnen worden uitgesloten van de laadbewerking.

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

**Antwoord**

Een succesvolle reactie keert een serie terug die identiteitskaart van de bijgewerkte dataset bevat. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. Het uitvoeren van een GET verzoek voor deze dataset toont nu dat slechts `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Bijwerken met JSON Patch-notatie

In het volgende voorbeeld wordt getoond hoe u een object kunt bijwerken met JSON Patch, zoals in [RFC-6902](https://tools.ietf.org/html/rfc6902).

Zie voor meer informatie over de JSON Patch-syntaxis de [Handleiding voor API-basisbeginselen](../../landing/api-fundamentals.md#json-patch).

**API-indeling**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type van [!DNL Catalog] te bijwerken object. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | De id van het specifieke object dat u wilt bijwerken. |

**Verzoek**

De volgende aanvraag werkt de `name` en `description` velden van een gegevensset naar de waarden in elk JSON-object Patch. Wanneer u JSON Patch gebruikt, moet u ook de header Content-Type instellen op `application/json-patch+json`.

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

**Antwoord**

Een geslaagde reactie retourneert een array met de id van het bijgewerkte object. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. Wanneer u een GET-aanvraag voor dit object uitvoert, wordt nu alleen getoond dat `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
