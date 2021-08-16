---
title: Ondernemingen, eindpunt
description: Leer hoe te om vraag aan het /companies eindpunt in Reactor API te maken.
source-git-commit: 59592154eeb8592fa171b5488ecb0385e0e59f39
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

---

# Ondernemingen, eindpunt

Een bedrijf vertegenwoordigt een klantenorganisatie, typisch een zaken. In de Reactor-API komen deze bedrijven overeen met 1:1 met IMS-organisatie-id. API-gebruikers hebben alleen zichtbaarheid in de bedrijven waartoe ze toegang hebben. Een bedrijf kan vele [eigenschappen](./properties.md) bevatten. Een eigendom behoort tot precies één bedrijf.

Het `/companies` eindpunt in Reactor API staat u toe om de bedrijven programmatically terug te winnen die u binnen uw ervaringstoepassing hebt toegang tot.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml). Lees voordat u doorgaat de [gids Aan de slag](../getting-started.md) voor belangrijke informatie over hoe u de API kunt verifiëren.

## Een lijst met bedrijven ophalen {#list}

U kunt van de bedrijven een lijst maken die u wordt gemachtigd om te gebruiken door een verzoek van de GET tot het `/companies` eindpunt te richten. In de meeste gevallen is er precies één.

**API-indeling**

```http
GET /companies
```

>[!NOTE]
>
>Gebruikend vraagparameters, kunnen de beursgenoteerde bedrijven worden gefiltreerd gebaseerd op de volgende attributen:<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>Zie de gids op [het filtreren reacties](../guides/filtering.md) voor meer informatie.

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvolle reactie keert een lijst van bedrijven terug die u toegang tot hebt.

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{IMS_ORG}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
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

## Een bedrijf opzoeken {#lookup}

U kunt een specifiek bedrijf opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET te omvatten.

**API-indeling**

```http
GET /companies/{COMPANY_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{COMPANY_ID}` | De `id` waarde van het bedrijf u omhoog wilt kijken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**Antwoord**

Een succesvol antwoord geeft de details van het bedrijf terug.

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{IMS_ORG}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
