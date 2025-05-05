---
keywords: Experience Platform;thuis;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Gegevensmodel;Gegevensmodel;audit;controlelogboek;changelog;veranderingslogboek;rpc;
solution: Experience Platform
title: Logboek-API-eindpunt controleren
description: Het /auditlog eindpunt in de Registratie API van het Schema staat u toe om een chronologische lijst van veranderingen terug te winnen die aan een bestaand middel XDM zijn aangebracht.
exl-id: 8d33ae7c-0aa4-4f38-a183-a2ff1801e291
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 1%

---

# Het eindpunt van het controlelogboek

Voor elke bron van het Gegevensmodel van de Ervaring (XDM), [!DNL Schema Registry] handhaaft een logboek van alle veranderingen die tussen verschillende updates zijn voorgekomen. Met het `/auditlog` -eindpunt in de [!DNL Schema Registry] API kunt u een controlelogboek ophalen voor een klasse, schemaveldgroep, gegevenstype of schema dat door de id is opgegeven.

## Aan de slag

Het eindpunt dat in deze gids wordt gebruikt maakt deel uit van [[!DNL Schema Registry]  API ](https://www.adobe.io/experience-platform-apis/references/schema-registry/). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welk Experience Platform API met succes te maken.

Het `/auditlog` eindpunt maakt deel uit van de verre procedurevraag (RPCs) die door [!DNL Schema Registry] wordt gesteund. In tegenstelling tot andere eindpunten in de [!DNL Schema Registry] API, vereisen RPC-eindpunten geen extra kopteksten zoals `Accept` of `Content-Type` en gebruiken ze geen `CONTAINER_ID` . In plaats daarvan moeten ze de naamruimte `/rpc` gebruiken, zoals wordt getoond in de API-aanroep hieronder.

## Hiermee wordt een controlelogbestand voor een bron opgehaald

U kunt een controlelogboek voor om het even welke klasse, gebiedsgroep, gegevenstype, of schema terugwinnen binnen de Bibliotheek van het Schema door identiteitskaart van het middel in de weg van een verzoek van de GET aan het `/auditlog` eindpunt te specificeren.

**API formaat**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de bron waarvan u het auditlogboek wilt ophalen. |

{style="table-layout:auto"}

**Verzoek**

Het volgende verzoek wint het controlelogboek voor een schema terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.schemas.50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een chronologische lijst van veranderingen terug die in het middel worden aangebracht, van meest recente tot minst recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "a14NMF0jd6BIfyXaHdTDl4bC4R0r9rht",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
        "xdmType": "schemas",
        "action": "remove",
        "path": "/meta:usageCount",
        "value": 0
      }
    ]
  },
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/schemas/50649eb1b040bf042d6400a0335901cd2a97d31a4eac4330",
    "updatedUser": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
    "updatedTime": "02-19-2021 05:43:56",
    "requestId": "pFQbgmWrdbJrNB9GdxTSGECpXYWspu68",
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "updates": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltySunday_ABC",
        "value": {
          "title": "LoyaltySundayABC",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/classes/11052164b588f0c29584bf6ae1a6663a59aa65426c82389f",
        "xdmType": "classes",
        "action": "remove",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/loyaltyMoxee_XYZ",
        "value": {
          "title": "LoyaltyMoxeeXYZ",
          "description": "",
          "type": "string",
          "isRequired": false,
          "required": [],
          "meta:xdmType": "string"
        }
      }
    ]
  }
]
```

| Eigenschap | Beschrijving |
| --- | --- |
| `updates` | Een array van objecten, waarbij elk object een wijziging vertegenwoordigt die is aangebracht in de opgegeven bron of een van de afhankelijke bronnen ervan. |
| `id` | De `$id` van de bron die is gewijzigd. Deze waarde vertegenwoordigt typisch het middel dat in de verzoekweg wordt gespecificeerd, maar kan een afhankelijke middel vertegenwoordigen als dat de bron van de verandering is. |
| `xdmType` | Het type bron dat is gewijzigd. |
| `action` | Het type wijziging dat is aangebracht. |
| `path` | A [&#128279;](../../landing/api-fundamentals.md#json-pointer) koord dat van de Aanwijzer JSON  op de weg wijst aan het specifieke gebied dat werd veranderd of toegevoegd. |
| `value` | De waarde die is toegewezen aan het nieuwe of bijgewerkte veld. |

{style="table-layout:auto"}
