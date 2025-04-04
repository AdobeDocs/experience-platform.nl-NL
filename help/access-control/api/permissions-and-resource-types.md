---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheermachtigingen;toegangsbeheermiddeltypen;toegangsbeheerAPI
solution: Experience Platform
title: Referentie-API-eindpunt
description: Het verwijzingspunten in Toegangsbeheer API staat u toe om de namen van beschikbare toestemmingen en middeltypes te bekijken, die dan kunnen worden gebruikt om efficiënt toegangsbeheerbeleid voor de huidige gebruiker te bekijken.
role: Developer
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Referentie-eindpunt

>[!NOTE]
>
>Als een gebruikerstoken wordt overgegaan, dan moet de gebruiker van het teken een &quot;org admin&quot;rol voor gevraagde org hebben.

U kunt een lijst maken van de namen van alle toestemmingen en middeltypes door een GET- verzoek aan het `/acl/reference` eindpunt te doen. Deze namen kunnen dan in API vraag worden gebruikt aan [ mening efficiënt toegangsbeheerbeleid ](./effective-policies.md) voor de huidige gebruiker.

Een toestemming is een beleid dat door Adobe Admin Console wordt beheerd, en kaarten aan nul of meer middel-type beleid. Een middeltype is een beleid dat lees toelaat, schrijft, en/of schrapt mogelijkheden voor een specifiek type van [!DNL Experience Platform] middel (zoals datasets of schema&#39;s).

**API formaat**

```http
GET /acl/reference
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/acl/reference \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Reactie**

Een geslaagde reactie retourneert een `permissions` -object en een `resource-types` -object, elk met een volledige lijst met namen voor respectievelijk toegangsmachtigingen en typen bronnen.

```json
{
  "permissions": {
    "export-audience-for-segment": {
      "segments": [
        "read"
      ]
    },
    "manage-datasets": {
      "connection": [
        "read",
        "write",
        "delete"
      ],
      "datasets": [
        "read",
        "write",
        "delete"
      ]
    }
    {"..."}
  },
  "resource-types": {
    "classes": [
      "read",
      "write",
      "delete"
    ],
    "connection": [
      "read",
      "write",
      "delete"
    ],
    "data-types": [
      "read",
      "write",
      "delete"
    ],
    "...": [
      "..."
    ]
  }
}
```
