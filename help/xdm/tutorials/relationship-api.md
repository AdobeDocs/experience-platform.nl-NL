---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Data Model;Schema Register;Schema;Schema;Schema;Schema's;Relationship;RelationshipDescriptor;RelationshipDescriptor;ReferentieIdentiteit;ReferentieIdentiteit;
solution: Experience Platform
title: Definieer een relatie tussen twee schema's met behulp van de API voor het schemaregister
description: Dit document verstrekt een zelfstudie voor het bepalen van een één-op-één verhouding tussen twee schema's die door uw organisatie worden bepaald gebruikend de Registratie API van het Schema.
topic: tutorial
type: Tutorial
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---


# Definieer een relatie tussen twee schema&#39;s met behulp van de [!DNL Schema Registry]-API

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Door deze relaties te definiëren binnen de structuur van uw [!DNL Experience Data Model] (XDM)-schema&#39;s kunt u complexe inzichten in uw klantgegevens opdoen.

Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het samenvoegingsschema en [!DNL Real-time Customer Profile], is dit alleen van toepassing op schema&#39;s die dezelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan een bronschema worden toegevoegd, dat de identiteit van een bestemmingsschema van verwijzingen voorziet.

Dit document biedt een zelfstudie voor het definiëren van een een-op-een relatie tussen twee schema&#39;s die door uw organisatie zijn gedefinieerd met de [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) en [!DNL XDM System]. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in  [!DNL Experience Platform].
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md):  [!DNL Experience Platform] biedt virtuele sandboxen die één enkele  [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Voordat u deze zelfstudie start, raadpleegt u de [ontwikkelaarshandleiding](../api/getting-started.md) voor belangrijke informatie die u moet weten om de [!DNL Schema Registry]-API te kunnen aanroepen. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot;, en de vereiste kopballen voor het maken van verzoeken (met speciale aandacht aan [!DNL Accept] kopbal en zijn mogelijke waarden).

## Een bron- en doelschema {#define-schemas} definiëren

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Deze zelfstudie maakt een relatie tussen leden van het huidige loyaliteitsprogramma van een organisatie (gedefinieerd in een schema &quot;[!DNL Loyalty Members]&quot;) en hun favoriete hotels (gedefinieerd in een schema &quot;[!DNL Hotels]&quot;).

Schemarelaties worden vertegenwoordigd door een **bronschema** met een veld dat verwijst naar een ander veld binnen een **doelschema**. In de stappen die volgen, &quot;[!DNL Loyalty Members]&quot;zal het bronschema zijn, terwijl &quot;[!DNL Hotels]&quot;als bestemmingsschema zal dienst doen.

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-time Customer Profile] worden toegelaten. Zie de sectie op [toelatend een schema voor gebruik in Profiel](./create-schema-api.md#profile) in de zelfstudie van de schemaverwezenlijking als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

Als u een relatie tussen twee schema&#39;s wilt definiëren, moet u eerst de `$id`-waarden voor beide schema&#39;s ophalen. Als u de vertoningsnamen (`title`) van de schema&#39;s kent, kunt u hun `$id` waarden vinden door een verzoek van de GET aan het `/tenant/schemas` eindpunt in [!DNL Schema Registry] API te richten.

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
>De [!DNL Accept] kopbal `application/vnd.adobe.xed-id+json` keert slechts de titels, IDs, en versies van de resulterende schema&#39;s terug.

**Antwoord**

Een geslaagde reactie retourneert een lijst met schema&#39;s die door uw organisatie zijn gedefinieerd, inclusief `name`, `$id`, `meta:altId` en `version`.

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

Registreer de `$id` waarden van de twee schema&#39;s u een verband tussen wilt bepalen. Deze waarden worden in latere stappen gebruikt.

## Een referentieveld definiëren voor het bronschema

Binnen [!DNL Schema Registry], werken de relatiebeschrijvers gelijkaardig aan buitenlandse sleutels in relationele gegevensbestandlijsten: Een veld in het bronschema fungeert als een verwijzing naar het primaire identiteitsveld van een doelschema. Als uw bronschema geen gebied voor dit doel heeft, kunt u een mengeling met het nieuwe gebied moeten tot stand brengen en het toevoegen aan het schema. Dit nieuwe veld moet de waarde `type` &quot;[!DNL string]&quot; hebben.

>[!IMPORTANT]
>
>In tegenstelling tot het bestemmingsschema, kan het bronschema zijn primaire identiteit als verwijzingsgebied niet gebruiken.

In dit leerprogramma, bevat het bestemmingsschema &quot;[!DNL Hotels]&quot;een `hotelId` gebied dat als primaire identiteit van het schema dient, en daarom ook als zijn verwijzingsgebied zal handelen. Nochtans, heeft het bronschema &quot;[!DNL Loyalty Members]&quot;geen specifiek gebied dat als verwijzing moet worden gebruikt, en moet een nieuwe mengeling worden gegeven die een nieuw gebied aan het schema toevoegt: `favoriteHotel`.

>[!NOTE]
>
>Als uw bronschema reeds een specifiek gebied heeft dat u als verwijzingsgebied van plan bent te gebruiken, kunt u vooruit naar de stap overslaan op [creërend een verwijzingsbeschrijver](#reference-identity).

### Een nieuwe mix maken

Als u een nieuw veld aan een schema wilt toevoegen, moet u dit eerst definiëren in een mix. U kunt een nieuwe mengeling tot stand brengen door een verzoek van de POST aan het `/tenant/mixins` eindpunt te doen.

**API-indeling**

```http
POST /tenant/mixins
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe mix gemaakt waarmee een veld `favoriteHotel` onder de naamruimte `_{TENANT_ID}` van een willekeurig schema wordt toegevoegd.

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

Registreer `$id` URI van de mix, die in de volgende stap van het toevoegen van de mix aan het bronschema moet worden gebruikt.

### De mix toevoegen aan het bronschema

Zodra u een mixin hebt gecreeerd, kunt u het aan het bronschema toevoegen door een verzoek van PATCH aan het `/tenant/schemas/{SCHEMA_ID}` eindpunt te doen.

**API-indeling**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het bronschema. |

**Verzoek**

Het volgende verzoek voegt &quot;[!DNL Favorite Hotel]&quot;mengsel aan &quot;[!DNL Loyalty Members]&quot;schema toe.

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
| `op` | De uit te voeren PATCH-bewerking. Dit verzoek gebruikt de `add` verrichting. |
| `path` | De weg aan het schemagebied waar het nieuwe middel zal worden toegevoegd. Wanneer u combinaties toevoegt aan schema&#39;s, moet de waarde &quot;/allOf/-&quot; zijn. |
| `value.$ref` | De `$id` van de toe te voegen mix. |

**Antwoord**

Een geslaagde reactie retourneert de details van het bijgewerkte schema, dat nu de `$ref`-waarde van de toegevoegde mix onder de `allOf`-array bevat.

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

## Een identiteitsbeschrijvingsbestand voor verwijzingen maken {#reference-identity}

Op schemavelden moet een identiteitsreferentie-descriptor zijn toegepast als deze worden gebruikt als referentie van andere schema&#39;s in een relatie. Aangezien het veld `favoriteHotel` in &quot;[!DNL Loyalty Members]&quot; verwijst naar het veld `hotelId` in &quot;[!DNL Hotels]&quot;, moet `hotelId` een beschrijvingsreferentie-id worden gegeven.

Creeer een verwijzingsbeschrijver voor het bestemmingsschema door een verzoek van de POST aan het `/tenant/descriptors` eindpunt te doen.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Het volgende verzoek leidt tot een verwijzingsbeschrijver voor het `hotelId` gebied in het bestemmingsschema &quot;[!DNL Hotels]&quot;.

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
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor verwijzingsbeschrijvingen moet de waarde &quot;xdm:descriptorReferenceIdentity&quot; zijn. |
| `xdm:sourceSchema` | De `$id` URL van het bestemmingsschema. |
| `xdm:sourceVersion` | Het versienummer van het doelschema. |
| `sourceProperty` | Het pad naar het primaire identiteitsveld van het doelschema. |
| `xdm:identityNamespace` | De naamruimte van de identiteit van het verwijzingsveld. Dit moet dezelfde naamruimte zijn die wordt gebruikt wanneer het veld wordt gedefinieerd als de primaire identiteit van het schema. Zie [Naamruimte overzicht](../../identity-service/home.md) voor meer informatie. |

**Antwoord**

Een succesvolle reactie keert de details van de pas gecreëerde verwijzingsbeschrijver voor het bestemmingsschema terug.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/d4ad4b8463a67f6755f2aabbeb9e02c7",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/hotelId",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Relatiebeschrijving maken {#create-descriptor}

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
    "xdm:destinationProperty": "/_{TENANT_ID}/hotelId"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat moet worden gemaakt. De waarde `@type` voor relatiebeschrijvers is &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | De `$id` URL van het bronschema. |
| `xdm:sourceVersion` | Het versienummer van het bronschema. |
| `xdm:sourceProperty` | Het pad naar het verwijzingsveld in het bronschema. |
| `xdm:destinationSchema` | De `$id` URL van het bestemmingsschema. |
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

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd. Voor meer informatie bij het werken met beschrijvers die [!DNL Schema Registry] API gebruiken, zie [de de ontwikkelaarsgids van de Registratie van het Schema](../api/descriptors.md). Voor stappen op hoe te om schemaverhoudingen in UI te bepalen, zie het leerprogramma op [het bepalen van schemaverhoudingen gebruikend de Redacteur van het Schema](relationship-ui.md).
