---
keywords: Experience Platform;home;populaire onderwerpen;identity xid;XID
solution: Experience Platform
title: Native ID ophalen voor een identiteit
description: Identiteitsgegevens worden doorgaans verstrekt als een ID-tekenreekswaarde en naamruimte in opgenomen XDM-gegevens en wanneer een identiteit wordt opgegeven voor gebruik in een API-aanroep. Wanneer identiteiten in de Dienst van de Identiteit worden voortgeduurd, wordt een identiteitskaart geproduceerd en aan die identiteit toegewezen, genoemd inheemse XID. Platform-API's die ondersteuning voor identiteitsgegevens vereisen, gebruiken dit compactere formulier voor de samengevoegde id en naamruimte. XID is een base64-gecodeerde tekenreeks.
role: Developer
exl-id: e734f5d8-e00b-43fa-b06c-97c73e1f7c71
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Native id ophalen voor een identiteit

Identiteitsgegevens worden doorgaans verstrekt als een ID-tekenreekswaarde en naamruimte in opgenomen XDM-gegevens en wanneer een identiteit wordt opgegeven voor gebruik in een API-aanroep. Wanneer identiteiten behouden blijven in [!DNL Identity Service], wordt een id gegenereerd en toegewezen aan die identiteit, genaamd de native XID. [!DNL Platform] API&#39;s die ondersteuning voor identiteitsgegevens vereisen, gebruiken dit compactere formulier voor de samengevoegde id en naamruimte. XID is een base64-gecodeerde tekenreeks.

>[!NOTE]
>
>Dit formaat is hoofdzakelijk voor gebruik binnen de Adobe. Native XID als een enkelvoudige waarde is ruimteefficiënter en is wat intern binnen wordt gebruikt [!DNL Platform] oplossingen voor opslag en serialisatie. Het is echter niet leesbaar voor mensen, het is ondoorzichtig en vereist een aparte aanroep om het te gebruiken.

Verkrijg XID voor een bepaalde waarde van identiteitskaart en namespace gebruikend de dienst die in deze sectie wordt beschreven.

**API-indeling**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/identity?namespace={NAMESPACE}&id={ID_VALUE}
```

**Verzoek**

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/identity?namespace=email&id=test@adobetest.com' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

```json
{
    "xid":"BVrqzwVuzbXrLfmnaG3rXrLf3KJg"
}
```
