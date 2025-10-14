---
title: Profielen, eindpunt
description: Leer hoe te om vraag aan het /profiles eindpunt in Reactor API te maken.
exl-id: d0434098-f49a-45f3-9772-488bd3c134aa
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 1%

---

# Profieleindpunt

In de Reactor-API vertegenwoordigt een profiel een Adobe Experience Platform-gebruiker. Reactor API handhaaft zijn eigen gegevensbestand van gebruikers en toestemmingen niet, en baseert in plaats daarvan op Adobe IDs die door [&#x200B; wordt beheerd het systeem van het identiteitsbeheer van de Adobe (IMS) &#x200B;](https://helpx.adobe.com/nl/enterprise/using/identity.html).

Een profiel bevat alle informatie over de aangemelde gebruiker, met inbegrip van alle organisaties waartot zij behoren, de productprofielen zij tot binnen elk Org behoren, en de rechten zij van elk productprofiel hebben.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [&#x200B; Reactor API &#x200B;](https://www.adobe.io/experience-platform-apis/references/reactor/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../getting-started.md) voor belangrijke informatie betreffende hoe te voor authentiek te verklaren aan API.

## Het huidige profiel ophalen {#lookup}

U kunt de details van het momenteel het programma geopende profiel terugwinnen door een verzoek van de GET tot het `/profile` eindpunt te richten.

**API formaat**

```http
GET /profile
```

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/profile \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Als de reactie is gelukt, worden de details van het profiel geretourneerd.

```json
{
  "data": {
    "id": "UR0bd696624e844d6ba5bfc248ba1eca11",
    "type": "users",
    "attributes": {
      "active_org": "{ORG_1}",
      "expires_in": 0,
      "display_name": "John Smith",
      "job_function": null,
      "email": "jsmith@example.com",
      "organizations": {
        "{ORG_1}": {
          "name": "Example organization A",
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
        "{ORG_2}": {
          "name": "Example organization B",
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
