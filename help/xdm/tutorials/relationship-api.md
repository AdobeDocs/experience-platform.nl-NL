---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Bepaal een verband tussen twee schema's gebruikend de Registratie API van het Schema
topic: tutorials
translation-type: tm+mt
source-git-commit: 7e867ee12578f599c0c596decff126420a9aca01

---


# Bepaal een verband tussen twee schema&#39;s gebruikend de Registratie API van het Schema


De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van het Adobe Experience Platform. Het bepalen van deze verhoudingen binnen de structuur van uw schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) staat u toe om complexe inzichten in uw klantengegevens te bereiken.

Dit document biedt een zelfstudie voor het definiëren van een een-op-een relatie tussen twee schema&#39;s die door uw organisatie zijn gedefinieerd met behulp van de [schemaregistratie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Aan de slag

Deze zelfstudie vereist een goed begrip van het Model van de Gegevens van de Ervaring (XDM) en het Systeem XDM. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in ervaringsplatform](../home.md): Een overzicht van XDM en zijn implementatie in het Platform van de Ervaring.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voordat u met deze zelfstudie begint, moet u eerst de [ontwikkelaarsgids](../api/getting-started.md) raadplegen voor belangrijke informatie die u moet weten om oproepen naar de API voor schemaregistratie te kunnen uitvoeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de Accept kopbal en zijn mogelijke waarden).

## Een bron- en doelschema definiëren {#define-schemas}

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Deze zelfstudie creëert een relatie tussen leden van het huidige loyaliteitsprogramma van een organisatie (gedefinieerd in een schema &quot;Loyalty Member&quot;) en hun favoriete hotels (gedefinieerd in een &quot;Hotels&quot;-schema).

De verhoudingen van het schema worden vertegenwoordigd door een **bronschema** die een gebied hebben dat naar een ander gebied binnen een **bestemmingsschema** verwijst. In de stappen die volgen, zullen de &quot;Leden van de Loyalty&quot;het bronschema zijn, terwijl &quot;Hotels&quot;als bestemmingsschema zal handelen.

Als u een relatie tussen twee schema&#39;s wilt definiëren, moet u eerst de `$id` waarden voor beide schema&#39;s ophalen. Als u de vertoningsnamen (`title`) van de schema&#39;s kent, kunt u hun `$id` waarden vinden door een GET verzoek aan het `/tenant/schemas` eindpunt in de Registratie API van het Schema te doen.

**API-indeling**

```http
GET /tenant/schemas
```

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE] De koptekst Accepteren `application/vnd.adobe.xed-id+json` retourneert alleen de titels, id&#39;s en versies van de resulterende schema&#39;s.

**Antwoord**

Een succesvolle reactie keert een lijst van schema&#39;s terug die door uw organisatie, met inbegrip van hun `name`, `$id`, `meta:altId`en `version`worden bepaald.

```json
{
    "results": [
        {
            "title": "Newsletter Subscriptions",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/192a66930afad02408429174c311ae73",
            "meta:altId": "_{TENANT_ID}.schemas.192a66930afad02408429174c311ae73",
            "version": "1.2"
        },
        {
            "title": "Loyalty Members",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
            "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
            "version": "1.5"
        },
        {
            "title": "Hotels",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
            "meta:altId": "_{TENANT_ID}.schemas.d4ad4b8463a67f6755f2aabbeb9e02c7",
            "version": "1.0"
        }
    ],
    "_page": {
        "orderby": "updated",
        "next": null,
        "count": 3
    },
    "_links": {
        "next": null,
        "global_schemas": {
            "href": "https://platform-stage.adobe.io/data/foundation/schemaregistry/global/schemas"
        }
    }
}
```

Registreer de `$id` waarden van de twee schema&#39;s u een verhouding tussen wilt bepalen. Deze waarden worden in latere stappen gebruikt.

## Referentievelden definiëren voor beide schema&#39;s

Binnen de Registratie van het Schema, werken de relatiebeschrijvers gelijkaardig aan buitenlandse sleutels in SQL lijsten: Een veld in het bronschema fungeert als een verwijzing naar een veld in een doelschema. Wanneer het bepalen van een verhouding, moet elk schema een specifiek gebied hebben dat als verwijzing naar het andere schema moet worden gebruikt.

>[!IMPORTANT] Als de schema&#39;s voor gebruik in het Profiel [van de Klant in](../../profile/home.md)real time moeten worden toegelaten, moet het verwijzingsgebied voor het bestemmingsschema zijn zijn **primaire identiteit**. Dit wordt nader uitgelegd in deze zelfstudie.

Als één van beide schema&#39;s geen gebied voor dit doel heeft, kunt u een mengeling met het nieuwe gebied moeten tot stand brengen en het toevoegen aan het schema. Dit nieuwe veld moet de `type` waarde &quot;string&quot; hebben.

In deze zelfstudie bevat het doelschema &quot;Hotels&quot; al een veld voor dit doel: `hotelId`. Nochtans, heeft het bronschema &quot;Leden van de Loyalty&quot;zulk een gebied niet, en moet een nieuwe mengeling worden gegeven die een nieuw gebied, onder zijn `favoriteHotel``TENANT_ID` namespace toevoegt.

### Een nieuwe mix maken

Als u een nieuw veld aan een schema wilt toevoegen, moet u dit eerst definiëren in een mix. U kunt een nieuwe mengeling tot stand brengen door een POST- verzoek aan het `/tenant/mixins` eindpunt te doen.

**API-indeling**

```http
POST /tenant/mixins
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe mix gemaakt waarmee een `favoriteHotel` veld wordt toegevoegd onder de `TENANT_ID` naamruimte van elk schema waaraan het wordt toegevoegd.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/mixins \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel mixin for the Loyalty Members schema.",
        "definitions": {
            "favoriteHotel": {
              "properties": {
                "_{TENANT_ID}": {
                  "type":"object",
                  "properties": {
                    "favoriteHotel": {
                      "title": "Favorite Hotel",
                      "type": "string",
                      "description": "Favorite hotel for a Loyalty Member."
                    }
                  }
                }
              }
            }
        },
        "allOf": [
            {
              "$ref": "#/definitions/favoriteHotel"
            }
        ]
      }'
```

**Antwoord**

Een geslaagde reactie retourneert de details van de zojuist gemaakte mix.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220",
    "meta:altId": "_{TENANT_ID}.mixins.3387945212ad76ee59b6d2b964afb220",
    "meta:resourceType": "mixins",
    "version": "1.0",
    "type": "object",
    "title": "Favorite Hotel",
    "meta:intendedToExtend": [
        "https://ns.adobe.com/xdm/context/profile"
    ],
    "description": "Favorite hotel mixin for the Loyalty Members schema.",
    "definitions": {
        "favoriteHotel": {
            "properties": {
                "_{TENANT_ID}": {
                    "type": "object",
                    "properties": {
                        "favoriteHotel": {
                            "title": "Favorite Hotel",
                            "type": "string",
                            "description": "Favorite hotel for a Loyalty Member.",
                            "meta:xdmType": "string"
                        }
                    },
                    "meta:xdmType": "object"
                }
            },
            "type": "object",
            "meta:xdmType": "object"
        }
    },
    "allOf": [
        {
            "$ref": "#/definitions/favoriteHotel"
        }
    ],
    "meta:xdmType": "object",
    "meta:abstract": true,
    "meta:extensible": true,
    "meta:containerId": "tenant",
    "meta:tenantNamespace": "_{TENANT_ID}",
    "meta:registryMetadata": {
        "eTag": "quM2aMPyb2NkkEiZHNCs/MG34E4=",
        "palm:sandboxName": "prod"
    }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `$id` | De alleen-lezen, door het systeem gegenereerde unieke id van de nieuwe mix. De vorm van een URI. |

Registreer de `$id` URI van de mix die in de volgende stap van het toevoegen van de mix aan het bronschema moet worden gebruikt.

### De mix toevoegen aan het bronschema

Zodra u een mixin hebt gecreeerd, kunt u het aan het bronschema toevoegen door een verzoek van de PATCH aan het `/tenant/schemas/{SCHEMA_ID}` eindpunt te doen.

**API-indeling**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het bronschema. |

**Verzoek**

Met het volgende verzoek voegt u de mix &quot;Favoriet hotel&quot; toe aan het schema &quot;Loyalty-leden&quot;.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
    { 
      "op": "add", 
      "path": "/allOf/-", 
      "value":  {
        "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
      }
    }
  ]'
```

| Eigenschap | Beschrijving |
| --- | --- |
| `op` | De PATCH-bewerking die moet worden uitgevoerd. In dit verzoek wordt de `add` bewerking gebruikt. |
| `path` | De weg aan het schemagebied waar het nieuwe middel zal worden toegevoegd. Wanneer u combinaties toevoegt aan schema&#39;s, moet de waarde `/allOf/-`zijn. |
| `value.$ref` | De hoeveelheid `$id` van het toe te voegen mengsel. |

**Antwoord**

Een succesvolle reactie retourneert de details van het bijgewerkte schema, dat nu de `$ref` waarde van de toegevoegde mixin onder de `allOf` array bevat.

```json
{
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "meta:altId": "_{TENANT_ID}.schemas.2c66c3a4323128d3701289df4468e8a6",
    "meta:resourceType": "schemas",
    "version": "1.1",
    "type": "object",
    "title": "Loyalty Members",
    "description": "",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/identitymap"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/3387945212ad76ee59b6d2b964afb220"
        }
    ],
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:tenantNamespace": "_{TENANT_ID}",
    "imsOrg": "{IMS_ORG}",
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/xdm/context/profile-personal-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/ec16dfa484358f80478b75cde8c430d3",
        "https://ns.adobe.com/{TENANT_ID}/mixins/61969bc646b66a6230a7e8840f4a4d33"
    ],
    "meta:xdmType": "object",
    "meta:registryMetadata": {
        "repo:createdDate": 1557525483804,
        "repo:lastModifiedDate": 1566419670915,
        "xdm:createdClientId": "{API_KEY}",
        "xdm:lastModifiedClientId": "{CLIENT_ID}",
        "eTag": "ITNzu8BVTO5pw9wfCtTTpk6U4WY="
    }
}
```

## Primaire identiteitsvelden definiëren voor beide schema&#39;s

>[!NOTE] Deze stap is alleen vereist voor schema&#39;s die zijn ingeschakeld voor gebruik in het [realtime profiel](../../profile/home.md)van de klant. Als u of schema niet aan een unie wilt deelnemen, of als uw schema&#39;s reeds primaire bepaalde identiteiten hebben, kunt u aan de volgende stap overslaan van het [creëren van een beschrijver](#create-descriptor) van de verwijzingsidentiteit voor het bestemmingsschema.

Om schema&#39;s voor gebruik in het Profiel van de Klant in real time te kunnen worden toegelaten, moeten zij een primaire bepaalde identiteit hebben. Bovendien moet het bestemmingsschema van een verhouding zijn primaire identiteit als zijn verwijzingsgebied gebruiken.

Voor deze zelfstudie is voor het bronschema al een primaire identiteit gedefinieerd, maar het doelschema niet. U kunt een schemaveld als primair identiteitsveld markeren door een identiteitsdescriptor te maken. Dit wordt gedaan door een POST- verzoek aan het `/tenant/descriptors` eindpunt te doen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe identiteitsdescriptor gemaakt die het `hotelId` veld van het doelschema &quot;Hotels&quot; definieert als een primair identiteitsveld.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat moet worden gemaakt. De `@type` waarde voor identiteitsbeschrijvers is `xdm:descriptorIdentity`. |
| `xdm:sourceSchema` | De `$id` waarde van het bestemmingsschema, dat in de [vorige stap](#define-schemas)wordt verkregen. |
| `xdm:sourceVersion` | Het versienummer van het schema. |
| `sourceProperty` | De weg aan het specifieke gebied dat als primaire identiteit van het schema zal dienen. Dit pad moet beginnen met een \&quot;/\&quot; en niet eindigen met een \&quot;/\&quot;, terwijl ook naamruimten van het type &quot;eigenschappen&quot; moeten worden uitgesloten. De bovenstaande aanvraag wordt bijvoorbeeld gebruikt `/_{TENANT_ID}/hotelId` in plaats van `/properties/_{TENANT_ID}/properties/hotelId`. |
| `xdm:namespace` | De naamruimte van de identiteit voor het naamveld. `hotelId` is een ECID-waarde in dit voorbeeld, daarom wordt de naamruimte &quot;ECID&quot; gebruikt. Zie het overzicht [van de naamruimte van de](../../identity-service/home.md) identiteit voor een lijst met beschikbare naamruimten. |
| `xdm:isPrimary` | Een Booleaanse eigenschap die bepaalt of het identiteitsveld de primaire identiteit voor het schema is. Aangezien deze aanvraag een primaire identiteit definieert, wordt de waarde ingesteld op true. |

**Antwoord**

Een succesvol antwoord retourneert de details van de nieuwe identiteitsbeschrijving.

```json
{
    "@type": "xdm:descriptorIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:namespace": "ECID",
    "xdm:property": "xdm:code",
    "xdm:isPrimary": true,
    "meta:containerId": "tenant",
    "@id": "e3cfa302d06dc27080e6b54663511a02dd61316f"
}
```

## Een beschrijving voor een referentie-id maken

Op schemavelden moet een identiteitsreferentie-descriptor zijn toegepast als deze worden gebruikt als referentie van andere schema&#39;s in een relatie. Aangezien het `favoriteHotel` veld &quot;Loyalty members&quot; verwijst naar het `hotelId` veld &quot;Hotels&quot;, `hotelId` moet een referentie-id worden gegeven.

Creeer een verwijzingsbeschrijver voor het bestemmingsschema door een POST- verzoek aan het `/tenant/descriptors` eindpunt te doen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Met het volgende verzoek maakt u een verwijzingsdescriptor voor het `hotelId` veld in het doelschema &quot;Hotels&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `xdm:sourceSchema` | De `$id` URL van het doelschema. |
| `xdm:sourceVersion` | Het versienummer van het doelschema. |
| `sourceProperty` | Het pad naar het primaire identiteitsveld van het doelschema. |
| `xdm:identityNamespace` | De naamruimte van de identiteit van het verwijzingsveld. `hotelId` is een ECID-waarde in dit voorbeeld, daarom wordt de naamruimte &quot;ECID&quot; gebruikt. Zie het overzicht [van de naamruimte van de](../../identity-service/home.md) identiteit voor een lijst met beschikbare naamruimten. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde verwijzingsbeschrijver voor het bestemmingsschema terug.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "ECID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Relatiebeschrijvingen maken {#create-descriptor}

Relatiebeschrijvingen maken een één-op-één relatie tussen een bronschema en een doelschema. U kunt een nieuwe relatiebeschrijver tot stand brengen door een POST- verzoek aan het `/tenant/descriptors` eindpunt te doen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe relatiebeschrijver, met &quot;Leden Loyalty&quot;als bronschema en &quot;Leden van de Loyalty van de Oudheid&quot;als bestemmingsschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat moet worden gemaakt. De `@type` waarde voor relatiebeschrijvers is `xdm:descriptorOneToOne`. |
| `xdm:sourceSchema` | De `$id` URL van het bronschema. |
| `xdm:sourceVersion` | Het versienummer van het bronschema. |
| `sourceProperty`: | Het pad naar het verwijzingsveld in het bronschema. |
| `xdm:destinationSchema` | De `$id` URL van het doelschema. |
| `xdm:destinationVersion` | Het versienummer van het doelschema. |
| `destinationProperty`: | Het pad naar het verwijzingsveld in het doelschema. |

### Antwoord

Een succesvol antwoord keert de details van de pas gecreëerde relatiebeschrijver terug.

```json
{
    "@type": "xdm:descriptorOneToOne",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/2c66c3a4323128d3701289df4468e8a6",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:destinationSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:destinationVersion": 1,
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId",
    "meta:containerId": "tenant",
    "@id": "76f6cc7105f4eaab7eb4a5e1cb4804cadc741669"
}
```

## Volgende stappen

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd. Voor meer informatie bij het werken met beschrijvers die de Registratie API van het Schema gebruiken, zie de de ontwikkelaarsgids [van de Registratie van het](../api/getting-started.md)Schema. Voor stappen op hoe te om schemaverhoudingen in UI te bepalen, zie het leerprogramma bij het [bepalen van schemaverhoudingen gebruikend de Redacteur](relationship-ui.md)van het Schema.