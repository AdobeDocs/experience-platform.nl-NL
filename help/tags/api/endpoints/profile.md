---
title: Profielen, eindpunt
description: Leer hoe te om vraag aan het /profiles eindpunt in Reactor API te maken.
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---

# Profieleindpunt

In de Reactor-API vertegenwoordigt een profiel een Adobe Experience Platform-gebruiker. De Reactor-API beschikt niet over een eigen database met gebruikers en machtigingen en is in plaats daarvan afhankelijk van Adobe-id&#39;s die worden beheerd door het identiteitsbeheersysteem (IMS)](https://helpx.adobe.com/enterprise/using/identity.html) van [Adobe.

Een profiel bevat alle informatie over de aangemelde gebruiker, inclusief alle IMS-organisaties waartoe ze behoren, de productprofielen waartoe ze behoren binnen elke organisatie en de rechten die ze hebben van elk productprofiel.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/experience-platform-apis/references/reactor/). Lees voordat u doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe u de API kunt verifiëren.

## Het huidige profiel ophalen {#lookup}

U kunt de details van het momenteel het programma geopende profiel terugwinnen door een verzoek van de GET tot het `/profile` eindpunt te richten.

**API-indeling**

```http
GET /profile
```

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Als de reactie is gelukt, worden de details van het profiel geretourneerd.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{IMS_ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{IMS_ORG_1}": {
          "name": "Example IMS Org A",
          "admin": true,
          "active": true,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_audiencemanager_int",
            "dma_tartan",
            "dma_dtm",
            "dma_reactor",
            "dma_auditor"
          ],
          "tenant_id": "{TENANT_ID_1}"
        },
        "{IMS_ORG_2}": {
          "name": "Example IMS Org B",
          "admin": false,
          "active": false,
          "login_companies": [

          ],
          "product_contexts": [
            "dma_reactor",
            "dma_auditor",
            "dma_tartan"
          ],
          "tenant_id": "{TENANT_ID_2}"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/profile"
    },
    "meta": {
      "rights": [
        "manage_companies"
      ]
    }
  }
}
```

