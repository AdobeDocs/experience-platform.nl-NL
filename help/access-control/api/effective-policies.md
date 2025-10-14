---
keywords: Experience Platform;thuis;populaire onderwerpen;effectief beleid;toegangsbeheer api
solution: Experience Platform
title: Efficiënt beleid API-eindpunt
description: Leer hoe u effectief toegangsbeleid kunt weergeven met de API voor toegangsbeheer voor Adobe Experience Platform.
role: Developer
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Doeltreffend beleidseindpunt

>[!NOTE]
>
>Als een gebruikerstoken wordt overgegaan, dan moet de gebruiker van het teken een &quot;org admin&quot;rol voor gevraagde org hebben.

Als u effectief toegangsbeheerbeleid voor de huidige gebruiker wilt weergeven, vraagt u een POST naar het eindpunt `/acl/effective-policies` in de [!DNL Access Control] API. De toestemmingen en middeltypes u wilt terugwinnen moeten in de verzoeklading in de vorm van een serie worden verstrekt. Dit wordt geïllustreerd in de voorbeeld-API-aanroep hieronder.

**API formaat**

```http
POST /acl/effective-policies
```

**Verzoek**

De volgende verzoeken wint informatie over &quot;[!UICONTROL Manage Datasets]&quot;toestemming en toegang tot &quot;[!UICONTROL schemas]&quot;middeltype voor de huidige gebruiker terug.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/access-control/acl/effective-policies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Voor een volledige lijst van toestemmingen en middeltypes die in de nuttige ladingsserie kunnen worden verstrekt, zie de bijlage sectie op [&#x200B; toegelaten toestemmingen en middeltypes &#x200B;](#accepted-permissions-and-resource-types).

**Reactie**

Een succesvolle reactie keert informatie over de toestemmingen en middeltypes terug die in het verzoek worden verstrekt. De reactie omvat de actieve toestemmingen de huidige gebruiker voor de middeltypes die in het verzoek worden gespecificeerd. Als om het even welke toestemmingen inbegrepen in de verzoeklading voor de huidige gebruiker actief zijn, keert API de toestemming met een asterisk (`*`) terug om erop te wijzen dat de toestemming actief is. Eventuele machtigingen die in de aanvraag zijn opgegeven en die niet actief zijn voor de gebruiker, worden weggelaten uit de antwoordlading.

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

In dit document wordt beschreven hoe u aanroepen van de [!DNL Access Control] API kunt uitvoeren om informatie te retourneren over actieve machtigingen en het gerelateerde toegangsbeleid voor typen bronnen. Voor meer informatie over toegangsbeheer voor [!DNL Experience Platform], zie het [&#x200B; overzicht van de toegangscontrole &#x200B;](../home.md).

## Bijlage

Deze sectie bevat aanvullende informatie voor het gebruik van de [!DNL Access Control] API.

### Toegelaten toestemmingen en middeltypes

Hier volgt een lijst met machtigingen en typen bronnen die u kunt opnemen in de lading van een verzoek van een POST aan het `/acl/active-permissions` -eindpunt.

**Toestemmingen**

```plaintext
permissions/activate-destinations
permissions/evaluate-segments
permissions/execute-decisioning-activities
permissions/export-audience-for-segment
permissions/manage-datasets
permissions/manage-decisioning-activities
permissions/manage-decisioning-options
permissions/manage-destinations
permissions/manage-dsw
permissions/manage-dule-labels
permissions/manage-dule-policies
permissions/manage-identity-namespaces
permissions/manage-privacy-workflows
permissions/manage-profile-configs
permissions/manage-profiles
permissions/manage-queries
permissions/manage-schemas
permissions/manage-segments
permissions/manage-sources
permissions/reset-sandboxes
permissions/view-datasets
permissions/view-destinations
permissions/view-dule-labels
permissions/view-dule-policies
permissions/view-identity-namespaces
permissions/view-monitoring-dashboard
permissions/view-privacy-workflows
permissions/view-profile-configs
permissions/view-profiles
permissions/view-sandboxes
permissions/view-schemas
permissions/view-segments
permissions/view-sources
```

**types van Middel**

```plaintext
resource-types/activation-associations
resource-types/activations
resource-types/activities
resource-types/analytics-source
resource-types/audience-manager-source
resource-types/bizible-source
resource-types/connection
resource-types/customer-attributes-source
resource-types/data-science-workspace
resource-types/dataset-preview
resource-types/datasets
resource-types/dule-label
resource-types/dule-policy
resource-types/enterprise-source
resource-types/identity-descriptor
resource-types/identity-namespaces
resource-types/launch-source
resource-types/marketing-action
resource-types/marketo-source
resource-types/monitoring
resource-types/offers
resource-types/placements
resource-types/privacy-consent
resource-types/privacy-content-delivery
resource-types/privacy-job
resource-types/profile-configs
resource-types/profile-datasets
resource-types/profiles
resource-types/query
resource-types/relationship-descriptor
resource-types/sandboxes
resource-types/schemas
resource-types/segment-jobs
resource-types/segments
resource-types/streaming-source
```
