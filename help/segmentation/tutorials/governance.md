---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Compatibiliteit van gegevensgebruik voor publiekssegmenten afdwingen
topic: tutorial
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07

---


# Compatibiliteit met gegevensgebruik afdwingen voor een publiekssegment met behulp van API&#39;s

Deze zelfstudie behandelt de stappen voor het afdwingen van naleving van gegevensgebruik voor de publiekssegmenten van het Profiel van de Klant in real time die APIs gebruiken.

## Aan de slag

Voor deze zelfstudie is een goed begrip vereist van de volgende componenten van het Adobe Experience Platform:

- [Klantprofiel](../../profile/home.md)in realtime: Klantprofiel in realtime is een algemene opslag van opzoekeenheden en wordt gebruikt voor het beheer van XDM-gegevens (Experience Data Model) binnen het platform. Het profiel voegt gegevens over diverse activa van ondernemingsgegevens samen en verleent toegang tot die gegevens in een verenigde presentatie.
   - [Beleid](../../profile/api/merge-policies.md)voor samenvoegen: Regels die door het Profiel van de Klant in real time worden gebruikt om te bepalen welke gegevens in een verenigde mening onder bepaalde voorwaarden kunnen worden samengevoegd. Het beleid van de fusie kan voor de doeleinden van het Beleid van Gegevens worden gevormd.
- [Segmentatie](../home.md): Hoe het Profiel van de Klant in real time een grote groep individuen in de profielopslag in kleinere groepen verdeelt die gelijkaardige eigenschappen delen en op gelijkaardige wijze aan marketing strategieën zullen antwoorden.
- [Gegevensbeheer](../../data-governance/home.md): Het Beheer van gegevens verstrekt de infrastructuur voor het etiketteren en de handhaving van het gegevensgebruik (DULE), gebruikend de volgende componenten:
   - [Labels](../../data-governance/labels/user-guide.md)voor gegevensgebruik: Etiketten die worden gebruikt om gegevenssets en velden te beschrijven in termen van het gevoeligheidsniveau waarmee hun respectieve gegevens worden verwerkt.
   - [Beleid](../../data-governance/api/getting-started.md)voor gegevensgebruik: Configuraties die aangeven welke marketingacties zijn toegestaan op gegevens die zijn gecategoriseerd door bepaalde labels voor gegevensgebruik.

De volgende secties verstrekken extra informatie die u zult moeten weten om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze zelfstudie biedt voorbeeld-API-aanroepen om aan te tonen hoe uw verzoeken moeten worden opgemaakt. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Een samenvoegbeleid voor een segmentdefinitie zoeken

Dit werkschema begint door tot een bekend publiekssegment toegang te hebben. De segmenten die voor gebruik in het Profiel van de Klant in real time worden toegelaten bevatten een identiteitskaart van het fusiebeleid binnen hun segmentdefinitie. Dit samenvoegbeleid bevat informatie over welke datasets in het segment moeten worden omvat, die beurtelings om het even welke toepasselijke etiketten van het gegevensgebruik bevatten.

Gebruikend de [Segmentatie API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml), kunt u een segmentdefinitie door zijn identiteitskaart zoeken om zijn bijbehorend fusiebeleid te vinden.

**API-indeling**

```http
GET /segment/definitions/{SEGMENT_DEFINITION_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{SEGMENT_DEFINITION_ID}` | De id van de segmentdefinitie die u wilt opzoeken. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/segment/definitions/24379cae-726a-4987-b7b9-79c32cddb5c1 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert de details van de segmentdefinitie terug.

```json
{
    "id": "24379cae-726a-4987-b7b9-79c32cddb5c1",
    "schema": { 
        "name": "_xdm.context.profile"
    },
    "ttlInDays": 90,
    "imsOrgId": "{IMS_ORG}",
    "name": "Cart abandons in CA",
    "description": "",
    "expression": {
        "type": "PQL", 
        "format": "pql/text", 
        "value": "homeAddress.countryISO = 'US'"
    },
    "mergePolicyId": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "evaluationInfo": {
        "batch": {
            "enabled": true
        },
        "continuous": {
            "enabled": false
        },
        "synchronous": {
            "enabled": false
        }
    },
    "creationTime": 1556094486000,
    "updateEpoch": 1556094486000,
    "updateTime": 1556094486000
  }
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `mergePolicyId` | De id van het samenvoegbeleid dat voor de segmentdefinitie wordt gebruikt. Dit wordt in de volgende stap gebruikt. |

## Vind de brondatasets van het fusiebeleid

Het beleid van de fusie bevat informatie over hun brondatasets, die beurtelings DULE etiketten bevatten. U kunt de details van een fusiebeleid opzoeken door identiteitskaart van het fusiebeleid in een GET verzoek aan het Profiel API te verstrekken.

**API-indeling**

```http
GET /config/mergePolicies/{MERGE_POLICY_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{MERGE_POLICY_ID}` | De id van het samenvoegbeleid dat in de [vorige stap](#lookup-a-merge-policy-for-a-segment-definition)is verkregen. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/config/mergePolicies/2b43d78d-0ad4-4c1e-ac2d-574c09b01119 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie retourneert de details van het samenvoegbeleid.

```json
{
    "id": "2b43d78d-0ad4-4c1e-ac2d-574c09b01119",
    "imsOrgId": "{IMS_ORG}",
    "schema": {
        "name": "_xdm.context.profile"
    },
    "version": 1,
    "identityGraph": {
        "type": "none"
    },
    "attributeMerge": {
        "type":"dataSetPrecedence", 
        "data": {
            "order" : ["5b95b155419ec801e6eee780", "5b7c86968f7b6501e21ba9df"]
        }
    },
    "default": false,
    "updateEpoch": 1551127597
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `schema.name` | De naam van het schema verbonden aan het fusiebeleid. |
| `attributeMerge.type` | Het configuratietype van de gegevensbelangrijkheid voor het samenvoegbeleid. Als de waarde is `dataSetPrecedence`, zijn de datasets verbonden aan dit fusiebeleid vermeld onder `attributeMerge > data > order`. Als de waarde is `timestampOrdered`, dan worden alle datasets verbonden aan het schema binnen van verwijzingen voorzien `schema.name` gebruikt door het fusiebeleid. |
| `attributeMerge.data.order` | Als `attributeMerge.type` is `dataSetPrecedence`, zal dit attribuut een serie die IDs van de datasets bevatten door dit fusiebeleid wordt gebruikt. Deze id&#39;s worden in de volgende stap gebruikt. |

## De etiketten van het het gegevensgebruik van de opzoekopdracht voor de brondatasets

Zodra u IDs van de brondatasets van het fusiebeleid hebt verzameld, kunt u deze IDs gebruiken om de etiketten van het gegevensgebruik te zoeken die voor de datasets zelf en om het even welke specifieke gegevensgebieden worden gevormd die daarin.

De volgende vraag aan de [Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) van de Catalogus wint de etikettenvan het gegevensgebruik verbonden aan één enkele dataset door zijn identiteitskaart in de verzoekweg te verstrekken terug:

**API-indeling**

```http
GET /dataSets/{DATASET_ID}/dule
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{DATASET_ID}` | Identiteitskaart van de dataset waarvan de etiketten van het gegevensgebruik u wilt opzoeken. |

**Verzoek**

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5b95b155419ec801e6eee780/dule \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een lijst van de etiketten van het gegevensgebruik verbonden aan de dataset als geheel, en om het even welke bepaalde gegevensgebieden verbonden aan het bronschema terug.

```json
{
    "connection": {},
    "dataset": {
        "identity": [],
        "contract": [
            "C3"
        ],
        "sensitive": [],
        "contracts": [
            "C3"
        ],
        "identifiability": [],
        "specialTypes": []
    },
    "fields": [],
    "schemaFields": [
        {
            "path": "/properties/personalEmail/properties/address",
            "identity": [
                "I1"
            ],
            "contract": [
                "C2",
                "C9"
            ],
            "sensitive": [],
            "contracts": [
                "C2",
                "C9"
            ],
            "identifiability": [
                "I1"
            ],
            "specialTypes": []
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `dataset` | Een object dat de labels voor gegevensgebruik bevat die op de gegevensset als geheel zijn toegepast. |
| `schemaFields` | Een array met objecten die specifieke schemavelden vertegenwoordigen waarop labels voor gegevensgebruik zijn toegepast. |
| `schemaFields.path` | Het pad van het schemaveld waarvan de labels voor gegevensgebruik in hetzelfde object worden vermeld. |

## Gegevensvelden filteren

>[!NOTE] Deze stap is optioneel. Als u de gegevens in uw segment niet wilt aanpassen op basis van uw bevindingen in de vorige stap van het [opzoeken van labels](#lookup-data-usage-labels-for-the-source-datasets)voor gegevensgebruik, kunt u verdergaan met de laatste stap van het [evalueren van de gegevens voor beleidsovertredingen](#evaluate-data-for-policy-violations).

Als u wenst om de gegevens aan te passen inbegrepen in uw publiekssegment, kunt u dit doen gebruikend één van de volgende twee methodes:

### Het samenvoegbeleid van de segmentdefinitie bijwerken

Het bijwerken van het samenvoegbeleid van een segmentdefinitie zal de datasets en de gebieden aanpassen die zullen worden omvat wanneer de segmentbaan in werking wordt gesteld. Zie de sectie over het [bijwerken van een bestaand samenvoegingsbeleid](../../profile/api/merge-policies.md) in de zelfstudie van het fusiebeleid voor meer informatie.

### Specifieke gegevensvelden beperken bij het exporteren van het segment

Wanneer u een segment naar een dataset exporteert met de Real-Time Customer Profile API, kunt u de gegevens die in de exportbewerking zijn opgenomen, filteren met de `fields` parameter. Alle gegevensvelden die aan deze parameter worden toegevoegd, worden in de exportbewerking opgenomen, terwijl alle andere gegevensvelden worden uitgesloten.

Neem bijvoorbeeld een segment met gegevensvelden met de naam &quot;A&quot;, &quot;B&quot; en &quot;C&quot;. Als u alleen veld C wilt exporteren, bevat de `fields` parameter alleen veld C. Op deze manier worden de velden A en B bij het exporteren van het segment uitgesloten.

Zie de sectie over het [exporteren van een segment](./evaluate-a-segment.md#export-a-segment) in de segmentatiezelfstudie voor meer informatie.

## Gegevens evalueren voor beleidsovertredingen

Nu u de etiketten van het gegevensgebruik verbonden aan uw publiekssegment hebt verzameld, kunt u deze etiketten tegen marketing acties testen om voor om het even welke schendingen van het beleid van het gegevensgebruik te evalueren. Voor gedetailleerde stappen op hoe te om beleidsevaluaties uit te voeren gebruikend de [DULE Dienst API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)van het Beleid, zie het document over [beleidsevaluatie](../../data-governance/enforcement/overview.md).

## Volgende stappen

Door deze zelfstudie te volgen, hebt u de labels van het gegevensgebruik verbonden aan een publiekssegment opgezocht en hen getest voor beleidsschendingen tegen specifieke marketing acties. Zie het overzicht [van](../../data-governance/home.md)gegevensbeheer voor meer informatie over Data Governance in Experience Platform.