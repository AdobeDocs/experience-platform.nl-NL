---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Unies
topic: developer guide
translation-type: tm+mt
source-git-commit: fabaabc3cc5b82cba084bddd081f5bba670b89f0

---


# Unies

De verenigingen (of verenigingsmeningen) zijn systeem-geproduceerde, read-only schema&#39;s die de gebieden van alle schema&#39;s samenvoegen die de zelfde klasse (XDM ExperienceEvent of Individueel Profiel XDM) delen en voor het Profiel [van de Klant in](../../profile/home.md)real time worden toegelaten.

Dit document behandelt essentiële concepten voor het werken met vakbonden in de API van de Registratie van het Schema, met inbegrip van steekproefvraag voor diverse verrichtingen. Voor meer algemene informatie over unies in XDM, zie de sectie over unies in de [grondbeginselen van schemacompositie](../schema/composition.md#union).

## Uniemengsels

Het Register van het Schema omvat automatisch drie mengen binnen het unieschema: `identityMap`, `timeSeriesEvents`, en `segmentMembership`.

### Identiteitskaart

Een verenigingsschema `identityMap` is een vertegenwoordiging van de bekende identiteiten binnen de bijbehorende verslagschema&#39;s van de unie. In het identiteitsoverzicht worden identiteiten gescheiden in verschillende arrays die door naamruimte worden gebruikt. Elke vermelde identiteit is zelf een object dat een unieke `id` waarde bevat.

Raadpleeg de documentatie [bij](../../identity-service/home.md) Identiteitsservice voor meer informatie.

### Gebeurtenissen uit de tijdreeks

De `timeSeriesEvents` array is een lijst met tijdreeksgebeurtenissen die betrekking hebben op de recordschema&#39;s die aan de union zijn gekoppeld. Wanneer profielgegevens naar gegevenssets worden geëxporteerd, wordt deze array opgenomen voor elke record. Dit is handig voor verschillende gebruiksgevallen, zoals het leren van machines waarbij modellen naast de recordkenmerken ook de gehele gedragsgeschiedenis van een profiel nodig hebben.

### Segmentlidmaatschapstoewijzing

De `segmentMembership` kaart slaat de resultaten van segmentevaluaties op. Wanneer segmenttaken met succes worden uitgevoerd met de [Real-Time Customer Profile API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml), wordt de kaart bijgewerkt. `segmentMembership` slaat ook om het even welke vooraf beoordeelde publiekssegmenten op die in Platform worden opgenomen, die voor integratie met andere oplossingen zoals de Manager van de Audience van Adobe toestaan.

Zie de zelfstudie over het [maken van segmenten met behulp van API&#39;s](../../segmentation/tutorials/create-a-segment.md) voor meer informatie.

## Een schema voor samenvoeging inschakelen

Om een schema in de samengevoegde verenigingsmening te omvatten, moet de markering &quot;union&quot;aan de `meta:immutableTags` attributen van het schema worden toegevoegd. Dit gebeurt via een PATCH-verzoek om het schema bij te werken en de `meta:immutableTags` array toe te voegen met de waarde &quot;union&quot;.

>[!NOTE] Onveranderbare tags zijn tags die zijn bedoeld om te worden ingesteld, maar die nooit worden verwijderd.

**API-indeling**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{SCHEMA_ID}` | De URL-gecodeerde `$id` URI of `meta:altId` het schema dat u wilt inschakelen voor gebruik in Profiel. |

**Verzoek**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**Antwoord**

Een succesvol antwoord retourneert de details van het bijgewerkte schema, dat nu een `meta:immutableTags` array bevat met de tekenreekswaarde &quot;union&quot;.

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## Lijstverenigingen

Wanneer u de tag union instelt op een schema, maakt en onderhoudt de schemaregistratie automatisch een samenvoeging voor de klasse waarop het schema is gebaseerd. De `$id` voor de Unie is vergelijkbaar met de standaard `$id` van een klasse, met als enige verschil dat twee onderstrepingen en het woord &quot;union&quot; (`"__union"`) worden toegevoegd.

Om een lijst van beschikbare unies te bekijken, kunt u een GET verzoek aan het `/unions` eindpunt uitvoeren.

**API-indeling**

```http
GET /tenant/unions
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en een `results` array in de hoofdtekst van de reactie. Als er samenvoegingen zijn gedefinieerd, worden de elementen `title`, `$id`, `meta:altId`en `version` voor elke samenvoeging als objecten in de array opgegeven. Als er geen samenvoegingen zijn gedefinieerd, wordt de HTTP-status 200 (OK) nog steeds geretourneerd, maar is de `results` array leeg.

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## Een specifieke unie opzoeken

U kunt een specifieke unie bekijken door een GET verzoek uit te voeren dat de `$id` en, afhankelijk van de Accept- kopbal, sommige of alle details van de unie omvat.

>[!NOTE] De raadplegingen van de Unie zijn beschikbaar gebruikend het `/unions` en `/schemas` eindpunt om hen voor gebruik in de uitvoer van het Profiel in een dataset toe te laten.

**API-indeling**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{UNION_ID}` | De URL-gecodeerde `$id` URI van de union die u wilt opzoeken. URI&#39;s voor union-schema&#39;s worden toegevoegd met &quot;__union&quot;. |

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Voor opzoekverzoeken van de Unie moet de header Accepteren `version` worden opgenomen.

De volgende Accept- kopballen zijn beschikbaar voor de raadplegingen van het unieschema:

| Accepteren | Beschrijving |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Onbewerkt met `$ref` en `allOf`. Hier vindt u titels en beschrijvingen. |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` kenmerken en `allOf` opgelost. Hier vindt u titels en beschrijvingen. |

**Antwoord**

Een succesvolle reactie keert de verenigingsmening van alle schema&#39;s terug die de klasse uitvoeren waarvan in de verzoekweg `$id` werd verstrekt.

De responsindeling is afhankelijk van de Accept-header die in de aanvraag wordt verzonden. Experimenteer met verschillende kopteksten voor Accepteren om de reacties te vergelijken en te bepalen welke koptekst het beste is voor uw gebruik.

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## Schema&#39;s weergeven in een union

Om te zien welke schema&#39;s deel van een specifieke unie uitmaken, kunt u een GET verzoek uitvoeren gebruikend vraagparameters om de schema&#39;s binnen de huurderscontainer te filtreren.

Gebruikend de `property` vraagparameter, kunt u de reactie vormen op slechts terugkeerschema&#39;s die een `meta:immutableTags` gebied en een `meta:class` gelijke aan de klasse bevatten waarvan unie u toegang hebt tot.

**API-indeling**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De `$id` klasse waartoe u toegang wilt hebben. |

**Verzoek**

Het volgende verzoek kijkt omhoog alle schema&#39;s die deel van de de klassenunie van het Profiel van XDM Individual uitmaken.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een gefilterde lijst van schema&#39;s terug, die slechts die bevatten die aan beide vereisten voldoen. Herinner dat wanneer het gebruiken van veelvoudige vraagparameters, EN verhouding wordt verondersteld. De indeling van de reactie is afhankelijk van de header Accepteren die in de aanvraag wordt verzonden.

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
