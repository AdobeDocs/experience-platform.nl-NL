---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Aan de slag met de API voor het schemaregister
description: Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Registratie API van het Schema te maken.
topic: developer guide
translation-type: tm+mt
source-git-commit: b79482635d87efd5b79cf4df781fc0a3a6eb1b56
workflow-type: tm+mt
source-wordcount: '1132'
ht-degree: 0%

---


# Getting started with the [!DNL Schema Registry] API

Met de [!DNL Schema Registry] API kunt u verschillende XDM-bronnen (Experience Data Model) maken en beheren. Dit document biedt een inleiding tot de kernconcepten u moet kennen alvorens te proberen om vraag aan [!DNL Schema Registry] API te maken.

## Vereisten

Voor het gebruik van de handleiding voor ontwikkelaars is een goed begrip van de volgende onderdelen van Adobe Experience Platform vereist:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Het gestandaardiseerde kader waardoor de gegevens van de klantenervaring worden [!DNL Experience Platform] georganiseerd.
   * [Basisbeginselen van de schemacompositie](../schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Verstrekt een verenigd, real-time consumentenprofiel dat op bijeengevoegde gegevens van veelvoudige bronnen wordt gebaseerd.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één enkele [!DNL Platform] instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Daarom wordt u ten zeerste aangeraden de [officiële JSON-schemadocumentatie](https://json-schema.org/) te herzien voor een beter inzicht in deze onderliggende technologie.

## API-voorbeeldaanroepen lezen

De API-documentatie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. [!DNL Schema Registry] Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeldAPI vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen

Als u aanroepen wilt uitvoeren naar [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](../../tutorials/authentication.md)voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen, zoals hieronder wordt getoond: [!DNL Experience Platform]

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Schema Registry]sandboxen behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie bij de [!DNL Platform]sandbox voor meer informatie over de sandboxen in [de](../../sandboxes/home.md)sandbox.

Alle opzoekverzoeken (GET) aan de gebruiker [!DNL Schema Registry] vereisen een extra `Accept` koptekst, waarvan de waarde de indeling van de informatie bepaalt die door de API wordt geretourneerd. Zie de koptekstsectie [Accepteren](#accept) hieronder voor meer informatie.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Weet uw TENANT_ID {#know-your-tenant_id}

In de API-hulplijnen worden verwijzingen naar een `TENANT_ID`voorbeeld weergegeven. Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich in uw IMS-organisatie bevinden. Als u uw id niet kent, kunt u deze openen door de volgende GET-aanvraag uit te voeren:

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

Een succesvolle reactie keert informatie betreffende het gebruik van uw organisatie van terug [!DNL Schema Registry]. Dit omvat een `tenantId` attribuut, waarvan de waarde uw `TENANT_ID`.

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

## Begrijp het `CONTAINER_ID` {#container}

Oproepen aan [!DNL Schema Registry] API vereisen het gebruik van een `CONTAINER_ID`. Er zijn twee containers waartegen API-aanroepen kunnen worden uitgevoerd: de `global` container en de `tenant` container.

### Algemene container

De `global` container houdt alle standaard Adobe en [!DNL Experience Platform] partner verstrekte klassen, mixins, gegevenstypes, en schema&#39;s. U kunt lijst en raadplegings (GET) verzoeken tegen de `global` container slechts uitvoeren.

Een voorbeeld van een vraag die de `global` container gebruikt zou als het volgende kijken:

```http
GET /global/classes
```

### Trekcontainer

Om niet met uw uniek te worden verward, houdt de `TENANT_ID``tenant` container alle klassen, mixins, gegevenstypes, schema&#39;s, en beschrijvers die door een organisatie IMS worden bepaald. Deze zijn uniek voor elke organisatie, die betekent zij niet zichtbaar of handelbaar door andere IMS Orgs zijn. U kunt alle CRUD verrichtingen (GET, POST, PUT, PATCH, DELETE) tegen middelen uitvoeren die u in de `tenant` container creeert.

Een voorbeeld van een vraag die de `tenant` container gebruikt zou als het volgende kijken:

```http
POST /tenant/mixins
```

Wanneer u een klasse, een combinatie, een schema of een gegevenstype in de `tenant` container creeert, wordt het bewaard aan [!DNL Schema Registry] en toegewezen `$id` URI die uw `TENANT_ID`. omvat. Dit `$id` wordt in de gehele API gebruikt om naar specifieke bronnen te verwijzen. De voorbeelden van `$id` waarden worden verstrekt in de volgende sectie.

## Bronidentificatie {#resource-identification}

XDM-bronnen worden aangeduid met een `$id` attribuut in de vorm van een URI, zoals de volgende voorbeelden:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Om URI meer REST-vriendelijk te maken, hebben de schema&#39;s ook een punt-aantekening het coderen van URI in een genoemd bezit `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Aanroepen naar de [!DNL Schema Registry] API ondersteunen de URL-gecodeerde `$id` URI of de `meta:altId` (puntnotatie). De beste manier is om de URL-gecodeerde `$id` URI te gebruiken bij het maken van een REST-aanroep naar de API, zoals:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Koptekst accepteren {#accept}

Bij het uitvoeren van lijst- en opzoekbewerkingen (GET) in de [!DNL Schema Registry] API is een `Accept` header vereist om de indeling te bepalen van de gegevens die door de API worden geretourneerd. Wanneer u specifieke bronnen opzoekt, moet ook een versienummer in de `Accept` koptekst worden opgenomen.

De volgende tabel bevat compatibele `Accept` koptekstwaarden, waaronder waarden met versienummers, en beschrijvingen van wat de API retourneert wanneer deze worden gebruikt.

| Accepteren | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retourneert alleen een lijst met id&#39;s. Dit wordt meestal gebruikt voor het aanbieden van resources. |
| `application/vnd.adobe.xed+json` | Retourneert een lijst met volledige JSON-schema met origineel `$ref` en `allOf` opgenomen. Dit wordt gebruikt om een lijst van volledige middelen terug te keren. |
| `application/vnd.adobe.xed+json; version={MAJOR_VERSION}` | Onbewerkte XDM met `$ref` en `allOf`. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version={MAJOR_VERSION}` | `$ref` kenmerken en `allOf` opgelost. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version={MAJOR_VERSION}` | Onbewerkte XDM met `$ref` en `allOf`. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version={MAJOR_VERSION}` | `$ref` kenmerken en `allOf` opgelost. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version={MAJOR_VERSION}` | `$ref` kenmerken en `allOf` opgelost. Beschrijvers worden opgenomen. |

>[!NOTE]
>
>Indien alleen de hoofdversie wordt geleverd (bv. 1, 2, 3), retourneert het register de laatste secundaire versie (bv. .1, .2, .3) automatisch.

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
   * Het veldtype kan ook worden gedefinieerd aan de hand van elk gegevenstype in het register. Zie de sectie over het [creëren van een gegevenstype](./data-types.md#create) in de gids van het gegevenstypeseindpunt voor meer informatie.
* In dit hoofdstuk worden het veld en relevante informatie over veldgegevens `description` uitgelegd. Het zou in volledige zinnen met duidelijke taal moeten worden geschreven zodat iedereen die tot het schema toegang heeft de intentie van het gebied kan begrijpen.

Zie het document over [gebiedsbeperkingen](../schema/field-constraints.md) voor meer informatie over hoe te om verschillende gebiedstypes in API te bepalen.

## Volgende stappen

Om beginnen het maken vraag gebruikend [!DNL Schema Registry] API, selecteer één van de beschikbare eindpuntgidsen.
