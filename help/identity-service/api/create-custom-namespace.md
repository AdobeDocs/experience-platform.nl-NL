---
keywords: Experience Platform;home;populaire onderwerpen;naamruimte;Naamruimte;naamruimten;Naamruimten;Naamruimte;Naamruimte;Identiteitsnaamruimte;Identiteit;Identiteit
solution: Experience Platform
title: Een aangepaste naamruimte maken in de API voor de identiteitsservice
description: Met de API Naamruimte-id kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.
role: Developer
exl-id: 6015a225-4508-49cc-9dda-fb9f73a8746c
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---

# Een aangepaste naamruimte maken in de Identity Service API

Met de API van [!DNL Identity Namespace] kunt u een naamruimte voor een aangepaste identiteit maken die alleen voor uw organisatie beschikbaar is.

Voor aanbevelingen rond het creëren van douane namespaces, zie [&#x200B; de documentatie van Veelgestelde vragen van de Dienst van de Identiteit &#x200B;](../troubleshooting-guide.md).

>[!NOTE]
>
>Naamruimten zijn een kwalificatie voor identiteiten. Als zodanig kan een naamruimte niet worden verwijderd nadat deze is gemaakt.

**API formaat**

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

**Reactie**

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

Ga aan het volgende leerprogramma te werk [&#x200B; lijst inheemse identiteitskaart van een identiteit &#x200B;](./list-native-id.md)
