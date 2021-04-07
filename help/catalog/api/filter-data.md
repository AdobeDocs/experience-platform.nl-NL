---
keywords: Experience Platform;home;populaire onderwerpen;filter;Filter;filtergegevens;Filter gegevens;Datumbereik
solution: Experience Platform
title: Catalogusgegevens filteren met zoekopdrachtparameters
topic: ontwikkelaarsgids
description: De dienst API van de Catalogus staat reactiegegevens toe om door het gebruik van de parameters van de verzoekvraag worden gefiltreerd. Een deel van beste praktijken voor Catalog is filters in alle API vraag te gebruiken, aangezien zij de lading op API verminderen en helpen algemene prestaties verbeteren.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 0%

---

# Gegevens [!DNL Catalog] filteren met behulp van queryparameters

Met de API [!DNL Catalog Service] kunnen responsgegevens worden gefilterd met behulp van aanvraagqueryparameters. Een deel van beste praktijken voor [!DNL Catalog] is filters in alle API vraag te gebruiken, aangezien zij de lading op API verminderen en helpen algemene prestaties verbeteren.

In dit document worden de meest gebruikte methoden beschreven voor het filteren van [!DNL Catalog]-objecten in de API. Het wordt aanbevolen naar dit document te verwijzen terwijl u de [Handleiding voor ontwikkelaars van catalogi](getting-started.md) leest voor meer informatie over hoe u met de [!DNL Catalog]-API werkt. Voor meer algemene informatie over [!DNL Catalog Service], zie [[!DNL Catalog] overzicht](../home.md).

## Teruggestuurde objecten beperken

Met de queryparameter `limit` beperkt u het aantal objecten dat in een reactie wordt geretourneerd. [!DNL Catalog] de reacties worden automatisch gemeten volgens geconfigureerde limieten:

* Als er geen parameter `limit` is opgegeven, is het maximumaantal objecten per antwoordlading 20.
* Voor datasetvragen, als `observableSchema` wordt gevraagd gebruikend de `properties` vraagparameter, is het maximumaantal teruggekeerde datasets 20.
* De algemene limiet voor alle andere catalogusquery&#39;s is 100 objecten.
* Ongeldige `limit` parameters (inclusief `limit=0`) resulteren in foutreacties op 400-niveau die een overzicht van juiste bereiken geven.
* Limieten of verschuivingen die worden doorgegeven als queryparameters hebben voorrang op parameters die als kopteksten worden doorgegeven.

**API-indeling**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden opgehaald. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{LIMIT}` | Een geheel getal dat het aantal objecten aangeeft dat moet worden geretourneerd, van 1 tot en met 100. |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terwijl het beperken van de reactie op drie voorwerpen terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van datasets terug, die tot het aantal wordt beperkt door de `limit` vraagparameter wordt vermeld.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSets/5ba9452f7de80400007fc52a/views/5ba9452f7de80400007fc52b/files"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSets/5bb276b03a14440000971552/views/5bb276b01250b012f9acc75b/files"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Weergegeven eigenschappen beperken

Zelfs wanneer het filtreren van het aantal voorwerpen teruggekeerd gebruikend de `limit` parameter, kunnen de teruggekeerde voorwerpen zelf vaak meer informatie bevatten dan u eigenlijk nodig hebt. Als u de belasting van het systeem verder wilt verminderen, kunt u het beste reacties filteren en alleen de gewenste eigenschappen opnemen.

Met de parameter `properties` worden objecten gefilterd om alleen een set opgegeven eigenschappen te retourneren. De parameter kan worden ingesteld om een of meerdere eigenschappen te retourneren.

De parameter `properties` accepteert alleen objecteigenschappen op hoofdniveau. Dit houdt in dat u voor het volgende voorbeeldobject filters kunt toepassen voor `name`, `description` en `subItem`, maar NIET voor `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API-indeling**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden opgehaald. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY}` | The name of an attribute to include in the response body. |
| `{OBJECT_ID}` | De unieke id van een specifiek [!DNL Catalog]-object dat wordt opgehaald. |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug. De komma-gescheiden lijst van bezitsnamen die onder de `properties` parameter worden verstrekt wijst op de eigenschappen die in de reactie moeten zijn teruggekeerd. Er wordt ook een `limit`-parameter opgenomen die het aantal geretourneerde gegevenssets beperkt. Als het verzoek geen parameter `limit` bevatte, zou de reactie een maximum van 20 voorwerpen bevatten.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie retourneert een lijst met [!DNL Catalog] objecten waarbij alleen de gevraagde eigenschappen worden weergegeven.

```json
{
    "Dataset1": {
        "name": "Dataset 1",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/bc82c518380478b59a95c63e0f843121",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "Dataset2": {},
    "Dataset3": {
        "name": {},
    },
    "Dataset4": {
        "name": "Dataset 4",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

Op basis van bovenstaande reactie kan het volgende worden afgeleid:

* Als een object gevraagde eigenschappen mist, worden alleen de gevraagde eigenschappen weergegeven die het bevat. (`Dataset1`)
* Als een object geen van de gevraagde eigenschappen bevat, wordt het weergegeven als een leeg object. (`Dataset2`)
* Een dataset kan een gevraagde bezit als leeg voorwerp terugkeren als het het bezit bevat maar er geen waarde is. (`Dataset3`)
* Anders, zal de dataset de volledige waarde van alle gevraagde eigenschappen tonen. (`Dataset4`)

>[!NOTE]
>
>In het `schemaRef` bezit voor elke dataset, wijst het versieaantal op de recentste minder belangrijke versie van het schema. Zie de sectie over [schemaversie](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie.

## Beginindex van verschuiving van reactielijst

Met de queryparameter `start` verschuift u de lijst met reacties met een opgegeven getal door op nul gebaseerde nummering te gebruiken. `start=2` verschuift bijvoorbeeld de reactie om te beginnen bij het derde vermelde object.

Als de parameter `start` niet met een `limit` parameter in paren wordt gebracht, is het maximumaantal teruggekeerde voorwerpen 20.

**API-indeling**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{OFFSET}` | Een geheel getal dat het aantal objecten aangeeft waarmee de reactie moet worden verschoven. |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug, die aan het vijfde voorwerp (`start=4`) compenseren en de reactie beperken tot twee teruggekeerde datasets (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie omvat een voorwerp JSON die twee top-level punten (`limit=2`) bevat, voor elke dataset en hun details (details zijn versmald in het voorbeeld). De respons wordt met vier (`start=4`) verschoven, wat betekent dat de getoonde datasets nummer vijf en zes chronologisch zijn.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filteren op tag

Sommige voorwerpen van de Catalogus steunen het gebruik van een `tags` attribuut. Tags kunnen informatie aan een object koppelen en later worden gebruikt om dat object op te halen. De keuze van de tags die u wilt gebruiken en hoe u deze wilt toepassen, is afhankelijk van uw organisatieprocessen.

Er zijn enkele beperkingen waarmee u rekening kunt houden wanneer u tags gebruikt:

* De enige voorwerpen van de Catalogus die momenteel markeringen steunen zijn datasets, partijen, en verbindingen.
* Tagnamen zijn uniek voor uw IMS-organisatie.
* Adobe-processen kunnen voor bepaalde gedragingen tags gebruiken. De namen van deze tags worden standaard voorafgegaan door &quot;adobe&quot;. Daarom moet u deze conventie vermijden bij het declareren van labelnamen.
* De volgende tagnamen zijn gereserveerd voor gebruik in [!DNL Experience Platform] en kunnen daarom niet worden gedeclareerd als een tagnaam voor uw organisatie:
   * `unifiedProfile`: Deze tagnaam is gereserveerd voor gegevenssets die moeten worden opgenomen door  [[!DNL Real-time Customer Profile]](../../profile/home.md).
   * `unifiedIdentity`: Deze tagnaam is gereserveerd voor gegevenssets die moeten worden opgenomen door  [[!DNL Identity Service]](../../identity-service/home.md).

Hieronder ziet u een voorbeeld van een gegevensset die een eigenschap `tags` bevat. De tags binnen die eigenschap hebben de vorm van sleutel-waardeparen, waarbij elke tagwaarde wordt weergegeven als een array met één tekenreeks:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{IMS_ORG}",
        "tags": {
            "sampleTag": [
                "123456"
            ],
            "secondTag": [
                "sample_tag_value"
            ]
        },
        "name": "Sample Dataset",
        "description": "Same dataset containing sample data.",
        "dule": {
            "identity": [
                "I1"
            ]
        },
        "statsCache": {},
        "state": "DRAFT",
        "lastBatchId": "ca12b29612bf4052872edad59573703c",
        "lastBatchStatus": "success",
        "lastSuccessfulBatch": "ca12b29612bf4052872edad59573703c",
        "namespace": "{NAMESPACE}",
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API-indeling**

Waarden voor de parameter `tags` hebben de vorm van sleutel-waardeparen, gebruikend het formaat `{TAG_NAME}:{TAG_VALUE}`. U kunt meerdere sleutelwaardeparen opgeven in de vorm van een door komma&#39;s gescheiden lijst. Wanneer veelvoudige markeringen worden verstrekt, wordt een EN verhouding verondersteld.

De parameter ondersteunt jokertekens (`*`) voor tagwaarden. Een zoektekenreeks van `test*` retourneert bijvoorbeeld een object waar de tagwaarde begint met &#39;test&#39;. Een zoektekenreeks die alleen uit een jokerteken bestaat, kan worden gebruikt om objecten te filteren op basis van het feit of ze een specifieke tag bevatten, ongeacht de waarde ervan.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden opgehaald. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | De naam van de tag waarop moet worden gefilterd. |
| `{TAG_VALUE}` | De waarde van de tag waarop moet worden gefilterd. Ondersteunt jokertekens (`*`). |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug, filtrerend door één markering die een specifieke waarde EN de tweede markering die aanwezig is.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie keert een lijst van datasets terug die `sampleTag` met een waarde van &quot;123456&quot;, EN `secondTag` met om het even welke waarde bevatten. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "Example tag value"
                ]
            },
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1533539550237,
            "updated": 1533539552416,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "tags": {
                "sampleTag": [
                    "123456"
                ],
                "secondTag": [
                    "A different tag value"
                ],
                "anotherTag": [
                    "2.0"
                ]
            },
            "dule": {},
            "statsCache": {}
    }
}
```

## Filteren op datumbereik

Sommige eindpunten in [!DNL Catalog] API hebben vraagparameters die voor gerangschikte vragen, het vaakst in het geval van data toestaan.

**API-indeling**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{TIMESTAMP }` | Een gegevenstijdgeheel getal in Unix Epoch-tijd. |

**Verzoek**

Met het volgende verzoek wordt een lijst opgehaald met batches die in de maand april 2019 zijn gemaakt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie bevat een lijst met [!DNL Catalog]-objecten die binnen het opgegeven datumbereik vallen. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{IMS_ORG}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Sorteren op eigenschap

Met de queryparameter `orderBy` kunt u (volgorde)antwoordgegevens sorteren op basis van een opgegeven eigenschapswaarde. Deze parameter vereist een &quot;richting&quot; (`asc` voor oplopend of `desc` voor aflopend), gevolgd door een dubbelpunt (`:`) en dan een bezit om de resultaten door te sorteren. Als er geen richting is opgegeven, wordt de standaardrichting oplopend.

U kunt meerdere sorteereigenschappen opgeven in een lijst met komma&#39;s als scheidingsteken. Als de eerste sorteereigenschap meerdere objecten produceert die dezelfde waarde voor die eigenschap bevatten, wordt de tweede sorteereigenschap gebruikt om die overeenkomende objecten verder te sorteren.

Neem bijvoorbeeld de volgende query: `orderBy=name,desc:created`. Resultaten worden in oplopende volgorde gesorteerd op basis van de eerste sorteereigenschap, `name`. Wanneer meerdere records dezelfde `name`-eigenschap delen, worden die overeenkomende records vervolgens gesorteerd op de tweede sorteereigenschap, `created`. Als geen teruggekeerde verslagen zelfde `name` delen, `created` het bezit niet in het sorteren van factor.


**API-indeling**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | De naam van een eigenschap waarop de resultaten moeten worden gesorteerd. |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug die door hun `name` bezit wordt gesorteerd. Als om het even welke datasets het zelfde `name` delen, zullen die datasets beurtelings door hun `updated` bezit in dalende orde worden bevolen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een geslaagde reactie bevat een lijst met [!DNL Catalog] objecten die zijn gesorteerd op basis van de parameter `orderBy`. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Filteren op eigenschap

[!DNL Catalog] biedt twee methoden voor filteren op eigenschap, die nader worden beschreven in de volgende secties:

* [Eenvoudige filters](#using-simple-filters) gebruiken: Filter op of een specifieke eigenschap overeenkomt met een specifieke waarde.
* [De parameter](#using-the-property-parameter) property gebruiken: Gebruik voorwaardelijke expressies om te filteren op basis van het feit of een eigenschap bestaat of als de waarde van een eigenschap overeenkomt met, benadert of vergelijkt met een andere opgegeven waarde of reguliere expressie.

### Eenvoudige filters gebruiken {#using-simple-filters}

Met eenvoudige filters kunt u reacties filteren op basis van specifieke eigenschapswaarden. Een eenvoudig filter heeft de vorm van `{PROPERTY_NAME}={VALUE}`.

De query `name=exampleName` retourneert bijvoorbeeld alleen objecten waarvan de eigenschap `name` de waarde &quot;exampleName&quot; bevat. De query `name=!exampleName` retourneert daarentegen alleen objecten waarvan de eigenschap `name` **not** &quot;exampleName&quot; is.

Bovendien ondersteunen eenvoudige filters de mogelijkheid om te zoeken naar meerdere waarden voor één eigenschap. Wanneer er meerdere waarden zijn opgegeven, retourneert de reactie objecten waarvan de eigenschap overeenkomt met **any** van de waarden in de opgegeven lijst. U kunt een multiwaardevraag omkeren door een `!` karakter aan de lijst vooraf te bepalen, die slechts voorwerpen terugkeert de waarvan bezitswaarde **not** in de verstrekte lijst (bijvoorbeeld, `name=!exampleName,anotherName`) is.

**API-indeling**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden opgehaald. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{PROPERTY_NAME}` | De naam van de eigenschap waarop u wilt filteren. |
| `{VALUE}` | Een eigenschapwaarde die bepaalt welke resultaten moeten worden opgenomen (of uitgesloten, afhankelijk van de query). |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug, gefiltreerd om slechts datasets te omvatten de waarvan `name` bezit een waarde van &quot;exampleName&quot;of &quot;anotherName&quot;heeft.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie bevat een lijst met datasets, exclusief datasets waarvan `name` &quot;exampleName&quot; of &quot;anotherName&quot; is. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

### De parameter `property` {#using-the-property-parameter} gebruiken

De `property` vraagparameter verstrekt meer flexibiliteit voor op bezit-gebaseerd filtreren dan eenvoudige filters. Naast het filtreren gebaseerd op of een bezit een specifieke waarde heeft, kan de `property` parameter andere vergelijkingsexploitanten (zoals &quot;meer-dan&quot;(`>`) en &quot;minder-dan&quot;(`<`)) evenals regelmatige uitdrukkingen gebruiken om door bezitswaarden te filtreren. Het filter kan ook filteren op het al dan niet bestaan van een eigenschap, ongeacht de waarde ervan.

De parameter `property` accepteert alleen objecteigenschappen op hoofdniveau. Dit houdt in dat u voor het volgende voorbeeldobject op eigenschap kunt filteren voor `name`, `description` en `subItem`, maar NIET voor `sampleKey`.

```json
{
  "5ba9452f7de80400007fc52a": {
      "name": "Sample Dataset",
      "description": "Sample dataset containing important data",
      "subitem": {
          "sampleKey": "sampleValue"
      }
  }
}
```

**API-indeling**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type object dat moet worden opgehaald. [!DNL Catalog] Geldige objecten zijn: <ul><li>`accounts`</li><li>`batches`</li><li>`connections`</li><li>`connectors`</li><li>`dataSets`</li><li>`dataSetFiles`</li><li>`dataSetViews`</li></ul> |
| `{CONDITION}` | Een voorwaardelijke expressie die aangeeft voor welke eigenschap query moet worden uitgevoerd en hoe de waarde ervan moet worden geëvalueerd. Hieronder vindt u voorbeelden. |

De waarde van de parameter `property` ondersteunt verschillende soorten voorwaardelijke expressies. In de volgende tabel wordt de basissyntaxis voor ondersteunde expressies beschreven:

| Symbool(en) | Beschrijving | Voorbeeld |
| --- | --- | --- |
| (Geen) | Wanneer de eigenschapnaam wordt opgegeven zonder operator, worden alleen objecten geretourneerd waar de eigenschap bestaat, ongeacht de waarde ervan. | `property=name` |
| ! | Als u een &quot;`!`&quot; als voorvoegsel toevoegt aan de waarde van een `property`-parameter, worden alleen objecten geretourneerd waarvan de eigenschap **not** bestaat. | `property=!name` |
| ~ | Retourneert alleen objecten waarvan de eigenschapswaarden (tekenreeks) overeenkomen met een reguliere expressie die wordt opgegeven na het tilde (`~`)-symbool. | `property=name~^example` |
| == | Retourneert alleen objecten waarvan de eigenschapswaarden exact overeenkomen met de tekenreeks die wordt opgegeven na het symbool dubbelequals (`==`). | `property=name==exampleName` |
| != | Retourneert alleen objecten waarvan de eigenschapswaarden **niet** overeenkomen met de tekenreeks die wordt opgegeven na het symbool niet gelijk aan (`!=`). | `property=name!=exampleName` |
| &lt;> | Retourneert alleen objecten waarvan de eigenschapswaarden kleiner zijn dan (maar niet gelijk zijn aan) een opgegeven hoeveelheid. | `property=version<1.0.0` |
| &lt;> | Retourneert alleen objecten waarvan de eigenschapswaarden kleiner zijn dan (of gelijk zijn aan) een opgegeven hoeveelheid. | `property=version<=1.0.0` |
| > | Retourneert alleen objecten waarvan de eigenschapswaarden groter zijn dan (maar niet gelijk zijn aan) een opgegeven hoeveelheid. | `property=version>1.0.0` |
| >= | Retourneert alleen objecten waarvan de eigenschapswaarden groter zijn dan (of gelijk zijn aan) een opgegeven hoeveelheid. | `property=version>=1.0.0` |

>[!NOTE]
>
>De eigenschap `name` ondersteunt het gebruik van een jokerteken `*`, ofwel als de volledige zoektekenreeks ofwel als onderdeel ervan. Jokertekens komen overeen met lege tekens, zodat de zoektekenreeks `te*st` overeenkomt met de waarde &quot;test&quot;. Sterretjes worden gevrijwaard door ze te verdubbelen (`**`). Een dubbele asterisk in een zoektekenreeks staat voor één sterretje als letterlijke tekenreeks.

**Verzoek**

Het volgende verzoek zal om het even welke datasets met een versieaantal groter dan 1.0.3 terugkeren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

Een succesvolle reactie bevat een lijst met datasets waarvan de versienummers groter zijn dan 1.0.3. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{IMS_ORG}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{IMS_ORG}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{IMS_ORG}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
            "dule": {},
            "statsCache": {}
    }
}
```

## Meerdere filters combineren

Gebruikend ampersand (`&`), kunt u veelvoudige filters in één enkel verzoek combineren. Wanneer de extra voorwaarden aan een verzoek worden toegevoegd, EN verhouding wordt verondersteld.

**API-indeling**

```http
GET /{OBJECT_TYPE}?{FILTER_1}={VALUE}&{FILTER_2}={VALUE}&{FILTER_3}={VALUE}
```
