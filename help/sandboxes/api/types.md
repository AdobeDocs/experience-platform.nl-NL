---
keywords: Experience Platform;home;populaire onderwerpen;lijstsandboxen
solution: Experience Platform
title: API-eindpunt voor sandboxtypen
description: U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET aan het /sandboxTypes eindpunt te richten.
role: Developer
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 1%

---

# Standaardboxtypen, eindpunt

U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET aan het `/sandboxTypes` eindpunt te richten.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Sandbox]  API ](https://www.adobe.io/experience-platform-apis/references/sandbox). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

## Een lijst met ondersteunde sandboxtypen ophalen

U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET aan het `/sandboxTypes` eindpunt te richten.

**API formaat**

```http
GET /sandboxTypes
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**Reactie**

Een geslaagde reactie retourneert een lijst met sandboxtypen die worden ondersteund voor uw organisatie.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
