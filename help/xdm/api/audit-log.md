---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;audit;audit log;changelog;change log;rpc;
solution: Experience Platform
title: Handleiding voor het eindpunt van het logboek controleren
description: Het /auditlog eindpunt in de Registratie API van het Schema staat u toe om een chronologische lijst van veranderingen terug te winnen die aan een bestaand middel XDM zijn aangebracht.
topic: developer guide
translation-type: tm+mt
source-git-commit: eb5e34dc3b48a6fe0757635cad1df08caa68b019
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 1%

---


# Het eindpunt van het controlelogboek

Voor elke bron van het Gegevensmodel van de Ervaring (XDM), [!DNL Schema Registry] handhaaft een logboek van alle veranderingen die tussen verschillende updates zijn voorgekomen. Het `/auditlog` eindpunt in [!DNL Schema Registry] API staat u toe om een controlelogboek voor om het even welke klasse terug te winnen, mixin, gegevenstype, of schema dat door identiteitskaart wordt gespecificeerd.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/mixin-registry.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API te kunnen uitvoeren.

Het `/auditlog` eindpunt is deel van de verre procedurevraag (RPCs) die door [!DNL Schema Registry] wordt gesteund. In tegenstelling tot andere eindpunten in de [!DNL Schema Registry] API, vereisen RPC eindpunten geen extra kopballen zoals `Accept` of `Content-Type`, en gebruiken geen `CONTAINER_ID`. In plaats daarvan moeten ze de naamruimte `/rpc` gebruiken, zoals in de API-aanroep hieronder wordt getoond.

## Hiermee wordt een controlelogbestand voor een bron opgehaald

U kunt een controlelogboek voor om het even welke klasse terugwinnen, mengt, gegevenstype, of schema binnen de Bibliotheek van het Schema door identiteitskaart van het middel in de weg van een verzoek van de GET aan het `/auditlog` eindpunt te specificeren.

**API-indeling**

```http
GET /rpc/auditlog/{RESOURCE_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{RESOURCE_ID}` | De `meta:altId` of URL-gecodeerde `$id` van de bron waarvan het controlelogboek u wilt terugwinnen. |

**Verzoek**

Het volgende verzoek wint het controlelogboek voor een `Restaurant` mengsel terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/rpc/auditlog/_{TENANT_ID}.mixins.922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een chronologische lijst van veranderingen terug die in het middel worden aangebracht, van meest recente tot minst recente.

```json
[
  {
    "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
    "auditTrails": [
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/definitions/customFields/properties/_{TENANT_ID}/properties/brand",
        "value": {
          "title": "Brand",
          "description": "",
          "type": "string",
          "isRequired": false,
          "meta:xdmType": "string"
        }
      },
      {
        "id": "https://ns.adobe.com/{TENANT_ID}/mixins/922a56b58c6b4e4aeb49e577ec82752106ffe8971b23b4d9",
        "xdmType": "mixins",
        "action": "add",
        "path": "/meta:usageCount",
        "value": 0
      }
    ],
    "updatedUser": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "updated": 1606255582281,
    "clientId": "{CLIENT_ID}",
    "sandBoxId": "{SANDBOX_ID}"
  }
]
```

| Eigenschap | Beschrijving |
| --- | --- |
| `auditTrails` | Een array van objecten, waarbij elk object een wijziging vertegenwoordigt die is aangebracht in de opgegeven bron of een van de afhankelijke bronnen ervan. |
| `id` | De `$id` van de bron die is gewijzigd. Deze waarde zal typisch het middel vertegenwoordigen dat in de verzoekweg wordt gespecificeerd, maar kan een afhankelijke middel vertegenwoordigen als dat de bron van de verandering is. |
| `action` | Het type wijziging dat is aangebracht. |
| `path` | Een [JSON-aanwijzer](../../landing/api-fundamentals.md#json-pointer)-tekenreeks die het pad naar het specifieke veld aangeeft dat is gewijzigd of toegevoegd. |
| `value` | De waarde die is toegewezen aan het nieuwe of bijgewerkte veld. |