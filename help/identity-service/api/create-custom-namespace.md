---
keywords: Experience Platform;home;popular topics;namespace;Namespace;namespaces;Namespaces;identity namespace;Identity namespace;identity;Identity
solution: Experience Platform
title: Een aangepaste naamruimte maken
topic: API guide
description: Met de API Naamruimte-id kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.
translation-type: tm+mt
source-git-commit: 3376d6cace9ab196f457e2bf7b84cde06693103c
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 2%

---


# Een aangepaste naamruimte maken

Met behulp van de [!DNL Identity Namespace] API kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.

Raadpleeg [de documentatie](../troubleshooting-guide.md)bij Identiteitsservice voor aanbevelingen over het maken van aangepaste naamruimten.

>[!NOTE]
>
>Naamruimten zijn een kwalificatie voor identiteiten. Als zodanig kan een naamruimte niet worden verwijderd nadat deze is gemaakt.

**API-indeling**

```http
POST /idnamespace/identities
```

**Verzoek**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/idnamespace/identities \
  -H 'Accept-Encoding: gzip, deflate' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -d '{
        "name": "Loyalty Member",
        "code": "Loyalty",
        "description": "Loyalty Program Member ID",
        "idType": "Cross_device"
      }'
```

**Antwoord**

```json
{
    "updateTime": 1576286879075,
    "code": "Loyalty",
    "status": "ACTIVE",
    "description": "Loyalty Program Member ID",
    "id": 10093197,
    "createTime": 1576286879075,
    "idType": "Cross_device",
    "name": "Loyalty Member",
    "custom": true
}
```

## Volgende stappen

Ga naar de volgende zelfstudie om de native id van een identiteit [weer te geven](./list-native-id.md)