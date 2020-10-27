---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema;Schema;schemas;Schemas;relationship;Relationship;relationship descriptor;Relationship descriptor;reference identity;Reference identity;
solution: Experience Platform
title: Bepaal een verband tussen twee schema's gebruikend de Registratie API van het Schema
description: Dit document verstrekt een zelfstudie voor het bepalen van een één-op-één verhouding tussen twee schema's die door uw organisatie worden bepaald gebruikend de Registratie API van het Schema.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: 097fe219e0d64090de758f388ba98e6024db2201
workflow-type: tm+mt
source-wordcount: '1296'
ht-degree: 0%

---


# Een relatie tussen twee schema&#39;s definiëren met behulp van de [!DNL Schema Registry] API

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Het bepalen van deze verhoudingen binnen de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s staat u toe om complexe inzichten in uw klantengegevens te bereiken.

Terwijl de schemaverhoudingen door het gebruik van het unieschema kunnen worden afgeleid en [!DNL Real-time Customer Profile], is dit slechts op schema&#39;s van toepassing die de zelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan een bronschema worden toegevoegd, dat de identiteit van een bestemmingsschema van verwijzingen voorziet.

Dit document biedt een zelfstudie voor het definiëren van een een-op-een relatie tussen twee schema&#39;s die door uw organisatie met de [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)code zijn gedefinieerd.

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) en [!DNL XDM System]. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voordat u deze zelfstudie start, moet u eerst de [ontwikkelaarsgids](../api/getting-started.md) raadplegen voor belangrijke informatie die u moet weten om oproepen naar de [!DNL Schema Registry] API te kunnen uitvoeren. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht voor de [!DNL Accept] kopbal en zijn mogelijke waarden).

## Een bron- en doelschema definiëren {#define-schemas}

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Deze zelfstudie maakt een relatie tussen leden van het huidige loyaliteitsprogramma van een organisatie (gedefinieerd in een &quot;[!DNL Loyalty Members]&quot; schema) en hun favoriete hotels (gedefinieerd in een &quot;[!DNL Hotels]&quot; schema).

De verhoudingen van het schema worden vertegenwoordigd door een **bronschema** die een gebied hebben dat naar een ander gebied binnen een **bestemmingsschema** verwijst. In de stappen die volgen, &quot;[!DNL Loyalty Members]&quot;zal het bronschema zijn, terwijl &quot;[!DNL Hotels]&quot;als bestemmingsschema zal handelen.

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-time Customer Profile]. Zie de sectie over het [toelaten van een schema voor gebruik in Profiel](./create-schema-api.md#profile) in de schemacreatie zelfstudie als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

Als u een relatie tussen twee schema&#39;s wilt definiëren, moet u eerst de `$id` waarden voor beide schema&#39;s ophalen. Als u de vertoningsnamen (`title`) van de schema&#39;s kent, kunt u hun `$id` waarden vinden door een verzoek van de GET tot het `/tenant/schemas` eindpunt in [!DNL Schema Registry] API te richten.

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

>[!NOTE]
>
>De [!DNL Accept] koptekst `application/vnd.adobe.xed-id+json` retourneert alleen de titels, id&#39;s en versies van de resulterende schema&#39;s.

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

## Een referentieveld definiëren voor het bronschema

Binnen de [!DNL Schema Registry], werken de relatiebeschrijvers gelijkaardig aan buitenlandse sleutels in relationele gegevensbestandlijsten: Een veld in het bronschema fungeert als een verwijzing naar het primaire identiteitsveld van een doelschema. Als uw bronschema geen gebied voor dit doel heeft, kunt u een mengeling met het nieuwe gebied moeten tot stand brengen en het toevoegen aan het schema. Dit nieuwe veld moet de `type` waarde &quot;[!DNL string]&quot; hebben.

>[!IMPORTANT]
>
>In tegenstelling tot het bestemmingsschema, kan het bronschema zijn primaire identiteit als verwijzingsgebied niet gebruiken.

In dit leerprogramma, bevat het bestemmingsschema &quot;[!DNL Hotels]&quot;een `email` gebied dat als primaire identiteit van het schema dient, en daarom ook als zijn verwijzingsgebied zal handelen. Nochtans, heeft het bronschema &quot;[!DNL Loyalty Members]&quot;geen specifiek gebied dat als verwijzing moet worden gebruikt, en moet een nieuwe mengeling worden gegeven die een nieuw gebied aan het schema toevoegt: `favoriteHotel`.

>[!NOTE]
>
>Als uw bronschema reeds een specifiek gebied heeft dat u als verwijzingsgebied van plan bent te gebruiken, kunt u vooruit aan de stap overslaan bij het [creëren van een verwijzingsbeschrijver](#reference-identity).

### Een nieuwe mix maken

Als u een nieuw veld aan een schema wilt toevoegen, moet u dit eerst definiëren in een mix. U kunt een nieuwe mengeling tot stand brengen door een verzoek van de POST aan het `/tenant/mixins` eindpunt te doen.

**API-indeling**

```http
POST /tenant/mixins
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe mix gemaakt waarmee een `favoriteHotel` veld wordt toegevoegd onder de `_{TENANT_ID}` naamruimte van elk schema waaraan het wordt toegevoegd.

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

Zodra u een mixin hebt gecreeerd, kunt u het aan het bronschema toevoegen door een verzoek van PATCH aan het `/tenant/schemas/{SCHEMA_ID}` eindpunt te doen.

**API-indeling**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het bronschema. |

**Verzoek**

Met het volgende verzoek voegt u de &#39;[!DNL Favorite Hotel]&#39; mix toe aan het &#39;[!DNL Loyalty Members]&#39; schema.

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
| `op` | De uit te voeren PATCH-bewerking. In dit verzoek wordt de `add` bewerking gebruikt. |
| `path` | De weg aan het schemagebied waar het nieuwe middel zal worden toegevoegd. Wanneer u combinaties toevoegt aan schema&#39;s, moet de waarde &quot;/allOf/-&quot; zijn. |
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

## Een beschrijving voor een referentie-id maken {#reference-identity}

Op schemavelden moet een identiteitsreferentie-descriptor zijn toegepast als deze worden gebruikt als referentie van andere schema&#39;s in een relatie. Aangezien het `favoriteHotel` veld in &quot;[!DNL Loyalty Members]&quot; verwijst naar het `email` veld in &quot;[!DNL Hotels]&quot;, moet `email` een identiteitsbeschrijving van een referentie worden gegeven.

Creeer een verwijzingsbeschrijver voor het bestemmingsschema door een verzoek van de POST aan het `/tenant/descriptors` eindpunt te doen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Met het volgende verzoek wordt een verwijzingsdescriptor voor het `email` veld in het doelschema &quot;[!DNL Hotels]&quot; gemaakt.

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
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor verwijzingsbeschrijvingen moet de waarde &quot;xdm:descriptorReferenceIdentity&quot; zijn. |
| `xdm:sourceSchema` | De `$id` URL van het doelschema. |
| `xdm:sourceVersion` | Het versienummer van het doelschema. |
| `sourceProperty` | Het pad naar het primaire identiteitsveld van het doelschema. |
| `xdm:identityNamespace` | De naamruimte van de identiteit van het verwijzingsveld. Dit moet dezelfde naamruimte zijn die wordt gebruikt wanneer het veld wordt gedefinieerd als de primaire identiteit van het schema. Zie het overzicht [van de naamruimte van de](../../identity-service/home.md) identiteit voor meer informatie. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde verwijzingsbeschrijver voor het bestemmingsschema terug.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/email",
    "xdm:identityNamespace": "Email",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Relatiebeschrijvingen maken {#create-descriptor}

Relatiebeschrijvingen maken een één-op-één relatie tussen een bronschema en een doelschema. Zodra u een verwijzingsbeschrijver voor het bestemmingsschema hebt bepaald, kunt u een nieuwe relatiebeschrijver tot stand brengen door een verzoek van de POST aan het `/tenant/descriptors` eindpunt te doen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe relatiebeschrijver, met &quot;[!DNL Loyalty Members]&quot;als bronschema en &quot;[!DNL Legacy Loyalty Members]&quot;als bestemmingsschema.

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
    "xdm:destinationProperty": "/_{TENANT_ID}/email"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat moet worden gemaakt. De `@type` waarde voor relatiebeschrijvers is &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | De `$id` URL van het bronschema. |
| `xdm:sourceVersion` | Het versienummer van het bronschema. |
| `xdm:sourceProperty` | Het pad naar het verwijzingsveld in het bronschema. |
| `xdm:destinationSchema` | De `$id` URL van het doelschema. |
| `xdm:destinationVersion` | Het versienummer van het doelschema. |
| `xdm:destinationProperty` | Het pad naar het verwijzingsveld in het doelschema. |

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

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd. Zie de handleiding voor ontwikkelaars van het [!DNL Schema Registry] schemaregister voor meer informatie over het werken met descriptors die de [API gebruiken](../api/descriptors.md). Voor stappen op hoe te om schemaverhoudingen in UI te bepalen, zie het leerprogramma bij het [bepalen van schemaverhoudingen gebruikend de Redacteur](relationship-ui.md)van het Schema.
