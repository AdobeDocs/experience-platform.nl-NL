---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Data Model;Schema Register;Schema Register;gedrag;gedrag;gedrag;gedrag; gedrag; gedrag
solution: Experience Platform
title: Eindpunt van gedrags-API
description: Het /behavior eindpunt in de Registratie API van het Schema staat u toe om al beschikbaar gedrag in de globale container terug te winnen.
topic-legacy: developer guide
exl-id: 3b45431f-1d55-4279-8b62-9b27863885ec
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Eindpunt gedrag

In het Model van Gegevens van de Ervaring (XDM), bepalen het gedrag de aard van gegevens die een schema beschrijft. Elke klasse XDM moet naar een specifiek gedrag verwijzen, dat alle schema&#39;s die die klasse gebruiken zullen erven. Voor bijna alle gebruiksgevallen in Platform zijn er twee beschikbare gedragingen:

* **[!UICONTROL Record]**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **[!UICONTROL Time-series]**: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

>[!NOTE]
>
>Er zijn sommige gebruiksgevallen in Platform die het gebruik van schema vereisen dat geen van de bovenstaande gedragingen gebruikt. In deze gevallen is een derde &quot;ad-hocgedrag&quot; beschikbaar. Zie de zelfstudie aan [een ad-hocschema maken](../tutorials/ad-hoc.md) voor meer informatie .
>
>Voor meer algemene informatie over gegevensgedrag in termen van hoe zij schemacompositie beïnvloeden, verwijs naar de gids over [grondbeginselen van de schemacompositie](../schema/composition.md).

De `/behaviors` in de [!DNL Schema Registry] Met API kunt u beschikbaar gedrag weergeven in het dialoogvenster `global` container.

## Aan de slag

Het eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Schema Registry] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/behavior-registry.yaml). Controleer voordat je doorgaat de [gids Aan de slag](./getting-started.md) voor verbindingen aan verwante documentatie, een gids aan lezing de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk Experience Platform API te maken.

## Een lijst met gedragingen ophalen {#list}

U kunt een lijst met alle beschikbare gedragingen ophalen door een GET-aanvraag in te dienen bij de `/behaviors` eindpunt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

U kunt een specifiek gedrag opzoeken door zijn identiteitskaart in de weg van een verzoek van de GET aan te geven `/behaviors` eindpunt.

**API-indeling**

```http
GET /global/behaviors/{BEHAVIOR_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{BEHAVIOR_ID}` | De `meta:altId` of URL-gecodeerd `$id` van het gedrag dat u wilt opzoeken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek worden de details van het recordgedrag opgehaald door het volgende op te geven `meta:altId` in het aanvraagpad.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/behaviors/_xdm.data.record \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

In deze handleiding wordt ingegaan op het gebruik van het `/behaviors` in de [!DNL Schema Registry] API. Zie voor meer informatie over het toewijzen van gedrag aan een klasse met behulp van de API [hulplijn voor klassen eindpunt](./classes.md).
