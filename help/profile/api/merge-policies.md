---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
title: Beleid voor samenvoegen - Real-time klantprofiel-API
topic: guide
translation-type: tm+mt
source-git-commit: 47c65ef5bdd083c2e57254189bb4a1f1d9c23ccc
workflow-type: tm+mt
source-wordcount: '2458'
ht-degree: 0%

---


# Het eindpunt van beleid samenvoegen

Met Adobe Experience Platform kunt u gegevensfragmenten uit meerdere bronnen samenvoegen en combineren om een volledig beeld van elk van uw individuele klanten te krijgen. Wanneer het brengen van deze gegevens samen, zijn het fusiebeleid de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen.

Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken. Wanneer de gegevens van veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl de andere klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het fusiebeleid welke informatie om in het profiel voor het individu te omvatten.

Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Deze handleiding bevat stappen voor het werken met de API voor samenvoegbeleid.

Om met samenvoegbeleid te werken gebruikend UI, gelieve te verwijzen naar de de gebruikersgids [van het](../ui/merge-policies.md)fusiebeleid.

## Aan de slag

Het API-eindpunt dat in deze handleiding wordt gebruikt, maakt deel uit van de [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)handleiding. Lees voordat u verdergaat de gids [Aan de](getting-started.md) slag voor koppelingen naar gerelateerde documentatie, een handleiding voor het lezen van de voorbeeld-API-aanroepen in dit document en belangrijke informatie over vereiste headers die nodig zijn om aanroepen naar een willekeurige [!DNL Experience Platform] API mogelijk te maken.

## Componenten van samenvoegingsbeleid {#components-of-merge-policies}

Het beleid van de fusie is privé aan uw organisatie IMS, toestaand u om verschillende beleid tot stand te brengen om schema&#39;s op de specifieke manier samen te voegen die u nodig hebt. Om het even welke API die tot [!DNL Profile] gegevens toegang hebben vereist een fusiebeleid, hoewel een gebrek zal worden gebruikt als niet uitdrukkelijk wordt verstrekt. [!DNL Platform] verstrekt een standaardsamenvoegbeleid, of u kunt een fusiebeleid voor een specifiek schema tot stand brengen en het merken als gebrek voor uw organisatie. Elke organisatie kan veelvoudige samenvoegingsbeleid per schema potentieel hebben, nochtans kan elk schema slechts één standaardsamenvoegbeleid hebben. Om het even welk die samenvoegbeleid als gebrek wordt geplaatst zal worden gebruikt in gevallen waar de schemanaam wordt verstrekt en een fusiebeleid wordt vereist maar niet verstrekt. Wanneer u een samenvoegbeleid als gebrek plaatst, zal om het even welk bestaand samenvoegbeleid dat eerder als gebrek werd geplaatst automatisch worden bijgewerkt om niet meer als gebrek te worden gebruikt.

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
        "default": "{BOOLEAN}",
        "updateEpoch": "{UPDATE_TIME}"
    }
```

| Eigenschap | Beschrijving |
|---|---|
| `id` | Door het systeem gegenereerde unieke id die tijdens het maken is toegewezen |
| `name` | Vriendelijke naam waarmee het samenvoegbeleid kan worden geïdentificeerd in lijstweergaven. |
| `imsOrgId` | Organisatie-id waartoe dit samenvoegbeleid behoort |
| `identityGraph` | [Object in identiteitsgrafiek](#identity-graph) dat de identiteitsgrafiek aangeeft waarvan gerelateerde identiteiten worden verkregen. Profielfragmenten die voor alle verwante identiteiten worden gevonden, worden samengevoegd. |
| `attributeMerge` | [Kenmerksamenvoegobject](#attribute-merge) dat aangeeft op welke manier in het samenvoegbeleid de profielkenmerken voorrang krijgen bij gegevensconflicten. |
| `schema` | Het [schemaobject](#schema) waarop het samenvoegbeleid kan worden gebruikt. |
| `default` | Een Booleaanse waarde die aangeeft of dit samenvoegbeleid de standaardinstelling is voor het opgegeven schema. |
| `version` | [!DNL Platform] onderhouden versie van samenvoegingsbeleid. Deze alleen-lezen waarde wordt verhoogd wanneer een samenvoegbeleid wordt bijgewerkt. |
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

[Adobe Experience Platform Identity Service](../../identity-service/home.md) beheert de identiteitsgrafieken die globaal en voor elke organisatie op worden gebruikt [!DNL Experience Platform]. Het `identityGraph` attribuut van het fusiebeleid bepaalt hoe te om de verwante identiteiten voor een gebruiker te bepalen.

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

Een profielfragment is de profielinformatie voor slechts één identiteit uit de lijst van identiteiten die voor een bepaalde gebruiker bestaan. Wanneer het gebruikte type identiteitsgrafiek meer dan één identiteit resulteert, is er een potentieel voor conflicterende profielattributen en de prioriteit moet worden gespecificeerd. Met `attributeMerge`behulp van deze optie kunt u opgeven welke profielkenmerken prioriteit moeten krijgen in geval van een samenvoegconflict tussen de gegevenssets van het type Key Value (recordgegevens).

**Object attributeMerge**

```json
    "attributeMerge": {
        "type": "{ATTRIBUTE_MERGE_TYPE}"
    }
```

Waar `{ATTRIBUTE_MERGE_TYPE}` is een van de volgende:

* **`timestampOrdered`**: (standaardwaarde) Geef prioriteit aan het profiel dat het laatst is bijgewerkt. Met dit samenvoegtype is het `data` kenmerk niet vereist. `timestampOrdered` ondersteunt ook aangepaste tijdstempels die voorrang hebben bij het samenvoegen van profielfragmenten binnen of tussen gegevenssets. Zie de sectie Bijlage over het [gebruik van aangepaste tijdstempels](#custom-timestamps)voor meer informatie.
* **`dataSetPrecedence`** : Geef voorrang aan profielfragmenten die op de dataset worden gebaseerd waaruit zij kwamen. Dit zou kunnen worden gebruikt wanneer de informatie aanwezig in één dataset over gegevens in een andere dataset wordt aangewezen of wordt vertrouwd. Wanneer het gebruiken van dit fusietype, wordt het `order` attribuut vereist, aangezien het van de datasets in de orde van prioriteit een lijst maakt.
   * **`order`**: Wanneer &quot;dataSetPrecedence&quot; wordt gebruikt, moet een `order` array worden voorzien van een lijst met gegevenssets. Gegevenssets die niet in de lijst zijn opgenomen, worden niet samengevoegd. Met andere woorden, gegevenssets moeten expliciet worden vermeld om te worden samengevoegd in een profiel. De `order` array bevat de id&#39;s van de gegevenssets in volgorde van prioriteit.

**Object ExampleMerge met `dataSetPrecedence` type**

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

**Object ExampleMerge met `timestampOrdered` type**

```json
    "attributeMerge": {
        "type": "timestampOrdered"
    }
```

### Schema {#schema}

Het schemavoorwerp specificeert het schema van de Gegevens van de Ervaring (XDM) waarvoor dit fusiebeleid wordt gecreeerd.

**`schema`object**

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

Om meer over XDM en het werken met schema&#39;s in Experience Platform te leren, begin door het overzicht [van het Systeem te lezen](../../xdm/home.md)XDM.

## Beleid voor samenvoegen openen {#access-merge-policies}

Gebruikend [!DNL Real-time Customer Profile] API, staat het `/config/mergePolicies` eindpunt u toe een raadplegingsverzoek om een specifiek fusiebeleid door zijn identiteitskaart uit te voeren, of toegang tot elk van het fusiebeleid in uw IMS Organisatie, die door specifieke criteria wordt gefiltreerd. U kunt het `/config/mergePolicies/bulk-get` eindpunt ook gebruiken om veelvoudige fusiebeleid door hun IDs terug te winnen. De stappen voor het uitvoeren van elk van deze vraag worden geschetst in de volgende secties.

### Heb toegang tot één enkel fusiebeleid door identiteitskaart

U kunt tot één enkel fusiebeleid door zijn identiteitskaart toegang hebben door een verzoek van de GET tot het `/config/mergePolicies` eindpunt en met inbegrip van `mergePolicyId` in de verzoekweg te richten.

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

### Hiermee worden meerdere samenvoegbeleidsregels via de id&#39;s opgehaald

U kunt veelvoudige fusiebeleid terugwinnen door een verzoek van de POST aan het `/config/mergePolicies/bulk-get` eindpunt en met inbegrip van identiteitskaarts van het fusiebeleid te doen u in het verzoeklichaam wenst terug te winnen.

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
            "default": false,
            "updateEpoch": 1576099719
        }
    }
}
```

Zie de [componenten van de sectie van het samenvoegingsbeleid](#components-of-merge-policies) aan het begin van dit document voor details op elk van de individuele elementen die omhoog een fusiebeleid maken.

### Meerdere vormen van samenvoegingsbeleid weergeven op basis van criteria

U kunt van veelvoudige fusiebeleid binnen uw IMS Organisatie een lijst maken door een verzoek van de GET aan het `/config/mergePolicies` eindpunt uit te geven en facultatieve vraagparameters te gebruiken om, de reactie te filtreren te orde te geven en te pagineren. U kunt meerdere parameters opnemen, gescheiden door ampersands (&amp;). Het maken van een vraag aan dit eindpunt zonder parameters zal al samenvoegbeleid beschikbaar voor uw organisatie terugwinnen.

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

U kunt een nieuw fusiebeleid voor uw organisatie tot stand brengen door een verzoek van de POST aan het `/config/mergePolicies` eindpunt te doen.

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

U kunt individuele gebieden voor een samenvoegbeleid uitgeven door een verzoek van PATCH aan het `/config/mergePolicies/{mergePolicyId}` eindpunt te doen:

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
| `op` | Geeft de bewerking aan die moet worden uitgevoerd. Voorbeelden van andere PATCH-bewerkingen vindt u in de documentatie bij [JSON-patch](http://jsonpatch.com) |
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

Een fusiebeleid kan worden geschrapt door een verzoek van de DELETE aan het `/config/mergePolicies` eindpunt en met inbegrip van identiteitskaart van het fusiebeleid te doen dat u wenst om in de verzoekweg te schrappen.

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

Nu u weet om samenvoegbeleid voor uw IMS Organisatie tot stand te brengen en te vormen, kunt u hen gebruiken om publiekssegmenten van uw [!DNL Real-time Customer Profile] gegevens tot stand te brengen. Raadpleeg de documentatie [van de](../../segmentation/home.md) Adobe Experience Platform Segmentation Service om te beginnen met het definiëren en werken met segmenten.

## Aanhangsel

Deze sectie verstrekt extra informatie met betrekking tot het werken met fusiebeleid.

### Aangepaste tijdstempels gebruiken {#custom-timestamps}

Wanneer records in het Experience Platform worden opgenomen, wordt een systeemtijdstempel opgehaald op het moment van inname en aan de record toegevoegd. Wanneer `timestampOrdered` is geselecteerd als het `attributeMerge` type voor een samenvoegbeleid, worden profielen samengevoegd op basis van de tijdstempel van het systeem. Met andere woorden, het samenvoegen wordt uitgevoerd op basis van de tijdstempel voor het tijdstip waarop de record in het Platform is opgenomen.

Er kunnen soms gebruiksgevallen zijn, zoals het terugvullen van gegevens of het verzekeren van de correcte orde van gebeurtenissen als de verslagen uit orde worden opgenomen, waar het noodzakelijk is om een douantimestamp te leveren en het fusiebeleid te hebben de douane timestamp eerder dan de systeemtimestamp respecteren.

Als u een aangepaste tijdstempel wilt gebruiken, [[!DNL External Source System Audit Details Mixin]](#mixin-details) moet u deze toevoegen aan het profielschema. Nadat u de aangepaste tijdstempel hebt toegevoegd, kunt u deze in het `xdm:lastUpdatedDate` veld vullen. Wanneer een verslag met het bevolkte `xdm:lastUpdatedDate` gebied wordt opgenomen, zal het Experience Platform dat gebied gebruiken om verslagen of profielfragmenten binnen en over datasets samen te voegen. Als `xdm:lastUpdatedDate` het Platform niet aanwezig of niet gevuld is, blijft het de tijdstempel van het systeem gebruiken.

>[!NOTE]
>
>U moet ervoor zorgen dat de `xdm:lastUpdatedDate` tijdstempel wordt gevuld wanneer u een PATCH in dezelfde record verzendt.

Voor geleidelijke instructies bij het werken met schema&#39;s die de Registratie API van het Schema gebruiken, met inbegrip van hoe te om mengelingen aan schema&#39;s toe te voegen, te bezoeken gelieve de [zelfstudie voor het creëren van een schema gebruikend API](../../xdm/tutorials/create-schema-api.md).

Als u met aangepaste tijdstempels wilt werken met de gebruikersinterface, raadpleegt u de sectie over het [gebruik van aangepaste tijdstempels](../ui/merge-policies.md#custom-timestamps) in de gebruikershandleiding [voor](../ui/merge-policies.md)samenvoegingsbeleid.

#### [!DNL External Source System Audit Details Mixin] details {#mixin-details}

In het volgende voorbeeld worden correct gevulde velden in de [!DNL External Source System Audit Details Mixin]map weergegeven. De volledige mix JSON kan ook in het [openbare Model van de Gegevens van de Ervaring (XDM) repo](https://github.com/adobe/xdm/blob/master/components/mixins/shared/external-source-system-audit-details.schema.json) op GitHub worden bekeken.

```json
{
  "xdm:createdBy": "{CREATED_BY}",
  "xdm:createdDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastUpdatedBy": "{LAST_UPDATED_BY}",
  "xdm:lastUpdatedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastActivityDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastReferencedDate": "2018-01-02T15:52:25+00:00",
  "xdm:lastViewedDate": "2018-01-02T15:52:25+00:00"
 }
```




