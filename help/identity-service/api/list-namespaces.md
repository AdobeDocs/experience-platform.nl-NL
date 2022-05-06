---
keywords: Experience Platform;home;populaire onderwerpen;naamruimtelijst;naamruimte voor lijst
solution: Experience Platform
title: Beschikbare naamruimten weergeven
topic-legacy: API guide
description: Alle beschikbare naamruimten weergeven.
exl-id: b65e5f86-143d-4ca5-8b3f-2c0a24433bbf
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '79'
ht-degree: 2%

---

# Beschikbare naamruimten weergeven

**API-indeling**

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

**Antwoord**

De reactie bevat een array met objecten, waarbij elk object een beschikbare naamruimte vertegenwoordigt. Naamruimten met een &quot;[!UICONTROL custom]&quot; waarde van &quot;[!UICONTROL false]&quot; zijn standaardnaamruimten, terwijl die met een &quot;[!UICONTROL custom]&quot; waarde van &quot;[!UICONTROL true]&quot; zijn naamruimten die uw organisatie heeft gemaakt.

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

Ga naar de volgende zelfstudie om [een aangepaste naamruimte maken](./create-custom-namespace.md)
