---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Een sandbox maken
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Een sandbox maken

U kunt een nieuwe sandbox maken door een POST-aanvraag in te dienen bij het `/sandboxes` eindpunt.

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

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat deze `state` is &#39;gemaakt&#39;.

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
>Sandboxen nemen ruwweg 15 minuten in beslag om door het systeem te worden ingericht, waarna de sandboxen &quot;actief&quot; of &quot;mislukt&quot; `state` worden.
