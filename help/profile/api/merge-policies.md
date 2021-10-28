---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: API-eindpunt voor beleid samenvoegen
topic-legacy: guide
type: Documentation
description: Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een verenigde mening tot stand te brengen.
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: 9af59d5a4fda693a2aef8e590a7754f0e1c1ac8d
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 0%

---

# Het eindpunt van beleid samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Bij het samenvoegen van deze gegevens gelden als samenvoegbeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een verenigde mening tot stand te brengen.

Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken. Wanneer de gegevens van veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl de andere klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het fusiebeleid welke informatie om in het profiel voor het individu te omvatten.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stappen voor het werken met de API voor samenvoegbeleid.

Als u met een UI voor het samenvoegen wilt werken, raadpleegt u de [UI-hulplijn voor samenvoegbeleid](../merge-policies/ui-guide.md). Als u meer wilt weten over samenvoegingsbeleid in het algemeen en hun rol in het Experience Platform, leest u eerst de [overzicht van samenvoegbeleid](../merge-policies/overview.md).

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van het [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). Controleer voordat je doorgaat de [gids Aan de slag](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document en belangrijke informatie betreffende vereiste kopballen die nodig zijn om met succes vraag aan om het even welk [!DNL Experience Platform] API.

## Componenten van samenvoegingsbeleid {#components-of-merge-policies}

Het beleid van de fusie is privé aan uw organisatie IMS, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manieren samen te voegen die u nodig hebt. API-toegang [!DNL Profile] de gegevens vereisen een fusiebeleid, hoewel een gebrek zal worden gebruikt als niet uitdrukkelijk wordt verstrekt. [!DNL Platform] voorziet organisaties van een standaardsamenvoegbeleid, of u kunt een samenvoegbeleid voor een specifieke het schemaklasse van de Gegevens van de Ervaring van het Model (XDM) tot stand brengen en het merken als gebrek voor uw organisatie.

Hoewel elke organisatie mogelijk meerdere samenvoegbeleidsregels per schemaklasse kan hebben, kan elke klasse slechts één standaardsamenvoegbeleid hebben. Om het even welk samenvoegbeleid dat als gebrek wordt geplaatst zal worden gebruikt in gevallen waar de naam van de schemacategorie wordt verstrekt en een fusiebeleid wordt vereist maar niet verstrekt.

>[!NOTE]
>
>Wanneer u een nieuw fusiebeleid als gebrek plaatst, zal om het even welk bestaand fusiebeleid dat eerder als gebrek werd geplaatst automatisch worden bijgewerkt om niet meer als gebrek te worden gebruikt.

Om ervoor te zorgen dat alle profielgebruikers met dezelfde weergave aan de randen werken, kan het samenvoegbeleid als actief aan de rand worden gemarkeerd. Als u wilt dat een segment aan de rand wordt geactiveerd (gemarkeerd als een randsegment), moet het segment zijn gekoppeld aan een samenvoegingsbeleid dat is gemarkeerd als actief aan de rand. Als een segment **niet** gekoppeld aan een samenvoegbeleid dat aan de rand is gemarkeerd als actief, wordt het segment niet gemarkeerd als actief aan de rand en wordt het gemarkeerd als een streaming segment.

Bovendien kan elke IMS-organisatie alleen **één** samenvoegbeleid dat op rand actief is. Als een samenvoegbeleid op rand actief is, kan het voor andere systemen op rand, zoals het Profiel van de Rand, de Segmentatie van de Rand, en Doelen op Rand worden gebruikt.

### Object voor samenvoegbeleid voltooien

Het volledige samenvoegbeleidsobject vertegenwoordigt een set voorkeuren waarmee aspecten van het samenvoegen van profielfragmenten worden beheerd.

**Beleidsobject samenvoegen**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{IMS_ORG}",
        "schema": {
            "name": "{SCHEMA_CLASS_NAME}"
        },
        "version": 1,
        "identityGraph": {
            "type": "{IDENTITY_GRAPH_TYPE}"
        },
        "attributeMerge": {
            "type": "{ATTRIBUTE_MERGE_TYPE}"
        },
        "isActiveOnEdge": "{BOOLEAN}",
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | Door het systeem gegenereerde unieke id die tijdens het maken is toegewezen |
| `name` | Vriendelijke naam waarmee het samenvoegbeleid kan worden geïdentificeerd in lijstweergaven. |
| `imsOrgId` | Organisatie-id waartoe dit samenvoegbeleid behoort |
| `schema.name` | Deel van de [`schema`](#schema) object, `name` bevat de XDM-schemaklasse waarop het samenvoegbeleid betrekking heeft. Voor meer informatie over schema&#39;s en klassen, gelieve te lezen [XDM-documentatie](../../xdm/home.md). |
| `version` | [!DNL Platform] onderhouden versie van samenvoegingsbeleid. Deze alleen-lezen waarde wordt verhoogd wanneer een samenvoegbeleid wordt bijgewerkt. |
| `identityGraph` | [Identiteitsgrafiek](#identity-graph) object dat de identiteitsgrafiek aangeeft waarvan gerelateerde identiteiten worden verkregen. Profielfragmenten die voor alle verwante identiteiten worden gevonden, worden samengevoegd. |
| `attributeMerge` | [Kenmerk samenvoegen](#attribute-merge) object dat aangeeft hoe in het samenvoegbeleid bij gegevensconflicten voorrang wordt gegeven aan profielkenmerken. |
| `isActiveOnEdge` | Een Booleaanse waarde die aangeeft of dit samenvoegbeleid aan de rand kan worden gebruikt. Deze waarde is standaard `false`. |
| `default` | Een Booleaanse waarde die aangeeft of dit samenvoegbeleid de standaardinstelling is voor het opgegeven schema. |
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
        "isActiveOnEdge": false,
        "default": true,
        "updateEpoch": 1551660639
    }
```

### Identiteitsgrafiek {#identity-graph}

[Adobe Experience Platform Identity Service](../../identity-service/home.md) beheert de identiteitsgrafieken die globaal en voor elke organisatie worden gebruikt op [!DNL Experience Platform]. De `identityGraph` kenmerk van het samenvoegbeleid definieert hoe de verwante identiteiten voor een gebruiker moeten worden bepaald.

**identityGraph-object**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Wanneer `{IDENTITY_GRAPH_TYPE}` is één van het volgende:

* **&quot;none&quot;:** Geen identiteitsstitching uitvoeren.
* **&quot;pdg&quot;:** Identiteitsstitching uitvoeren op basis van uw persoonlijke identiteitsgrafiek.

**Voorbeeld`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Kenmerk samenvoegen {#attribute-merge}

Een profielfragment is de profielinformatie voor slechts één identiteit uit de lijst van identiteiten die voor een bepaalde gebruiker bestaan. Wanneer het gebruikte type identiteitsgrafiek meer dan één identiteit resulteert, is er een potentieel voor conflicterende profielattributen en de prioriteit moet worden gespecificeerd. Gebruiken `attributeMerge`, kunt u specificeren welke profielattributen om voorrang te geven in het geval van een fusieconflict tussen Zeer belangrijke het type datasets van de Waarde (verslaggegevens).

**Object attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Wanneer `{ATTRIBUTE_MERGE_TYPE}` is één van het volgende:

* **`timestampOrdered`**: (standaardwaarde) Geef prioriteit aan het profiel dat het laatst is bijgewerkt. Met dit samenvoegtype `data` attribuut is not required.
* **`dataSetPrecedence`** : Geef voorrang aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Dit zou kunnen worden gebruikt wanneer de informatie aanwezig in één dataset over gegevens in een andere dataset wordt aangewezen of wordt vertrouwd. Wanneer u dit samenvoegtype gebruikt, wordt `order` attribuut wordt vereist, aangezien het van de datasets in de orde van prioriteit een lijst maakt.
   * **`order`**: Wanneer &quot;dataSetPrecision&quot; wordt gebruikt, wordt een `order` array moet worden voorzien van een lijst met gegevenssets. Gegevenssets die niet in de lijst zijn opgenomen, worden niet samengevoegd. Met andere woorden, gegevenssets moeten expliciet worden vermeld om te worden samengevoegd in een profiel. De `order` De serie maakt een lijst van IDs van de datasets in orde van prioriteit.

#### Voorbeeld `attributeMerge` object gebruiken `dataSetPrecedence` type

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

#### Voorbeeld `attributeMerge` object gebruiken `timestampOrdered` type

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Het schemavoorwerp specificeert de het schemaklasse van de Gegevens van de Ervaring (XDM) waarvoor dit fusiebeleid wordt gecreeerd.

**`schema`object**

```json
    "schema": {
        "name": "{SCHEMA_NAME}"
    }
```

Wanneer de waarde van `name` is de naam van de klasse XDM waarop het schema verbonden aan het fusiebeleid wordt gebaseerd.

**Voorbeeld`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Om meer over XDM en het werken met schema&#39;s in Experience Platform te leren, begin door te lezen [XDM System, overzicht](../../xdm/home.md).

## Beleid voor samenvoegen openen {#access-merge-policies}

Met de [!DNL Real-time Customer Profile] API, de `/config/mergePolicies` het eindpunt staat u toe een raadplegingsverzoek uitvoert om een specifiek samenvoegbeleid door zijn identiteitskaart te bekijken, of toegang tot elk van het fusiebeleid in uw IMS Organisatie, die door specifieke criteria wordt gefiltreerd. U kunt ook de opdracht `/config/mergePolicies/bulk-get` eindpunt om veelvoudige samenvoegbeleid door hun IDs terug te winnen. De stappen voor het uitvoeren van elk van deze vraag worden geschetst in de volgende secties.

### Heb toegang tot één enkel fusiebeleid door identiteitskaart

U kunt tot één enkel fusiebeleid door zijn identiteitskaart toegang hebben door een verzoek van de GET tot `/config/mergePolicies` en met inbegrip van de `mergePolicyId` in het aanvraagpad.

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
    "isActiveOnEdge": "false",
    "default": false,
    "updateEpoch": 1551127597
}
```

Zie de [componenten van samenvoegingsbeleid](#components-of-merge-policies) aan het begin van dit document voor meer informatie over de afzonderlijke elementen die samen een samenvoegbeleid vormen.

### Hiermee worden meerdere samenvoegbeleidsregels via de id&#39;s opgehaald

U kunt meerdere samenvoegbeleidsregels ophalen door een POST aan te vragen bij de `/config/mergePolicies/bulk-get` eindpunt en met inbegrip van IDs van het fusiebeleid u in het verzoeklichaam wenst terug te winnen.

**API-indeling**

```http
POST /config/mergePolicies/bulk-get
```

**Verzoek**

De aanvraaginstantie bevat een array &#39;ids&#39; met afzonderlijke objecten die de &#39;id&#39; bevatten voor elk samenvoegbeleid waarvoor u details wilt ophalen.

```shell
curl -X POST \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies/bulk-get' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "ids": [
          {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b"
          },
          {
            "id": "42d4a596-b1c6-46c0-994e-ca5ef1f85130"
          }
        ]
      }'
```

**Antwoord**

Een succesvolle reactie keert de Status 207 van HTTP (multi-Status) en de details van het fusiebeleid terug waarvan IDs in het verzoek van de POST werd verstrekt.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
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
            "isActiveOnEdge": true,
            "default": true,
            "updateEpoch": 1552086578
        },
        "42d4a596-b1c6-46c0-994e-ca5ef1f85130": {
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
            "isActiveOnEdge": false,
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Zie de [componenten van samenvoegingsbeleid](#components-of-merge-policies) aan het begin van dit document voor meer informatie over de afzonderlijke elementen die samen een samenvoegbeleid vormen.

### Meerdere vormen van samenvoegingsbeleid weergeven op basis van criteria

U kunt meerdere samenvoegbeleidsregels weergeven binnen uw IMS-organisatie door een verzoek tot GET te richten aan de `/config/mergePolicies` eindpunt en het gebruiken van facultatieve vraagparameters aan filter, orde, en pagineren de reactie. U kunt meerdere parameters opnemen, gescheiden door ampersands (&amp;). Het maken van een vraag aan dit eindpunt zonder parameters zal al samenvoegbeleid beschikbaar voor uw organisatie terugwinnen.

**API-indeling**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
|---|---|
| `default` | Een Booleaanse waarde die het resultaat is van filters, ongeacht of het samenvoegbeleid de standaardinstelling voor een schemaklasse is. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. Standaardwaarde: 20 |
| `orderBy` | Hiermee geeft u het veld op waarin de resultaten moeten worden geordend als in `orderBy=name` of `orderBy=+name` op naam in oplopende volgorde te sorteren, of `orderBy=-name`om in aflopende volgorde te sorteren. Als u deze waarde weglaat, wordt de standaardsortering van `name` in oplopende volgorde. |
| `isActiveOnEdge` | Een booleaanse waarde die filtert, bepaalt of het samenvoegbeleid al dan niet actief is op de rand. |
| `schema.name` | Naam van het schema waarvoor om beschikbaar samenvoegbeleid terug te winnen. |
| `identityGraph.type` | Hiermee filtert u de resultaten op basis van het type identiteitsgrafiek. Mogelijke waarden zijn &quot;none&quot; en &quot;pdg&quot; (privégrafiek). |
| `attributeMerge.type` | Filterresultaten op basis van het gebruikte samenvoegtype voor kenmerken. Mogelijke waarden zijn &quot;timestampOrdered&quot; en &quot;dataSetPrecedence&quot;. |
| `start` | Paginaverschuiving - geef de eerste id op voor de gegevens die moeten worden opgehaald. Standaardwaarde: 0 |
| `version` | Geef dit op als u een specifieke versie van het samenvoegbeleid wilt gebruiken. Standaard wordt de nieuwste versie gebruikt. |

Voor meer informatie over `schema.name`, `identityGraph.type`, en `attributeMerge.type`, verwijst u naar de [componenten van samenvoegingsbeleid](#components-of-merge-policies) in deze handleiding.


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
            "isActiveOnEdge": true,
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
            "isActiveOnEdge": false,
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

U kunt een nieuw samenvoegbeleid voor uw organisatie tot stand brengen door een verzoek van de POST aan `/config/mergePolicies` eindpunt.

**API-indeling**

```http
POST /config/mergePolicies
```

**Verzoek**
Het volgende verzoek leidt tot een nieuw samenvoegbeleid, dat door de attributenwaarden wordt gevormd die in de lading worden verstrekt:

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
    "isActiveOnEdge": true,
    "default": true
}'
```

| Eigenschap | Beschrijving |
|---|---|
| `name` | Een mensvriendelijke naam waarmee het samenvoegbeleid in lijstweergaven kan worden geïdentificeerd. |
| `identityGraph.type` | Het type identiteitsgrafiek waaruit gerelateerde identiteiten moeten worden opgehaald om samen te voegen. Mogelijke waarden: &quot;none&quot; of &quot;pdg&quot; (privégrafiek). |
| `attributeMerge` | De manier waarop aan profielkenmerkwaarden in het geval van gegevensconflicten voorrang moet worden gegeven. |
| `schema` | De XDM-schemaklasse die aan het samenvoegbeleid is gekoppeld. |
| `isActiveOnEdge` | Geeft aan of dit samenvoegbeleid op de rand actief is. |
| `default` | Geeft aan of dit samenvoegbeleid het standaardbeleid voor het schema is. |

Zie de [componenten van samenvoegingsbeleid](#components-of-merge-policies) voor meer informatie.

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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

Zie de [componenten van samenvoegingsbeleid](#components-of-merge-policies) aan het begin van dit document voor meer informatie over de afzonderlijke elementen die samen een samenvoegbeleid vormen.

## Een samenvoegingsbeleid bijwerken {#update}

U kunt een bestaand samenvoegingsbeleid wijzigen door individuele attributen (PATCH) uit te geven of door het volledige fusiebeleid met nieuwe attributen (PUT) te beschrijven. Hieronder worden voorbeelden van beide weergegeven.

### Afzonderlijke velden voor samenvoegbeleid bewerken

U kunt afzonderlijke velden voor een samenvoegbeleid bewerken door een PATCH-aanvraag in te dienen bij de `/config/mergePolicies/{mergePolicyId}` eindpunt:

**API-indeling**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschrijving |
|---|---|
| `{mergePolicyId}` | De id van het samenvoegbeleid dat u wilt verwijderen. |

**Verzoek**

Met het volgende verzoek wordt een opgegeven samenvoegingsbeleid bijgewerkt door de waarde van het samenvoegbeleid te wijzigen `default` eigenschap aan `true`:

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
| `op` | Geeft de bewerking aan die moet worden uitgevoerd. Voorbeelden van andere PATCH-bewerkingen vindt u in het gedeelte [JSON-patchdocumentatie](http://jsonpatch.com) |
| `path` | Het pad van het veld dat moet worden bijgewerkt. Accepteerde waarden zijn: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | De waarde waarop het opgegeven veld moet worden ingesteld. |

Zie de [componenten van samenvoegingsbeleid](#components-of-merge-policies) voor meer informatie.


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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

### Een samenvoegbeleid overschrijven

Een andere manier om een fusiebeleid te wijzigen is een verzoek van de PUT te gebruiken, dat het volledige fusiebeleid beschrijft.

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
        "isActiveOnEdge": true,
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
| `isActiveOnEdge` | Geeft aan of dit samenvoegbeleid op de rand actief is. |
| `default` | Geeft aan of dit samenvoegbeleid het standaardbeleid voor het schema is. |

Zie de [componenten van samenvoegingsbeleid](#components-of-merge-policies) voor meer informatie.

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
    "isActiveOnEdge": true,
    "default": true,
    "updateEpoch": 1551898378
}
```

## Een samenvoegingsbeleid verwijderen

Een samenvoegingsbeleid kan worden verwijderd door een DELETE-verzoek in te dienen bij de `/config/mergePolicies` eindpunt en met inbegrip van identiteitskaart van het fusiebeleid dat u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
>Als het samenvoegbeleid `isActiveOnEdge` ingesteld op true, het samenvoegbeleid **kan** worden geschrapt. Gebruik een van de [PATCH](#edit-individual-merge-policy-fields) of [PUT](#overwrite-a-merge-policy) eindpunten om het samenvoegbeleid bij te werken voordat het wordt verwijderd.

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

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. Om de schrapping te bevestigen succesvol was, kunt u een verzoek van de GET uitvoeren om het fusiebeleid door zijn identiteitskaart te bekijken. Als het samenvoegbeleid is verwijderd, ontvangt u een HTTP Status 404 (Not Found)-fout.

## Volgende stappen

Nu u weet om samenvoegbeleid voor uw organisatie tot stand te brengen en te vormen, kunt u hen gebruiken om de mening van klantenprofielen binnen Platform aan te passen en publiekssegmenten van uw te creëren [!DNL Real-time Customer Profile] gegevens.

Zie de [Adobe Experience Platform Segmentation Service-documentatie](../../segmentation/home.md) om te beginnen met het definiëren en werken met segmenten.
