---
keywords: Experience Platform;home;populaire onderwerpen;lijstsandboxen
solution: Experience Platform
title: API-eindpunt voor sandboxtypen
topic-legacy: developer guide
description: U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET aan het /sandboxTypes eindpunt te richten.
exl-id: eb5e1b44-37f5-4ed5-98f5-ac8db8792c7d
source-git-commit: f5ce7b7f09c624c53065757bb8a9b09f989dce0a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 1%

---

# Standaardboxtypen, eindpunt

U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET tot het `/sandboxTypes` eindpunt te richten.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Sandbox] API](https://www.adobe.io/experience-platform-apis/references/sandbox). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API te kunnen uitvoeren.

## Een lijst met ondersteunde sandboxtypen ophalen

U kunt een lijst van gesteunde zandbaktypes voor uw organisatie terugwinnen door een verzoek van de GET tot het `/sandboxTypes` eindpunt te richten.

**API-indeling**

```http
GET /sandboxTypes
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxTypes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met sandboxtypen die worden ondersteund voor uw organisatie.

```json
{
    "sandboxTypes": [
        "production",
        "development"
    ]
}
```
