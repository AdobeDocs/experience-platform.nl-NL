---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen oplossen;API
title: API-eindpunt voor beleid samenvoegen
type: Documentation
description: Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het samenbrengen van deze gegevens, is het fusiebeleid de regels die Experience Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om een verenigde mening tot stand te brengen.
role: Developer
exl-id: fb49977d-d5ca-4de9-b185-a5ac1d504970
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2468'
ht-degree: 0%

---

# Het eindpunt van beleid samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer u deze gegevens samenbrengt, zijn samenvoegbeleidsregels de regels die [!DNL Experience Platform] gebruikt om te bepalen hoe de prioriteit van gegevens wordt bepaald en welke gegevens worden gecombineerd om een uniforme weergave te maken.

Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Experience Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken. Wanneer de gegevens van veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl de andere klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het fusiebeleid welke informatie om in het profiel voor het individu te omvatten.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stappen voor het werken met de API voor samenvoegbeleid.

Om met samenvoegbeleid te werken gebruikend UI, gelieve te verwijzen naar de [ gids UI van het samenvoegingsbeleid ](../merge-policies/ui-guide.md). Meer over samenvoegingsbeleid in het algemeen, en hun rol binnen Experience Platform leren, gelieve te beginnen door het [ overzicht van het fusiebeleid ](../merge-policies/overview.md) te lezen.

## Aan de slag

Het API eindpunt dat in deze gids wordt gebruikt is een deel van [[!DNL Real-Time Customer Profile API] ](https://www.adobe.com/go/profile-apis-en). Alvorens verder te gaan, te herzien gelieve [ begonnen gids ](getting-started.md) voor verbindingen aan verwante documentatie, een gids aan het lezen van de steekproefAPI vraag in dit document, en belangrijke informatie betreffende vereiste kopballen die nodig zijn om vraag aan om het even welke [!DNL Experience Platform] API met succes te maken.

## Componenten van samenvoegingsbeleid {#components-of-merge-policies}

Het beleid van de fusie is privé aan uw organisatie, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manieren samen te voegen die u nodig hebt. Voor elke API die toegang wil tot [!DNL Profile] -gegevens, is een samenvoegbeleid vereist, maar er wordt een standaard gebruikt als dit niet expliciet wordt opgegeven. [!DNL Experience Platform] voorziet organisaties van een standaardsamenvoegbeleid, of u kunt een fusiebeleid voor een specifieke het schemaklasse van de Gegevens van de Ervaring van het Model (XDM) tot stand brengen en het merken als gebrek voor uw organisatie.

Hoewel elke organisatie mogelijk meerdere samenvoegbeleidsregels per schemaklasse kan hebben, kan elke klasse slechts één standaardsamenvoegbeleid hebben. Om het even welk samenvoegbeleid dat als gebrek wordt geplaatst zal worden gebruikt in gevallen waar de naam van de schemacategorie wordt verstrekt en een fusiebeleid wordt vereist maar niet verstrekt.

>[!NOTE]
>
>Wanneer u een nieuw fusiebeleid als gebrek plaatst, zal om het even welk bestaand fusiebeleid dat eerder als gebrek werd geplaatst automatisch worden bijgewerkt om niet meer als gebrek te worden gebruikt.

Om ervoor te zorgen dat alle profielgebruikers met dezelfde weergave aan de randen werken, kan het samenvoegbeleid als actief aan de rand worden gemarkeerd. Een publiek kan alleen aan de rand worden geactiveerd (gemarkeerd als een randpubliek) als het is gekoppeld aan een samenvoegbeleid dat als actief aan de rand is gemarkeerd. Als een publiek **niet** gebonden aan een fusiebeleid is dat als actief op rand duidelijk is, zal het publiek niet als actief op rand worden gemerkt, en zal als het stromen publiek worden gemerkt.

Bovendien, kan elke organisatie **slechts één** fusiebeleid hebben dat op rand actief is. Als een samenvoegbeleid op rand actief is, kan het voor andere systemen op rand, zoals het Profiel van Edge, de Segmentatie van Edge, en Doelen op Edge worden gebruikt.

### Object voor samenvoegbeleid voltooien

Het volledige samenvoegbeleidsobject vertegenwoordigt een set voorkeuren waarmee aspecten van het samenvoegen van profielfragmenten worden beheerd.

**het beleidsvoorwerp van de Fusie**

```json
    {
        "id": "{MERGE_POLICY_ID}",
        "name": "{NAME}",
        "imsOrgId": "{ORG_ID}",
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
| `schema.name` | Het veld `name` bevat een deel van het object [`schema`](#schema) dat de XDM-schemaklasse bevat waarop het samenvoegbeleid betrekking heeft. Voor meer informatie over schema&#39;s en klassen, te lezen gelieve de [ documentatie XDM ](../../xdm/home.md). |
| `version` | [!DNL Experience Platform] bijgewerkte versie van het samenvoegbeleid. Deze alleen-lezen waarde wordt verhoogd wanneer een samenvoegbeleid wordt bijgewerkt. |
| `identityGraph` | [ de grafiekvoorwerp van de Identiteit ](#identity-graph) die op de identiteitsgrafiek wijst waarvan verwante identiteiten zullen worden verkregen. Profielfragmenten die voor alle verwante identiteiten worden gevonden, worden samengevoegd. |
| `attributeMerge` | [ de fusie van Attributen ](#attribute-merge) die op de manier wijzen waarop het fusiebeleid profielattributen in het geval van gegevensconflicten voorrang zal geven. |
| `isActiveOnEdge` | Een Booleaanse waarde die aangeeft of dit samenvoegbeleid aan de rand kan worden gebruikt. Deze waarde is standaard `false` . |
| `default` | Een Booleaanse waarde die aangeeft of dit samenvoegbeleid de standaardinstelling is voor het opgegeven schema. |
| `updateEpoch` | Datum van de laatste update van het samenvoegbeleid. |

**Samenvoegbeleid van het Voorbeeld**

```json
    {
        "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
        "name": "profile-default",
        "imsOrgId": "{ORG_ID}",
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

[ de Dienst van de Identiteit van Adobe Experience Platform ](../../identity-service/home.md) beheert de identiteitsgrafieken die globaal en voor elke organisatie op [!DNL Experience Platform] worden gebruikt. Het kenmerk `identityGraph` van het samenvoegbeleid definieert hoe de verwante identiteiten voor een gebruiker moeten worden bepaald.

**identityGraph voorwerp**

```json
    "identityGraph": {
        "type": "{IDENTITY_GRAPH_TYPE}"
    }
```

Waar `{IDENTITY_GRAPH_TYPE}` een van de volgende is:

* **&quot;none&quot;:** voer geen identiteitsstitching uit.
* **&quot;pdg&quot;:** voer identiteitsstitching uit op basis van uw persoonlijke identiteitsgrafiek.

**Voorbeeld`identityGraph`**

```json
    "identityGraph": {
        "type": "pdg"
    }
```

### Kenmerk samenvoegen {#attribute-merge}

Een profielfragment is de profielinformatie voor slechts één identiteit uit de lijst van identiteiten die voor een bepaalde gebruiker bestaan. Wanneer het gebruikte type identiteitsgrafiek meer dan één identiteit resulteert, is er een potentieel voor conflicterende profielattributen en de prioriteit moet worden gespecificeerd. Met `attributeMerge` kunt u opgeven welke profielkenmerken prioriteit moeten krijgen in geval van een samenvoegconflict tussen gegevenssets van het type Key Value (recordgegevens).

**attributeMerge voorwerp**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Waar `{ATTRIBUTE_MERGE_TYPE}` een van de volgende is:

* **`timestampOrdered`**: (standaard) Geef prioriteit aan het profiel dat het laatst is bijgewerkt. Met dit samenvoegtype is het kenmerk `data` niet vereist.
* **`dataSetPrecedence`**: geef prioriteit aan profielfragmenten die zijn gebaseerd op de gegevensset waaruit ze afkomstig zijn. Dit zou kunnen worden gebruikt wanneer de informatie aanwezig in één dataset over gegevens in een andere dataset wordt aangewezen of wordt vertrouwd. Wanneer het gebruiken van dit fusietype, wordt het `order` attribuut vereist, aangezien het van de datasets in de orde van prioriteit een lijst maakt.
   * **`order`**: Wanneer &quot;dataSetPriority&quot; wordt gebruikt, moet een `order` -array worden voorzien van een lijst met gegevenssets. Gegevenssets die niet in de lijst zijn opgenomen, worden niet samengevoegd. Met andere woorden, gegevenssets moeten expliciet worden vermeld om te worden samengevoegd in een profiel. De array `order` geeft de id&#39;s van de gegevenssets weer in volgorde van prioriteit.

#### Voorbeeld `attributeMerge` -object met `dataSetPrecedence` type

```json
    "attributeMerge": {
        "type": "dataSetPrecedence",
        "order": [
            "dataSetId_2", 
            "dataSetId_3", 
            "dataSetId_1", 
            "dataSetId_4"
        ]
    }
```

#### Voorbeeld `attributeMerge` -object met `timestampOrdered` type

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

Waar de waarde van `name` de naam van de klasse XDM is waarop het schema verbonden aan het fusiebeleid wordt gebaseerd.

**Voorbeeld`schema`**

```json
    "schema": {
        "name": "_xdm.context.profile"
    }
```

Om meer over XDM en het werken met schema&#39;s in Experience Platform te leren, begin door het [ overzicht van het Systeem XDM ](../../xdm/home.md) te lezen.

## Beleid voor samenvoegen openen {#access-merge-policies}

Met behulp van de [!DNL Real-Time Customer Profile] API kunt u aan de hand van het `/config/mergePolicies` -eindpunt een opzoekverzoek uitvoeren om een specifiek samenvoegbeleid op basis van de id weer te geven, of hebt u toegang tot alle samenvoegbeleidsregels in uw organisatie, gefilterd op specifieke criteria. U kunt het `/config/mergePolicies/bulk-get` eindpunt ook gebruiken om veelvoudige samenvoegbeleid door hun IDs terug te winnen. De stappen voor het uitvoeren van elk van deze vraag worden geschetst in de volgende secties.

### Heb toegang tot één enkel fusiebeleid door identiteitskaart

U hebt toegang tot één samenvoegbeleid met de id van de toepassing door een GET-aanvraag in te dienen bij het eindpunt `/config/mergePolicies` en de `mergePolicyId` op te nemen in het aanvraagpad.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Reactie**

Een succesvolle reactie retourneert de details van het samenvoegingsbeleid.

```json
{
    "id": "10648288-cda5-11e8-a8d5-f2801f1b9fd1",
    "imsOrgId": "{ORG_ID}",
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

Zie de [ componenten van het beleid van de fusie ](#components-of-merge-policies) sectie aan het begin van dit document voor details op elk van de individuele elementen die omhoog een fusiebeleid maken.

### Hiermee worden meerdere samenvoegbeleidsregels via de id&#39;s opgehaald

U kunt veelvoudige fusiebeleid terugwinnen door een POST- verzoek aan het `/config/mergePolicies/bulk-get` eindpunt en met inbegrip van identiteitskaarts van het fusiebeleid te doen u in het verzoeklichaam wenst terug te winnen.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

**Reactie**

Een succesvolle reactie keert de Status 207 van HTTP (multi-Status) en de details van het fusiebeleid terug waarvan IDs in het POST- verzoek werd verstrekt.

```json
{ 
    "results": { 
        "0bf16e61-90e9-4204-b8fa-ad250360957b": {
            "id": "0bf16e61-90e9-4204-b8fa-ad250360957b",
            "name": "Profile Default Merge Policy",
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

Zie de [ componenten van het beleid van de fusie ](#components-of-merge-policies) sectie aan het begin van dit document voor details op elk van de individuele elementen die omhoog een fusiebeleid maken.

### Meerdere vormen van samenvoegingsbeleid weergeven op basis van criteria

U kunt een lijst maken van de veelvoudige samenvoegbeleidsvormen binnen uw organisatie door een GET- verzoek aan het `/config/mergePolicies` eindpunt uit te geven en facultatieve vraagparameters te gebruiken om de reactie te filtreren, te ordenen en te pagineren. U kunt meerdere parameters opnemen, gescheiden door ampersands (&amp;). Het maken van een vraag aan dit eindpunt zonder parameters zal al samenvoegbeleid beschikbaar voor uw organisatie terugwinnen.

**API formaat**

```http
GET /config/mergePolicies?{QUERY_PARAMS}
```

| Parameter | Beschrijving |
|---|---|
| `default` | Een Booleaanse waarde die het resultaat is van filters, ongeacht of het samenvoegbeleid de standaardinstelling voor een schemaklasse is. |
| `limit` | Hiermee geeft u de maximale paginagrootte op om het aantal resultaten op te geven dat in een pagina wordt opgenomen. Standaardwaarde: 20 |
| `orderBy` | Hiermee geeft u het veld op waarin de resultaten moeten worden geordend, zoals in `orderBy=name` of `orderBy=+name` bij het sorteren op naam in oplopende volgorde (of `orderBy=-name` bij het sorteren in aflopende volgorde). Als u deze waarde weglaat, wordt `name` standaard oplopend gesorteerd. |
| `isActiveOnEdge` | Een booleaanse waarde die filtert, bepaalt of het samenvoegbeleid al dan niet actief is op de rand. |
| `schema.name` | Naam van het schema waarvoor om beschikbaar samenvoegbeleid terug te winnen. |
| `identityGraph.type` | Hiermee filtert u de resultaten op basis van het type identiteitsgrafiek. Mogelijke waarden zijn &quot;none&quot; en &quot;pdg&quot; (privégrafiek). |
| `attributeMerge.type` | Filterresultaten op basis van het gebruikte samenvoegtype voor kenmerken. Mogelijke waarden zijn &quot;timestampOrdered&quot; en &quot;dataSetPrecision&quot;. |
| `start` | Paginaverschuiving - geef de eerste id op voor de gegevens die moeten worden opgehaald. Standaardwaarde: 0 |
| `version` | Geef dit op als u een specifieke versie van het samenvoegbeleid wilt gebruiken. Standaard wordt de nieuwste versie gebruikt. |

Voor meer informatie betreffende `schema.name`, `identityGraph.type`, en `attributeMerge.type`, verwijs naar de [ componenten van de sectie van het fusiebeleid ](#components-of-merge-policies) vroeger in deze gids wordt verstrekt.


**Verzoek**

In het volgende verzoek worden alle samenvoegingsbeleidsregels voor een bepaald schema weergegeven:

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/config/mergePolicies?schema.name=_xdm.context.profile' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}
```

**Reactie**

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
            "imsOrgId": "{ORG_ID}",
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
            "imsOrgId": "{ORG_ID}",
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

U kunt een nieuw samenvoegbeleid voor uw organisatie tot stand brengen door een POST- verzoek aan het `/config/mergePolicies` eindpunt te doen.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Loyalty members ordered by ID",
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence",
        "order": [
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

Verwijs naar de [ componenten van de sectie van het samenvoegbeleid ](#components-of-merge-policies) voor meer informatie.

**Reactie**

Een geslaagde reactie retourneert de details van het nieuwe samenvoegbeleid.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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

Zie de [ componenten van het beleid van de fusie ](#components-of-merge-policies) sectie aan het begin van dit document voor details op elk van de individuele elementen die omhoog een fusiebeleid maken.

## Een samenvoegingsbeleid bijwerken {#update}

U kunt een bestaand samenvoegbeleid wijzigen door afzonderlijke kenmerken te bewerken (PATCH) of door het gehele samenvoegbeleid te overschrijven met nieuwe kenmerken (PUT). Hieronder worden voorbeelden van beide weergegeven.

### Afzonderlijke velden voor samenvoegbeleid bewerken

U kunt afzonderlijke velden voor een samenvoegbeleid bewerken door een PATCH-aanvraag in te dienen bij het eindpunt `/config/mergePolicies/{mergePolicyId}` :

**API formaat**

```http
PATCH /config/mergePolicies/{mergePolicyId}
```

| Parameter | Beschrijving |
|---|---|
| `{mergePolicyId}` | De id van het samenvoegbeleid dat u wilt verwijderen. |

**Verzoek**

Met de volgende aanvraag wordt een opgegeven samenvoegingsbeleid bijgewerkt door de waarde van de eigenschap `default` te wijzigen in `true` :

```shell
curl -X PATCH \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `op` | Geeft de bewerking aan die moet worden uitgevoerd. De voorbeelden van andere verrichtingen van PATCH kunnen in de [ documentatie van het Reparatie JSON ](https://datatracker.ietf.org/doc/html/rfc6902) worden gevonden |
| `path` | Het pad van het veld dat moet worden bijgewerkt. Accepteerde waarden zijn: &quot;/name&quot;, &quot;/identityGraph.type&quot;, &quot;/attributeMerge.type&quot;, &quot;/schema.name&quot;, &quot;/version&quot;, &quot;/default&quot;, &quot;/isActiveOnEdge&quot; |
| `value` | De waarde waarop het opgegeven veld moet worden ingesteld. |

Verwijs naar de [ componenten van de sectie van het samenvoegbeleid ](#components-of-merge-policies) voor meer informatie.


**Reactie**

Een succesvolle reactie keert de details van het onlangs bijgewerkte fusiebeleid terug.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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

Een andere manier om een fusiebeleid te wijzigen is een verzoek van PUT te gebruiken, dat het volledige fusiebeleid beschrijft.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "name": "Loyalty members ordered by ID",
        "imsOrgId": "{ORG_ID}",
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

Verwijs naar de [ componenten van de sectie van het samenvoegbeleid ](#components-of-merge-policies) voor meer informatie.

**Reactie**

Een geslaagde reactie retourneert de details van het bijgewerkte samenvoegingsbeleid.

```json
{
    "id": "e5bc94de-cd14-4cdf-a2bc-88b6e8cbfac2",
    "name": "Loyalty members ordered by ID",
    "imsOrgId": "{ORG_ID}",
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

Een samenvoegingsbeleid kan worden geschrapt door een DELETE- verzoek aan het `/config/mergePolicies` eindpunt en met inbegrip van identiteitskaart van het fusiebeleid te doen dat u wenst om in de verzoekweg te schrappen.

>[!NOTE]
>
>Als het fusiebeleid `isActiveOnEdge` aan waar heeft, kan het fusiebeleid **niet** worden geschrapt. Gebruik of de [ PATCH ](#edit-individual-merge-policy-fields) of [ PUT ](#overwrite-a-merge-policy) eindpunten om het fusiebeleid bij te werken alvorens het te schrappen.

**API formaat**

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**Reactie**

Een succesvol verwijderingsverzoek retourneert HTTP Status 200 (OK) en een lege antwoordinstantie. Om te bevestigen dat het verwijderen is gelukt, kunt u een GET-aanvraag uitvoeren om het samenvoegbeleid met de bijbehorende id weer te geven. Als het samenvoegbeleid is verwijderd, ontvangt u een HTTP Status 404 (Not Found)-fout.

## Volgende stappen

Nu u weet hoe u samenvoegbeleid voor uw organisatie kunt maken en configureren, kunt u deze gebruiken om de weergave van klantprofielen in Experience Platform aan te passen en om publiek te maken op basis van uw [!DNL Real-Time Customer Profile] -gegevens.

Gelieve te zien de [ documentatie van de Dienst van de Segmentatie van Adobe Experience Platform ](../../segmentation/home.md) beginnen bepalend en werkend met publiek.
