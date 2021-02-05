---
solution: Experience Platform
title: XDM-schema's exporteren in de gebruikersinterface
description: Leer hoe u een bestaand schema exporteert naar een andere sandbox of IMS-organisatie in de Adobe Experience Platform-gebruikersinterface.
topic: user guide
type: Tutorial
translation-type: tm+mt
source-git-commit: 2d6e833db7cd79135e6da4c68c9dca8cbed09ce4
workflow-type: tm+mt
source-wordcount: '502'
ht-degree: 0%

---


# XDM-schema&#39;s exporteren in de gebruikersinterface

Alle bronnen in de Schemabibliotheek bevinden zich in een specifieke sandbox binnen een IMS-organisatie. In sommige gevallen wilt u mogelijk bronnen van het Experience Data Model (XDM) delen tussen sandboxen en IMS Orgs.

Om deze behoefte te richten, staat [!UICONTROL Schemas] werkruimte in Adobe Experience Platform UI u toe om een de uitvoerlading voor om het even welk schema binnen in de Bibliotheek van het Schema te produceren. Deze nuttige lading kan dan in een vraag aan de Registratie-API van het Schema worden gebruikt om het schema (en alle afhankelijke middelen) in een doelzandbak en IMS Org in te voeren.

>[!NOTE]
>
>U kunt de Registratie API van het Schema ook gebruiken om andere middelen naast schema&#39;s, met inbegrip van klassen, mixins, en gegevenstypes uit te voeren. Zie de handleiding op [export/import endpoints](../api/export-import.md) voor meer informatie.

## Vereisten

Terwijl de interface van het Platform u toelaat de middelen van XDM uitvoeren, moet u de Registratie API van het Schema gebruiken om die middelen in andere zandbakken of IMS te importeren Orgs om het werkschema te voltooien. Raadpleeg de handleiding [Aan de slag met de schemaregistratie-API](../api/getting-started.md) voor belangrijke informatie over vereiste verificatieheaders voordat u deze handleiding volgt.

## Een exportlading genereren

Selecteer **[!UICONTROL Schema&#39;s]** in de linkernavigatie in de interface van het Platform. Zoek in de werkruimte [!UICONTROL Schema&#39;s] het schema dat u wilt exporteren en open het schema in [!DNL Schema Editor].

>[!TIP]
>
>Zie de gids op [het onderzoeken van Middelen XDM](./explore.md) voor details op hoe te om de bron te vinden XDM u zoekt.

Als u het schema hebt geopend, selecteert u het pictogram **[!UICONTROL JSON kopiëren]** (![Pictogram kopiëren](../images/ui/export/icon.png)) rechtsboven in het canvas.

![](../images/ui/export/copy-json.png)

Hiermee wordt een JSON-lading naar het klembord gekopieerd, die op basis van de schemastructuur wordt gegenereerd. Voor het schema &quot;[!DNL Loyalty Members]&quot; hierboven wordt getoond, wordt het volgende JSON geproduceerd:

```json
[
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.mixins.9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "title": "Loyalty details",
    "type": "object",
    "description": "",
    "definitions": {
      "customFields": {
        "type": "object",
        "properties": {
          "_<XDM_TENANTID_PLACEHOLDER>": {
            "type": "object",
            "properties": {
              "loyalty": {
                "title": "Loyalty",
                "description": "",
                "type": "object",
                "isRequired": false,
                "required": [
                  
                ],
                "properties": {
                  "loyaltyId": {
                    "title": "Loyalty ID",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "string"
                  },
                  "memberSince": {
                    "title": "Member Since",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "format": "date",
                    "meta:xdmType": "date"
                  },
                  "points": {
                    "title": "Points",
                    "description": "",
                    "type": "integer",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "meta:xdmType": "int"
                  },
                  "loyaltyLevel": {
                    "title": "Loyalty Level",
                    "description": "",
                    "type": "string",
                    "isRequired": false,
                    "required": [
                      
                    ],
                    "enum": [
                      "platinum",
                      "gold",
                      "silver",
                      "bronze"
                    ],
                    "meta:enum": {
                      "platinum": "Platinum",
                      "gold": "Gold",
                      "silver": "Silver",
                      "bronze": "Bronze"
                    },
                    "meta:xdmType": "string"
                  }
                },
                "meta:xdmType": "object"
              }
            },
            "meta:xdmType": "object"
          }
        },
        "meta:xdmType": "object"
      }
    },
    "allOf": [
      {
        "$ref": "#/definitions/customFields",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": true,
    "meta:abstract": true,
    "meta:intendedToExtend": [
      
    ],
    "meta:xdmType": "object",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production"
  },
  {
    "$id": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/schemas/1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:altId": "_<XDM_TENANTID_PLACEHOLDER>.schemas.1e5a739ded8fd1d766a0e06e881a38031874dddd1c7020ad",
    "meta:resourceType": "schemas",
    "version": "1.4",
    "title": "Loyalty Members",
    "type": "object",
    "description": "Describes customers who are members of a loyalty program.",
    "allOf": [
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-person-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
        "type": "object",
        "meta:xdmType": "object"
      },
      {
        "$ref": "https://ns.adobe.com/xdm/mixins/profile-consents",
        "type": "object",
        "meta:xdmType": "object"
      }
    ],
    "meta:extensible": false,
    "meta:abstract": false,
    "meta:extends": [
      "https://ns.adobe.com/xdm/context/profile-person-details",
      "https://ns.adobe.com/xdm/context/profile-personal-details",
      "https://ns.adobe.com/xdm/common/auditable",
      "https://ns.adobe.com/xdm/data/record",
      "https://ns.adobe.com/xdm/context/profile",
      "https://ns.adobe.com/<XDM_TENANTID_PLACEHOLDER>/mixins/9ecfd881d0053568d277b792e4d24c6b70ffa7782bd31265",
      "https://ns.adobe.com/xdm/mixins/profile-consents"
    ],
    "meta:xdmType": "object",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:sandboxId": "1bd86660-c5da-11e9-93d4-6d5fc3a66a8e",
    "meta:sandboxType": "production",
    "meta:immutableTags": [
      
    ]
  }
]
```

De payload heeft de vorm van een array, waarbij elk arrayitem een object is dat een aangepaste XDM-bron vertegenwoordigt die geëxporteerd moet worden. In het bovenstaande voorbeeld zijn de aangepaste mix &quot;[!DNL Loyalty details]&quot; en het schema &quot;[!DNL Loyalty Members]&quot; opgenomen. Alle kernbronnen die door het schema worden gebruikt, worden niet in de exportbewerking opgenomen, aangezien deze bronnen beschikbaar zijn in alle sandboxen en IMS-organisaties.

Merk op dat elk geval van huurder identiteitskaart van uw organisatie als `<XDM_TENANTID_PLACEHOLDER>` in de lading verschijnt. Deze placeholders zullen automatisch met de aangewezen waarde van huurdersidentiteitskaart afhankelijk van worden vervangen waar u het schema in de volgende stap uitvoert.

## De bron importeren met de API

Zodra u de uitvoer JSON voor het schema hebt gekopieerd, kunt u het als nuttige lading voor een verzoek van de POST aan het `/import` eindpunt in de Registratie API van het Schema gebruiken. Zie de sectie over [het invoeren van een middel XDM in API](../api/export-import.md#import) voor details op hoe te om de vraag te vormen om het schema naar correcte Ms te verzenden Org en zandbak.

## Volgende stappen

Als u deze handleiding volgt, hebt u een XDM-schema geëxporteerd naar een andere IMS-organisatie of -sandbox. Voor meer informatie over de mogelijkheden van [!UICONTROL Schemas] UI, verwijs naar [[!UICONTROL Schemas] UI overview](./overview.md).