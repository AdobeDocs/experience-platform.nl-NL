---
keywords: Experience Platform;home;populaire onderwerpen;filter;Filter;filtergegevens;Filter gegevens;Filter gegevens;datumbereik
solution: Experience Platform
title: Catalogusgegevens filteren met zoekopdrachtparameters
description: Gebruik queryparameters om reactiegegevens te filteren in de Catalogusservice-API en alleen de informatie op te halen die u nodig hebt. Pas filters toe op uw API-aanroepen om de belasting te verminderen en de prestaties te verbeteren, zodat gegevens sneller en efficiënter kunnen worden opgehaald.
exl-id: 0cdb5a7e-527b-46be-9ad8-5337c8dc72b7
source-git-commit: 14ecb971af3f6cdcc605caa05ef6609ecb9b38fd
workflow-type: tm+mt
source-wordcount: '2339'
ht-degree: 0%

---

# [!DNL Catalog] -gegevens filteren met behulp van queryparameters

Als u de prestaties wilt verbeteren en relevante resultaten wilt ophalen, gebruikt u queryparameters om [!DNL Catalog Service] API-responsgegevens te filteren.

Leer meer over algemene filtermethoden voor [!DNL Catalog] -objecten in de API. Gebruik dit document naast de [ Gids van de Ontwikkelaar van de Catalogus ](getting-started.md) voor meer details op API interactie. Voor algemene [!DNL Catalog Service] informatie, zie het [[!DNL Catalog]  overzicht ](../home.md).

## Teruggestuurde objecten beperken {#limit-returned-objects}

De query-parameter `limit` beperkt het aantal objecten dat in een reactie wordt geretourneerd. [!DNL Catalog] reacties volgen vooraf gedefinieerde limieten:

* Wanneer de parameter `limit` niet is opgegeven, is het maximumaantal objecten per reactie 20.
* Als voor datasetquery&#39;s `observableSchema` wordt aangevraagd met de parameter `properties` query, is het maximale aantal geretourneerde datasets 20.
* Voor gebruikerstokens, is de maximumgrens 1.
* Voor de diensttokens, is de maximumgrens 20.
* De algemene limiet voor andere catalogusquery&#39;s is 100 objecten.
* Ongeldige `limit` -waarden (inclusief `limit=0` ) resulteren in foutreacties op 400-niveau die juiste bereiken opgeven.
* Beperkingen of verschuivingen die worden doorgegeven als queryparameters hebben voorrang op die in kopteksten.

**API formaat**

```http
GET /{OBJECT_TYPE}?limit={LIMIT}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{LIMIT}` | Een geheel getal dat aangeeft hoeveel objecten moeten worden geretourneerd (bereik: 1-100). |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terwijl het beperken van de reactie op drie voorwerpen terug.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie keert een lijst van datasets terug, die tot het aantal wordt beperkt door de `limit` vraagparameter wordt vermeld.

```json
{
    "5ba9452f7de80400007fc52a": {
        "name": "Sample Dataset 1",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5ba9452f7de80400007fc52a"
    },
    "5bb276b03a14440000971552": {
        "name": "Sample Dataset 2",
        "description": "Description of dataset.",
        "files": "@/dataSetFiles?dataSetId=5bb276b03a14440000971552"
    },
    "5bceaa4c26c115000039b24b": {
        "name": "Sample Dataset 3"
    }
}
```

## Weergegeven eigenschappen beperken {#limit-displayed-properties}

Zelfs bij het filteren van het aantal objecten dat wordt geretourneerd met de parameter `limit` , kunnen de geretourneerde objecten zelf vaak meer informatie bevatten dan u eigenlijk nodig hebt. Als u de belasting van het systeem verder wilt verminderen, kunt u het beste reacties filteren en alleen de gewenste eigenschappen opnemen.

De `properties` -parameterfilters reageren op objecten om alleen een set opgegeven eigenschappen te retourneren. De parameter kan worden ingesteld om een of meerdere eigenschappen te retourneren.

De parameter `properties` kan alle objecteigenschappen op niveau accepteren. `sampleKey` kan worden geëxtraheerd met `?properties=subItem.sampleKey` .

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

**API formaat**

```http
GET /{OBJECT_TYPE}?properties={PROPERTY}
GET /{OBJECT_TYPE}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
GET /{OBJECT_TYPE}/{OBJECT_ID}?properties={PROPERTY_1},{PROPERTY_2},{PROPERTY_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY}` | The name of an attribute to include in the response body. |
| `{OBJECT_ID}` | De unieke id van een specifiek [!DNL Catalog] -object dat wordt opgehaald. |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug. De door komma&#39;s gescheiden lijst met namen van eigenschappen die wordt geleverd onder de parameter `properties` geeft de eigenschappen aan die moeten worden geretourneerd in de reactie. Er wordt ook een parameter `limit` opgenomen die het aantal geretourneerde gegevenssets beperkt. Als de aanvraag geen parameter `limit` bevat, bevat de reactie maximaal 20 objecten.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?limit=4&properties=name,schemaRef' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord retourneert een lijst met [!DNL Catalog] -objecten waarbij alleen de gevraagde eigenschappen worden weergegeven.

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
>In het `schemaRef` bezit voor elke dataset, wijst het versieaantal op de recentste minder belangrijke versie van het schema. Zie de sectie over [ schema versioning ](../../xdm/api/getting-started.md#versioning) in de gids XDM API voor meer informatie.

## Beginindex van verschuiving van reactielijst {#offset-starting-index}

Met de query-parameter `start` verschuift u de lijst met reacties met een opgegeven getal door op nul gebaseerde nummering te gebruiken. `start=2` verschuift bijvoorbeeld de reactie naar het begin van het derde weergegeven object.

Wanneer de parameter `start` niet aan een parameter `limit` is gekoppeld, is het maximale aantal geretourneerde objecten 20.

**API formaat**

```http
GET /{OBJECT_TYPE}?start={OFFSET}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OFFSET}` | Een geheel getal dat het aantal objecten aangeeft waarmee de reactie moet worden verschoven. |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug, die aan het vijfde voorwerp (`start=4`) compenseren en de reactie beperken tot twee teruggekeerde datasets (`limit=2`).

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?start=4&limit=2 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

De reactie omvat een voorwerp JSON dat twee top-level punten (`limit=2`) bevat, voor elke dataset en hun details (details zijn versmald in het voorbeeld). De reactie wordt verschoven door vier (`start=4`), betekenend zijn de getoonde datasets aantal vijf en zes chronologisch.

```json
{
    "Dataset5": {},
    "Dataset6": {}
}
```

## Filteren op tag

Sommige catalogusobjecten ondersteunen het gebruik van een `tags` -kenmerk. Tags kunnen informatie aan een object koppelen en later worden gebruikt om dat object op te halen. De keuze van de tags die u wilt gebruiken en hoe u deze wilt toepassen, is afhankelijk van uw organisatieprocessen.

Er zijn enkele beperkingen waarmee u rekening kunt houden bij het gebruik van tags:

* De enige voorwerpen van de Catalogus die momenteel markeringen steunen zijn datasets, partijen, en verbindingen.
* Tagnamen zijn uniek voor uw organisatie.
* Adobe-processen kunnen tags voor bepaalde gedragingen gebruiken. De namen van deze tags worden standaard voorafgegaan door &quot;adobe&quot;. Daarom moet u deze conventie vermijden bij het declareren van labelnamen.
* De volgende tagnamen zijn gereserveerd voor gebruik in [!DNL Experience Platform] en kunnen daarom niet worden gedeclareerd als tagnaam voor uw organisatie:
   * `unifiedProfile`: Deze tagnaam is gereserveerd voor gegevenssets die door [[!DNL Real-Time Customer Profile]](../../profile/home.md) worden ingevoerd.
   * `unifiedIdentity`: Deze tagnaam is gereserveerd voor gegevenssets die door [[!DNL Identity Service]](../../identity-service/home.md) worden ingevoerd.

Hieronder ziet u een voorbeeld van een gegevensset die een eigenschap `tags` bevat. De tags binnen die eigenschap hebben de vorm van sleutel-waardeparen, waarbij elke tagwaarde wordt weergegeven als een array met één tekenreeks:

```json
{
    "5be1f2ecc73c1714ceba66e2": {
        "imsOrg": "{ORG_ID}",
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
        "createdUser": "{CREATED_USER}",
        "createdClient": "{CREATED_CLIENT}",
        "updatedUser": "{UPDATED_USER}",
        "version": "1.0.0",
        "created": 1541534444286,
        "updated": 1541534444286
    }
}
```

**API formaat**

Waarden voor de parameter `tags` hebben de vorm van sleutel-waardeparen, die het formaat `{TAG_NAME}:{TAG_VALUE}` gebruiken. U kunt meerdere sleutelwaardeparen opgeven in de vorm van een lijst met komma&#39;s als scheidingsteken. Wanneer veelvoudige markeringen worden verstrekt, wordt een EN verhouding verondersteld.

De parameter steunt vervangingskarakters (`*`) voor markeringswaarden. Een zoektekenreeks van `test*` retourneert bijvoorbeeld een object waar de tagwaarde begint met &#39;test&#39;. Een zoektekenreeks die alleen uit een jokerteken bestaat, kan worden gebruikt om objecten te filteren op basis van het feit of ze een specifieke tag bevatten, ongeacht de waarde ervan.

```http
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}
GET /{OBJECT_TYPE}?tags={TAG_NAME_1}:{TAG_VALUE_1},{TAG_NAME_2}:{TAG_VALUE_2}
GET /{OBJECT_TYPE}?tags={TAG_NAME}:{TAG_VALUE}*
GET /{OBJECT_TYPE}?tags={TAG_NAME}:*
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li></ul> |
| `{TAG_NAME}` | De naam van de tag waarop moet worden gefilterd. |
| `{TAG_VALUE}` | De waarde van de tag waarop moet worden gefilterd. Steunt vervangingskarakters (`*`). |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug, filtrerend door één markering die een specifieke waarde EN de tweede markering die aanwezig is.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?tags=sampleTag:123456,secondTag:* \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvol antwoord retourneert een lijst met gegevenssets die `sampleTag` met de waarde &quot;123456&quot; EN `secondTag` bevatten, met een willekeurige waarde. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
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
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
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
    }
}
```

## Filteren op datumbereik

Sommige eindpunten in de API van [!DNL Catalog] hebben vraagparameters die voor gerangschikte vragen, het vaakst in het geval van data toestaan.

**API formaat**

```http
GET /batches?createdAfter={TIMESTAMP_1}&createdBefore={TIMESTAMP_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{TIMESTAMP }` | Een geheel getal in tijd in Unix Epoch. |

**Verzoek**

Met het volgende verzoek wordt een lijst opgehaald met batches die in de maand april 2019 zijn gemaakt.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/batches?createdAfter=1554076800000&createdBefore=1556668799000' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie bevat een lijst met [!DNL Catalog] -objecten die binnen het opgegeven datumbereik vallen. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 1",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.0",
            "imsOrg": "{ORG_ID}",
            "name": "Example Dataset 2",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Sorteren op eigenschap

Met de parameter `orderBy` query kunt u reactiegegevens sorteren (ordenen) op basis van een opgegeven eigenschapswaarde. Deze parameter vereist een &quot;richting&quot; (`asc` voor het stijgen of `desc` voor het dalen), gevolgd door een dubbelepunt (`:`) en dan een bezit om de resultaten door te sorteren. Als er geen richting is opgegeven, wordt de standaardrichting oplopend.

U kunt meerdere sorteereigenschappen opgeven in een lijst met komma&#39;s als scheidingsteken. Als de eerste sorteereigenschap meerdere objecten produceert die dezelfde waarde voor die eigenschap bevatten, wordt de tweede sorteereigenschap gebruikt om die overeenkomende objecten verder te sorteren.

Neem bijvoorbeeld de volgende query: `orderBy=name,desc:created` . De resultaten worden in oplopende volgorde gesorteerd op basis van de eerste sorteereigenschap, `name` . Wanneer meerdere records dezelfde `name` -eigenschap delen, worden die overeenkomende records vervolgens gesorteerd op de tweede sorteereigenschap, `created` . Als geen geretourneerde records dezelfde `name` delen, wordt de sortering niet beïnvloed door de eigenschap `created` .


**API formaat**

```http
GET /{OBJECT_TYPE}?orderBy=asc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy=desc:{PROPERTY_NAME}
GET /{OBJECT_TYPE}?orderBy={PROPERTY_NAME_1},desc:{PROPERTY_NAME_2}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type Catalog-object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | De naam van een eigenschap waarop de resultaten moeten worden gesorteerd. |

**Verzoek**

Met het volgende verzoek wordt een lijst opgehaald met gegevenssets die zijn gesorteerd op hun eigenschap `name` . Als om het even welke datasets het zelfde `name` delen, zullen die datasets beurtelings door hun `updated` bezit in dalende orde worden bevolen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?orderBy=name,desc:updated' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie bevat een lijst met [!DNL Catalog] -objecten die worden gesorteerd op basis van de parameter `orderBy` . Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "0405",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "AAM Dataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Filteren op eigenschap

[!DNL Catalog] biedt twee methoden voor het filteren op eigenschap, die nader worden beschreven in de volgende secties:

* [ Gebruikend eenvoudige filters ](#using-simple-filters): Filter door of een specifiek bezit een specifieke waarde aanpast.
* [ Gebruikend de bezitsparameter ](#using-the-property-parameter): Gebruik voorwaardelijke uitdrukkingen aan filter gebaseerd of een bezit bestaat, of als de waarde van een bezit aanpast, benadert, of met een andere gespecificeerde waarde of regelmatige uitdrukking vergelijkt.

>[!NOTE]
>
>Om het even welk attribuut van een voorwerp van de Catalogus kan worden gebruikt om resultaten in de Dienst API van de Catalogus te filtreren.

### Eenvoudige filters gebruiken {#using-simple-filters}

Met eenvoudige filters kunt u reacties filteren op basis van specifieke eigenschapswaarden. Een eenvoudig filter heeft de vorm van `{PROPERTY_NAME}={VALUE}`.

De query `name=exampleName` retourneert bijvoorbeeld alleen objecten waarvan de eigenschap `name` de waarde &#39;exampleName&#39; bevat. Door contrast, keert de vraag `name=!exampleName` slechts voorwerpen terug het waarvan `name` bezit **niet** &quot;exampleName&quot; is.

Bovendien ondersteunen eenvoudige filters de mogelijkheid om te zoeken naar meerdere waarden voor één eigenschap. Wanneer de veelvoudige waarden worden verstrekt, keert de reactie voorwerpen terug het waarvan bezit **om het even welk** van de waarden in de verstrekte lijst aanpast. U kunt een multi-waardevraag omkeren door a `!` karakter aan de lijst vooraf te bepalen, terugkerend slechts voorwerpen de waarvan bezitswaarde **niet** in de verstrekte lijst is (bijvoorbeeld, `name=!exampleName,anotherName`).

**API formaat**

```http
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}={VALUE_1},{VALUE_2},{VALUE_3}
GET /{OBJECT_TYPE}?{PROPERTY_NAME}=!{VALUE_1},{VALUE_2},{VALUE_3}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{PROPERTY_NAME}` | De naam van de eigenschap waarop u wilt filteren. |
| `{VALUE}` | Een eigenschapwaarde die bepaalt welke resultaten moeten worden opgenomen (of uitgesloten, afhankelijk van de query). |

**Verzoek**

Het volgende verzoek wint een lijst van datasets terug, gefiltreerd om slechts datasets te omvatten de waarvan `name` bezit een waarde van &quot;exampleName&quot;of &quot;anotherName&quot;heeft.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/catalog/dataSets?name=exampleName,anotherName' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een geslaagde reactie bevat een lijst met gegevenssets, exclusief gegevenssets waarvan `name` &quot;exampleName&quot; of &quot;anotherName&quot; is. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.0.2",
            "imsOrg": "{ORG_ID}",
            "name": "exampleName",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.3",
            "imsOrg": "{ORG_ID}",
            "name": "anotherName",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

### De parameter `property` gebruiken {#using-the-property-parameter}

De query-parameter `property` biedt meer flexibiliteit voor op eigenschappen gebaseerde filtering dan eenvoudige filters. Naast het filtreren gebaseerd op of een bezit een specifieke waarde heeft, kan de `property` parameter andere vergelijkingsexploitanten (zoals &quot;meer-dan&quot; (`>`) en &quot;minder-dan&quot; (`<`)) evenals regelmatige uitdrukkingen gebruiken om door bezitswaarden te filtreren. Het kan ook filteren door of een eigenschap bestaat, ongeacht de waarde ervan.

Gebruik ampersand (`&`) om veelvoudige filters te combineren en uw vraag in één enkel verzoek te verfijnen. Wanneer u met meerdere velden filtert, wordt standaard een `AND` -relatie toegepast.

>[!NOTE]
>
>Als u meerdere `property` -parameters in één query combineert, moet ten minste één parameter van toepassing zijn op het veld `id` of `created` . De volgende vraag keert voorwerpen terug waar `id` `abc123` **EN** `name` niet `test` is:
>
>```http
>GET /datasets?property=id==abc123&property=name!=test
>```

Wanneer u meerdere `property` -parameters in hetzelfde veld gebruikt, wordt alleen de laatst opgegeven parameter van kracht.

>[!IMPORTANT]
>
>U **kunt niet** één enkele `property` parameter gebruiken om veelvoudige gebieden in één keer te filtreren. Elk veld moet een eigen `property` -parameter hebben. Het volgende voorbeeld (`property=id>abc,name==myDataset`) wordt **niet** toegestaan omdat het probeert om voorwaarden op `id` en `name` binnen a **enige `property` parameter** toe te passen.

De parameter `property` kan alle objecteigenschappen op niveau accepteren. `sampleKey` kan worden gebruikt voor filtering met `?properties=subItem.sampleKey` .

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

**API formaat**

```http
GET /{OBJECT_TYPE}?property={CONDITION}
```

| Parameter | Beschrijving |
| --- | --- |
| `{OBJECT_TYPE}` | Het type [!DNL Catalog] -object dat moet worden opgehaald. Geldige objecten zijn: <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{CONDITION}` | Een voorwaardelijke expressie die aangeeft voor welke eigenschap query moet worden uitgevoerd en hoe de waarde ervan moet worden geëvalueerd. Hieronder vindt u voorbeelden. |

De waarde van de parameter `property` ondersteunt verschillende soorten voorwaardelijke expressies. In de volgende tabel wordt de basissyntaxis voor ondersteunde expressies beschreven:

| Symbool(en) | Beschrijving | Voorbeeld |
| --- | --- | --- |
| (Geen) | Wanneer de eigenschapnaam wordt opgegeven zonder operator, worden alleen objecten geretourneerd waar de eigenschap bestaat, ongeacht de waarde ervan. | `property=name` |
| ! | Het voorschrijven van &quot;`!`&quot;aan de waarde van a `property` parameter keert slechts voorwerpen terug waar het bezit **niet** bestaat. | `property=!name` |
| ~ | Retourneert alleen objecten waarvan de eigenschapswaarden (tekenreeks) overeenkomen met een reguliere expressie die wordt opgegeven na het tilde-symbool (`~`). | `property=name~^example` |
| == | Retourneert alleen objecten waarvan de eigenschapswaarden exact overeenkomen met de tekenreeks die wordt opgegeven na het symbool double-equals (`==`). | `property=name==exampleName` |
| != | Keert slechts voorwerpen terug de waarvan bezitswaarden **niet** koord aanpassen dat na het symbool niet-evenaart (`!=`) wordt verstrekt. | `property=name!=exampleName` |
| &lt; | Retourneert alleen objecten waarvan de eigenschapswaarden kleiner zijn dan (maar niet gelijk zijn aan) een opgegeven hoeveelheid. | `property=version<1.0.0` |
| &lt;= | Retourneert alleen objecten waarvan de eigenschapswaarden kleiner zijn dan (of gelijk zijn aan) een opgegeven hoeveelheid. | `property=version<=1.0.0` |
| > | Retourneert alleen objecten waarvan de eigenschapswaarden groter zijn dan (maar niet gelijk zijn aan) een opgegeven hoeveelheid. | `property=version>1.0.0` |
| >= | Retourneert alleen objecten waarvan de eigenschapswaarden groter zijn dan (of gelijk zijn aan) een opgegeven hoeveelheid. | `property=version>=1.0.0` |
| * | Een jokerteken is van toepassing op elke tekenreekseigenschap en komt overeen met een willekeurige reeks tekens. Gebruik `**` om een letterlijk sterretje te verwijderen. | `property=name==te*st` |
| &amp; | Combineert meerdere `property` -parameters met een `AND` -relatie tussen deze parameters. | `property=id==abc&property=name!=test` |

>[!NOTE]
>
>De eigenschap `name` ondersteunt het gebruik van een jokerteken `*` als de volledige zoektekenreeks of als onderdeel ervan. Jokertekens komen overeen met lege tekens, zodat de zoektekenreeks `te*st` overeenkomt met de waarde &#39;test&#39;. Sterretjes worden voorkomen door ze te verdubbelen (`**`). Een dubbele asterisk in een zoektekenreeks staat voor één sterretje als letterlijke tekenreeks.

**Verzoek**

Het volgende verzoek zal om het even welke datasets met een versieaantal groter dan 1.0.3 terugkeren.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/catalog/dataSets?property=version>1.0.3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Reactie**

Een succesvolle reactie bevat een lijst met datasets waarvan de versienummers groter zijn dan 1.0.3. Tenzij ook een limiet is opgegeven, bevat het antwoord maximaal 20 objecten.

```json
{
    "5b67f4dd9f6e710000ea9da4": {
            "version": "1.1.2",
            "imsOrg": "{ORG_ID}",
            "name": "sampleDataset",
            "created": 1554930967705,
            "updated": 1554931119718,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5b1e3c867e6d2600003d5b49": {
            "version": "1.0.6",
            "imsOrg": "{ORG_ID}",
            "name": "exampleDataset",
            "created": 1554974386247,
            "updated": 1554974386268,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    },
    "5cd3a129ec106214b722a939": {
            "version": "1.0.4",
            "imsOrg": "{ORG_ID}",
            "name": "anotherDataset",
            "created": 1554028394852,
            "updated": 1554130582960,
            "createdClient": "{API_KEY}",
            "createdUser": "{USER_ID}",
            "updatedUser": "{USER_ID}",
    }
}
```

## Arrays filteren met de parameter property {#filter-arrays}

Gebruik gelijkheids- en ongelijkheidsoperatoren om specifieke waarden op te nemen of uit te sluiten bij het filteren van resultaten op basis van array-eigenschappen.

### Gelijkheidsfilters {#equality-filters}

Als u een arrayveld met meerdere waarden wilt filteren, gebruikt u voor elke waarde afzonderlijke eigenschapparameters. Gebruik gelijkheidsfilters om alleen de items in de arraygegevens te retourneren die overeenkomen met de opgegeven waarden.

>[!NOTE]
>
>Het vereiste om `id` of `created` te omvatten wanneer het filtreren van veelvoudige gebieden **&#x200B;**&#x200B;is niet van toepassing wanneer het filtreren van veelvoudige waarden binnen een seriegebied.

De voorbeeldquery hieronder geeft alleen resultaten van de array die zowel `val1` als `val2` bevat.

**API formaat**

```http
GET /{OBJECT_TYPE}?property=arrayField=val1&property=arrayField=val2
```

### Onkwaliteitsfilters {#inequality-filters}

Gebruik ongelijkheidsoperatoren (`!=`) op een arrayveld om items in de gegevens uit te sluiten waar de array de opgegeven waarden bevat.

**API formaat**

```http
GET /{OBJECT_TYPE}?property=arrayField!=val1&property=arrayField!=val2
```

Deze query retourneert documenten waarin arrayField niet `val1` of `val2` bevat.

### Beperkingen van het filter Gelijkheid en ongelijkheid {#equality-inequality-limitations}

U kunt niet zowel gelijkheid (`=`) als ongelijkheid (`!=`) op het zelfde gebied in één enkele vraag toepassen.
