---
keywords: Experience Platform;home;popular topics;find sandbox;look up a sandbox
solution: Experience Platform
title: Sandbox opzoeken
topic: developer guide
description: U kunt een afzonderlijke sandbox opzoeken door een aanvraag voor een GET in te dienen waarin de eigenschap name van de sandbox is opgenomen in het aanvraagpad.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Sandbox opzoeken

U kunt een afzonderlijke sandbox opzoeken door een verzoek in te dienen om de `name` eigenschap van de sandbox op te nemen in het aanvraagpad.

**API-indeling**

```http
GET /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag wordt een sandbox met de naam &quot;dev-2&quot; opgehaald.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de sandbox, inclusief de sandbox `name`, `title`, `state`en `type`.

```json
{
    "name": "dev-2",
    "title": "Development 2",
    "state": "creating",
    "type": "development",
    "region": "VA7",
    "isDefault": false,
    "eTag": 1,
    "createdDate": "2019-09-07 10:16:02",
    "lastModifiedDate": "2019-09-07 10:16:02",
    "createdBy": "{USER_ID}",
    "modifiedBy": "{USER_ID}"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De naam van de sandbox. Wordt gebruikt voor opzoekdoeleinden in API-aanroepen. |
| `title` | De weergavenaam voor de sandbox. |
| `state` | De huidige verwerkingsstatus van de sandbox. De status van een sandbox kan een van de volgende zijn: <ul><li>**maken**: De sandbox is gemaakt, maar wordt nog steeds door het systeem ingericht.</li><li>**actief**: De sandbox wordt gemaakt en actief.</li><li>**mislukt**: Door een fout kon de sandbox niet door het systeem worden ingericht en is deze uitgeschakeld.</li><li>**geschrapt**: De sandbox is handmatig uitgeschakeld.</li></ul> |
| `type` | Het type sandbox, &#39;development&#39; of &#39;production&#39;. |
| `isDefault` | Een Booleaanse eigenschap die aangeeft of deze sandbox de standaardsandbox voor de organisatie is. Dit is doorgaans de productiesandbox. |
| `eTag` | Een id voor een specifieke versie van de sandbox. Deze waarde wordt gebruikt voor versiebeheer en caching-efficiëntie en wordt telkens bijgewerkt wanneer een wijziging in de sandbox wordt aangebracht. |