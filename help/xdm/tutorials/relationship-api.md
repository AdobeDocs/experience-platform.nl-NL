---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience Data Model;Experience Data Model;Data Model;Data Model;Schema Register;Schema;Schema;Schema;Schema's;Relationship;RelationshipDescriptor;RelationshipDescriptor;ReferentieIdentiteit;ReferentieIdentiteit;
solution: Experience Platform
title: Definieer een relatie tussen twee schema's met behulp van de API voor het schemaregister
description: Dit document verstrekt een zelfstudie voor het bepalen van een één-op-één verhouding tussen twee schema's die door uw organisatie worden bepaald gebruikend de Registratie API van het Schema.
topic-legacy: tutorial
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1365'
ht-degree: 0%

---

# Bepaal een verband tussen twee schema&#39;s gebruikend [!DNL Schema Registry] API

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Deze relaties definiëren binnen de structuur van uw [!DNL Experience Data Model] (XDM) schema&#39;s staan u toe om complexe inzichten in uw klantengegevens te bereiken.

Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het union-schema en [!DNL Real-time Customer Profile]Dit geldt alleen voor schema&#39;s die dezelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan een bronschema worden toegevoegd, dat de identiteit van een bestemmingsschema van verwijzingen voorziet.

Dit document biedt een zelfstudie voor het definiëren van een een-op-een relatie tussen twee schema&#39;s die door uw organisatie met behulp van de [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) en [!DNL XDM System]. Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [XDM-systeem in Experience Platform](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

Lees voordat u deze zelfstudie start de [ontwikkelaarsgids](../api/getting-started.md) voor belangrijke informatie die u moet weten om met succes vraag aan te maken [!DNL Schema Registry] API. Dit omvat uw `{TENANT_ID}`, het concept &quot;containers&quot; en de vereiste opschriften voor het indienen van aanvragen (met bijzondere aandacht voor de [!DNL Accept] en de mogelijke waarden ervan).

## Een bron- en doelschema definiëren {#define-schemas}

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Deze zelfstudie maakt een relatie tussen leden van het huidige loyaliteitsprogramma van een organisatie (gedefinieerd in een &quot;[!DNL Loyalty Members]&quot; schema) en hun favoriete hotels (gedefinieerd in &quot;[!DNL Hotels]&quot; schema).

Schemarelaties worden vertegenwoordigd door een **bronschema** met een veld dat verwijst naar een ander veld binnen een **doelschema**. In de volgende stappen: &quot;[!DNL Loyalty Members]&quot; wordt het bronschema, terwijl &quot;[!DNL Hotels]&quot; fungeert als het doelschema.

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en geschikt zijn gemaakt voor [!DNL Real-time Customer Profile]. Zie de sectie over [een schema inschakelen voor gebruik in profiel](./create-schema-api.md#profile) in de zelfstudie van de schemaverwezenlijking als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

Als u een relatie tussen twee schema&#39;s wilt definiëren, moet u eerst het `$id` waarden voor beide schema&#39;s. Als u de weergavenamen kent (`title`) van de schema&#39;s, kunt u hun vinden `$id` waarden door een GET-aanvraag in te dienen bij de `/tenant/schemas` in de [!DNL Schema Registry] API.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

>[!NOTE]
>
>De [!DNL Accept] header `application/vnd.adobe.xed-id+json` Retourneert alleen de titels, id&#39;s en versies van de resulterende schema&#39;s.

**Antwoord**

Een succesvolle reactie keert een lijst van schema&#39;s terug die door uw organisatie, met inbegrip van hun worden bepaald `name`, `$id`, `meta:altId`, en `version`.

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

Neem de `$id` De waarden van de twee schema&#39;s u een verband tussen wilt bepalen. Deze waarden worden in latere stappen gebruikt.

## Een referentieveld definiëren voor het bronschema

Binnen de [!DNL Schema Registry]Relatiebeschrijvers werken hetzelfde als buitenlandse sleutels in relationele databasetabellen: Een veld in het bronschema fungeert als een verwijzing naar het primaire identiteitsveld van een doelschema. Als uw bronschema geen gebied voor dit doel heeft, kunt u een groep van het schemagebied met het nieuwe gebied moeten tot stand brengen en het toevoegen aan het schema. Dit nieuwe veld moet een `type` waarde van &quot;[!DNL string]&quot;.

>[!IMPORTANT]
>
>In tegenstelling tot het bestemmingsschema, kan het bronschema zijn primaire identiteit als verwijzingsgebied niet gebruiken.

In deze zelfstudie wordt het doelschema &quot;[!DNL Hotels]&quot; bevat een `hotelId` gebied dat als primaire identiteit van het schema dient, en daarom ook als zijn verwijzingsgebied zal handelen. Het bronschema &quot;[!DNL Loyalty Members]&quot; heeft geen speciaal veld dat als referentie moet worden gebruikt en moet een nieuwe veldgroep krijgen die een nieuw veld aan het schema toevoegt: `favoriteHotel`.

>[!NOTE]
>
>Als uw bronschema reeds een specifiek gebied heeft dat u als verwijzingsgebied van plan bent te gebruiken, kunt u vooruit naar de stap overslaan [een verwijzingsdescriptor maken](#reference-identity).

### Een nieuwe veldgroep maken

Als u een nieuw veld aan een schema wilt toevoegen, moet u dit eerst definiëren in een veldgroep. U kunt een nieuwe veldgroep maken door een POST aan te vragen bij de `/tenant/fieldgroups` eindpunt.

**API-indeling**

```http
POST /tenant/fieldgroups
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe veldgroep gemaakt die een `favoriteHotel` onder de `_{TENANT_ID}` naamruimte van elk schema waaraan de naamruimte is toegevoegd.

```shell
curl -X POST\
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/fieldgroups \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'content-type: application/json' \
  -d '{
        "type": "object",
        "title": "Favorite Hotel",
        "meta:intendedToExtend": ["https://ns.adobe.com/xdm/context/profile"],
        "description": "Favorite hotel field group for the Loyalty Members schema.",
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

Een geslaagde reactie retourneert de details van de nieuwe veldgroep.

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
    "description": "Favorite hotel field group for the Loyalty Members schema.",
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
| `$id` | De alleen-lezen, door het systeem gegenereerde unieke id van de nieuwe veldgroep. De vorm van een URI. |

{style=&quot;table-layout:auto&quot;}

Neem de `$id` URI van de veldgroep, te gebruiken in de volgende stap van het toevoegen van de veldgroep aan het bronschema.

### De veldgroep toevoegen aan het bronschema

Nadat u een veldgroep hebt gemaakt, kunt u deze toevoegen aan het bronschema door een PATCH-aanvraag in te dienen bij de `/tenant/schemas/{SCHEMA_ID}` eindpunt.

**API-indeling**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | URL-gecodeerd `$id` URI of `meta:altId` van het bronschema. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Met het volgende verzoek wordt de toevoeging &quot;[!DNL Favorite Hotel]&quot; veldgroep naar &quot;[!DNL Loyalty Members]&quot; schema.

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.533ca5da28087c44344810891b0f03d9 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | De uit te voeren PATCH-bewerking. In dit verzoek wordt het `add` bewerking. |
| `path` | De weg aan het schemagebied waar het nieuwe middel zal worden toegevoegd. Wanneer u veldgroepen toevoegt aan schema&#39;s, moet de waarde &quot;/allOf/-&quot; zijn. |
| `value.$ref` | De `$id` van de veldgroep die moet worden toegevoegd. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvol antwoord keert de details van het bijgewerkte schema terug, dat nu omvat `$ref` waarde van de toegevoegde veldgroep onder de `allOf` array.

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
    "imsOrg": "{ORG_ID}",
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

Op schemavelden moet een identiteitsreferentie-descriptor zijn toegepast als deze worden gebruikt als referentie van andere schema&#39;s in een relatie. Aangezien `favoriteHotel` veld in &quot;[!DNL Loyalty Members]&quot; verwijst naar de `hotelId` veld in &quot;[!DNL Hotels]&quot;, `hotelId` moet een referentie-identiteitsbeschrijving krijgen.

Creeer een verwijzingsbeschrijver voor het bestemmingsschema door een verzoek van de POST aan het `/tenant/descriptors` eindpunt.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Met de volgende aanvraag wordt een verwijzingsdescriptor gemaakt voor de `hotelId` veld in het doelschema &quot;[!DNL Hotels]&quot;.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `xdm:sourceSchema` | De `$id` URL van het doelschema. |
| `xdm:sourceVersion` | Het versienummer van het doelschema. |
| `sourceProperty` | Het pad naar het primaire identiteitsveld van het doelschema. |
| `xdm:identityNamespace` | De naamruimte van de identiteit van het verwijzingsveld. Dit moet dezelfde naamruimte zijn die wordt gebruikt wanneer het veld wordt gedefinieerd als de primaire identiteit van het schema. Zie de [Overzicht van naamruimte in identiteit](../../identity-service/home.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

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

## Relatiebeschrijvingen maken {#create-descriptor}

Relatiebeschrijvingen maken een één-op-één relatie tussen een bronschema en een doelschema. Zodra u een verwijzingsbeschrijver voor het bestemmingsschema hebt bepaald, kunt u een nieuwe relatiebeschrijver tot stand brengen door een verzoek van de POST aan `/tenant/descriptors` eindpunt.

**API-indeling**

```http
POST /tenant/descriptors
```

**Verzoek**

Met het volgende verzoek wordt een nieuwe relatiebeschrijving gemaakt met &quot;[!DNL Loyalty Members]&quot; als het bronschema en &quot;[!DNL Legacy Loyalty Members]&quot; als het doelschema.

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/descriptors \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `@type` | Het type descriptor dat moet worden gemaakt. De `@type` value for relationship descriptors is &quot;xdm:descriptorOneToOne&quot;. |
| `xdm:sourceSchema` | De `$id` URL van het bronschema. |
| `xdm:sourceVersion` | Het versienummer van het bronschema. |
| `xdm:sourceProperty` | Het pad naar het verwijzingsveld in het bronschema. |
| `xdm:destinationSchema` | De `$id` URL van het doelschema. |
| `xdm:destinationVersion` | Het versienummer van het doelschema. |
| `xdm:destinationProperty` | Het pad naar het verwijzingsveld in het doelschema. |

{style=&quot;table-layout:auto&quot;}

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

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd. Voor meer informatie over het werken met descriptoren gebruikt u de opdracht [!DNL Schema Registry] API, zie [Handleiding voor ontwikkelaars van het schema Register](../api/descriptors.md). Voor stappen op hoe te om schemaverhoudingen in UI te bepalen, zie het leerprogramma op [schemarelaties definiëren met de Schema-editor](relationship-ui.md).
