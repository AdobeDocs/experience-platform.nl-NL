---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Effectief beleid weergeven
topic: developer guide
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Effectief beleid weergeven

Om efficiënt beleid voor de huidige gebruiker te bekijken, doe een POST- verzoek aan het `/acl/effective-policies` eindpunt in Toegangsbeheer API. De toestemmingen en middeltypes u wilt terugwinnen moeten in de verzoeklading in de vorm van een serie worden verstrekt. Dit wordt geïllustreerd in de voorbeeld-API-aanroep hieronder.

**API-indeling**

```http
POST /acl/effective-policies
```

**Verzoek**

De volgende verzoeken wint informatie over de &quot;Manage toestemmingen van Datasets&quot;en toegang tot het &quot;schema&#39;s&quot;middeltype voor de huidige gebruiker terug.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE] Voor een volledige lijst van toestemmingen en middeltypes die in de ladingsserie kunnen worden verstrekt, zie de bijlage sectie over [toegelaten toestemmingen en middeltypes](#accepted-permissions-and-resource-types).

**Antwoord**

Een succesvolle reactie keert informatie over de toestemmingen en middeltypes terug die in het verzoek worden verstrekt. De reactie omvat de actieve toestemmingen de huidige gebruiker voor de middeltypes die in het verzoek worden gespecificeerd. Als om het even welke toestemmingen inbegrepen in de verzoeklading voor de huidige gebruiker actief zijn, keert API de toestemming met een lawaai (`*`) terug om erop te wijzen dat de toestemming actief is. Eventuele machtigingen die in de aanvraag zijn opgegeven en die niet actief zijn voor de gebruiker, worden weggelaten uit de antwoordlading.

```json
{
    "policies": {
        "/resource-types/schemas": [
            "read",
            "write",
            "delete"
        ],
        "/permissions/manage-datasets": [
            "*"
        ]
    }
}
```

## Volgende stappen

In dit document wordt beschreven hoe u aanroepen van de API voor toegangsbeheer kunt uitvoeren om informatie te retourneren over actieve machtigingen en het bijbehorende beleid voor typen bronnen. Voor meer informatie over toegangsbeheer voor het Platform van de Ervaring, zie het overzicht [van de](../home.md)toegangscontrole.

## Aanhangsel

Deze sectie biedt aanvullende informatie voor het gebruik van de API voor toegangsbeheer.

### Toegelaten toestemmingen en middeltypes

Het volgende is een lijst van toestemmingen en middeltypes u in de lading van een POST- verzoek aan het `/acl/active-permissions` eindpunt kunt omvatten.

**Machtigingen**

```plaintext
"permissions/activate-destinations"
"permissions/export-audience-for-segments"
"permissions/manage-datasets"
"permissions/manage-destinations"
"permissions/manage-identity-namespaces"
"permissions/manage-profiles"
"permissions/manage-sandboxes"
"permissions/manage-schemas"
"permissions/reset-sandboxes"
"permissions/view-datasets"
"permissions/view-destinations"
"permissions/view-identity-namespaces"
"permissions/view-monitoring-dashboard"
"permissions/view-profiles"
"permissions/view-sandboxes"
"permissions/view-schemas"
```

**Brontypen**

```plaintext
"resource-types/classes"
"resource-types/connections"
"resource-types/data-types"
"resource-types/dataset-data"
"resource-types/datasets"
"resource-types/destinations"
"resource-types/dule-labels"
"resource-types/identity-descriptors"
"resource-types/identity-namespaces"
"resource-types/mixins"
"resource-types/monitoring"
"resource-types/profile-configs
"resource-types/profile-datasets"
"resource-types/profiles"
"resource-types/relationship-descriptors"
"resource-types/reset-sandboxes"
"resource-types/sandboxes"
"resource-types/schemas"
"resource-types/segment-jobs"
"resource-types/segments"
```
