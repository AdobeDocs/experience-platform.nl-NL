---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;behavior;behaviour;behaviors;behaviours;
solution: Experience Platform
title: Hulplijn eindpunt Gedrag
description: Het /behavior eindpunt in de Registratie API van het Schema staat u toe om al beschikbaar gedrag in de globale container terug te winnen.
topic: developer guide
translation-type: tm+mt
source-git-commit: 1f18bf7367addd204f3ef8ce23583de78c70b70c
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 1%

---


# Eindpunt gedrag

In het Model van Gegevens van de Ervaring (XDM), bepalen het gedrag de aard van gegevens die een schema beschrijft. Elke klasse XDM moet naar een specifiek gedrag verwijzen, dat alle schema&#39;s die die klasse gebruiken zullen erven. Voor bijna alle gebruiksgevallen in Platform zijn er twee beschikbare gedragingen:

* **[!UICONTROL Opnemen]**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **[!UICONTROL Tijdreeks]**: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

>[!NOTE]
>
>Er zijn sommige gebruiksgevallen in Platform die het gebruik van schema vereisen dat geen van de bovenstaande gedragingen gebruikt. In deze gevallen is een derde &quot;ad-hocgedrag&quot; beschikbaar. Zie de zelfstudie over [het maken van een ad-hocschema](../tutorials/ad-hoc.md) voor meer informatie.
>
>Voor meer algemene informatie over gegevensgedrag in termen van hoe zij schemacompositie beïnvloeden, verwijs naar de gids op de [grondbeginselen van schemacompositie](../schema/composition.md).

Het `/behaviors` eindpunt in [!DNL Schema Registry] API staat u toe om beschikbaar gedrag in de `global` container te bekijken.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Lees voordat u doorgaat de [Aan de slag-handleiding](./getting-started.md) voor koppelingen naar verwante documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een Experience Platform-API te kunnen uitvoeren.

## Een lijst met gedragingen {#list} ophalen

U kunt een lijst van al beschikbaar gedrag terugwinnen door een verzoek van de GET aan het `/behaviors` eindpunt te doen.

**API-indeling**

```http
GET /global/behaviors
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Antwoord**

```json
{
    "results": [
        {
            "$id": "https://ns.adobe.com/xdm/data/record",
            "meta:altId": "_xdm.data.record",
            "version": "1.16.4",
            "title": "Record Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/adhoc",
            "meta:altId": "_xdm.data.adhoc",
            "version": "1.16.4",
            "title": "Ad Hoc Schema"
        },
        {
            "$id": "https://ns.adobe.com/xdm/data/time-series",
            "meta:altId": "_xdm.data.time-series",
            "version": "1.16.4",
            "title": "Time-series Schema"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null
    }
}
```

## Gedrag opzoeken {#lookup}

U kunt omhoog een specifiek gedrag kijken door zijn identiteitskaart in de weg van een verzoek van de GET aan het `/behaviors` eindpunt te verstrekken.

**API-indeling**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BEHAVIOR_ID}` | De `meta:altId` of URL-gecodeerde `$id` van het gedrag dat u wilt opzoeken. |

**Verzoek**

Het volgende verzoek wint de details van het verslaggedrag door zijn `meta:altId` in de verzoekweg te verstrekken terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json;version=1'
```

**Antwoord**

Een geslaagde reactie retourneert de details van het gedrag, inclusief de versie, beschrijving en de kenmerken die het gedrag verschaft aan de klassen die het gedrag toepassen.

```json
{
    "$id": "https://ns.adobe.com/xdm/data/record",
    "meta:altId": "_xdm.data.record",
    "meta:resourceType": "behaviors",
    "version": "1.16.4",
    "title": "Record Schema",
    "type": "object",
    "description": "Used to indicate the behavior of record data semantic when composed into data schemas.",
    "definitions": {
        "record": {
            "properties": {
                "_id": {
                    "title": "Identifier",
                    "type": "string",
                    "format": "uri-reference",
                    "description": "A unique identifier for the record.",
                    "meta:xdmType": "string",
                    "meta:xdmField": "@id"
                }
            }
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/record",
            "type": "object",
            "meta:xdmType": "object"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/common/extensible#/definitions/@context",
            "type": "object",
            "meta:xdmType": "object"
        }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:xdmType": "object",
    "meta:status": "stable",
    "$schema": "http://json-schema.org/draft-06/schema#",
    "meta:registryMetadata": {
        "repo:createdDate": 1606266789446,
        "repo:lastModifiedDate": 1606266789446,
        "eTag": "2cc114a54949a9668fe2ad046ccece59192e1bfa28f14e5ac7c893acb7820ba2",
        "meta:globalLibVersion": "1.16.4"
    }
}
```

## Volgende stappen

Deze gids behandelde het gebruik van het `/behaviors` eindpunt in [!DNL Schema Registry] API. Zie de [gids voor klassen](./classes.md) voor meer informatie over het toewijzen van een gedrag aan een klasse met behulp van de API.