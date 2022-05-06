---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema Register;Union;Union;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unions API-eindpunt
description: Het /union eindpunt in de Registratie API van het Schema staat u toe om XDM vakingsschema's in uw ervaringstoepassing programmatically te beheren.
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 0%

---

# Uniepunten

Unions (of verenigingsmeningen) zijn systeem-geproduceerde, read-only schema&#39;s die de gebieden van alle schema&#39;s samenvoegen die de zelfde klasse delen ([!DNL XDM ExperienceEvent] of [!DNL XDM Individual Profile]) en zijn ingeschakeld voor [[!DNL Real-time Customer Profile]](../../profile/home.md).

Dit document behandelt essentiële concepten voor het werken met vakbonden in de API van de Registratie van het Schema, met inbegrip van steekproefvraag voor diverse verrichtingen. Voor meer algemene informatie over vakbonden in XDM, zie de sectie over vakbonden in [grondbeginselen van de schemacompositie](../schema/composition.md#union).

## Unieschemavelden

De [!DNL Schema Registry] omvat automatisch drie zeer belangrijke gebieden binnen een verenigingsschema: `identityMap`, `timeSeriesEvents`, en `segmentMembership`.

### Identiteitskaart

Een samenvoegingsschema&#39;s `identityMap` is een weergave van de bekende identiteiten in de bijbehorende recordschema &#39; s van de unie . In het identiteitsoverzicht worden identiteiten gescheiden in verschillende arrays die door naamruimte worden gebruikt. Elke vermelde identiteit is zelf een object dat een uniek object bevat `id` waarde. Zie de [Identiteitsdocumentatie](../../identity-service/home.md) voor meer informatie .

### Gebeurtenissen uit de tijdreeks

De `timeSeriesEvents` array is een lijst met tijdreeksgebeurtenissen die betrekking hebben op de recordschema&#39;s die aan de union zijn gekoppeld. Wanneer profielgegevens naar datasets worden geëxporteerd, wordt deze array opgenomen voor elke record. Dit is handig voor verschillende gebruiksgevallen, zoals het leren van machines waarbij modellen naast de recordkenmerken ook de gehele gedragsgeschiedenis van een profiel nodig hebben.

### Segmentlidmaatschapstoewijzing

De `segmentMembership` map slaat de resultaten van segmentevaluaties op. Wanneer segmenttaken correct worden uitgevoerd met de opdracht [Segmentatie-API](https://www.adobe.io/experience-platform-apis/references/segmentation/), wordt de kaart bijgewerkt. `segmentMembership` slaat ook om het even welke vooraf beoordeelde publiekssegmenten op die in Platform worden opgenomen, die voor integratie met andere oplossingen zoals Adobe Audience Manager toestaan. Zie de zelfstudie aan [segmenten maken met behulp van API&#39;s](../../segmentation/tutorials/create-a-segment.md) voor meer informatie .

## Een lijst met vakbonden ophalen {#list}

Wanneer u de `union` tag op een schema, [!DNL Schema Registry] voegt automatisch het schema aan de unie voor de klasse toe waarop het schema wordt gebaseerd. Als er voor de betreffende klasse geen vakbond bestaat, wordt automatisch een nieuwe vakbond gemaakt. De `$id` voor de unie is dit een soortgelijke norm `$id` van andere [!DNL Schema Registry] middelen, met het enige verschil dat wordt toegevoegd door twee onderstrepingen en het woord &quot; unie &quot; (`__union`).

U kunt een lijst met beschikbare vakbonden weergeven door de GET aan te vragen `/tenant/unions` eindpunt.

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Het volgende `Accept` Kopteksten zijn beschikbaar voor samenvoegingen:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-klasse voor elke bron, met origineel `$ref` en `allOf` opgenomen. (Limiet: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en een `results` in de responsstructuur. Als vakbonden zijn gedefinieerd, worden de gegevens voor elke samenvoeging als objecten in de array gegeven. Als er geen samenvoeging is gedefinieerd, wordt de HTTP-status 200 (OK) wel geretourneerd, maar wordt de waarde `results` array is leeg.

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

## Vereniging opzoeken {#lookup}

U kunt een specifieke samenvoeging bekijken door een verzoek uit te voeren dat omvat `$id` en, afhankelijk van de Accept-header, sommige of alle details van de union.

>[!NOTE]
>
>U kunt zoeken naar de Unie met de `/unions` en `/schemas` eindpunt om hen toe te laten voor gebruik in [!DNL Profile] de uitvoer naar een dataset.

**API-indeling**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{UNION_ID}` | URL-gecodeerd `$id` URI van de union die u wilt opzoeken. URI&#39;s voor union-schema&#39;s worden toegevoegd met &quot;__union&quot;. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

Voor verzoeken om opzoekingen door de Unie is een `version` worden opgenomen in de koptekst Accepteren.

De volgende Accept- kopballen zijn beschikbaar voor de raadplegingen van het unieschema:

| Accepteren | Beschrijving |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Onbewerkt met `$ref` en `allOf`. Hier vindt u titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` kenmerken en `allOf` opgelost. Hier vindt u titels en beschrijvingen. |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert de verenigingsmening van alle schema&#39;s terug die de klasse uitvoeren waarvan `$id` is opgegeven in het aanvraagpad.

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

## Een schema voor samenvoeging inschakelen {#enable}

Om een schema voor zijn klasse in de unie te omvatten, `union` -tag moet worden toegevoegd aan het schema `meta:immutableTags` kenmerk. U kunt dit bereiken door een PATCH-verzoek in te dienen om een `meta:immutableTags` array met één tekenreekswaarde van `union` op het betrokken schema. Zie de [schema&#39;s eindpuntgids](./schemas.md#union) voor een gedetailleerd voorbeeld.

## Schema&#39;s weergeven in een union {#list-schemas}

Om te zien welke schema&#39;s deel van een specifieke vereniging uitmaken, kunt u een verzoek van de GET tot uitvoeren `/tenant/schemas` eindpunt. Met de `property` de vraagparameter, kunt u de reactie vormen om slechts schema&#39;s terug te keren die een bevatten `meta:immutableTags` en `meta:class` is gelijk aan de klasse waarvan u de unie opent.

**API-indeling**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De `$id` van de klasse waarvan de unie-Toegelaten schema&#39;s u wilt een lijst maken. |

{style=&quot;table-layout:auto&quot;}

**Verzoek**

Het volgende verzoek wint een lijst van alle schema&#39;s terug die deel van de unie voor de unie uitmaken [!DNL XDM Individual Profile] klasse.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De responsindeling is afhankelijk van `Accept` in de aanvraag verzonden. Het volgende `Accept` Kopteksten zijn beschikbaar voor aanbiedingsschema&#39;s:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert het volledige JSON-schema voor elke bron, met het origineel `$ref` en `allOf` opgenomen. (Limiet: 300) |

{style=&quot;table-layout:auto&quot;}

**Antwoord**

Een succesvolle reactie keert een gefilterde lijst van schema&#39;s terug, die slechts die bevatten die tot de gespecificeerde klasse behoren die voor vakbondslidmaatschap zijn toegelaten. Herinner dat wanneer het gebruiken van veelvoudige vraagparameters, EN verhouding wordt verondersteld.

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
