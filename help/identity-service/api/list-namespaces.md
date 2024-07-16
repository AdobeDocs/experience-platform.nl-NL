---
keywords: Experience Platform;home;populaire onderwerpen;naamruimtelijst;naamruimte voor lijst
solution: Experience Platform
title: Beschikbare naamruimten weergeven
description: Alle beschikbare naamruimten weergeven.
role: Developer
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 0%

---

# Beschikbare naamruimten weergeven

**API formaat**

```http
GET /idnamespace/identities
```

**Verzoek**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/idnamespace/identities' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

De reactie bevat een array met objecten, waarbij elk object een beschikbare naamruimte vertegenwoordigt. Namespaces met een &quot;[!UICONTROL custom]&quot;waarde van &quot;[!UICONTROL false]&quot;zijn standaardnamespaces, terwijl die met een &quot;[!UICONTROL custom]&quot;waarde van &quot;[!UICONTROL true]&quot;zijn namespaces die uw organisatie heeft gecreeerd.

>[!NOTE]
>
>Deze reactie is afgebroken voor de ruimte.

```json
[
  {
        "updateTime": 1441122419000,
        "code": "CORE",
        "status": "ACTIVE",
        "description": "CORE Namespace",
        "id": 0,
        "createTime": 1441122419000,
        "idType": "COOKIE",
        "name": "CORE",
        "custom": false
    },
    {
        "updateTime": 1495153678000,
        "code": "ECID",
        "status": "ACTIVE",
        "description": "ECID Namespace",
        "id": 4,
        "createTime": 1495153678000,
        "idType": "COOKIE",
        "name": "ECID",
        "custom": false
    },
    {
        "updateTime": 1522783145000,
        "code": "AdCloud",
        "status": "ACTIVE",
        "description": "Adobe AdCloud - ID Syncing Partner",
        "id": 411,
        "createTime": 1522783145000,
        "idType": "COOKIE",
        "name": "AdCloud",
        "custom": false
    }
]
```

## Volgende stappen

Ga aan het volgende leerprogramma te werk om [ een douane te creëren namespace ](./create-custom-namespace.md)
