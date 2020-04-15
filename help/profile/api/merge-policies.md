---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Handleiding voor ontwikkelaars van API voor gebruikersprofiel in realtime
topic: guide
translation-type: tm+mt
source-git-commit: 21935bb36d8c2a0ef17e586c0909cf316ef026cf

---


# Beleid samenvoegen

Met het Adobe Experience Platform kunt u gegevens uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stappen voor het werken met samenvoegbeleid met de API. Om met samenvoegbeleid te werken gebruikend UI, gelieve te verwijzen naar de de gebruikersgids [van het](../ui/merge-policies.md)fusiebeleid.

## Aan de slag

De API eindpunten die in deze gids worden gebruikt maken deel uit van Real-time API van het Profiel van de Klant. Lees voordat u verdergaat de handleiding voor ontwikkelaars van de [realtime-API voor klantprofielen](getting-started.md). Met name bevat de sectie [Aan de](getting-started.md#getting-started) slag van de handleiding voor ontwikkelaars van profielen koppelingen naar verwante onderwerpen, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar API&#39;s van het Experience Platform met succes uit te voeren.

## Componenten van samenvoegingsbeleid {#components-of-merge-policies}

Het beleid van de fusie is privé aan uw organisatie IMS, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manier samen te voegen die u nodig hebt. Om het even welke API die tot de gegevens van het Profiel toegang hebben vereist een fusiebeleid, hoewel een gebrek zal worden gebruikt als niet uitdrukkelijk wordt verstrekt. Het platform verstrekt een standaardsamenvoegbeleid, of u kunt een fusiebeleid voor een specifiek schema tot stand brengen en het merken als gebrek voor uw organisatie. Elke organisatie kan veelvoudige samenvoegingsbeleid per schema potentieel hebben, nochtans kan elk schema slechts één standaardsamenvoegbeleid hebben. Om het even welk die samenvoegbeleid als gebrek wordt geplaatst zal worden gebruikt in gevallen waar de schemanaam wordt verstrekt en een fusiebeleid wordt vereist maar niet verstrekt. Wanneer u een samenvoegbeleid als gebrek plaatst, zal om het even welk bestaand samenvoegbeleid dat eerder als gebrek werd geplaatst automatisch worden bijgewerkt om niet meer als gebrek te worden gebruikt.

### Object voor samenvoegbeleid voltooien

Het volledige samenvoegbeleidsobject vertegenwoordigt een set voorkeuren waarmee aspecten van het samenvoegen van profielfragmenten worden beheerd.

**Beleidsobject samenvoegen**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "default": {BOOLEAN},
        "updateEpoch": {UPDATE_TIME}
    }
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | Door het systeem gegenereerde unieke id die tijdens het maken is toegewezen |
| `name` | Vriendelijke naam waarmee het samenvoegbeleid kan worden geïdentificeerd in lijstweergaven. |
| `imsOrgId` | Organisatie-id waartoe dit samenvoegbeleid behoort |
| `identityGraph` | [Object in identiteitsgrafiek](#identity-graph) dat de identiteitsgrafiek aangeeft waarvan gerelateerde identiteiten worden verkregen. Profielfragmenten die voor alle verwante identiteiten worden gevonden, worden samengevoegd. |
| `attributeMerge` | [Kenmerksamenvoegobject](#attribute-merge) dat aangeeft op welke manier in het samenvoegbeleid voorrang wordt gegeven aan profielkenmerkwaarden in het geval van gegevensconflicten. |
| `schema` | Het [schemaobject](#schema) waarop het samenvoegbeleid kan worden gebruikt. |
| `default` | Een Booleaanse waarde die aangeeft of dit samenvoegbeleid de standaardinstelling is voor het opgegeven schema. |
| `version` | Door het platform bijgehouden versie van het samenvoegbeleid. Deze alleen-lezen waarde wordt verhoogd wanneer een samenvoegbeleid wordt bijgewerkt. |
| `updateEpoch` | Datum van de laatste update van het samenvoegbeleid. |

**Voorbeeld van samenvoegingsbeleid**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "timestampOrdered"
        },
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identiteitsgrafiek {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) beheert de identiteitsgrafieken die wereldwijd en voor elke organisatie op Experience Platform worden gebruikt. Het `identityGraph` attribuut van het fusiebeleid bepaalt hoe te om de verwante identiteiten voor een gebruiker te bepalen.

**identityGraph-object**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Waar `{IDENTITY_GRAPH_TYPE}` is een van de volgende:

* **&quot;none&quot;:** Geen identiteitsstitching uitvoeren.
* **&quot;pdg&quot;:** Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek.

**Voorbeeld`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Kenmerk samenvoegen {#attribute-merge}

Een profielfragment is de profielinformatie voor slechts één identiteit uit de lijst van identiteiten die voor een bepaalde gebruiker bestaan. Wanneer het gebruikte grafiektype van de identiteit in meer dan één identiteit resulteert, is er een potentieel voor conflicterende waarden voor profieleigenschappen en de prioriteit moet worden gespecificeerd. Gebruikend `attributeMerge`, kunt u specificeren welke waarden van het datasetprofiel aan voorrang in het geval van een fusieconflict.

**Object attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Waar `{ATTRIBUTE_MERGE_TYPE}` is een van de volgende:

* **&quot;timestampOrdered&quot;**: (standaardwaarde) Geef prioriteit aan het profiel dat als laatste is bijgewerkt in geval van een conflict. Met dit samenvoegtype is het `data` kenmerk niet vereist.
* **&quot;dataSetPrecedence&quot;** : Geef voorrang aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Dit zou kunnen worden gebruikt wanneer de informatie aanwezig in één dataset over gegevens in een andere dataset wordt aangewezen of wordt vertrouwd. Wanneer het gebruiken van dit fusietype, wordt het `order` attribuut vereist, aangezien het van de datasets in de orde van prioriteit een lijst maakt.
   * **&quot;order&quot;**: Wanneer &quot;dataSetPrecedence&quot; wordt gebruikt, moet een `order` array worden voorzien van een lijst met gegevenssets. Gegevenssets die niet in de lijst zijn opgenomen, worden niet samengevoegd. Met andere woorden, gegevenssets moeten expliciet worden vermeld om te worden samengevoegd in een profiel. De `order` array bevat de id&#39;s van de gegevenssets in volgorde van prioriteit.

**Object ExampleMerge met gegevenstype dataSetPrecision**

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order" : [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

**Object ExampleMerge met type timestampOrdered**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Het schemavoorwerp specificeert het schema XDM waarvoor dit fusiebeleid wordt gecreeerd.

**`schema`object **

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Waar de waarde van `name` is de naam van de klasse XDM waarop het schema verbonden aan het fusiebeleid wordt gebaseerd.

**Voorbeeld`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

## Beleid voor samenvoegen openen {#access-merge-policies}

Gebruikend het In real time API van het Profiel van de Klant, staat het `/config/mergePolicies` eindpunt u een raadplegingsverzoek toe om een specifiek fusiebeleid door zijn identiteitskaart te bekijken, of tot alle fusiebeleid in uw IMS Organisatie toegang te hebben, die door specifieke criteria wordt gefiltreerd.

### Heb toegang tot één enkel fusiebeleid door identiteitskaart

U kunt tot één enkel samenvoegbeleid door zijn identiteitskaart toegang hebben door een GET verzoek aan het `/config/mergePolicies` eindpunt en met inbegrip van `mergePolicyId` in de verzoekweg te doen.

**API-indeling**

```http
GET /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschrijving |
|---|---|
| `{mergePolicyId}` | De id van het samenvoegbeleid dat u wilt verwijderen. |

**Verzoek**

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/10648288-cda5-11e8-a8d5-f2801f1b9fd1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwoord**

Een succesvolle reactie retourneert de details van het samenvoegbeleid.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "pdg"
    },
    "attributeMerge": {
        "type": "timestampOrdered"
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

Zie de [componenten van de sectie van het samenvoegingsbeleid](#components-of-merge-policies) aan het begin van dit document voor details op elk van de individuele elementen die omhoog een fusiebeleid maken.

### Meerdere vormen van samenvoegingsbeleid weergeven op basis van criteria

U kunt van veelvoudige fusiebeleid binnen uw IMS Organisatie een lijst maken door een GET verzoek aan het `/config/mergePolicies` eindpunt uit te geven en facultatieve vraagparameters te gebruiken om, de reactie te filtreren te orde te geven en te pagineren. U kunt meerdere parameters opnemen, gescheiden door ampersands (&amp;). Het maken van een vraag aan dit eindpunt zonder parameters zal al samenvoegbeleid beschikbaar voor uw organisatie terugwinnen.

**API-indeling**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
|---|---|
| `default` | Een Booleaanse waarde die het resultaat is van filters, ongeacht of het samenvoegbeleid de standaardinstelling voor een schemaklasse is. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. Standaardwaarde: 20 |
| `orderBy` | Hiermee geeft u het veld op waarmee de resultaten worden gerangschikt zoals in `orderBy=name` of `orderBy=+name` om op naam te sorteren in oplopende volgorde of `orderBy=-name`, in aflopende volgorde. Als u deze waarde weglaat, wordt standaard in oplopende volgorde gesorteerd. `name` |
| `schema.name` | Naam van het schema waarvoor om beschikbaar samenvoegbeleid terug te winnen. |
| `identityGraph.type` | Hiermee filtert u de resultaten op basis van het type identiteitsgrafiek. Mogelijke waarden zijn &quot;none&quot; en &quot;pdg&quot; (privégrafiek). |
| `attributeMerge.type` | Filterresultaten op basis van het gebruikte samenvoegtype voor kenmerken. Mogelijke waarden zijn &quot;timestampOrdered&quot; en &quot;dataSetPrecedence&quot;. |
| `start` | Paginaverschuiving - geef de eerste id op voor de gegevens die moeten worden opgehaald. Standaardwaarde: 0 |
| `version` | Geef dit op als u een specifieke versie van het samenvoegbeleid wilt gebruiken. Standaard wordt de nieuwste versie gebruikt. |

Voor meer informatie betreffende `schema.name`, `identityGraph.type`, en `attributeMerge.type`, verwijs naar de [componenten van de sectie van het fusiebeleid](#components-of-merge-policies) die vroeger in deze gids wordt verstrekt.


**Verzoek**

In het volgende verzoek worden alle samenvoegingsbeleidsregels voor een bepaald schema weergegeven:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Antwoord**

Een succesvolle reactie keert een gepagineerde lijst van fusiebeleid terug dat aan de criteria voldoet die door de vraagparameters worden gespecificeerd die in het verzoek worden verzonden.

```json
{
    "_page": {
        "totalCount": 2,
        "pageSize": 2
    },
    "children": [
        {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "none"
            },
            "attributeMerge": {
                "type": "timestampOrdered"
            },
            "default": true,
            "updateEpoch": 1552086578
        },
        {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130",
            "name": "Dataset Precedence Merge Policy",
            "imsOrgId": "{IMS_ORG}",
            "sandbox": {
                "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
                "sandboxName": "prod",
                "type": "production",
                "default": true
            },
            "schema": {
                "name": "_xdm.context.profile"
            },
            "version": 1,
            "identityGraph": {
                "type": "pdg"
            },
            "attributeMerge": {
                "type": "dataSetPrecedence",
                "order": [
                    "5b76f86b85d0e00000be5c8b",
                    "5b76f8d787a6af01e2ceda18"
                ]
            },
            "default": false,
            "updateEpoch": 1576099719
        }
    ],
    "_links": {
        "next": {
            "href": "@/mergePolicies?start=K1JJRDpFaWc5QUpZWHY1c2JBQUFBQUFBQUFBPT0jUlQ6MSNUUkM6MiNGUEM6QWdFQUFBQldBQkVBQVBnaFFQLzM4VUIvL2tKQi8rLysvMUpBLzMrMi8wRkFmLzR4UUwvL0VrRC85em4zRTBEcmNmYi92Kzh4UUwvL05rQVgzRi8rMStqNS80WHQwN2NhUUVzQUFBUUFleGpLQ1JnVXRVcEFCQUFFQVBBRA==&orderBy=&limit=2"
        }
    }
}
```

| Eigenschap | Beschrijving |
|---|---|
| `_links.next.href` | A URI address for the next page of results. Gebruik deze URI als verzoekparameter voor een andere API vraag aan het zelfde eindpunt om de pagina te bekijken. Als er geen volgende pagina bestaat, is deze waarde een lege tekenreeks. |

## Samenvoegbeleid maken

U kunt een nieuw fusiebeleid voor uw organisatie tot stand brengen door een POST- verzoek aan het `/config/mergePolicies` eindpunt te doen.

**API-indeling**

```http
POST /config/mergePolicies
```

**Verzoek** het volgende verzoek leidt tot een nieuw samenvoegbeleid, dat door de attributenwaarden wordt gevormd die in de nuttige lading worden verstrekt:

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/config/mergePolicies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph" : {
        "type": "none"
    },
    "attributeMerge" : {
        "type":"dataSetPrecedence",
        "order" : [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "schema": {
        "name":"_xdm.context.profile"
    },
    "default": true
}'
```

| Eigenschap | Beschrijving |
|---|---|
| `name` | Een mensvriendelijke naam waarmee het samenvoegbeleid in lijstweergaven kan worden geïdentificeerd. |
| `identityGraph.type` | Het type identiteitsgrafiek waaruit gerelateerde identiteiten moeten worden opgehaald om samen te voegen. Mogelijke waarden: &quot;none&quot; of &quot;pdg&quot; (privégrafiek). |
| `attributeMerge` | De manier waarop aan profielkenmerkwaarden in het geval van gegevensconflicten voorrang moet worden gegeven. |
| `schema` | De XDM-schemaklasse die aan het samenvoegbeleid is gekoppeld. |
| `default` | Geeft aan of dit samenvoegbeleid het standaardbeleid voor het schema is. |

Raadpleeg de sectie [Componenten van het](#components-of-merge-policies) samenvoegbeleid voor meer informatie.

**Antwoord**

Een geslaagde reactie retourneert de details van het nieuwe samenvoegbeleid.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

Zie de [componenten van de sectie van het samenvoegingsbeleid](#components-of-merge-policies) aan het begin van dit document voor details op elk van de individuele elementen die omhoog een fusiebeleid maken.

## Een samenvoegingsbeleid bijwerken {#update}

U kunt een bestaand samenvoegingsbeleid wijzigen door individuele attributen (PATCH) uit te geven of door het volledige fusiebeleid met nieuwe attributen (PUT) te beschrijven. Hieronder worden voorbeelden van beide weergegeven.

### Afzonderlijke velden voor samenvoegbeleid bewerken

U kunt individuele gebieden voor een samenvoegbeleid uitgeven door een verzoek van de PATCH aan het `/config/mergePolicies/{mergePolicyId}` eindpunt te doen:

**API-indeling**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschrijving |
|---|---|
| `{mergePolicyId}` | De id van het samenvoegbeleid dat u wilt verwijderen. |

**Verzoek**

Met het volgende verzoek wordt een opgegeven samenvoegingsbeleid bijgewerkt door de waarde van de `default` eigenschap te wijzigen in `true`:

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "op": "add",
    "path": "/default",
    "value": "true"
  }'
```

| Eigenschap | Beschrijving |
|---|---|
| `op` | Geeft de bewerking aan die moet worden uitgevoerd. Voorbeelden van andere PATCH-bewerkingen vindt u in de documentatie bij [JSON Patch](http://jsonpatch.com) |
| `path` | Het pad van het veld dat moet worden bijgewerkt. Accepteerde waarden zijn: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot; |
| `value` | De waarde waarop het opgegeven veld moet worden ingesteld. |

Raadpleeg de sectie [Componenten van het](#components-of-merge-policies) samenvoegbeleid voor meer informatie.


**Antwoord**

Een succesvolle reactie keert de details van het onlangs bijgewerkte fusiebeleid terug.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

### Een samenvoegbeleid overschrijven

Een andere manier om een samenvoegbeleid te wijzigen is een PPUT- verzoek te gebruiken, dat het volledige fusiebeleid beschrijft.

**API-indeling**

```http
PUT /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschrijving |
|---|---|
| `{mergePolicyId}` | De id van het samenvoegbeleid dat u wilt overschrijven. |

**Verzoek**

Het volgende verzoek beschrijft het gespecificeerde fusiebeleid, die zijn attributenwaarden met die vervangt die in de nuttige lading worden geleverd. Aangezien dit verzoek een bestaand samenvoegingsbeleid volledig vervangt, moet u alle zelfde gebieden leveren die toen oorspronkelijk het fusiebeleid bepaalde werden vereist. Dit keer geeft u echter bijgewerkte waarden op voor de velden die u wilt wijzigen.

```shell
curl -X PUT \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "_xdm.context.profile"
        },
        "version": 1,
        "identityGraph": {
            "type": "none"
        },
        "attributeMerge": {
            "type": "dataSetPrecedence",
            "order": [
                "5b76f86b85d0e00000be5c8b",
                "5b76f8d787a6af01e2ceda18"
            ]
        },
        "default": true,
        "updateEpoch": 1551898378
    }'
```

| Eigenschap | Beschrijving |
|---|---|
| `name` | Een mensvriendelijke naam waarmee het samenvoegbeleid in lijstweergaven kan worden geïdentificeerd. |
| `identityGraph` | De identiteitsgrafiek waaruit gerelateerde identiteiten moeten worden opgehaald om samen te voegen. |
| `attributeMerge` | De manier waarop aan profielkenmerkwaarden in het geval van gegevensconflicten voorrang moet worden gegeven. |
| `schema` | De XDM-schemaklasse die aan het samenvoegbeleid is gekoppeld. |
| `default` | Geeft aan of dit samenvoegbeleid het standaardbeleid voor het schema is. |

Raadpleeg de sectie [Componenten van het](#components-of-merge-policies) samenvoegbeleid voor meer informatie.


**Antwoord**

Een geslaagde reactie retourneert de details van het bijgewerkte samenvoegingsbeleid.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{IMS_ORG}",
    "sandbox": {
        "sandboxId": "ff0f6870-c46d-11e9-8ca3-036939a64204",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "5b76f86b85d0e00000be5c8b",
            "5b76f8d787a6af01e2ceda18"
        ]
    },
    "default": true,
    "updateEpoch": 1551898378
}
```

## Een samenvoegingsbeleid verwijderen

Een samenvoegingsbeleid kan worden geschrapt door een verzoek van de SCHRAPPING aan het `/config/mergePolicies` eindpunt en met inbegrip van identiteitskaart van het fusiebeleid te doen dat u wenst om in de verzoekweg te schrappen.

**API-indeling**

```http
DELETE /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschrijving |
|---|---|
| `{mergePolicyId}` | De id van het samenvoegbeleid dat u wilt verwijderen. |

**Verzoek**

Met de volgende aanvraag wordt een samenvoegbeleid verwijderd.

```shell
curl -X DELETE \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Antwoord**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. Om de schrapping te bevestigen succesvol was, kunt u een GET verzoek uitvoeren om het fusiebeleid door zijn identiteitskaart te bekijken. Als het samenvoegbeleid is verwijderd, ontvangt u een HTTP Status 404 (Not Found)-fout.

## Volgende stappen

Nu u weet om samenvoegbeleid voor uw IMS Organisatie tot stand te brengen en te vormen, kunt u hen gebruiken om publiekssegmenten van uw gegevens van het Profiel van de Klant in real time tot stand te brengen. Raadpleeg de documentatie bij [de Segmentatieservice van het](../../segmentation/home.md) Adobe Experience Platform voor meer informatie over het definiëren en werken met segmenten.



