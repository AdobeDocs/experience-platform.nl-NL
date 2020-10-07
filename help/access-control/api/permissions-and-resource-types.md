---
keywords: Experience Platform;home;popular topics;access control permissions;access control resource types;access control api
solution: Experience Platform
title: De namen van de lijst van toestemmingen en middeltypes
topic: developer guide
description: Met toegangsbeheer in Adobe Experience Platform kunt u rollen en machtigingen voor verschillende mogelijkheden van Platforms beheren met de Adobe Admin Console. U kunt van de namen van alle toestemmingen en middeltypes een lijst maken door een verzoek van de GET aan het /acl/verwijzingspunten te richten. Deze namen kunnen vervolgens worden gebruikt in API-aanroepen om effectief beleid voor de huidige gebruiker weer te geven.
translation-type: tm+mt
source-git-commit: 28b733a16b067f951a885c299d59e079f0074df8
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# De namen van de lijst van toestemmingen en middeltypes

U kunt van de namen van alle toestemmingen en middeltypes een lijst maken door een verzoek van de GET tot het `/acl/reference` eindpunt te richten. Deze namen kunnen vervolgens worden gebruikt in API-aanroepen om effectief beleid [voor de huidige gebruiker](./effective-policies.md) weer te geven.

Een toestemming is een beleid dat door Adobe Admin Console wordt beheerd, en kaarten aan nul of meer middel-type beleid. Een middeltype is een beleid dat lees toelaat, schrijft, en/of schrapt mogelijkheden voor een specifiek type van [!DNL Platform] middel (zoals datasets of schema&#39;s).

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
