---
title: Een XDM-veld in de API verwijderen
description: Leer hoe u XDM-velden (Experience Data Model) in de Schema Registry-API kunt vervangen.
exl-id: e49517c4-608d-4e05-8466-75724ca984a8
source-git-commit: f9f783b75bff66d1bf3e9c6d1ed1c543bd248302
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# Een XDM-veld in de API verwijderen

In het Model van Gegevens van de Ervaring (XDM), kunt u een gebied binnen een schema of douanemiddel verwerpen door de [ Registratie API van het Schema te gebruiken ](https://developer.adobe.com/experience-platform-apis/references/schema-registry/). Als u een veld verwijdert, wordt dit verborgen in downstreamgebruikersinterface&#39;s zoals de [!UICONTROL Profiles] -werkruimte en -Customer Journey Analytics, maar anders is het een vaste wijziging die geen negatieve invloed heeft op bestaande gegevensstromen.

In dit document wordt beschreven hoe velden voor verschillende XDM-bronnen moeten worden vervangen. Voor stappen bij het afschilderen van een XDM gebied gebruikend de Redacteur van het Schema in het gebruikersinterface van het Experience Platform, zie het leerprogramma op [ afschilderend een XDM gebied in UI ](./field-deprecation-ui.md).

## Aan de slag

Deze zelfstudie vereist het maken van aanroepen naar de Schemaregistratie-API. Gelieve te herzien de [ ontwikkelaarsgids ](../api/getting-started.md) voor belangrijke informatie die u moet kennen om deze API vraag te maken. Dit omvat uw `{TENANT_ID}` , het concept &quot;containers&quot; en de vereiste kopteksten voor het indienen van aanvragen (met speciale aandacht voor de header `Accept` en de mogelijke waarden ervan).

## Een aangepast veld verwijderen {#custom}

Als u een veld in een aangepaste klasse, veldgroep of gegevenstype wilt vervangen, werkt u de aangepaste bron bij via een PUT- of PATCH-aanvraag en voegt u het kenmerk `meta:status: deprecated` toe aan het desbetreffende veld.

>[!NOTE]
>
>Raadpleeg de volgende documentatie voor algemene informatie over het bijwerken van aangepaste bronnen in XDM:
>
>* [ werk een klasse ](../api/classes.md#patch) bij
>* [ werk een gebiedsgroep ](../api/field-groups.md#patch) bij
>* [ werk een gegevenstype ](../api/data-types.md#patch) bij

Met de API-voorbeeldaanroep hieronder wordt een veld in een aangepast gegevenstype vervangen.

**API formaat**

```http
PATCH /tenant/datatypes/{DATA_TYPE_ID}
```

**Verzoek**

In het volgende verzoek wordt het veld `expansionArea` vervangen voor een gegevenstype dat een eigenschap real-property beschrijft.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/datatypes/_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '[
        { 
          "op": "add",
          "path": "/properties/expansionArea/meta:status",
          "value": "deprecated"
        }
      ]'
```

**Reactie**

Een geslaagde reactie retourneert de updatedetails van de aangepaste bron, waarbij het vervangen veld de `meta:status` waarde `deprecated` bevat. De voorbeeldreactie hieronder is afgebroken voor de ruimte.

```json
{
  "$id": "https://ns.adobe.com/{TENANT_ID}/datatypes/8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:altId": "_{TENANT_ID}.datatypes.8779fd45d6e4eb074300023a439862bbba359b60d451627a",
  "meta:resourceType": "datatypes",
  "version": "1.2",
  "title": "Property Details",
  "type": "object",
  "description": "Details relating to a real-estate property operated by the company.",
  "definitions": {
    "property": {
      "properties": {
        "_{TENANT_ID}": {
        "type":"object",
        "properties": {
            "expansionArea": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
              "meta:status": "deprecated",
            },
            "propertyName": {
              "title": "Property Name",
              "description": "Name of the property",
              "type": "string"
            },
            "propertyCity": {
              "title": "Property City",
              "description": "City where the property is located.",
              "type": "string"
            },
            "propertyCountry": {
              "title": "Property Country",
              "description": "Country where the property is located.",
              "type": "string"
            },
            "phoneNumber": {
              "title": "Phone Number",
              "description": "Primary phone number for the property.",
              "type": "string"
            },
            "propertyType": {
              "type": "string",
              "title": "Property Type",
              "description": "Type and primary use of property.",
              "enum": [
                  "retail",
                  "yoga",
                  "fitness"
              ],
              "meta:enum": {
                  "retail": "Retail Store",
                  "yoga": "Yoga Studio",
                  "fitness": "Fitness Center"
              }
            },
            "propertyConstruction": {
              "$ref": "https://ns.adobe.com/{TENANT_ID}/datatypes/24c643f618647344606222c494bd0102"
            },
            "squareFeet": {
              "title": "Expansion Area",
              "description": "Square footage for renovated additions to the property.",
              "type": "integer",
            }
          }
        }
      }
    }
  },
  "allOf": [
    {
      "$ref": "#/definitions/customFields",
      "type": "object",
      "meta:xdmType": "object"
    }
  ],
  "imsOrg": "{IMS_ORG}",
  "meta:extensible": true,
  "meta:abstract": true,
  "meta:intendedToExtend": [
    "https://ns.adobe.com/xdm/context/profile"
  ],
  "meta:xdmType": "object",
  "meta:registryMetadata": {
    "repo:createdDate": 1594941263588,
    "repo:lastModifiedDate": 1594941538433,
    "xdm:createdClientId": "{CLIENT_ID}",
    "xdm:lastModifiedClientId": "{CLIENT_ID}",
    "xdm:createdUserId": "{USER_ID}",
    "xdm:lastModifiedUserId": "{USER_ID}",
    "eTag": "5e8a5e508eb2ed344c08cb23ed27cfb60c841bec59a2f7513deda0f7af903021",
    "meta:globalLibVersion": "1.15.4"
  },
  "meta:containerId": "tenant",
  "meta:tenantNamespace": "_{TENANT_ID}"
}
```

## Een standaardveld in een schema verwijderen {#standard}

Velden van standaardklassen, veldgroepen en gegevenstypen kunnen niet rechtstreeks worden vervangen. In plaats daarvan, kunt u hun gebruik in de individuele schema&#39;s verwerpen die deze standaardmiddelen door een beschrijver gebruiken.

### Een beschrijving van de veldafdrukking maken {#create-descriptor}

Als u een descriptor wilt maken voor de schemavelden die u wilt vervangen, vraagt u een POST om het `/tenant/descriptors` -eindpunt.

**API formaat**

```http
POST /tenant/descriptors
```

**Verzoek**

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "@type": "xdm:descriptorDeprecated",
        "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
        "xdm:sourceVersion": 1,
        "xdm:sourceProperty": "/faxPhone"
      }'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor. Voor een beschrijving van de gebiedsafbeelding moet deze waarde worden ingesteld op `xdm:descriptorDeprecated` . |
| `xdm:sourceSchema` | De URI `$id` van het schema waarop u de descriptor toepast. |
| `xdm:sourceVersion` | De versie van het schema waarop u de descriptor toepast. Moet worden ingesteld op `1` . |
| `xdm:sourceProperty` | Het pad naar de eigenschap in het schema waarop u de descriptor toepast. Als u de descriptor op meerdere eigenschappen wilt toepassen, kunt u een lijst met paden opgeven in de vorm van een array (bijvoorbeeld `["/firstName", "/lastName"]` ). |

**Reactie**

```json
{
    "@id": "d882b1202bac0ac71f1e31fbcd9afbcc37f364270186b4b3",
    "@type": "xdm:descriptorDeprecated",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/faxPhone",
    "imsOrg": "{IMS_ORG}",
    "version": "1",
    "meta:containerId": "tenant",
    "meta:sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
    "meta:sandboxType": "production"
}
```

### Het vervangen veld controleren {#verify-deprecation}

Nadat de descriptor is toegepast, kunt u controleren of het veld is vervangen door het betreffende schema op te zoeken terwijl u de juiste `Accept` header gebruikt.

>[!NOTE]
>
>Afgekeurde velden worden weergegeven als aanbiedingsschema&#39;s momenteel niet worden ondersteund.

**API formaat**

```http
GET /tenant/schemas
```

**Verzoek**

Als u informatie over vervangen velden wilt opnemen in de API-reactie, moet u de header `Accept` instellen op `application/vnd.adobe.xed-deprecatefield+json; version=1` .

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.c65ddf08cf2d4a2fe94bd06113bf4bc4c855e12a936410d5 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-deprecatefield+json; version=1'
```

**Reactie**

Wanneer de reactie met succes is uitgevoerd, worden de details van het schema geretourneerd. Het vervangen veld bevat de waarde `meta:status` `deprecated` . De voorbeeldreactie hieronder is afgebroken voor de ruimte.

```json
"faxPhone": {
    "title": "Fax phone",
    "description": "Fax phone number.",
    "type": "object",
    "meta:xdmType": "object",
    "properties": {},
    "meta:referencedFrom": "https://ns.adobe.com/xdm/context/phonenumber",
    "meta:xdmField": "xdm:faxPhone",
    "meta:status": "deprecated"
}
```

## Volgende stappen

In dit document wordt beschreven hoe u XDM-velden kunt vervangen met de API voor schemaregistratie. Voor meer informatie bij het vormen van gebieden voor douanemiddelen, zie de gids bij [ het bepalen van gebieden XDM in API ](./custom-fields-api.md). Voor meer informatie bij het beheren van beschrijvers, zie de [ gids van het beschrijvingseindpunt ](../api/descriptors.md).
