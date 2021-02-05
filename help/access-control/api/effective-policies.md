---
keywords: Experience Platform;thuis;populaire onderwerpen;effectief beleid;toegangsbeheer api
solution: Experience Platform
title: Efficiënt beleid API-eindpunt
topic: developer guide
description: Met toegangsbeheer in Adobe Experience Platform kunt u rollen en machtigingen voor verschillende mogelijkheden van Platforms beheren met de Adobe Admin Console. Dit document dient als richtlijn voor het weergeven van effectief beleid met behulp van de API voor toegangsbeheer voor Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 0%

---


# Doeltreffend beleidseindpunt

Om efficiënt beleid voor de huidige gebruiker te bekijken, doe een verzoek van de POST aan het `/acl/effective-policies` eindpunt in [!DNL Access Control] API. De toestemmingen en middeltypes u wilt terugwinnen moeten in de verzoeklading in de vorm van een serie worden verstrekt. Dit wordt geïllustreerd in de voorbeeld-API-aanroep hieronder.

**API-indeling**

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
    "/permissions/manage-datasets",
    "/resource-types/schemas"
  ]'
```

>[!NOTE]
>
>Voor een volledige lijst van toestemmingen en middeltypes die in de ladingsserie kunnen worden verstrekt, zie de bijlage sectie op [toegelaten toestemmingen en middeltypes](#accepted-permissions-and-resource-types).

**Antwoord**

Een succesvolle reactie keert informatie over de toestemmingen en middeltypes terug die in het verzoek worden verstrekt. De reactie omvat de actieve toestemmingen de huidige gebruiker voor de middeltypes die in het verzoek worden gespecificeerd. Als om het even welke toestemmingen inbegrepen in de verzoeklading voor de huidige gebruiker actief zijn, keert API de toestemming met een koord (`*`) terug om erop te wijzen dat de toestemming actief is. Eventuele machtigingen die in de aanvraag zijn opgegeven en die niet actief zijn voor de gebruiker, worden weggelaten uit de antwoordlading.

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

Dit document besprak hoe te om vraag aan [!DNL Access Control] API te maken om informatie over actieve toestemmingen en verwant beleid voor middeltypes terug te keren. Voor meer informatie over toegangsbeheer voor [!DNL Experience Platform], zie [toegangsbeheeroverzicht](../home.md).

## Aanhangsel

Deze sectie bevat aanvullende informatie voor het gebruik van de [!DNL Access Control]-API.

### Toegelaten toestemmingen en middeltypes

Het volgende is een lijst van toestemmingen en middeltypes u in de nuttige lading van een verzoek van de POST aan het `/acl/active-permissions` eindpunt kunt omvatten.

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

**Brontypen**

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
