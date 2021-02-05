---
keywords: Experience Platform;home;populaire onderwerpen;naamruimte;Naamruimte;naamruimten;Naamruimten;Naamruimte;Naamruimte;Identiteitsnaamruimte;Identiteit;Identiteit
solution: Experience Platform
title: Een aangepaste naamruimte maken in de API voor de identiteitsservice
topic: API guide
description: Met de API Naamruimte-id kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.
translation-type: tm+mt
source-git-commit: 73035aec86297cfc4ee9337cf922d599001379c3
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 1%

---


# Een aangepaste naamruimte maken in de Identity Service API

Met de API [!DNL Identity Namespace] kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.

Raadpleeg [de documentatie bij Veelgestelde vragen over identiteitsservice](../troubleshooting-guide.md) voor aanbevelingen over het maken van aangepaste naamruimten.

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

Ga naar de volgende zelfstudie om de native id van een identiteit ](./list-native-id.md) weer te geven[