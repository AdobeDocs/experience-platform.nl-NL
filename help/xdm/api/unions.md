---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Schema Register;Schema Register;Union;Union;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Unions API-eindpunt
description: Het /union eindpunt in de Registratie API van het Schema staat u toe om XDM vakingsschema's in uw ervaringstoepassing programmatically te beheren.
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 3da2e8f66f08a7bb9533795f7854ad583734911c
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---

# Uniepunten

Unions (of samenvoegingsweergaven) zijn door het systeem gegenereerde, alleen-lezen schema&#39;s die de velden samenvoegen van alle schema&#39;s die dezelfde klasse delen ([!DNL XDM ExperienceEvent] of [!DNL XDM Individual Profile] ) en die zijn ingeschakeld voor [[!DNL Real-Time Customer Profile]](../../profile/home.md) .

Dit document behandelt essentiële concepten voor het werken met vakbonden in de API van de Registratie van het Schema, met inbegrip van steekproefvraag voor diverse verrichtingen. Voor meer algemene informatie over unies in XDM, zie de sectie over unies in de [ grondbeginselen van schemacompositie ](../schema/composition.md#union).

## Unieschemavelden

[!DNL Schema Registry] bevat automatisch drie belangrijke velden binnen een samenvoegingsschema: `identityMap` , `timeSeriesEvents` en `segmentMembership` .

### Identiteitskaart

Het schema van de unie `identityMap` is een vertegenwoordiging van de bekende identiteiten binnen de bijbehorende verslagschema&#39;s van de unie. In het identiteitsoverzicht worden identiteiten gescheiden in verschillende arrays die door naamruimte worden gebruikt. Elke vermelde identiteit is zelf een object dat een unieke `id` -waarde bevat. Zie de [ documentatie van de Dienst van de Identiteit ](../../identity-service/home.md) voor meer informatie.

### Gebeurtenissen uit de tijdreeks

De array `timeSeriesEvents` is een lijst met tijdreeksgebeurtenissen die betrekking hebben op de recordschema&#39;s die aan de union zijn gekoppeld. Wanneer profielgegevens naar datasets worden geëxporteerd, wordt deze array opgenomen voor elke record. Dit is handig voor verschillende gebruiksgevallen, zoals het leren van machines waarbij modellen naast de recordkenmerken ook de gehele gedragsgeschiedenis van een profiel nodig hebben.

### Segmentlidmaatschapstoewijzing

In de `segmentMembership` -kaart worden de resultaten opgeslagen van de evaluatie van een segmentdefinitie. Wanneer de segmentbanen met succes gebruikend de [ Segmentatie API ](https://www.adobe.io/experience-platform-apis/references/segmentation/) in werking worden gesteld, wordt de kaart bijgewerkt. `segmentMembership` slaat ook vooraf beoordeelde soorten publiek op die in Platform worden opgenomen, waardoor integratie met andere oplossingen zoals Adobe Audience Manager mogelijk wordt. Zie het leerprogramma op [ creërend publiek gebruikend APIs ](../../segmentation/tutorials/create-a-segment.md) voor meer informatie.

## Een lijst met vakbonden ophalen {#list}

Wanneer u de tag `union` instelt op een schema, voegt [!DNL Schema Registry] automatisch het schema toe aan de union voor de klasse waarop het schema is gebaseerd. Als er voor de betreffende klasse geen vakbond bestaat, wordt automatisch een nieuwe vakbond gemaakt. `$id` voor de union is gelijkaardig aan de norm `$id` van andere [!DNL Schema Registry] middelen, met het enige verschil dat door twee onderstrepingstekens en het woord &quot;union&quot; (`__union`) wordt toegevoegd.

U kunt een lijst met beschikbare samenvoegingen weergeven door een aanvraag voor GET in te dienen bij het eindpunt van `/tenant/unions` .

**API formaat**

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

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor samenvoegingen:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert de volledige JSON-klasse voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

{style="table-layout:auto"}

**Reactie**

Een geslaagde reactie retourneert HTTP-status 200 (OK) en een `results` -array in de hoofdtekst van de reactie. Als vakbonden zijn gedefinieerd, worden de gegevens voor elke samenvoeging als objecten in de array gegeven. Als er geen samenvoegingen zijn gedefinieerd, wordt de HTTP-status 200 (OK) nog steeds geretourneerd, maar is de array `results` leeg.

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

U kunt een specifieke samenvoeging bekijken door een verzoek van de GET uit te voeren die `$id` omvat en, afhankelijk van de Accept- kopbal, sommige of alle details van de unie.

>[!NOTE]
>
>Er zijn Unieverkenningen beschikbaar met behulp van het `/unions` - en `/schemas` -eindpunt, zodat deze kunnen worden gebruikt bij [!DNL Profile] -export naar een gegevensset.

**API formaat**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{UNION_ID}` | De URL-gecodeerde `$id` URI van de union die u wilt opzoeken. URI&#39;s voor union-schema&#39;s worden toegevoegd met &quot;__union&quot;. |

{style="table-layout:auto"}

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

Voor opzoekverzoeken naar een Vereniging moet een `version` worden opgenomen in de koptekst Accepteren.

De volgende Accept-koppen zijn beschikbaar voor samenvoegschema-lookups:

| Accepteren | Beschrijving |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Onbewerkt met `$ref` en `allOf` . Hier vindt u titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` -kenmerken en `allOf` opgelost. Hier vindt u titels en beschrijvingen. |

{style="table-layout:auto"}

**Reactie**

Een geslaagde reactie retourneert de samenvoegweergave van alle schema&#39;s waarmee de klasse wordt geïmplementeerd waarvan `$id` is opgegeven in het aanvraagpad.

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

Als u een schema voor de klasse wilt opnemen in de samenvoeging, moet u een tag `union` toevoegen aan het kenmerk `meta:immutableTags` van het schema. U kunt dit bereiken door een PATCH-verzoek in te dienen om een `meta:immutableTags` -array met een enkele tekenreekswaarde van `union` aan het desbetreffende schema toe te voegen. Zie de [ gids van het schemaeindpunt ](./schemas.md#union) voor een gedetailleerd voorbeeld.

## Schema&#39;s weergeven in een union {#list-schemas}

Om te zien welke schema&#39;s deel van een specifieke vereniging uitmaken, kunt u een verzoek van de GET tot het `/tenant/schemas` eindpunt uitvoeren. Met de query-parameter `property` kunt u de reactie alleen configureren voor retourschema&#39;s die een `meta:immutableTags` field en een `meta:class` bevatten die gelijk zijn aan de klasse waartoe u toegang hebt.

**API Formaat**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| Parameter | Beschrijving |
| --- | --- |
| `{CLASS_ID}` | De `$id` van de klasse waarvan unie-Toegelaten schema&#39;s u wilt een lijst maken. |

{style="table-layout:auto"}

**Verzoek**

Met het volgende verzoek wordt een lijst opgehaald van alle schema&#39;s die deel uitmaken van de union voor de [!DNL XDM Individual Profile] -klasse.

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

De antwoordindeling is afhankelijk van de header `Accept` die in de aanvraag wordt verzonden. De volgende `Accept` kopteksten zijn beschikbaar voor aanbiedingsschema&#39;s:

| `Accept` header | Beschrijving |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | Retourneert een korte samenvatting van elke bron. Dit is de aanbevolen koptekst voor aanbiedingsbronnen. (Limiet: 300) |
| `application/vnd.adobe.xed+json` | Retourneert het volledige JSON-schema voor elke bron, met origineel `$ref` en `allOf` inbegrepen. (Limiet: 300) |

{style="table-layout:auto"}

**Reactie**

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
