---
solution: Experience Platform
title: XDM-schema's exporteren in de gebruikersinterface
description: Leer hoe u een bestaand schema exporteert naar een andere sandbox of organisatie in de Adobe Experience Platform-gebruikersinterface.
type: Tutorial
exl-id: c467666d-55bc-4134-b8f4-7758d49c4786
source-git-commit: d25042e80ca5f655a50deac6a65ce9168225d6e6
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 0%

---

# XDM-schema&#39;s exporteren in de gebruikersinterface

Alle bronnen in de Schemabibliotheek bevinden zich in een specifieke sandbox binnen een organisatie. In sommige gevallen wilt u wellicht XDM-bronnen (Experience Data Model) delen tussen sandboxen en organisaties.

Om aan deze behoefte tegemoet te komen, [!UICONTROL Schemas] in de Adobe Experience Platform-gebruikersinterface kunt u een exportlading genereren voor elk schema in de Schemabibliotheek. Deze nuttige lading kan dan in een vraag aan de Registratie API van het Schema worden gebruikt om het schema (en alle afhankelijke middelen) in een doelzandbak en een organisatie in te voeren.

>[!NOTE]
>
>U kunt de Registratie API van het Schema ook gebruiken om andere middelen naast schema&#39;s, met inbegrip van klassen, de groepen van het schemagebied, en gegevenstypes uit te voeren. Zie de [eindgebruikershandleiding exporteren](../api/export.md) voor meer informatie .

## Vereisten

Terwijl de UI van het Platform u toelaat de middelen van XDM uitvoeren, moet u de Registratie API van het Schema gebruiken om die middelen in andere zandbakken of organisaties in te voeren om het werkschema te voltooien. Zie voor handleiding [aan de slag gaan met de Schema Registry-API](../api/getting-started.md) voor belangrijke informatie betreffende vereiste authentificatiekopballen alvorens deze gids te volgen.

## Een payload voor exporteren genereren {#generate-export-payload}

U kunt in de gebruikersinterface van het platform ladlasten voor exporteren genereren via het deelvenster Details in het dialoogvenster [!UICONTROL Browse] of rechtstreeks vanaf het canvas van het schema in de Schema-editor.

Selecteer **[!UICONTROL Schemas]** in de linkernavigatie. Binnen de [!UICONTROL Schemas] in de werkruimte selecteert u de rij voor het schema dat u wilt exporteren naar de schemagegevens in de rechterzijbalk.

>[!TIP]
>
>Zie de handleiding op [XDM-bronnen verkennen](./explore.md) voor details op hoe te om het middel te vinden XDM u zoekt.

Selecteer vervolgens de **[!UICONTROL Copy JSON]** icon (![Pictogram kopiëren](../images/ui/export/icon.png)) van de beschikbare opties.

![De werkruimte Schema&#39;s met een schemarij en [!UICONTROL Copy to JSON] gemarkeerd.](../images/ui/export/copy-json.png)

Hiermee wordt een JSON-lading naar het klembord gekopieerd, die op basis van de schemastructuur wordt gegenereerd. Voor &quot;[!DNL Loyalty Members]&quot; hierboven weergegeven schema, wordt de volgende JSON gegenereerd:

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

U kunt de Payload ook kopiëren door [!UICONTROL More] rechtsboven in de Schema-editor. Een vervolgkeuzemenu bevat twee opties. [!UICONTROL Copy JSON structure] en [!UICONTROL Delete schema].

>[!NOTE]
>
>Een schema kan niet worden geschrapt wanneer het voor Profiel wordt toegelaten of bijbehorende datasets heeft.

![De Schemas Editor met [!UICONTROL More] en [!UICONTROL Copy to JSON] gemarkeerd.](../images/ui/export/schema-editor-copy-json.png)

De payload heeft de vorm van een array, waarbij elk arrayitem een object is dat een aangepaste XDM-bron vertegenwoordigt die geëxporteerd moet worden. In het bovenstaande voorbeeld wordt &quot;[!DNL Loyalty details]&quot; aangepaste veldgroep en &quot;[!DNL Loyalty Members]&quot; schema is opgenomen. Alle kernbronnen die door het schema worden gebruikt, worden niet opgenomen in de exportbewerking, aangezien deze bronnen beschikbaar zijn in alle sandboxen en organisaties.

Merk op dat elk geval van de huurder ID van uw organisatie verschijnt zoals `<XDM_TENANTID_PLACEHOLDER>` in de lading. Deze placeholders zullen automatisch met de aangewezen waarde van huurdersidentiteitskaart afhankelijk van worden vervangen waar u het schema in de volgende stap invoert.

## De bron importeren met de API

Nadat u de JSON-exportbewerking voor het schema hebt gekopieerd, kunt u deze gebruiken als de payload voor een aanvraag van een POST naar de `/rpc/import` eindpunt in de schemaregistratie-API. Zie de [hulplijn voor importeindpunt](../api/import.md) voor details op hoe te om de vraag te vormen om het schema naar de gewenste organisatie en zandbak te verzenden.

## Volgende stappen

In deze handleiding hebt u een XDM-schema geëxporteerd naar een andere organisatie of sandbox. Voor meer informatie over de mogelijkheden van de [!UICONTROL Schemas] UI, verwijs naar [[!UICONTROL Schemas] Overzicht van gebruikersinterface](./overview.md).
