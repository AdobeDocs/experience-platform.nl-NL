---
keywords: Experience Platform;home;populaire onderwerpen;Sandbox;sandbox
solution: Experience Platform
title: Een sandbox maken in de API
topic: ontwikkelaarsgids
description: U kunt een nieuwe zandbak tot stand brengen door een verzoek van de POST aan het `/zandbakeneindpunt te richten.
translation-type: tm+mt
source-git-commit: ee2fb54ba59f22a1ace56a6afd78277baba5271e
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 0%

---


# Een sandbox maken in de API

U kunt een ontwikkeling of productiestandaard tot stand brengen door een verzoek van de POST aan het `/sandboxes` eindpunt te doen.

## Een ontwikkelingssandbox maken

Als u een ontwikkelingssandbox wilt maken, vraagt u een POST naar het `/sandboxes`-eindpunt en geeft u de waarde `development` op voor de eigenschap `type`.

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
  -H 'Content-Type: application/json' \
  -d '{
    "name": "dev-3",
    "title": "Development 3",
    "type": "development"
  }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De id die wordt gebruikt voor toegang tot de sandbox in toekomstige aanvragen. Deze waarde moet uniek zijn, en de beste praktijken moeten het zo beschrijvend mogelijk maken. Deze waarde mag geen spaties of speciale tekens bevatten. |
| `title` | Een leesbare naam die voor weergavedoeleinden in de gebruikersinterface van het Platform wordt gebruikt. |
| `type` | Het type sandbox dat moet worden gemaakt. De waarde voor het `type` bezit kan of ontwikkeling of productie zijn. |

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

## Een productiesandbox maken

>[!NOTE]
>
>De functie Meerdere productiesandboxen is in bèta.

Als u een productiesandbox wilt maken, vraagt u een POST naar het `/sandboxes`-eindpunt en geeft u de waarde `production` op voor de eigenschap `type`.

**API-indeling**

```http
POST /sandboxes
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe productiesandbox gemaakt met de naam &quot;test-prod-sandbox&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/sandbox-management/sandboxes \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "test-prod-sandbox",
    "title": "Test Production Sandbox",
    "type": "production"
}'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `name` | De id die wordt gebruikt voor toegang tot de sandbox in toekomstige aanvragen. Deze waarde moet uniek zijn, en de beste praktijken moeten het zo beschrijvend mogelijk maken. Deze waarde mag geen spaties of speciale tekens bevatten. |
| `title` | Een leesbare naam die voor weergavedoeleinden in de gebruikersinterface van het Platform wordt gebruikt. |
| `type` | Het type sandbox dat moet worden gemaakt. De waarde voor het `type` bezit kan of ontwikkeling of productie zijn. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe sandbox, waarbij wordt getoond dat de `state` &#39;maakt&#39;.

```json
{
    "name": "test-production-sandbox",
    "title": "Test Production Sandbox",
    "state": "creating",
    "type": "production",
    "region": "VA7"
}
```
