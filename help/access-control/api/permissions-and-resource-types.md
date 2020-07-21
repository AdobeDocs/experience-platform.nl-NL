---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: De namen van de lijst van toestemmingen en middeltypes
topic: developer guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# De namen van de lijst van toestemmingen en middeltypes

U kunt van de namen van alle toestemmingen en middeltypes een lijst maken door een GET verzoek aan het `/acl/reference` eindpunt te doen. Deze namen kunnen vervolgens worden gebruikt in API-aanroepen om effectief beleid [voor de huidige gebruiker](./effective-policies.md) weer te geven.

Een **toestemming** is een beleid dat door de Admin Console van Adobe wordt beheerd, en kaarten aan nul of meer middel-type beleid. Een **middeltype** is een beleid dat lees toelaat, schrijft, en/of schrapt mogelijkheden voor een specifiek type van [!DNL Platform] middel (zoals datasets of schema&#39;s).

**API-indeling**

```http
GET /acl/reference
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwoord**

Een geslaagde reactie retourneert een `permissions` object en een `resource-types` object, elk met een volledige lijst met namen voor respectievelijk toegangsmachtigingen of typen bronnen.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
