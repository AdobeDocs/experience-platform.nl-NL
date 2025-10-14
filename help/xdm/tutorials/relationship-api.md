---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema;Schema;schema's;Schema's;Relationship;Relationship;Relationship descriptor;Relationship descriptor;reference identity;Reference identity;
title: Definieer een relatie tussen twee schema's met behulp van de API voor het schemaregister
description: Dit document verstrekt een zelfstudie voor het bepalen van een één-op-één verhouding tussen twee schema's die door uw organisatie worden bepaald gebruikend de Registratie API van het Schema.
type: Tutorial
exl-id: ef9910b5-2777-4d8b-a6fe-aee51d809ad5
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Een relatie tussen twee schema&#39;s definiëren met de API [!DNL Schema Registry]

De mogelijkheid om de relaties tussen uw klanten en hun interactie met uw merk op verschillende kanalen te begrijpen is een belangrijk onderdeel van Adobe Experience Platform. Door deze relaties te definiëren binnen de structuur van uw [!DNL Experience Data Model] (XDM)-schema&#39;s kunt u complexe inzichten in uw klantgegevens opdoen.

Hoewel schemarelaties kunnen worden afgeleid door het gebruik van het samenvoegingsschema en [!DNL Real-Time Customer Profile] , geldt dit alleen voor schema&#39;s die dezelfde klasse delen. Om een verband tussen twee schema&#39;s te vestigen die tot verschillende klassen behoren, moet een specifiek relatiegebied aan a **bronschema** worden toegevoegd, dat op de identiteit van een afzonderlijk **verwijzingsschema** wijst.

>[!NOTE]
>
>De API van de Registratie van het Schema verwijst naar verwijzingsschema&#39;s als &quot;bestemmingsschema&#39;s&quot;. Deze moeten niet met bestemmingsschema&#39;s in [&#x200B; de kaartreeksen van Prep van Gegevens &#x200B;](../../data-prep/mapping-set.md) of schema&#39;s voor [&#x200B; bestemmingsverbindingen &#x200B;](../../destinations/home.md) worden verward.

Dit document verstrekt een zelfstudie voor het bepalen van een één-aan-één verhouding tussen twee schema&#39;s die door uw organisatie worden bepaald gebruikend [[!DNL Schema Registry API] &#x200B;](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Aan de slag

Deze zelfstudie vereist een goed begrip van [!DNL Experience Data Model] (XDM) en [!DNL XDM System] . Lees de volgende documentatie voordat u met deze zelfstudie begint:

* [&#x200B; XDM Systeem in Experience Platform &#x200B;](../home.md): Een overzicht van XDM en zijn implementatie in [!DNL Experience Platform].
   * [&#x200B; Grondbeginselen van schemacompositie &#x200B;](../schema/composition.md): Een inleiding van de bouwstenen van schema&#39;s XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [&#x200B; Sandboxen &#x200B;](../../sandboxes/home.md): [!DNL Experience Platform] verstrekt virtuele zandbakken die één enkele [!DNL Experience Platform] instantie in afzonderlijke virtuele milieu&#39;s verdelen helpen digitale ervaringstoepassingen ontwikkelen en ontwikkelen.

Alvorens dit leerprogramma te beginnen, te herzien gelieve de [&#x200B; ontwikkelaarsgids &#x200B;](../api/getting-started.md) voor belangrijke informatie die u moet kennen om vraag aan [!DNL Schema Registry] API met succes te maken. Dit omvat uw `{TENANT_ID}` , het concept &quot;containers&quot; en de vereiste kopteksten voor het indienen van aanvragen (met speciale aandacht voor de header [!DNL Accept] en de mogelijke waarden ervan).

## Een bron- en referentieschema definiëren {#define-schemas}

Verwacht wordt dat u reeds de twee schema&#39;s hebt gecreeerd die in de verhouding zullen worden bepaald. Dit leerprogramma leidt tot een verband tussen leden van het huidige loyaliteitsprogramma van een organisatie (die in een &quot;[!DNL Loyalty Members]&quot;schema wordt bepaald) en hun favoriete hotels (die in een &quot;[!DNL Hotels]&quot;schema wordt bepaald).

De verhoudingen van het schema worden vertegenwoordigd door a **bronschema** hebbend een gebied dat naar een ander gebied binnen a **verwijzingsschema** verwijst. In de stappen die volgen, &quot;[!DNL Loyalty Members]&quot;zal het bronschema zijn, terwijl &quot;[!DNL Hotels]&quot;als verwijzingsschema zal dienst doen.

>[!IMPORTANT]
>
>Om een relatie tot stand te brengen, moeten beide schema&#39;s primaire identiteiten hebben bepaald en voor [!DNL Real-Time Customer Profile] worden toegelaten. Zie de sectie op [&#x200B; toelatend een schema voor gebruik in Profiel &#x200B;](./create-schema-api.md#profile) in het leerprogramma van de schemaverwezenlijking als u begeleiding op hoe te om uw schema&#39;s dienovereenkomstig te vormen vereist.

Als u een relatie tussen twee schema&#39;s wilt definiëren, moet u eerst de `$id` -waarden voor beide schema&#39;s ophalen. Als u de weergavenamen (`title`) van de schema&#39;s kent, kunt u hun `$id` -waarden vinden door een GET-aanvraag in te dienen bij het `/tenant/schemas` -eindpunt in de [!DNL Schema Registry] API.

**API formaat**

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
>De [!DNL Accept] header `application/vnd.adobe.xed-id+json` retourneert alleen de titels, id&#39;s en versies van de resulterende schema&#39;s.

**Reactie**

Een geslaagde reactie retourneert een lijst met schema&#39;s die door uw organisatie zijn gedefinieerd, inclusief de schema&#39;s `name` , `$id` , `meta:altId` en `version` .

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

Binnen [!DNL Schema Registry], werken de relatiebeschrijvers gelijkaardig aan buitenlandse sleutels in relationele gegevensbestandlijsten: een gebied in het bronschema dienst als verwijzing naar het primaire identiteitsgebied van een verwijzingsschema. Als uw bronschema geen gebied voor dit doel heeft, kunt u een groep van het schemagebied met het nieuwe gebied moeten tot stand brengen en het toevoegen aan het schema. Dit nieuwe veld moet een `type` waarde `string` hebben.

>[!IMPORTANT]
>
>Het bronschema kan zijn primaire identiteit niet als verwijzingsgebied gebruiken.

In deze zelfstudie, bevat het verwijzingsschema &quot;[!DNL Hotels]&quot;een `hotelId` gebied dat als primaire identiteit van het schema dient. Nochtans, heeft het bronschema &quot;[!DNL Loyalty Members]&quot;geen specifiek gebied dat als verwijzing naar `hotelId` moet worden gebruikt, en daarom moet een groep van het douanegebied worden gecreeerd om een nieuw gebied aan het schema toe te voegen: `favoriteHotel`.

>[!NOTE]
>
>Als uw bronschema reeds een specifiek gebied heeft dat u van plan bent als verwijzingsgebied te gebruiken, kunt u vooruit aan de stap overslaan op [&#x200B; creërend een verwijzingsbeschrijver &#x200B;](#reference-identity).

### Een nieuwe veldgroep maken

Als u een nieuw veld aan een schema wilt toevoegen, moet u dit eerst definiëren in een veldgroep. U kunt een nieuwe veldgroep maken door een POST-aanvraag in te dienen bij het eindpunt van `/tenant/fieldgroups` .

**API formaat**

```http
POST /tenant/fieldgroups
```

**Verzoek**

Met de volgende aanvraag wordt een nieuwe veldgroep gemaakt die een veld `favoriteHotel` onder de naamruimte `_{TENANT_ID}` toevoegt van een schema waaraan het wordt toegevoegd.

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

**Reactie**

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

{style="table-layout:auto"}

Neem de `$id` URI van de veldgroep op, die moet worden gebruikt in de volgende stap bij het toevoegen van de veldgroep aan het bronschema.

### De veldgroep toevoegen aan het bronschema

Nadat u een veldgroep hebt gemaakt, kunt u deze toevoegen aan het bronschema door een PATCH-aanvraag in te dienen bij het `/tenant/schemas/{SCHEMA_ID}` -eindpunt.

**API formaat**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` van het bronschema. |

{style="table-layout:auto"}

**Verzoek**

Het volgende verzoek voegt de &quot;[!DNL Favorite Hotel]&quot;gebiedsgroep aan het &quot;[!DNL Loyalty Members]&quot;schema toe.

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
| `op` | De PATCH-bewerking die moet worden uitgevoerd. In deze aanvraag wordt de bewerking `add` gebruikt. |
| `path` | De weg aan het schemagebied waar het nieuwe middel zal worden toegevoegd. Wanneer u veldgroepen aan schema&#39;s toevoegt, moet de waarde &quot;/allOf/-&quot; zijn. |
| `value.$ref` | De `$id` van de veldgroep die moet worden toegevoegd. |

{style="table-layout:auto"}

**Reactie**

Een geslaagde reactie retourneert de details van het bijgewerkte schema, dat nu de `$ref` -waarde van de toegevoegde veldgroep onder de `allOf` -array bevat.

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

Op schemavelden moet een identiteitsbeschrijving van de referentie zijn toegepast als deze worden gebruikt als een verwijzing naar een ander schema in een relatie. Aangezien het veld `favoriteHotel` in &quot;[!DNL Loyalty Members]&quot; verwijst naar het veld `hotelId` in &quot;[!DNL Hotels]&quot;, moet aan `favoriteHotel` een identiteitsbeschrijvingsreferentie worden gegeven.

Creeer een verwijzingsbeschrijver voor het bronschema door een POST- verzoek aan het `/tenant/descriptors` eindpunt te doen.

**API formaat**

```http
POST /tenant/descriptors
```

**Verzoek**

Met de volgende aanvraag wordt een verwijzingsdescriptor gemaakt voor het veld `favoriteHotel` in het bronschema &quot;[!DNL Loyalty Members]&quot;.

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
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID"
  }'
```

| Parameter | Beschrijving |
| --- | --- |
| `@type` | Het type descriptor dat wordt gedefinieerd. Voor verwijzingsbeschrijvingen moet de waarde `xdm:descriptorReferenceIdentity` zijn. |
| `xdm:sourceSchema` | De `$id` URL van het bronschema. |
| `xdm:sourceVersion` | Het versienummer van het bronschema. |
| `sourceProperty` | Het pad naar het veld in het bronschema dat wordt gebruikt om naar de primaire identiteit van het referentieschema te verwijzen. |
| `xdm:identityNamespace` | De naamruimte van de identiteit van het verwijzingsveld. Dit moet dezelfde naamruimte zijn als de primaire identiteit van het referentieschema. Zie het [&#x200B; overzicht van identiteitskaart namespace &#x200B;](../../identity-service/home.md) voor meer informatie. |

{style="table-layout:auto"}

**Reactie**

Een succesvol antwoord retourneert de details van de zojuist gemaakte verwijzingsdescriptor voor het bronveld.

```json
{
    "@type": "xdm:descriptorReferenceIdentity",
    "xdm:sourceSchema": "https://ns.adobe.com/{TENANT_ID}/schemas/533ca5da28087c44344810891b0f03d9",
    "xdm:sourceVersion": 1,
    "xdm:sourceProperty": "/_{TENANT_ID}/favoriteHotel",
    "xdm:identityNamespace": "Hotel ID",
    "meta:containerId": "tenant",
    "@id": "53180e9f86eed731f6bf8bf42af4f59d81949ba6"
}
```

## Relatiebeschrijvingen maken {#create-descriptor}

Relatiebeschrijvingen maken een één-op-één relatie tussen een bronschema en een referentieschema. Zodra u een beschrijver van de verwijzingsidentiteit voor het aangewezen gebied in het bronschema hebt bepaald, kunt u een nieuwe relatiebeschrijver tot stand brengen door een POST- verzoek aan het `/tenant/descriptors` eindpunt te doen.

**API formaat**

```http
POST /tenant/descriptors
```

**Verzoek**

Het volgende verzoek leidt tot een nieuwe relatiebeschrijver, met &quot;[!DNL Loyalty Members]&quot;als bronschema en &quot;[!DNL Hotels]&quot;als verwijzingsschema.

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
| `@type` | Het type descriptor dat moet worden gemaakt. De `@type` -waarde voor relatiebeschrijvingen is `xdm:descriptorOneToOne` . |
| `xdm:sourceSchema` | De `$id` URL van het bronschema. |
| `xdm:sourceVersion` | Het versienummer van het bronschema. |
| `xdm:sourceProperty` | Het pad naar het verwijzingsveld in het bronschema. |
| `xdm:destinationSchema` | De `$id` URL van het referentieschema. |
| `xdm:destinationVersion` | The version number of the reference schema. |
| `xdm:destinationProperty` | Het pad naar het primaire identiteitsveld in het referentieschema. |

{style="table-layout:auto"}

### Antwoord

Een succesvolle reactie retourneert de details van de zojuist gemaakte relatiebeschrijving.

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

Door deze zelfstudie te volgen, hebt u met succes een één-op-één verhouding tussen twee schema&#39;s gecreeerd. Voor meer informatie bij het werken met beschrijvers die [!DNL Schema Registry] API gebruiken, zie de [&#x200B; de ontwikkelaarsgids van de Registratie van het Schema &#x200B;](../api/descriptors.md). Voor stappen op hoe te om schemaverhoudingen in UI te bepalen, zie het leerprogramma op [&#x200B; bepalend schemaverhoudingen gebruikend de Redacteur van het Schema &#x200B;](relationship-ui.md).
