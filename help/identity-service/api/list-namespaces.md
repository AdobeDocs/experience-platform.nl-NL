---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschikbare naamruimten weergeven
topic: API guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie bevat een array met objecten, waarbij elk object een beschikbare naamruimte vertegenwoordigt. Naamruimten met de waarde &quot;custom&quot; van &quot;false&quot; zijn standaardnaamruimten, terwijl naamruimten met de waarde &quot;custom&quot; van &quot;true&quot; naamruimten zijn die uw organisatie heeft gemaakt.

>[!NOTE] Deze reactie is afgebroken voor de ruimte.

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

Ga naar de volgende zelfstudie om een aangepaste naamruimte te [maken](./create-custom-namespace.md)