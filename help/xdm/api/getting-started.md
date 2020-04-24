---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Handleiding voor ontwikkelaars van de API voor schemaregister
topic: developer guide
translation-type: tm+mt
source-git-commit: 387cbdebccb9ae54a2907d1afe220e9711927ca6

---


# Handleiding voor ontwikkelaars van de API voor schemaregister

Het Schemaregister wordt gebruikt om toegang te krijgen tot de Schemabibliotheek binnen het Adobe Experience Platform en biedt een gebruikersinterface en RESTful-API waaruit alle beschikbare bibliotheekbronnen toegankelijk zijn.

Met de API voor het registreren van het schema kunt u standaard CRUD-bewerkingen uitvoeren om alle schema&#39;s en gerelateerde bronnen die u binnen het Adobe Experience Platform hebt, weer te geven en te beheren. Hieronder vallen de gedefinieerde toepassingen van Adobe, Experience Platform-partners en leveranciers van wie u de toepassingen gebruikt. U kunt ook API-aanroepen gebruiken om nieuwe schema&#39;s en bronnen voor uw organisatie te maken, en bronnen die u al hebt gedefinieerd, weer te geven en te bewerken.

Deze ontwikkelaarsgids verstrekt stappen helpen u beginnen te gebruiken de Registratie API van het Schema. De gids verstrekt dan steekproefAPI vraag voor het uitvoeren van zeer belangrijke verrichtingen gebruikend de Registratie van het Schema.

## Vereisten

Voor deze handleiding is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

* [XDM-systeem](../home.md)(Experience Data Model): Het gestandaardiseerde kader waardoor het Platform van de Ervaring gegevens van de klantenervaring organiseert.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [Klantprofiel](../../profile/home.md)in realtime: Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [Sandboxen](../../sandboxes/home.md): Het ervaringsplatform biedt virtuele sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan de Registratie API van het Schema te maken.

## API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

* Autorisatie: Drager `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform, inclusief die welke tot het schemaregister behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle opzoekverzoeken (GET) aan de Registratie van het Schema vereisen extra Accept kopbal, de waarvan waarde de formaat van informatie bepaalt die door API is teruggekeerd. Zie de koptekstsectie [Accepteren](#accept) hieronder voor meer informatie.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* Inhoudstype: application/json

## Weet uw TENANT_ID {#know-your-tenant_id}

In deze handleiding ziet u verwijzingen naar een `TENANT_ID`. Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. Als u uw id niet kent, kunt u deze openen door het volgende GET verzoek uit te voeren:

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

Een succesvolle reactie keert informatie betreffende het gebruik van uw organisatie van de Registratie van het Schema terug. Dit omvat een `tenantId` attribuut, waarvan de waarde uw `TENANT_ID`.

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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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
      "title": "Sample Mixin",
      "description": "New Sample Mixin.",
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

* `tenantId`: De `TENANT_ID` waarde voor uw IMS-organisatie.

## Begrijp het `CONTAINER_ID`{#container}

De vraag aan de Registratie API van het Schema vereist het gebruik van een `CONTAINER_ID`. Er zijn twee containers waartegen API-aanroepen kunnen worden uitgevoerd: de **globale container** en de **huurderscontainer**.

### Algemene container

De globale container bevat alle standaard door Adobe en Experience Platform geleverde klassen, mixins, gegevenstypen en schema&#39;s. U kunt lijst en raadplegingsverzoeken (GET) slechts tegen de globale container uitvoeren.

### Trekcontainer

Om niet met uw uniek te worden verward `TENANT_ID`, houdt de huurderscontainer alle klassen, mixins, gegevenstypes, schema&#39;s, en beschrijvers die door een IMS Organisatie worden bepaald. Deze zijn uniek voor elke organisatie, die betekent zij niet zichtbaar of handelbaar door andere IMS Orgs zijn. U kunt alle CRUD-bewerkingen (GET, POST, PUT, PATCH, DELETE) uitvoeren op bronnen die u maakt in de huurderscontainer.

Wanneer u een klasse, een mixin, een schema of een gegevenstype in de huurderscontainer creeert, wordt het bewaard aan de Registratie van het Schema en toegewezen `$id` URI die uw `TENANT_ID`omvat. Dit `$id` wordt in de gehele API gebruikt om naar specifieke bronnen te verwijzen. In de volgende sectie worden voorbeelden van `$id` waarden gegeven.

## Schema-identificatie {#schema-identification}

Schema&#39;s worden geïdentificeerd met een `$id` kenmerk in de vorm van een URI, zoals:
* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Om URI meer REST-vriendelijk te maken, hebben de schema&#39;s ook een punt-aantekening het coderen van URI in een genoemd bezit `meta:altId`:
* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Oproepen aan de Registratie API van het Schema zullen of URL-Gecodeerde `$id` URI of het `meta:altId` (punt-aantekening formaat) steunen. De beste manier is om de URL-gecodeerde `$id` URI te gebruiken bij het maken van een REST-aanroep naar de API, zoals:
* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Koptekst accepteren {#accept}

Wanneer het uitvoeren van lijst en raadplegings (KRIJG) verrichtingen in de Registratie API van het Schema, wordt een Accept kopbal vereist om het formaat van de gegevens te bepalen die door API zijn teruggekeerd. Wanneer het omhoog zoeken van specifieke middelen, moet een versieaantal ook in de Accept kopbal worden omvat.

In de volgende tabel vindt u compatibele Accept-headerwaarden, inclusief waarden met versienummers, en een beschrijving van wat de API retourneert wanneer deze worden gebruikt.

| Accepteren | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retourneert alleen een lijst met id&#39;s. Dit wordt meestal gebruikt voor het aanbieden van resources. |
| `application/vnd.adobe.xed+json` | Retourneert een lijst met volledige JSON-schema met origineel `$ref` en `allOf` opgenomen. Dit wordt gebruikt om een lijst van volledige middelen terug te keren. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Onbewerkte XDM met `$ref` en `allOf`. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` kenmerken en `allOf` opgelost. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Onbewerkte XDM met `$ref` en `allOf`. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` kenmerken en `allOf` opgelost. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` kenmerken en `allOf` opgelost. Beschrijvers worden opgenomen. |

>[!NOTE] Indien alleen de `major` versie wordt geleverd (bv. 1, 2, 3), retourneert het register de laatste `minor` versie (bv. .1, .2, .3) automatisch.

## Beperkingen en aanbevolen procedures voor XDM-velden

De velden van een schema worden vermeld in het bijbehorende `properties` object. Elk veld is zelf een object dat kenmerken bevat voor het beschrijven en beperken van de gegevens die het veld kan bevatten.

Meer informatie over het definiëren van veldtypen in de API vindt u in de [bijlage](appendix.md) voor deze handleiding, inclusief codevoorbeelden en optionele beperkingen voor de meest gebruikte gegevenstypen.

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

* De naam van een veldobject mag alfanumerieke tekens, streepjes of onderstrepingstekens bevatten, maar **mag niet** beginnen met een onderstrepingsteken.
   * **Juist:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Onjuist:** `_fieldName`
* kamelCase heeft de voorkeur voor de naam van het veldobject. Voorbeeld: `fieldName`
* Het veld moet een `title`, geschreven in het hoofdlettergebruik bevatten. Voorbeeld: `Field Name`
* Het veld vereist een `type`.
   * Voor het definiëren van bepaalde typen is mogelijk een optioneel type vereist `format`.
   * Wanneer een specifieke opmaak van gegevens vereist is, `examples` kan deze als een array worden toegevoegd.
   * Het veldtype kan ook worden gedefinieerd aan de hand van elk gegevenstype in het register. Zie de sectie over het [maken van een gegevenstype](create-data-type.md) in deze handleiding voor meer informatie.
* In dit hoofdstuk worden het veld en relevante informatie over veldgegevens `description` uitgelegd. Het zou in volledige zinnen met duidelijke taal moeten worden geschreven zodat iedereen die tot het schema toegang heeft de intentie van het gebied kan begrijpen.

Zie de [bijlage](appendix.md) voor meer informatie over het definiëren van veldtypen in de API.

## Volgende stappen

Dit document behandelde de vereiste kennis die wordt vereist om vraag aan de Registratie API van het Schema, met inbegrip van vereiste authentificatiegeloofsbrieven te maken. U kunt nu aan de steekproefvraag verdergaan die in deze ontwikkelaarsgids wordt verstrekt en samen met hun instructies volgen. Voor een volledige geleidelijke analyse van hoe te om een schema in API te maken, gelieve te verwijzen naar het volgende [leerprogramma](../tutorials/create-schema-api.md).
