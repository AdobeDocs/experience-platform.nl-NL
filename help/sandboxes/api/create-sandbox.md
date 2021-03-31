---
keywords: Experience Platform;home;populaire onderwerpen;Sandbox;sandbox
solution: Experience Platform
title: Een sandbox maken in de API
topic: ontwikkelaarsgids
description: U kunt een nieuwe zandbak tot stand brengen door een verzoek van de POST aan het `/zandbakeneindpunt te richten.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 0%

---


# Een sandbox maken in de API

U kunt een nieuwe zandbak tot stand brengen door een verzoek van de POST aan het `/sandboxes` eindpunt te richten.

**API-indeling**

```http
POST /sandboxes
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe ontwikkelingssandbox gemaakt met de naam &quot;dev-3&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De id die wordt gebruikt voor toegang tot de sandbox in toekomstige aanvragen. Deze waarde moet uniek zijn, en de beste praktijken moeten het zo beschrijvend mogelijk maken. Kan geen spaties of hoofdletters bevatten. |
| `title` | Een leesbare naam die voor weergavedoeleinden in de gebruikersinterface van het Platform wordt gebruikt. |
| `type` | Het type sandbox dat moet worden gemaakt. Momenteel kan een organisatie alleen sandboxen van het type &quot;ontwikkeling&quot; maken. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat de `state` &#39;maakt&#39;.

```json
{
    "name": "dev-3",
    "title": "Development 3",
    "state": "creating",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Sandboxen nemen ongeveer 15 minuten in beslag om door het systeem te worden ingericht, waarna hun `state` &quot;actief&quot; of &quot;mislukt&quot; worden.
