---
keywords: Experience Platform;thuis;populaire onderwerpen;effectief beleid;toegangsbeheer api
solution: Experience Platform
title: Efficiënt beleid API-eindpunt
topic-legacy: developer guide
description: Met toegangsbeheer in Adobe Experience Platform kunt u rollen en machtigingen voor verschillende mogelijkheden van Platforms beheren met de Adobe Admin Console. Dit document dient als richtlijn voor het weergeven van effectief beleid met behulp van de API voor toegangsbeheer voor Adobe Experience Platform.
exl-id: 555d73db-115d-4f4c-8bd2-b91477799591
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 0%

---

# Doeltreffend beleidseindpunt

Om effectief beleid voor de huidige gebruiker te bekijken, doe een verzoek van de POST aan `/acl/effective-policies` in de [!DNL Access Control] API. De toestemmingen en middeltypes u wilt terugwinnen moeten in de verzoeklading in de vorm van een serie worden verstrekt. Dit wordt geïllustreerd in de voorbeeld-API-aanroep hieronder.

**API-indeling**

```http
POST /acl/effective-policies
```

**Verzoek**

Met de volgende verzoeken wordt informatie opgehaald over &quot;[!UICONTROL Manage Datasets]&quot; toestemming en toegang tot &quot;[!UICONTROL schemas]&quot; resource type voor de huidige gebruiker.

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
>Voor een volledige lijst van toestemmingen en middeltypes die in de ladingsserie kunnen worden verstrekt, zie de bijlage sectie op [geaccepteerde machtigingen en brontypen](#accepted-permissions-and-resource-types).

**Antwoord**

Een succesvolle reactie keert informatie over de toestemmingen en middeltypes terug die in het verzoek worden verstrekt. De reactie omvat de actieve toestemmingen de huidige gebruiker voor de middeltypes die in het verzoek worden gespecificeerd. Als er machtigingen in de payload van de aanvraag actief zijn voor de huidige gebruiker, retourneert de API de bevoegdheid met een asterisk (`*`) om aan te geven dat de machtiging actief is. Eventuele machtigingen die in de aanvraag zijn opgegeven en die niet actief zijn voor de gebruiker, worden weggelaten uit de antwoordlading.

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

In dit document wordt beschreven hoe u de [!DNL Access Control] API om informatie over actieve toestemmingen en verwant beleid voor middeltypes terug te keren. Voor meer informatie over toegangsbeheer voor [!DNL Experience Platform], zie de [toegangsbeheeroverzicht](../home.md).

## Aanhangsel

Deze sectie verstrekt aanvullende informatie voor het gebruiken van [!DNL Access Control] API.

### Toegelaten toestemmingen en middeltypes

Hier volgt een lijst met machtigingen en typen bronnen die u kunt opnemen in de lading van een verzoek van een POST aan de `/acl/active-permissions` eindpunt.

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
