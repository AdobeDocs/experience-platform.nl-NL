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

U kunt een deel van een [!DNL Catalog] -object bijwerken door de id ervan op te nemen in het pad van een PATCH-aanvraag. In dit document worden de twee methoden beschreven voor het uitvoeren van PATCH-bewerkingen op Catalog-objecten:

* Velden gebruiken
* JSON-patchnotatie gebruiken

>[!NOTE]
>
>PATCH-bewerkingen op een object kunnen de uitbreidbare velden van het object, die onderling verwante objecten vertegenwoordigen, niet wijzigen. Wijzigingen in onderling verwante objecten moeten rechtstreeks worden aangebracht.

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

Een succesvolle reactie keert een serie terug die identiteitskaart van de bijgewerkte dataset bevat. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. Wanneer u een GET-aanvraag voor deze gegevensset uitvoert, tonen nu dat alleen de `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## Bijwerken met JSON Patch-notatie

De volgende voorbeeldvraag toont aan hoe te om een voorwerp bij te werken gebruikend Reparatie JSON, zoals die in [ wordt geschetst rFC-6902 ](https://tools.ietf.org/html/rfc6902).

Voor meer informatie over de syntaxis van het Reparatie JSON, zie de [ API grondbeginselen gids ](../../landing/api-fundamentals.md#json-patch).

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

Een geslaagde reactie retourneert een array met de id van het bijgewerkte object. Deze id moet overeenkomen met de id die in de aanvraag voor PATCH is verzonden. Wanneer u een GET-aanvraag voor dit object uitvoert, tonen nu dat alleen de waarden `name` en `description` zijn bijgewerkt terwijl alle andere waarden ongewijzigd blijven.

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
