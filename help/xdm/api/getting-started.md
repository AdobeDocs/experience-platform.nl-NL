---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Beleidsgegevensmodel;Gegevensmodel;Gegevensmodel;Schema register;Schemaregister
solution: Experience Platform
title: Aan de slag met de API voor schemaregistratie
description: Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Registratie API van het Schema te maken.
topic-legacy: developer guide
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: a26c8d43ff7874bcedd2adb3d6da995986198c96
workflow-type: tm+mt
source-wordcount: '1342'
ht-degree: 0%

---

# Aan de slag met de [!DNL Schema Registry] API

De [!DNL Schema Registry] Met API kunt u verschillende XDM-bronnen (Experience Data Model) maken en beheren. Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen vraag aan te maken [!DNL Schema Registry] API.

## Vereisten

Voor het gebruik van de handleiding voor ontwikkelaars is een goed begrip van de volgende onderdelen van Adobe Experience Platform vereist:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele partitie maken [!DNL Platform] in afzonderlijke virtuele omgevingen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Daarom wordt u ten zeerste aangeraden de [Officiële JSON-schemadocumentatie](https://json-schema.org/) voor een beter inzicht in deze onderliggende technologie.

## API-voorbeeldaanroepen lezen

De [!DNL Schema Registry] API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de gids voor het oplossen van problemen met Experience Platforms.

## Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], met inbegrip van die welke tot de [!DNL Schema Registry], geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [sandbox-documentatie](../../sandboxes/home.md).

Alle opzoekverzoeken (GET) aan de [!DNL Schema Registry] aanvullende `Accept` header, wiens waarde de indeling van de informatie bepaalt die door de API wordt geretourneerd. Zie de [Koptekst accepteren](#accept) voor meer informatie hieronder.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Weet uw TENANT_ID {#know-your-tenant_id}

In de API-hulplijnen worden verwijzingen naar een `TENANT_ID`. Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. Als u uw id niet kent, kunt u deze openen door de volgende GET-aanvraag uit te voeren:

**API-indeling**

```http
GET /stats
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert informatie betreffende het gebruik van uw organisatie van terug [!DNL Schema Registry]. Dit omvat een `tenantId` attribuut, waarvan de waarde uw is `TENANT_ID`.

```JSON
{
  "imsOrg":"{IMS_ORG}",
  "tenantId":"{TENANT_ID}",
  "counts": {
    "schemas": 4,
    "mixins": 3,
    "datatypes": 1,
    "classes": 2,
    "unions": 0,
  },
  "recentlyCreatedResources": [ 
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:created": "Sat Feb 02 2019 00:24:30 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "$id": "https://ns.adobe.com/{TENANT_ID}/classes/5bdb5582be0c0f3ebfc1c603b705764f",
      "title": "Tenant Class",
      "description": "Tenant Defined Class",
      "meta:resourceType": "classes",
      "meta:created": "Fri Feb 01 2019 22:46:21 GMT+0000 (UTC)",
      "version": "1.0"
    } 
  ],
  "recentlyUpdatedResources": [
    {
      "title": "Sample Field Group",
      "description": "New Sample Field Group.",
      "meta:resourceType": "mixins",
      "meta:updated": "Sat Feb 02 2019 00:34:06 GMT+0000 (UTC)",
      "version": "1.1"
    },
    {
      "title": "Data Schema",
      "description": "Schema for Data Information",
      "meta:resourceType": "schemas",
      "meta:updated": "Fri Feb 01 2019 23:47:43 GMT+0000 (UTC)",
      "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab",
      "meta:classTitle": "Sample Class",
      "version": "1.1"
    }
 ],
 "classUsage": {
    "https://ns.adobe.com/{TENANT_ID}/classes/47b2189fc135e03c844b4f25139d10ab": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
        "title": "Tenant Data Schema",
        "description": "Schema for tenant-specific data."
      }
    ],
    "https://ns.adobe.com/xdm/context/profile": [
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/3ac6499f0a43618bba6b138226ae3542",
        "title": "Simple Profile",
        "description": "A simple profile schema."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
        "title": "Program Schema",
        "description": "Schema for program-related data."
      },
      {
        "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/4025a705890c6d4a4a06b16f8cf6f4ca",
        "title": "Sample Schema",
        "description": "A sample schema."
      }
    ]
  }
 }
```

## Begrijp het `CONTAINER_ID` {#container}

verzoekt de [!DNL Schema Registry] API vereist het gebruik van een `CONTAINER_ID`. Er zijn twee containers waartegen API-aanroepen kunnen worden uitgevoerd: de `global` en de `tenant` container.

### Algemene container

De `global` houder bevat alle standaard Adobe en [!DNL Experience Platform] de partner verstrekte klassen, de groepen van het schemagebied, gegevenstypes, en schema&#39;s. U kunt lijst en raadpleging (GET) verzoeken tegen slechts uitvoeren `global` container.

Een voorbeeld van een vraag die gebruikt `global` de container ziet er als volgt uit:

```http
GET /global/classes
```

### Trekcontainer

Niet verward met je unieke `TENANT_ID`de `tenant` container bevat alle klassen, veldgroepen, gegevenstypen, schema&#39;s en descriptoren die zijn gedefinieerd door een IMS-organisatie. Deze zijn uniek voor elke organisatie, die betekent zij niet zichtbaar of handelbaar door andere IMS Orgs zijn. U kunt alle CRUD-bewerkingen (GET, POST, PUT, PATCH, DELETE) uitvoeren tegen bronnen die u maakt in het dialoogvenster `tenant` container.

Een voorbeeld van een vraag die gebruikt `tenant` de container ziet er als volgt uit:

```http
POST /tenant/fieldgroups
```

Wanneer u een klasse, veldgroep, schema of gegevenstype maakt in het dialoogvenster `tenant` container, wordt het opgeslagen in de [!DNL Schema Registry] en een `$id` URI die uw `TENANT_ID`. Dit `$id` wordt in de gehele API gebruikt om naar specifieke bronnen te verwijzen. Voorbeelden van `$id` waarden worden gegeven in de volgende sectie.

## Bronidentificatie {#resource-identification}

XDM-bronnen worden geïdentificeerd met een `$id` attribuut in de vorm van URI, zoals de volgende voorbeelden:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Om URI meer REST-vriendelijk te maken, hebben de schema&#39;s ook een punt-aantekening codering van URI in een genoemd bezit `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

verzoekt de [!DNL Schema Registry] API ondersteunt de URL-codering `$id` URI of de `meta:altId` (puntnotatie). U kunt het beste de URL-codering gebruiken `$id` URI wanneer het maken van een REST vraag aan API, als zo:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Koptekst accepteren {#accept}

Wanneer u lijst- en opzoekbewerkingen (GET) uitvoert in het dialoogvenster [!DNL Schema Registry] API, en `Accept` header is vereist om de indeling van de gegevens te bepalen die door de API worden geretourneerd. Wanneer u specifieke bronnen opzoekt, moet u ook een versienummer opnemen in het dialoogvenster `Accept` header.

De volgende tabel bevat compatibele `Accept` headerwaarden, inclusief waarden met versienummers, samen met beschrijvingen van wat de API retourneert wanneer deze worden gebruikt.

| Accepteren | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retourneert alleen een lijst met id&#39;s. Dit wordt meestal gebruikt voor het aanbieden van resources. |
| `application/vnd.adobe.xed+json` | Retourneert een lijst met volledige JSON-schema met origineel `$ref` en `allOf` opgenomen. Dit wordt gebruikt om een lijst van volledige middelen terug te keren. |
| `application/vnd.adobe.xed+json; version=1` | Onbewerkte XDM met `$ref` en `allOf`. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` kenmerken en `allOf` opgelost. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Onbewerkte XDM met `$ref` en `allOf`. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` kenmerken en `allOf` opgelost. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` kenmerken en `allOf` opgelost. Beschrijvers worden opgenomen. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Platform ondersteunt momenteel slechts één hoofdversie voor elk schema (`1`). De waarde voor `version` moet altijd `1` wanneer het uitvoeren van raadplegingsverzoeken om de recentste minder belangrijke versie van het schema terug te keren. Zie de subsectie hieronder voor meer informatie over schemaversie.

### Schema versioning {#versioning}

Er wordt naar schemaversies verwezen door `Accept` headers in de Schema Registry API en in `schemaRef.contentType` eigenschappen in downstream Platform service-API-ladingen.

Platform ondersteunt momenteel slechts één hoofdversie (`1`) voor elk schema. Volgens de [regels voor schemaontwikkeling](../schema/composition.md#evolution), moet elke update van een schema niet-destructief zijn, wat betekent dat nieuwe kleine versies van een schema (`1.2`, `1.3`, enz.) zijn altijd achterwaarts compatibel met eerdere secundaire versies. Daarom bij het specificeren van `version=1`, retourneert het Schemaregister altijd de **nieuwste** hoofdversie `1` van een schema, wat betekent dat vorige secundaire versies niet worden geretourneerd.

>[!NOTE]
>
>Het niet-destructieve vereiste voor schemaevolutie wordt slechts afgedwongen nadat het schema door een dataset van verwijzingen is voorzien en één van de volgende gevallen waar is:
>
>* De gegevens zijn opgenomen in de dataset.
>* De dataset is toegelaten voor gebruik in het Profiel van de Klant in real time (zelfs als geen gegevens is opgenomen).
>
>Als het schema niet aan een dataset is geassocieerd die aan één van bovengenoemde criteria voldoet, dan kan om het even welke verandering worden aangebracht. In alle gevallen echter `version` nog steeds component aanwezig `1`.

## Beperkingen en aanbevolen procedures voor XDM-velden

De velden van een schema worden weergegeven binnen het schema `properties` object. Elk veld is zelf een object dat kenmerken bevat voor het beschrijven en beperken van de gegevens die het veld kan bevatten. Raadpleeg de handleiding op [aangepaste velden in de API definiëren](../tutorials/custom-fields-api.md) voor codesteekproeven en facultatieve beperkingen voor de meest algemeen gebruikte gegevenstypes.

In het volgende voorbeeldveld wordt een correct opgemaakt XDM-veld weergegeven met nadere informatie over de naamgevingsbeperkingen en de onderstaande aanbevolen procedures. Deze praktijken kunnen ook worden toegepast wanneer het bepalen van andere middelen die gelijkaardige attributen bevatten.

```JSON
"fieldName": {
    "title": "Field Name",
    "type": "string",
    "format": "date-time",
    "examples": [
        "2004-10-23T12:00:00-06:00"
    ],
    "description": "Full sentence describing the field, using proper grammar and punctuation.",
}
```

* De naam van een veldobject mag alfanumerieke tekens, streepjestekens of onderstrepingstekens bevatten, maar **mag** begint met een onderstrepingsteken.
   * **Juist:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Onjuist:** `_fieldName`
* kamelCase heeft de voorkeur voor de naam van het veldobject. Voorbeeld: `fieldName`
* Het veld moet een `title`, geschreven in geval van titel. Voorbeeld: `Field Name`
* Voor het veld is een `type`.
   * Voor het definiëren van bepaalde typen is mogelijk een optionele `format`.
   * Wanneer een specifieke opmaak van gegevens vereist is, `examples` kan als een array worden toegevoegd.
   * Het veldtype kan ook worden gedefinieerd aan de hand van elk gegevenstype in het register. Zie de sectie over [een gegevenstype maken](./data-types.md#create) in de gids van het gegevenstypeseindpunt voor meer informatie.
* De `description` geeft uitleg over het veld en relevante informatie over veldgegevens. Het zou in volledige zinnen met duidelijke taal moeten worden geschreven zodat iedereen die tot het schema toegang heeft de intentie van het gebied kan begrijpen.

## Volgende stappen

Beginnen het maken vraag gebruikend [!DNL Schema Registry] API, selecteert u een van de beschikbare eindpunthulplijnen.
