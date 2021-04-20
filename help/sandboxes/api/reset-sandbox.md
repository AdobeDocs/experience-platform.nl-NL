---
keywords: Experience Platform;home;populaire onderwerpen;sandbox opnieuw instellen
solution: Experience Platform
title: Een sandbox in de API opnieuw instellen
topic: developer guide
description: Ontwikkelingssandboxen beschikken over een functie voor fabrieksinstellingen waarmee alle niet-standaardbronnen uit een sandbox worden verwijderd. U kunt een sandbox opnieuw instellen door een PUT-aanvraag in te dienen die de naam van de sandbox in het aanvraagpad bevat.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 1%

---


# Een sandbox in de API opnieuw instellen

Ontwikkelingssandboxen beschikken over een functie voor fabrieksinstellingen waarmee alle niet-standaardbronnen uit een sandbox worden verwijderd. U kunt een sandbox opnieuw instellen door een verzoek voor een PUT in te dienen dat de sandbox `name` bevat in het aanvraagpad.

**API-indeling**

```http
PUT /sandboxes/{SANDBOX_NAME}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SANDBOX_NAME}` | De eigenschap `name` van de sandbox die u wilt herstellen. |

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

Een succesvol antwoord retourneert de details van de bijgewerkte sandbox, waarbij wordt getoond dat `state` opnieuw wordt ingesteld.

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
>Wanneer een sandbox opnieuw is ingesteld, duurt het ongeveer 15 minuten voordat het systeem de sandbox heeft ingericht. Nadat de sandbox is ingericht, wordt `state` &quot;actief&quot; of &quot;mislukt&quot;.