---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Beleidsgegevensmodel;Gegevensmodel;Gegevensmodel;Schema register;Schemaregister
solution: Experience Platform
title: Aan de slag met de API voor schemaregistratie
description: Dit document verstrekt een inleiding aan de kernconcepten u moet kennen alvorens te proberen om vraag aan de Registratie API van het Schema te maken.
exl-id: 7daebb7d-72d2-4967-b4f7-1886736db69f
source-git-commit: eb1cf204e95591082b27dc97cd3c709a23b20b08
workflow-type: tm+mt
source-wordcount: '1361'
ht-degree: 0%

---

# Aan de slag met de [!DNL Schema Registry] API

Met de API van [!DNL Schema Registry] kunt u verschillende XDM-bronnen (Experience Data Model) maken en beheren. Dit document bevat een inleiding op de kernconcepten die u moet kennen voordat u de API van [!DNL Schema Registry] aanroept.

## Vereisten

Voor het gebruik van de handleiding voor ontwikkelaars is een goed begrip van de volgende onderdelen van Adobe Experience Platform vereist:

* [[!DNL Experience Data Model (XDM) System]](../home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.
   * [ Grondbeginselen van schemacompositie ](../schema/composition.md): Leer over de basisbouwstenen van schema&#39;s XDM.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): biedt een uniform, real-time consumentenprofiel dat is gebaseerd op geaggregeerde gegevens van meerdere bronnen.
* [[!DNL Sandboxes]](../../sandboxes/home.md): [!DNL Experience Platform] biedt virtuele sandboxen die één [!DNL Platform] -instantie in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Daarom wordt sterk geadviseerd dat u de [ officiële documentatie van het Schema JSON ](https://json-schema.org/) voor een beter inzicht in deze onderliggende technologie herziet.

## API-voorbeeldaanroepen lezen

De API-documentatie van [!DNL Schema Registry] biedt voorbeeld-API-aanroepen om aan te tonen hoe uw aanvragen moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Experience Platform te lezen.

## Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Alle bronnen in [!DNL Experience Platform], inclusief de bronnen die tot de [!DNL Schema Registry] behoren, zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

* `x-sandbox-name: {SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Platform], zie de [ zandbakdocumentatie ](../../sandboxes/home.md).

Voor alle opzoekverzoeken (GET) naar de [!DNL Schema Registry] is een extra `Accept` -header nodig, waarvan de waarde de indeling van de informatie bepaalt die door de API wordt geretourneerd. Zie [ kopbal ](#accept) hieronder sectie goedkeuren voor meer details.

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

* `Content-Type: application/json`

## Weet uw TENANT_ID {#know-your-tenant_id}

In de API-hulplijnen worden verwijzingen naar een `TENANT_ID` weergegeven. Deze id wordt gebruikt om ervoor te zorgen dat bronnen die u maakt, op de juiste wijze worden benoemd en zich binnen uw organisatie bevinden. Als u uw id niet kent, kunt u deze openen door de volgende GET-aanvraag uit te voeren:

**API formaat**

```http
GET /stats
```

**Verzoek**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/stats \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie geeft informatie over het gebruik van [!DNL Schema Registry] door uw organisatie. Dit omvat een `tenantId` -kenmerk, waarvan de waarde uw `TENANT_ID` is.

```JSON
{
  "imsOrg":"{ORG_ID}",
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

## Begrijp `CONTAINER_ID` {#container}

Oproepen aan de [!DNL Schema Registry] API vereisen het gebruik van `CONTAINER_ID`. Er zijn twee containers waartegen API-aanroepen kunnen worden uitgevoerd: de container `global` en de container `tenant` .

### Algemene container

De container `global` bevat alle standaard Adobe en door [!DNL Experience Platform] verschafte klassen, groepen met schemavelden, gegevenstypen en schema&#39;s. U kunt alleen lijst- en opzoekverzoeken (GET) uitvoeren in de `global` -container.

Een voorbeeld van een aanroep die de container `global` gebruikt, ziet er als volgt uit:

```http
GET /global/classes
```

### Trekcontainer

De `tenant` -container bevat alle klassen, veldgroepen, gegevenstypen, schema&#39;s en beschrijvingen die door een organisatie zijn gedefinieerd, zodat deze niet worden verward met uw unieke `TENANT_ID` -container. Deze zijn uniek voor elke organisatie, die betekent zij niet zichtbaar of handelbaar door andere organisaties zijn. U kunt alle CRUD-bewerkingen (GET, POST, PUT, PATCH, DELETE) uitvoeren tegen bronnen die u maakt in de `tenant` -container.

Een voorbeeld van een aanroep die de container `tenant` gebruikt, ziet er als volgt uit:

```http
POST /tenant/fieldgroups
```

Wanneer u een klasse, veldgroep, schema of gegevenstype maakt in de `tenant` -container, wordt deze opgeslagen in de [!DNL Schema Registry] en toegewezen aan een `$id` -URI die de `TENANT_ID` -container bevat. Deze `$id` wordt in de gehele API gebruikt om naar specifieke bronnen te verwijzen. In de volgende sectie vindt u voorbeelden van `$id` -waarden.

## Bronidentificatie {#resource-identification}

XDM-bronnen worden geïdentificeerd met een `$id` -kenmerk in de vorm van een URI, zoals de volgende voorbeelden:

* `https://ns.adobe.com/xdm/context/profile`
* `https://ns.adobe.com/{TENANT_ID}/schemas/7442343-abs2343-21232421`

Om de URI REST-vriendelijker te maken, hebben schema&#39;s ook een punt-aantekening het coderen van URI in een bezit genoemd `meta:altId`:

* `_xdm.context.profile`
* `_{TENANT_ID}.schemas.7442343-abs2343-21232421`

Oproepen aan de [!DNL Schema Registry] API zullen of URL-Gecodeerde `$id` URI of `meta:altId` (punt-aantekening formaat) steunen. De beste manier is om de URL-gecodeerde `$id` URI te gebruiken wanneer u een REST-aanroep naar de API uitvoert, zoals:

* `https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile`
* `https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F7442343-abs2343-21232421`

## Koptekst accepteren {#accept}

Wanneer u lijst- en opzoekbewerkingen (GET) uitvoert in de [!DNL Schema Registry] API, is een `Accept` -header vereist om de indeling te bepalen van de gegevens die door de API worden geretourneerd. Wanneer u specifieke bronnen opzoekt, moet ook een versienummer in de `Accept` -header worden opgenomen.

De volgende tabel bevat een lijst met compatibele `Accept` headerwaarden, inclusief waarden met versienummers, en beschrijvingen van wat de API retourneert wanneer deze worden gebruikt.

| Accepteren | Beschrijving |
| ------- | ------------ |
| `application/vnd.adobe.xed-id+json` | Retourneert alleen een lijst met id&#39;s. Dit wordt het meest gebruikt voor het aanbieden van middelen. |
| `application/vnd.adobe.xed+json` | Retourneert een lijst met volledige JSON-schema met origineel `$ref` en `allOf` opgenomen. Dit wordt gebruikt om een lijst van volledige middelen terug te keren. |
| `application/vnd.adobe.xed+json; version=1` | Onbewerkte XDM met `$ref` en `allOf` . Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` -kenmerken en `allOf` opgelost. Bevat titels en beschrijvingen. |
| `application/vnd.adobe.xed-notext+json; version=1` | Onbewerkte XDM met `$ref` en `allOf` . Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-notext+json; version=1` | `$ref` -kenmerken en `allOf` opgelost. Geen titels of beschrijvingen. |
| `application/vnd.adobe.xed-full-desc+json; version=1` | `$ref` -kenmerken en `allOf` opgelost. Beschrijvers worden opgenomen. |
| `application/vnd.adobe.xed-deprecatefield+json; version=1` | `$ref` en `allOf` resolve, heeft titels en beschrijvingen. Vervangen velden worden aangegeven met een `meta:status` -kenmerk van `deprecated` . |

{style="table-layout:auto"}

>[!NOTE]
>
>Platform steunt momenteel slechts één belangrijke versie voor elk schema (`1`). Daarom moet de waarde voor `version` altijd `1` zijn wanneer het uitvoeren van raadplegingsverzoeken om de recentste minder belangrijke versie van het schema terug te keren. Zie de subsectie hieronder voor meer informatie over schemaversie.

### Schema versioning {#versioning}

In schemaversies wordt verwezen door `Accept` headers in de Schema Registry API en in `schemaRef.contentType` -eigenschappen in downstream Platform service API-payloads.

Momenteel, steunt het Platform slechts één enkele belangrijkste versie (`1`) voor elk schema. Volgens de [ regels van schemaevolutie ](../schema/composition.md#evolution), moet elke update aan een schema niet-destructief zijn, betekenend dat nieuwe minder belangrijke versies van een schema (`1.2`, `1.3`, enz.) zijn altijd achterwaarts compatibel met eerdere secundaire versies. Daarom wanneer het specificeren van `version=1`, keert de Registratie van het Schema altijd de **recentste** belangrijkste versie `1` van een schema terug, betekenend dat de vorige minder belangrijke versies niet zijn teruggekeerd.

>[!NOTE]
>
>Het niet-destructieve vereiste voor schemaevolutie wordt slechts afgedwongen nadat het schema door een dataset van verwijzingen is voorzien en één van de volgende gevallen waar is:
>
>* De gegevens zijn opgenomen in de dataset.
>* De dataset is toegelaten voor gebruik in het Profiel van de Klant in real time (zelfs als geen gegevens is opgenomen).
>
>Als het schema niet aan een dataset is geassocieerd die aan één van bovengenoemde criteria voldoet, dan kan om het even welke verandering worden aangebracht. In alle gevallen blijft de component `version` echter op `1` staan.

## Beperkingen en aanbevolen procedures voor XDM-velden

De velden van een schema worden vermeld in het bijbehorende `properties` -object. Elk veld is zelf een object dat kenmerken bevat voor het beschrijven en beperken van de gegevens die het veld kan bevatten. Verwijs naar de gids op [ bepalend douanegebieden in API ](../tutorials/custom-fields-api.md) voor codesteekproeven en facultatieve beperkingen voor de het meest algemeen gebruikte gegevenstypes.

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

* De naam van een veldobject kan alfanumerieke, streepje- of onderstrepingstekens bevatten, maar **kan** niet met een onderstrepingsteken beginnen.
   * **Correct:** `fieldName`, `field_name2`, `Field-Name`, `field-name_3`
   * **Onjuist:** `_fieldName`
* Veldnamen zijn niet hoofdlettergevoelig en moeten verschillende namen op hetzelfde niveau in het schema hebben.
* kamelCase heeft de voorkeur voor de naam van het veldobject. Voorbeeld: `fieldName`
* Het veld moet een `title` bevatten, geschreven in Alles Beginhoofdletter. Voorbeeld: `Field Name`
* Voor dit veld is een `type` vereist.
   * Voor het definiëren van bepaalde typen is mogelijk een optionele `format` vereist.
   * Wanneer een specifieke opmaak van gegevens vereist is, kan `examples` als een array worden toegevoegd.
   * Het veldtype kan ook worden gedefinieerd aan de hand van elk gegevenstype in het register. Zie de sectie over [ het creëren van een gegevenstype ](./data-types.md#create) in de gids van het gegevenstypepunteindpunt voor meer informatie.
* In `description` worden het veld en de relevante informatie met betrekking tot veldgegevens uitgelegd. Het zou in volledige zinnen met duidelijke taal moeten worden geschreven zodat iedereen die tot het schema toegang heeft de intentie van het gebied kan begrijpen.

## Volgende stappen

Selecteer een van de beschikbare eindpunthulplijnen als u wilt beginnen met het aanroepen van de API [!DNL Schema Registry] .
