---
keywords: Experience Platform;home;populaire onderwerpen;api;Op kenmerk-Gebaseerd Toegangsbeheer;op attributen-gebaseerd toegangsbeheer
solution: Experience Platform
title: API-eindpunt voor producten
description: Het /products eindpunt in op attributen-Gebaseerde Controle API van de Toegang staat u toe om producten in Adobe Experience Platform programmatically te beheren.
role: Developer
exl-id: 44ee9a9d-7a13-4d59-a1a9-97764dbd3763
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 1%

---

# Het eindpunt van producten

>[!NOTE]
>
>Als een gebruikerstoken wordt overgegaan, dan moet de gebruiker van het teken een &quot;org admin&quot;rol voor gevraagde org hebben.

Het `/products` eindpunt in op attribuut-gebaseerde toegangsbeheer API staat u toe om producten evenals toestemmingscategorieën en toestemmingsreeksen programmatically te beheren verbonden aan producten in uw organisatie.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt maakt deel uit van op attribuut-gebaseerde toegangsbeheer API. Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke Experience Platform API met succes te maken.

## Een lijst met producten met rechten ophalen {#list}

U kunt een lijst met producten met rechten ophalen door een GET-aanvraag in te dienen bij het eindpunt van `/products` .

**API formaat**

```http
GET /products/
```

**Verzoek**

In het volgende verzoek wordt een lijst opgehaald met producten die tot uw organisatie behoren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvolle reactie keert een lijst van gerechtigde producten terug die tot uw organisatie behoren.

```json
{
  "products": [
    {
      "id": "{ID}",
      "name": "Adobe Experience Platform",
      "serviceCode": "{SERVICE_CODE}"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De bijbehorende id van het betrokken product. |
| `name` | De naam van het product waarop de vraag betrekking heeft. |
| `serviceCode` | De overeenkomstige dienstcode van het onderzochte product. |

## Machtigingscategorieën opzoeken op product-id

U kunt machtigingencategorieën voor een bepaald product opzoeken door een GET-aanvraag in te dienen bij het eindpunt van `/products/{PRODUCT_ID}/categories` terwijl u uw product-id opgeeft.

**API formaat**

```http
GET /products/{PRODUCT_ID}/categories
```

| Parameter | Beschrijving |
| --- | --- |
| {PRODUCT_ID} | De id van het product die is gekoppeld aan de machtigingencategorieën die u wilt opzoeken. |

**Verzoek**

Met de volgende aanvraag worden machtigingscategorieën opgehaald die aan `{PRODUCT_ID}` zijn gekoppeld.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/categories \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvolle reactie keert de toestemmingscategorieën verbonden aan productID terug u vroeg.

```json
{
  "categories": [
    {
        "name": "Profile Management"
    },
    {
        "name": "Data Ingestion"
    },
    {
        "name": "Sandbox Administration"
    },
    {
        "name": "Query Service"
    },
    {
        "name": "Data Management"
    },
    {
        "name": "Identity Management"
    },
    {
        "name": "Data Modeling"
    },
    {
        "name": "Data Science Workspace"
    },
    {
        "name": "Dashboards"
    },
    {
        "name": "Alerts"
    },
    {
        "name": "Data Governance"
    }
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `category` | De machtigingscategorieën die beschikbaar zijn in de desbetreffende product-id. |
| `name` | De naam van de categorie met bevoegdheden. |

## Machtigingssets opzoeken op product-id

U kunt rechtensets opzoeken voor een bepaald product door een GET-aanvraag in te dienen bij het eindpunt van `/products/{PRODUCT_ID}/permission-sets` terwijl u uw product-id opgeeft.

**API formaat**

```http
GET /products/{PRODUCT_ID}/permission-sets
```

| Parameter | Beschrijving |
| --- | --- |
| {PRODUCT_ID} | De id van het product dat is gekoppeld aan de rechtensets die u wilt opzoeken. |

**Verzoek**

De volgende aanvraag haalt rechtensets op die zijn gekoppeld aan `{PRODUCT_ID}` .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/access-control/administration/products/{PRODUCT_ID}/permission-sets \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
```

**Reactie**

Een succesvolle reactie keert de toestemmingsreeksen verbonden aan productID terug u vroeg.

```json
{
  "permission-sets": [
      {
          "id": "manage-schemas",
          "name": "Manage Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read",
                      "write",
                      "delete"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
      {
          "id": "view-schemas",
          "name": "View Schemas",
          "category": "Data Modeling",
          "permissions": [
              {
                  "resource": "schemas",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "schema-fields",
                  "actions": [
                      "read"
                  ]
              },
              {
                  "resource": "sandboxes",
                  "actions": [
                      "view"
                  ]
              }
          ]
      },
  ]
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `permission-sets` | Machtigingssets vertegenwoordigen een groep machtigingen die een beheerder op een rol kan toepassen. Een beheerder kan rechtensets toewijzen aan een rol in plaats van individuele machtigingen toe te wijzen. Dit staat u toe om douanerollen van een vooraf bepaalde rol tot stand te brengen die een groep toestemmingen bevat. |
| `id` | De bijbehorende id van de set met bevoegdheden waarnaar wordt gevraagd. |
| `name` | De corresponderende naam van de desbetreffende rechtenset. |
| `category` | De beschikbare machtigingencategorie. |
| `permissions` | De toestemmingen omvatten de capaciteit om de eigenschappen van Experience Platform te bekijken en/of te gebruiken, zoals het creëren van zandbakken, het bepalen van schema&#39;s, en het beheren van datasets. |
| `permissions.resource` | Het element of object waartoe een onderwerp al dan niet toegang heeft. Bronnen kunnen bestanden, toepassingen, servers of zelfs API&#39;s zijn. |
| `permissions.actions` | De handeling die een onderwerp mag uitvoeren tegen een bron met vragen. Mogelijke waarden zijn: `view` , `read` , `create` , `edit` en `delete` |
