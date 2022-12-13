---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheertoestemmingen;de types van toegangsbeheermiddel;toegangsbeheer api
solution: Experience Platform
title: Referentie-API-eindpunt
topic-legacy: developer guide
description: Het verwijzingspunten in Toegangsbeheer API staat u toe om de namen van beschikbare toestemmingen en middeltypes te bekijken, die dan kunnen worden gebruikt om efficiënt toegangsbeheerbeleid voor de huidige gebruiker te bekijken.
exl-id: 18d84d54-9258-4451-9aa8-7c647b45a8da
source-git-commit: 38447348bc96b2f3f330ca363369eb423efea1c8
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Referentie-eindpunt

U kunt een lijst maken van de namen van alle toestemmingen en middeltypes door een verzoek van de GET tot de `/acl/reference` eindpunt. Deze namen kunnen vervolgens worden gebruikt in API-aanroepen naar [doeltreffend beleid voor toegangscontrole weergeven](./effective-policies.md) voor de huidige gebruiker.

Een toestemming is een beleid dat door Adobe Admin Console wordt beheerd, en kaarten aan nul of meer middel-type beleid. Een middeltype is een beleid dat gelezen toelaat, schrijft, en/of schrapt mogelijkheden voor een specifiek type van [!DNL Platform] bron (zoals datasets of schema&#39;s).

**API-indeling**

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

**Antwoord**

Een geslaagde reactie retourneert een `permissions` en `resource-types` object, elk met een volledige lijst met namen voor respectievelijk toegangsmachtigingen of typen bronnen.

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
