---
keywords: Experience Platform;home;popular topics;reset sandbox
solution: Experience Platform
title: Een sandbox opnieuw instellen
topic: developer guide
description: Ontwikkelingssandboxen beschikken over een functie voor fabrieksinstellingen waarmee alle niet-standaardbronnen uit een sandbox worden verwijderd. U kunt een sandbox opnieuw instellen door een PUT-aanvraag in te dienen die de naam van de sandbox in het aanvraagpad bevat.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 1%

---


# Een sandbox opnieuw instellen

Ontwikkelingssandboxen beschikken over een functie voor fabrieksinstellingen waarmee alle niet-standaardbronnen uit een sandbox worden verwijderd. U kunt een sandbox opnieuw instellen door een PUT-aanvraag in te dienen die de sandbox&#39;s bevat `name` in het aanvraagpad.

**API-indeling**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De `name` eigenschap van de sandbox die u wilt herstellen. |

**Verzoek**

Met de volgende aanvraag wordt een sandbox met de naam &quot;dev-2&quot; opnieuw ingesteld.

```shell
curl -X PUT \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes/dev-2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "action": "reset"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `action` | Deze parameter moet in de payload van de aanvraag worden opgegeven met de waarde &quot;reset&quot; om de sandbox opnieuw in te stellen. |

**Antwoord**

Wanneer de reactie met succes is uitgevoerd, worden de details van de bijgewerkte sandbox geretourneerd, waarbij wordt getoond dat de sandbox opnieuw `state` wordt ingesteld.

```json
{
    "id": "d8184350-dbf5-11e9-875f-6bf1873fec16",
    "name": "dev-2",
    "title": "Development 2",
    "state": "resetting",
    "type": "development",
    "region": "VA7"
}
```

>[!NOTE]
>
>Wanneer een sandbox opnieuw is ingesteld, duurt het ongeveer 15 minuten voordat het systeem de sandbox heeft ingericht. Nadat de sandbox is ingericht, `state` wordt deze actief of mislukt.