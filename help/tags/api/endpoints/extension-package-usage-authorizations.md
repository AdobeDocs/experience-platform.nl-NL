---
title: Eindpunt voor autorisaties voor extensiepakket
description: Leer hoe te om vraag aan het /extension_package_usage toestemmingeneindpunt in Reactor API te maken.
exl-id: ad3fb704-7d2f-45ec-b80b-ea4d327f2205
source-git-commit: 9cdd349e0eccb4498d88f24a84b0f1c116b0adfe
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 1%

---

# Het eindpunt van de gebruiksautorisaties voor extensiepakketten

Een uitbreidingspakket vertegenwoordigt een [&#x200B; uitbreiding &#x200B;](./extensions.md) zoals authored door een uitbreidingsontwikkelaar. Aanvullende functies die beschikbaar kunnen worden gesteld aan gebruikers van tags, worden gedefinieerd door een extensiepakket. Deze mogelijkheden kunnen belangrijkste modules en gedeelde modules omvatten, hoewel zij het vaakst als [&#x200B; regelcomponenten &#x200B;](./rule-components.md) (gebeurtenissen, voorwaarden, en acties) en [&#x200B; gegevenselementen &#x200B;](./data-elements.md) worden verstrekt.

Een uitbreidingspakket wordt bezeten door het bedrijf van de ontwikkelaar [&#128279;](./companies.md). Eigenaars van extensiepakketten kunnen andere bedrijven toestaan hun persoonlijke versies van de pakketten te gebruiken. Elke geautoriseerde onderneming krijgt een gebruiksvergunning voor één extensiepakket, dat geldig is voor alle toekomstige en huidige privéversies van het pakket.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [&#x200B; Reactor API &#x200B;](https://www.adobe.io/experience-platform-apis/references/reactor/). Alvorens verder te gaan, te herzien gelieve [&#x200B; begonnen gids &#x200B;](../getting-started.md) voor belangrijke informatie betreffende hoe te voor authentiek te verklaren aan API.

## Licenties voor het gebruik van extensiepakketten ophalen voor een extensiepakket {#list}

Om een lijst van gebruiksvergunningen voor een uitbreidingspakket terug te winnen, doe een verzoek van de GET aan het volgende eindpunt.

**API formaat**

```http
GET /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschrijving |
| --- | --- |
| `{PROPERTY_ID}` | De `ID` van de eigenschap waarvan u de gebruiksmachtiging voor het extensiepakket wilt weergeven. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een succesvolle reactie keert een lijst van uitbreidingspakketten terug.

```json
{
  "data": [
    {
      "id": "EA722482c30fe44b54aa6a7317890b3bdb",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:35.776Z",
        "updated_at": "2024-06-05T23:17:35.776Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "example@adobe.com",
        "created_by_display_name": "john snow",
        "updated_by_email": "Restricted",
        "updated_by_display_name": "Restricted"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb/extension_package"
          },
          "data": {
            "id": "EPecefc8291ae346c3b3887d5b2da533b8",
            "type": "extension_packages"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA722482c30fe44b54aa6a7317890b3bdb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## Een gebruiksvergunning voor een extensiepakket maken {#create}

Creeer een vergunning van het het gebruikspakket van de extensiepakket voor elk [&#x200B; uitbreidingspakket &#x200B;](./extension-packages.md) en `{ORG_ID}` van de organisatie u wilt machtigen. Om een nieuwe vergunning van het het gebruikspakket van de extensiepakket tot stand te brengen, doe een verzoek van de POST aan het hieronder eindpunt.

**API formaat**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschrijving |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | De `ID` van het extensiepakket waarvoor u een autorisatie wilt maken.&quot; |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes.authorized_org_id` | De `ID` van de organisatie die u wilt autoriseren. |

**Reactie**

Een succesvolle reactie retourneert de details van de nieuwe gebruiksautorisatie voor het uitbreidingspakket.

```json
{
  "data": {
    "id": "EA35d0e731f73645e6972df9fcac101434",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:30.308Z",
      "updated_at": "2024-06-05T23:17:30.308Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "pending_approval",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "Restricted",
      "updated_by_display_name": "Restricted"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
        },
        "data": {
          "id": "EP43649cc8856d4f09a7c2a21a4b1e449d",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
    }
  }
}
```

>[!NOTE]
>
>In het bovenstaande voorbeeldantwoord bevindt de autorisatie zich momenteel in het `pending_approval` -werkgebied. Alvorens het extensiepakket te gebruiken, moet de organisatie de vergunning goedkeuren. Gebruikers van de organisatie kunnen door het persoonlijke extensiepakket bladeren terwijl de autorisatie in afwachting is van goedkeuring, maar ze kunnen het niet installeren en vinden het niet in hun extensiecatalogus.

## Een lijst met gebruiksmachtigingen voor extensiepakketten ophalen {#list-authorizations}

U kunt een lijst met gebruiksmachtigingen voor extensiepakketten ophalen door een aanvraag voor een GET in te dienen.

**API formaat**

```http
GET /extension_package_usage_authorizations
```

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een succesvolle reactie keert een lijst van uitbreidingspakketten terug.

```json
{
  "data": [
    {
      "id": "EA35d0e731f73645e6972df9fcac101434",
      "type": "extension_package_usage_authorizations",
      "attributes": {
        "created_at": "2024-06-05T23:17:30.308Z",
        "updated_at": "2024-06-05T23:17:30.308Z",
        "name": "Acme",
        "platform": "web",
        "owner_org_id": "{ORG_ID}",
        "owner_org_name": "Reactor QE",
        "authorized_org_id": "{ORG_ID}",
        "authorized_org_name": "Acme Inc'",
        "state": "pending_approval",
        "created_by_email": "Restricted",
        "created_by_display_name": "Restricted",
        "updated_by_email": "example@adobe.com",
        "updated_by_display_name": "john snow"
      },
      "relationships": {
        "extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434/extension_package"
          },
          "data": null
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA35d0e731f73645e6972df9fcac101434"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/extension_package_usage_authorizations?page%5Bnumber%5D=3&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": 2,
      "prev_page": null,
      "total_pages": 3,
      "total_count": 57
    }
  }
}
```

## Een gebruiksvergunning voor extensiepakketten verwijderen {#delete}

Als u een gebruiksautorisatie voor extensiepakketten wilt verwijderen, neemt u de `ID` ervan op in het pad van een DELETE-aanvraag. Zo voorkomt u dat de geautoriseerde organisatie de privéversies van het extensiepakket in de catalogus weergeeft en het op de eigenschappen installeert.

>[!NOTE]
>
>Eerder geïnstalleerde privéversies blijven werken zoals u had verwacht.

**API formaat**

```http
DELETE /extension_package_usage_authorizations/{ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `ID` | De `ID` van de gebruiksmachtiging voor het extensiepakket die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**Reactie**

Een geslaagde reactie retourneert HTTP-status 204 (Geen inhoud) zonder hoofdtekst van de reactie. Dit geeft aan dat de extensie is verwijderd.

## Een gebruiksvergunning voor een extensiepakket bijwerken {#update}

Als u een gebruiksautorisatie voor een extensiepakket wilt goedkeuren of afwijzen, neemt u de `ID` ervan op in het pad van een PATCH-aanvraag.

>[!NOTE]
>
>U moet `manage_properties` rechten hebben om een gebruiksvergunning voor extensiepakketten voor uw bedrijf goed te keuren of af te wijzen.

**API formaat**

```http
PATCH /extension_package_usage_authorizations/{ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `ID` | De `ID` van de gebruiksmachtiging voor het extensiepakket die u wilt verwijderen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
          },
          "type": "extension_package_usage_authorizations",
          "id": "EA86f54b48dd7042a68686508e03be8ba9"
        }
      } 
```

| Eigenschap | Beschrijving |
| --- | --- |
| `attributes` | De kenmerken die u wilt herzien. Voor vergunningen voor het gebruik van extensiepakketten kunt u de `state` ervan herzien. |

**Reactie**

Een succesvolle reactie retourneert de details van de herziene gebruiksvergunning voor extensiepakketten.

```json
{
  "data": {
    "id": "EA86f54b48dd7042a68686508e03be8ba9",
    "type": "extension_package_usage_authorizations",
    "attributes": {
      "created_at": "2024-06-05T23:17:59.480Z",
      "updated_at": "2024-06-05T23:18:00.115Z",
      "name": "Acme",
      "platform": "web",
      "owner_org_id": "{ORG_ID}",
      "owner_org_name": "Reactor QE",
      "authorized_org_id": "{ORG_ID}",
      "authorized_org_name": "Acme Inc'",
      "state": "approved",
      "created_by_email": "Restricted",
      "created_by_display_name": "Restricted",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9/extension_package"
        },
        "data": {
          "id": "EPb91d54cad9f749dba4e5566459f84c9c",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_package_usage_authorizations/EA86f54b48dd7042a68686508e03be8ba9"
    }
  }
}
```

>[!NOTE]
>
>Zodra de vergunning wordt goedgekeurd, kan uw organisatie het uitbreidingspakket op uw eigenschappen installeren.

## Gegevens ophalen voor het extensiepakket voor een gebruiksvergunning voor een extensiepakket {#retrieve-data}

U kunt gegevens voor het extensiepakket voor een gebruiksautorisatie voor een extensiepakket ophalen door een GET-aanvraag in te dienen.

**API formaat**

```http
GET /extension_package_usage_authorizations/{ID}/extension_package
```

| Parameter | Beschrijving |
| --- | --- |
| `ID` | De `ID` van de gebruiksmachtiging voor het extensiepakket die u wilt ophalen. |

{style="table-layout:auto"}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/extension_package_usage_authorizations/{ID}/extension_package \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Reactie**

Een geslaagde reactie retourneert gegevens voor een extensiepakket voor een autorisatie van een extensiepakket.

```json
{
  "data": {
    "id": "EP45ae063fd75c4c22936d3d456c858cfa",
    "type": "extension_packages",
    "attributes": {
      "actions": [],
      "author": {
        "url": "http://adobe.com",
        "name": "Acme",
        "email": "acme@adobe.com"
      },
      "availability": "private",
      "cdn_path": "https://assets.adobedtm.com/staging/extensions/EP45ae063fd75c4c22936d3d456c858cfa",
      "conditions": [],
      "configuration": null,
      "created_at": "2024-06-05T23:17:48.607Z",
      "data_elements": [],
      "description": "Provides nothing.",
      "discontinued": false,
      "display_name": "Acme Template Test",
      "ecma_version": null,
      "events": [],
      "exchange_url": null,
      "hosted_lib_files": null,
      "icon_path": "resources/icons/core.svg",
      "main": "null",
      "name": "Acme",
      "owner_org_id": "{ORG_ID}",
      "resources": null,
      "shared_modules": null,
      "status": "succeeded",
      "platform": "web",
      "updated_at": "2024-06-05T23:17:53.806Z",
      "version": "1.0.0",
      "view_base_path": "dist/",
      "created_by_email": "example@adobe.com",
      "created_by_display_name": "john snow",
      "updated_by_email": "example@adobe.com",
      "updated_by_display_name": "john snow"
    },
    "relationships": {
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa/extension_package_usage_authorizations"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/extension_packages/EP45ae063fd75c4c22936d3d456c858cfa"
    }
  }
}
```
