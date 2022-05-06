---
keywords: Experience Platform;home;populaire onderwerpen;naamruimte;Naamruimte;naamruimten;Naamruimten;Naamruimte;Naamruimte;Identiteitsnaamruimte;Identiteit;Identiteit
solution: Experience Platform
title: Een aangepaste naamruimte maken in de API voor de identiteitsservice
topic-legacy: API guide
description: Met de API Naamruimte-id kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 1%

---

# Een aangepaste naamruimte maken in de Identity Service API

Met de [!DNL Identity Namespace] API, kunt u een naamruimte van de aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.

Zie voor aanbevelingen over het maken van aangepaste naamruimten [de documentatie bij de veelgestelde vragen over de identiteitsservice](../troubleshooting-guide.md).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

Ga naar de volgende zelfstudie om [de native id van een identiteit weergeven](./list-native-id.md)
