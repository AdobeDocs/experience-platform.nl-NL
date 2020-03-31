---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: ETL-integratie maken
topic: overview
translation-type: tm+mt
source-git-commit: 4817162fe2b7cbf4ae4c1ed325db2af31da5b5d3

---


# ETL-integratie ontwikkelen voor Adobe Experience Platform

De ETL-integratiehandleiding bevat algemene stappen voor het maken van krachtige, veilige connectors voor het Experience Platform en het opnemen van gegevens in Platform.


- [Catalogus](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [Gegevenstoegang](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [Gegevensinname](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [API&#39;s voor verificatie en autorisatie](../tutorials/authentication.md)
- [Schema-register](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Deze handleiding bevat ook voorbeeld-API-aanroepen die moeten worden gebruikt bij het ontwerpen van een ETL-connector, met koppelingen naar documentatie waarin elke Experience Platform-service en het gebruik van de bijbehorende API nader worden beschreven.

Een steekproefintegratie is beschikbaar op GitHub via de Referentiecode [van de Integratie van het Ecosysteem van](https://github.com/adobe/acp-data-services-etl-reference) ETL onder de Vergunning van de Apache Versie 2.0.

## Workflow

Het volgende werkstroomdiagram biedt een overzicht op hoog niveau voor de integratie van componenten van het Adobe Experience Platform met een ETL-toepassing en -aansluiting.

![](images/etl.png)

## Adobe Experience Platform-componenten

Er zijn veelvoudige componenten van het Platform van de Ervaring betrokken bij ETL schakelaarintegratie. In de volgende lijst worden verschillende belangrijke componenten en functies beschreven:

- **Adobe Identity Management System (IMS)** - Biedt een framework voor verificatie voor Adobe-services.
- **IMS-organisatie** - een organisatie die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden.
- **IMS-gebruiker** - leden van een IMS-organisatie. De relatie Organisatie met gebruiker is veel te veel.
- **Sandbox** - Een virtuele partitie is één instantie Platform voor het ontwikkelen en ontwikkelen van toepassingen voor digitale ervaringen.
- **Gegevensdetectie** - Registreert de metagegevens van opgenomen en getransformeerde gegevens in het Experience Platform.
- **Gegevenstoegang** - Biedt gebruikers een interface om toegang te krijgen tot hun gegevens in Experience Platform.
- **Gegevensinname** - Past gegevens naar Experience Platform met API&#39;s voor gegevensinname.
- **Het Register** van het schema - bepaalt en slaat schema op dat de structuur van gegevens beschrijft die in het Platform van de Ervaring moeten worden gebruikt.

## Aan de slag met de API&#39;s van Experience Platform

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben om met succes vraag aan Platform APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../landing/troubleshooting.md#how-do-i-format-an-api-request) in de het oplossen van problemengids van het Platform van de Ervaring te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan Platform APIs te maken, moet u de [authentificatieleerprogramma](../tutorials/authentication.md)eerst voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen van het Experience Platform, zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in het ervaringsplatform zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE] Raadpleeg de documentatie bij het overzicht van de [sandbox voor meer informatie over sandboxen in Platform](../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Algemene gebruikersstroom

Om te beginnen, registreert een gebruiker ETL in het gebruikersinterface van het Platform van de Ervaring (UI) en leidt datasets voor opname gebruikend een standaardschakelaar of een duw-dienst schakelaar.

In UI, leidt de gebruiker tot de outputdataset door een datasetschema te selecteren. De keuze van het schema hangt af van het type gegevens (record- of tijdreeks) dat in Platform wordt opgenomen. Door op het lusje van Schema binnen UI te klikken, zal de gebruiker alle beschikbare schema&#39;s, met inbegrip van het gedragstype kunnen bekijken dat het schema steunt.

In ETL zal de gebruiker beginnen hun toewijzingstransformaties te ontwerpen nadat de aangewezen verbinding (gebruikend hun geloofsbrieven) wordt gevormd. Er wordt aangenomen dat de ETL-tool al connectors van het Experience Platform heeft geïnstalleerd (proces niet gedefinieerd in deze integratiegids).

In de [ETL-workflow](./workflow.md)zijn modellen voor een voorbeeld-ETL-tool en -workflow opgenomen. Hoewel de ETL-gereedschappen verschillende indelingen kunnen hebben, zijn de meeste toepassingen beschikbaar voor vergelijkbare functies.

>[!NOTE] De ETL-aansluiting moet een tijdstempelfilter opgeven waarmee de datum voor het invoeren van gegevens en verschuiving (d.w.z. het venster waarvoor gegevens moeten worden gelezen) wordt aangegeven. Het ETL-hulpmiddel moet het gebruik van deze twee parameters in deze of een andere relevante interface ondersteunen. In het Adobe Experience Platform worden deze parameters toegewezen aan beschikbare datums (indien aanwezig) of vastgelegde datums in het batchobject van de gegevensset.

### Lijst met gegevenssets weergeven

Met behulp van de gegevensbron voor toewijzing, kan een lijst van alle beschikbare datasets worden gehaald gebruikend [Catalog API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

U kunt één API-verzoek indienen om alle beschikbare gegevenssets te bekijken (bijvoorbeeld `GET /dataSets`), met beste praktijken het zijn om vraagparameters te omvatten die de grootte van de reactie beperken.

In gevallen waarin om _volledige_ gegevenssetinformatie wordt verzocht, kan de antwoordlading voorbij 3 GB in grootte bereiken, die algemene prestaties kan vertragen. Daarom zal het gebruiken van vraagparameters om slechts de informatie te filtreren nodig vragen van de Catalogus efficiënter maken.

#### Filteren op List

Wanneer het filtreren van reacties, kunt u veelvoudige filters in één enkele vraag gebruiken door parameters met een ampersand (`&`) te scheiden. Sommige queryparameters accepteren door komma&#39;s gescheiden lijsten met waarden, zoals het filter &quot;Eigenschappen&quot; in de voorbeeldaanvraag hieronder.

De reacties van de catalogus worden automatisch gemeten volgens gevormde grenzen, nochtans kan de &quot;grens&quot;vraagparameter worden gebruikt om de beperkingen aan te passen en het aantal teruggekeerde voorwerpen te beperken. De vooraf geconfigureerde responslimieten voor catalogi zijn:

- Als er geen limietparameter is opgegeven, is het maximumaantal objecten per antwoordlading 20.
- De algemene limiet voor alle andere catalogusquery&#39;s is 100 objecten.
- Voor datasetvragen, als observableSchema wordt gevraagd gebruikend de parameter van de eigenschappenvraag, is het maximumaantal teruggekeerde datasets 20.
- Ongeldige limietparameters (inclusief `limit=0`) worden gevonden met een HTTP 400-fout die juiste bereiken omlijnt.
- Als limieten of verschuivingen als queryparameters worden doorgegeven, hebben ze voorrang op de parameters die als kopteksten worden doorgegeven.

De parameters van de vraag worden behandeld meer in detail in het overzicht [van de Dienst van de](../catalog/home.md)Catalogus.

**API-indeling**

```http
GET /catalog/dataSets
GET /catalog/dataSets?{filter1}={value1},{value2}&{filter2}={value3}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=3&properties=name,description,schemaRef" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Raadpleeg het overzicht [van de](../catalog/home.md) Catalogusservice voor gedetailleerde voorbeelden van het maken van aanroepen naar de [Catalog-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**Antwoord**

De reactie omvat drie (`limit=3`) datasets die de &quot;naam&quot;, &quot;beschrijving&quot;, en &quot;schemaRef&quot;zoals die door de `properties` vraagparameter wordt vermeld tonen.

```json
{
    "5b95b155419ec801e6eee780": {
        "name": "Store Transactions",
        "description": "Retails Store Transactions",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c351fa2f5fee300000fa9e8": {
        "name": "Loyalty Members",
        "description": "Loyalty Program Members",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/fbc52b243d04b5d4f41eaa72a8ba58be",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    },
    "5c1823b19e6f400000993885": {
        "name": "Web Traffic",
        "description": "Retail Web Traffic",
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/2025a705890c6d4a4a06b16f8cf6f4ca",
            "contentType": "application/vnd.adobe.xed+json;version=1"
        }
    }
}
```

### Gegevenssetschema weergeven

Het &quot;schemaRef&quot;bezit van een dataset bevat URI die het XDM schema van verwijzingen voorzien waarop de dataset gebaseerd is. Het XDM-schema (&quot;schemaRef&quot;) vertegenwoordigt alle _potentiële_ velden die door de dataset kunnen worden gebruikt, niet noodzakelijkerwijs de velden die _worden_ gebruikt (zie &quot;observableSchema&quot; hieronder).

Het XDM-schema is het schema dat u gebruikt wanneer u de gebruiker een lijst moet geven met alle beschikbare velden waarnaar kan worden geschreven.

De eerste &quot;schemaRef.id&quot;waarde in het vorige reactievoorwerp (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) is URI die aan een specifiek schema XDM in de Registratie van het Schema richt. Het schema kan worden teruggewonnen door een raadpleging (GET) verzoek aan de Registratie API van het Schema te maken.

>[!NOTE] De eigenschap &quot;schemaRef&quot; vervangt de nu afgekeurde eigenschap &quot;schema&quot;. Als &quot;schemaRef&quot;van de dataset afwezig is of geen waarde bevat, zult u de aanwezigheid van een &quot;schema&quot;bezit moeten controleren. Dit zou kunnen worden gedaan door &quot;schemaRef&quot;met &quot;schema&quot;in de `properties` vraagparameter in de vorige vraag te vervangen. Meer details over het &quot;schema&quot;bezit zijn beschikbaar in de sectie van het Bezit [van de](#dataset-schema-property-deprecated---eol-2019-05-30) Dataset &quot;schema&quot;die volgt.

**API-indeling**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Verzoek**

In de aanvraag wordt de URL-gecodeerde `id` URI van het schema (de waarde van het kenmerk &quot;schemaRef.id&quot;) gebruikt en wordt de header Accept vereist.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

De responsindeling is afhankelijk van het type Accept-header dat in de aanvraag wordt verzonden. Voor opzoekverzoeken moet u ook een bestand in de koptekst Accepteren `version` opnemen. In de volgende tabel worden de beschikbare kopteksten voor zoekopdrachten geaccepteerd:

| Accepteren | Beschrijving |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Aanvragen, titels, id&#39;s en versies van List (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs en allOf opgelost, heeft titels en beschrijvingen |
| `application/vnd.adobe.xed+json; version={major version}` | Onbewerkt met $ref en alles, heeft titels en beschrijvingen |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Onbewerkt met $ref en alles, geen titels of beschrijvingen |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs en allOf opgelost, geen titels of beschrijvingen |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs en alle opgeloste, omschrijvingen inbegrepen |

>[!NOTE] en `application/vnd.adobe.xed-id+json` `application/vnd.adobe.xed-full+json; version={major version}` zijn de meestgebruikte Accepterende koppen. `application/vnd.adobe.xed-id+json` heeft de voorkeur voor het opnemen van bronnen in het schemaregister, aangezien alleen de titel, id en version worden geretourneerd. `application/vnd.adobe.xed-full+json; version={major version}` heeft de voorkeur voor het weergeven van een specifieke bron (aan de hand van de id), aangezien deze alle velden (genest onder &quot;eigenschappen&quot;) retourneert, evenals titels en beschrijvingen.

**Antwoord**

Het JSON-schema dat wordt geretourneerd, beschrijft de structuur en veldniveaugegevens (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, enz.) van de gegevens, met serienummering gecodeerd als JSON. Als het gebruiken van een rangschikkingsformaat buiten JSON voor opname (zoals Parquet of Scala), bevat de Gids [van de Registratie van het](../xdm/tutorials/create-schema-api.md) Schema een lijst die het gewenste type JSON (&quot;meta:xdmType&quot;) en zijn overeenkomstige vertegenwoordiging in andere formaten toont.

Samen met deze lijst, bevat de Gids van de Ontwikkelaar van de Registratie van het Schema diepgaande voorbeelden van alle mogelijke vraag die kan worden gemaakt gebruikend de Registratie API van het Schema.

### De eigenschap &quot;schema&quot; van de gegevensset (GEDEPRECEERD - EOL 2019-05-30)

Datasets kunnen een &quot;schema&quot;bezit bevatten dat nu verouderd is en tijdelijk beschikbaar voor achterwaartse verenigbaarheid blijft. Bijvoorbeeld, zou een lijst (GET) verzoek gelijkend op eerder gemaakt, waar &quot;schema&quot;voor &quot;schemaRef&quot;in de `properties` vraagparameter werd vervangen, het volgende kunnen terugkeren:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Als het &quot;schema&quot;bezit van een dataset bevolkt is, geeft dit aan dat het schema een afgekeurd `/xdms` schema is en, waar gesteund, zou de schakelaar ETL de waarde in het &quot;schema&quot;bezit met het `/xdms` eindpunt (een afgekeurd eindpunt in de [Catalogus API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) moeten gebruiken om het erfenisschema terug te winnen.

**API-indeling**

```http
GET /catalog/{"schema" property without the "@"}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE] Een facultatieve vraagparameter, `expansion=xdm`, vertelt API om volledig uit te breiden en in-lijn om het even welke referenced schema&#39;s. Dit kunt u doen wanneer u een lijst met alle mogelijke velden aan de gebruiker presenteert.

**Antwoord**

Gelijkaardig aan de stappen voor het [bekijken van datasetschema](#view-dataset-schema), bevat de reactie een schema JSON dat de structuur en gebied-vlakke informatie van de gegevens beschrijft, die als JSON in series worden vervaardigd.

>[!NOTE] Wanneer het &quot;schema&quot;gebied leeg is of volledig ontbreekt, zou de schakelaar het &quot;schemaRef&quot;gebied moeten lezen en de [Registratie API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van het Schema zoals aangetoond in de vorige stappen gebruiken om een datasetschema [te](#view-dataset-schema)bekijken.

### De eigenschap &quot;observableSchema&quot;

De eigenschap &quot;observableSchema&quot; van een dataset heeft een JSON-structuur die overeenkomt met die van het XDM-schema JSON. Het &quot;observableSchema&quot; bevat de velden die aanwezig waren in de binnenkomende invoerbestanden. Wanneer het schrijven van gegevens aan het Platform van de Ervaring, wordt een gebruiker vereist niet om elk gebied van het doelschema te gebruiken. In plaats daarvan moeten ze alleen die velden leveren die worden gebruikt.

Het waarneembare schema is het schema dat u zou gebruiken als u de gegevens leest of een lijst presenteert met velden die beschikbaar zijn om van te lezen/in kaart te brengen.

```json
{
    "598d6e81b2745f000015edcb": {
        "observableSchema": {
            "type": "object",
            "meta:xdmType": "object",
            "properties": {
                "name": {
                    "type": "string",
                },
                "age": {
                    "type": "string",
                }
            }
        }
    }
}
```

### Gegevens voorvertonen

De ETL-toepassing kan een mogelijkheid bieden om gegevens voor te vertonen ([&quot;Afbeelding 8&quot; in de ETL-workflow](./workflow.md)). De API voor gegevenstoegang biedt verschillende opties voor het weergeven van voorvertoningen van gegevens.

Aanvullende informatie, waaronder stapsgewijze instructies voor het voorvertonen van gegevens met behulp van de API voor gegevenstoegang, vindt u in de zelfstudie over [gegevenstoegang](../data-access/tutorials/dataset-data.md).

### Krijg datasetdetails gebruikend de &quot;eigenschappen&quot;vraagparameter

Zoals aangetoond in de stappen hierboven om een lijst van datasets [te](#view-list-of-datasets)bekijken, kunt u &quot;dossiers&quot;verzoeken gebruikend de &quot;eigenschappen&quot;vraagparameter.

U kunt naar het overzicht [van de Dienst van de](../catalog/home.md) Catalogus voor gedetailleerde informatie over het vragen van datasets en beschikbare reactiefilters verwijzen.

**API-indeling**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Antwoord**

De reactie zal één dataset (`limit=1`) omvatten die het &quot;dossiers&quot;bezit tonen.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files"
  }
}
```

### Gegevenssetbestanden weergeven met het kenmerk &quot;files&quot;

U kunt ook een GET-aanvraag gebruiken om bestandsgegevens op te halen met het kenmerk &quot;files&quot;.

**API-indeling**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Antwoord**

De reactie omvat identiteitskaart van het Dossier van de Dataset als top-level bezit, met dossierdetails bevat binnen het voorwerp van identiteitskaart van het Dossier van de Dataset.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542749145828,
        "updated": 1542749145828
    },
    "14d5758c107443e1a83c714e56ca79d0-1": {
        "batchId": "14d5758c107443e1a83c714e56ca79d0",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542752699111,
        "updated": 1542752699111
    },
    "ea40946ac03140ec8ac4f25da360620a-1": {
        "batchId": "ea40946ac03140ec8ac4f25da360620a",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{IMS_ORG}",
        "availableDates": {},
        "createdUser": "{USER_ID}",
        "createdClient": "{API_KEY}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "created": 1542756935535,
        "updated": 1542756935535
    }
}
```

### Bestandsgegevens ophalen

De id&#39;s van het gegevenssetbestand die in de vorige reactie zijn geretourneerd, kunnen worden gebruikt in een GET-verzoek om meer bestandsgegevens op te halen via de API voor gegevenstoegang.

Het overzicht [van de](../data-access/home.md) gegevenstoegang bevat informatie over het gebruik van de API voor gegevenstoegang.

**API-indeling**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

**Antwoord**

```json
[
    {
    "name": "{FILE_NAME}.parquet",
    "length": 2576,
    "_links": {
        "self": {
            "href": "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet"
            }
        }
    }
]
```

### Bestandsgegevens voorvertonen

De eigenschap &quot;href&quot; kan worden gebruikt om voorvertoningsgegevens op te halen via de API [voor](../data-access/home.md)gegevenstoegang.

**API-indeling**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Het antwoord op het bovenstaande verzoek bevat een voorvertoning van de inhoud van het bestand.

Meer informatie over de API voor gegevenstoegang, inclusief gedetailleerde verzoeken en reacties, is beschikbaar in het overzicht [van de](../data-access/home.md)gegevenstoegang.

### &quot;fileDescription&quot; ophalen uit gegevensset

De bestemmingscomponent als output van getransformeerde gegevens, zal de Ingenieur van Gegevens een Dataset van de Output ([&quot;Figuur 12&quot;in het ETL- Werkschema](workflow.md)) kiezen. Het XDM-schema is gekoppeld aan de uitvoergegevensset. De te schrijven gegevens worden geïdentificeerd door het kenmerk &quot;fileDescription&quot; van de gegevenssetentiteit van de API&#39;s voor gegevensdetectie. Deze informatie kan worden opgehaald gebruikend een dataset identiteitskaart (`{DATASET_ID}`). De eigenschap &quot;fileDescription&quot; in het JSON-antwoord geeft de gevraagde informatie.

**API-indeling**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{DATASET_ID}` | De `id` waarde van de dataset u probeert toegang te hebben. |

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {IMS_ORG}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key : {API_KEY}"
```

**Antwoord**

```JSON
{
  "59c93f3da7d0c00000798f68": {
    "version": "1.0.4",
    "fileDescription": {
        "persisted": false,
        "format": "parquet"
    }
  }
}
```

Gegevens worden geschreven naar Experience Platform met behulp van [Data Ingestie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).  Het schrijven van gegevens is een asynchroon proces. Wanneer gegevens naar het Adobe Experience Platform worden geschreven, wordt pas een batch gemaakt en gemarkeerd als een succes als de gegevens volledig zijn geschreven.

Gegevens in het ervaringsplatform moeten worden geschreven in de vorm van parketbestanden.

## Uitvoeringsfase

Wanneer de uitvoering start, leest de connector (zoals gedefinieerd in de broncomponent) de gegevens van het Experience Platform met de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)gegevenstoegang. Het transformatieproces leest de gegevens voor een bepaald tijdbereik. Intern, zal het partijen brondatasets vragen. Tijdens het vragen, zal het een geparameterized (het rollen voor tijdreeksgegevens, of stijgende gegevens) begindatum en lijstdatasetdossiers voor die partijen gebruiken, en begint verzoeken om gegevens voor die datasetdossiers te doen.

### Voorbeeldtransformaties

Het [voorbeelddocument voor ETL-transformaties](./transformations.md) bevat een aantal voorbeeldtransformaties, waaronder identiteitsbeheer en gegevenstypetoewijzingen. Gebruik deze transformaties ter referentie.

### Gegevens van het Experience Platform lezen

Met de [Catalog-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)kunt u alle batches ophalen tussen een opgegeven begintijd en eindtijd en ze sorteren op de volgorde waarin ze zijn gemaakt.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Details over het filteren van batches vindt u in de zelfstudie over [gegevenstoegang](../data-access/tutorials/dataset-data.md).

### Bestanden ophalen uit een batch

Als u de id hebt voor de batch die u zoekt (`{BATCH_ID}`), kan een lijst met bestanden die tot een specifieke batch behoren, worden opgehaald via de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)gegevenstoegang.  Details hiervoor zijn beschikbaar in de zelfstudie over [gegevenstoegang](../data-access/tutorials/dataset-data.md).

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Bestanden openen met bestands-id

Met de unieke id van een bestand (`{FILE_ID`) kunt u de API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) gegevenstoegang gebruiken om toegang te krijgen tot de specifieke details van het bestand, zoals de naam, grootte in bytes en een koppeling om het bestand te downloaden.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

De reactie kan naar één bestand of naar een map verwijzen. De details over elk kunnen in de [gegevenstoegangszelfstudie](../data-access/tutorials/dataset-data.md)worden gevonden.

### Bestandsinhoud openen

De API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) gegevenstoegang kan worden gebruikt om toegang te krijgen tot de inhoud van een specifiek bestand. Om de inhoud op te halen, wordt een GET verzoek gemaakt gebruikend de waarde voor `_links.self.href` wanneer het toegang tot van een dossier gebruikend dossieridentiteitskaart is teruggekeerd.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Het antwoord op deze aanvraag bevat de inhoud van het bestand. Voor meer informatie, met inbegrip van details over reactiepaginering, zie [hoe te de Gegevens van de Vraag via gegeven toegang API](../data-access/tutorials/dataset-data.md) leerprogramma.

### Records voor schemaconformiteit valideren

Wanneer gegevens worden geschreven, kunnen gebruikers ervoor kiezen om gegevens te valideren volgens de validatieregels die in het XDM-schema zijn gedefinieerd. Meer informatie over schemabevestiging kan in de Code van de Verwijzing van de Integratie van het Ecosysteem van [ETL op GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation)worden gevonden.

Als u de verwijzingsimplementatie gebruikt die op [GitHub](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)wordt gevonden, kunt u schemabevestiging in deze implementatie aanzetten gebruikend het systeembezit `-DenableSchemaValidation=true`.

Validatie kan voor logische types worden uitgevoerd XDM, gebruikend attributen zoals `minLength` en `maxlength` voor koorden, `minimum` en `maximum` voor gehelen, en meer. De ontwikkelaarsgids voor [de](../xdm/api/getting-started.md) schemaregistratie-API bevat een tabel met XDM-typen en de eigenschappen die voor validatie kunnen worden gebruikt.

>[!NOTE] De minimum- en maximumwaarden die voor verschillende `integer` typen worden opgegeven, zijn de MIN- en MAX-waarden die door het type worden ondersteund, maar deze waarden kunnen verder worden beperkt tot de minimum- en maximumwaarden van uw keuze.

### Een batch maken

Zodra de gegevens zijn verwerkt, schrijft het ETL-hulpprogramma de gegevens terug naar het Experience Platform met behulp van de [Batch Ingestie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Voordat gegevens kunnen worden toegevoegd aan een gegevensset, moet deze worden gekoppeld aan een batch die later wordt geüpload naar een specifieke gegevensset.

**Verzoek**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Details voor het maken van een batch, inclusief voorbeeldaanvragen en reacties, vindt u in het overzicht [](../ingestion/batch-ingestion/overview.md)Batch-inname.

### Schrijven naar gegevensset

Nadat een nieuwe partij met succes tot stand is gebracht, kunnen de dossiers dan aan een specifieke dataset worden geupload. U kunt meerdere bestanden in een batch plaatsen totdat deze worden gepromoot. Bestanden kunnen worden geüpload met de _Small File Upload API_; als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden, kunt u de API _voor het uploaden van_ grote bestanden gebruiken. Meer informatie over het gebruik van zowel grote als kleine bestanden kunt u vinden in het overzicht [van de](../ingestion/batch-ingestion/overview.md)batchverwerking.

**Verzoek**

Gegevens in het ervaringsplatform moeten worden geschreven in de vorm van parketbestanden.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{IMS_ORG}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Batchupload voltooien

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Op deze manier worden de Catalogus &quot;DataSetFile&quot;-items gemaakt voor de voltooide bestanden en gekoppeld aan de gegenereerde batch. De catalogusbatch wordt vervolgens gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd om de beschikbare gegevens in te voeren.

Gegevens worden eerst landd op de testlocatie op het Adobe Experience Platform en vervolgens verplaatst naar de uiteindelijke locatie na catalogisering en validatie. Batches worden gemarkeerd als succesvol zodra alle gegevens naar een vaste locatie worden verplaatst.

**Verzoek**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

Als dit lukt, retourneert de reactie HTTP Status 200 OK en is de hoofdtekst van de reactie leeg.

Het ETL-hulpmiddel zorgt ervoor dat de tijdstempel van de brongegevensset(s) wordt genoteerd wanneer de gegevens worden gelezen.

Bij de volgende transformatie-uitvoering, waarschijnlijk door planning of aanroeping van de gebeurtenis, zal ETL beginnen om de gegevens van eerder-bewaarde timestamp en alle gegevens te vragen die door:gaan.

### Laatste batchstatus ophalen

Voordat u nieuwe taken uitvoert met het gereedschap ETL, moet u controleren of de laatste batch is voltooid. De API [voor](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) catalogusservice biedt een batchspecifieke optie die de details van de desbetreffende batches bevat.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwoord**

Nieuwe taken kunnen worden gepland als de vorige batch-&quot;status&quot;-waarde &quot;success&quot; is, zoals hieronder wordt getoond:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "CLIENT_USER_ID@AdobeID",
    "updatedUser": "CLIENT_USER_ID@AdobeID",
    "updated": 1494349963467,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

### Laatste batchstatus ophalen op id

Een individuele partijstatus kan door de Dienst van de [Catalogus API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) worden teruggewonnen door een GET verzoek uit te geven gebruikend `{BATCH_ID}`. De `{BATCH_ID}` gebruikte id is hetzelfde als de id die wordt geretourneerd toen de batch werd gemaakt.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie - geslaagd**

De volgende reactie laat een &quot;succes&quot; zien:

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "success",
    "errors": [],
    "version": "1.0.1",
    "availableDates": {}
}
```

**Respons - Mislukt**

In geval van een storing kunnen de &quot;fouten&quot; worden opgehaald uit het antwoord en op het ETL-gereedschap worden weergegeven als foutberichten.

```json
"{BATCH_ID}": {
    "imsOrg": "{IMS_ORG}",
    "created": 1494349962314,
    "createdClient": "{API_KEY}",
    "createdUser": "{CREATED_USER}",
    "updatedUser": "{UPDATED_USER}",
    "updated": 1494349962314,
    "status": "failure",
    "errors": [
        {
            "code": "200",
            "description": "Error in validating schema for file: 'adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv' with errorMessage=adl://dataLake.azuredatalakestore.net/connectors-dev/stage/BATCHID/dataSetId/contact.csv is not a Parquet file. expected magic number at tail [80, 65, 82, 49] but found [57, 98, 55, 10] and errorType=java.lang.RuntimeException",
            "rows": []
        }
    ],
    "version": "1.0.1",
    "availableDates": {}
}
```

## Incrementele versus momentopnamegegevens en gebeurtenissen vs. profielen

Gegevens kunnen als volgt in een twee bij twee matrix worden vertegenwoordigd:

| Incrementele gebeurtenissen | Incrementele profielen |
|-------------------------------|----------------------|
| Gebeurtenissen voor momentopnamen (minder waarschijnlijk) | Profielen voor momentopnamen |

Gebeurtenisgegevens zijn doorgaans wanneer elke rij geïndexeerde tijdstempelkolommen bevat.

Profielgegevens worden doorgaans gebruikt wanneer er geen tijdstempel in de gegevens staat en elke rij kan worden geïdentificeerd met een primaire/samengestelde sleutel.

Met incrementele gegevens worden alleen nieuwe/bijgewerkte gegevens in het systeem opgenomen en toegevoegd aan de huidige gegevens in de gegevenssets.

De gegevens van de momentopname zijn wanneer alle gegevens in het systeem komen en sommige of alle vorige gegevens in een dataset vervangen.

In het geval van incrementele gebeurtenissen moet het ETL-gereedschap de beschikbare datums gebruiken/de aanmaakdatum van de batchentiteit. In het geval van de pushservice zijn er geen beschikbare datums. Voor het markeren van toenamen wordt dus gebruikgemaakt van een batch gemaakt/bijgewerkte datum. Elke batch incrementele gebeurtenissen moet worden verwerkt.

Voor incrementele profielen gebruikt ETL-tool gemaakte/bijgewerkte datums van batchentiteiten. Doorgaans moet elke batch incrementele profielgegevens worden verwerkt.

Gebeurtenissen voor momentopnamen zijn zeer minder waarschijnlijk als gevolg van de grootte van de gegevens. Maar als dit vereist zou zijn, moet het ETL hulpmiddel slechts de laatste partij voor verwerking kiezen.

Wanneer momentopnameprofielen worden gebruikt, zal het hulpmiddel ETL de laatste partij van de gegevens moeten kiezen die in het systeem aankwamen. Maar als de vereiste is om de versies van veranderingen te volgen, dan zullen alle partijen moeten worden verwerkt. De verwerking van deduplicatie binnen het ETL-proces zal helpen de opslagkosten te beheersen.

## Batch opnieuw afspelen en gegevens opnieuw verwerken

Het opnieuw afspelen van batches en het opwerken van gegevens kunnen vereist zijn in gevallen waarin een klant ontdekt dat de laatste &#39;n&#39; dagen, de gegevens die worden verwerkt niet zoals verwacht hebben plaatsgevonden of de brongegevens zelf wellicht niet correct zijn geweest.

Hiertoe gebruiken de gegevensbeheerders van de client de interface van het platform om de batches met beschadigde gegevens te verwijderen. Vervolgens zal de ETL waarschijnlijk opnieuw moeten worden uitgevoerd, zodat de ETL met correcte gegevens kan worden gerepareerd. Als de bron zelf corrupte gegevens had, zal de gegevensingenieur/beheerder de bronpartijen moeten verbeteren en de gegevens (of in het Platform van de Ervaring van Adobe of via ETL schakelaars) opnieuw opnemen.

Gebaseerd op het type van gegevens die worden geproduceerd, zal het de keus van de gegevensingenieur zijn om één enkele partij of alle partijen uit bepaalde datasets te verwijderen. Gegevens worden verwijderd/gearchiveerd volgens de richtlijnen van het Experience Platform.

Het is waarschijnlijk een scenario dat de functionaliteit ETL om gegevens te zuiveren belangrijk zal zijn.

Zodra het leegmaken is voltooid, moeten de clientbeheerders het Adobe Experience Platform opnieuw configureren om de verwerking voor de kernservices opnieuw te starten vanaf het moment dat de batches worden verwijderd.

## Gelijktijdige batchverwerking

Naar eigen goeddunken van de klant kunnen gegevensbeheerders/engineers besluiten gegevens op sequentiële wijze of op gelijktijdige wijze te extraheren, te transformeren en te laden, afhankelijk van de kenmerken van een bepaalde gegevensset. Dit wordt ook gebaseerd op het geval waarin de client de getransformeerde gegevens gebruikt.

Bijvoorbeeld, als de cliënt aan een updatable persistentieopslag voortduurt en de opeenvolging of de orde van gebeurtenissen belangrijk is, kan de cliënt banen met opeenvolgende transformaties strikt moeten verwerken ETL.

In andere gevallen kunnen gegevens in de vorm van een out-of-order worden verwerkt door downstreamtoepassingen/processen die intern worden gesorteerd met een opgegeven tijdstempel. In die gevallen kunnen parallelle ETL-transformaties levensvatbaar zijn om de verwerkingstijd te verbeteren.

Voor bronbatches is dit weer afhankelijk van de voorkeur van de klant en de beperking van de consument. Als de brongegevens parallel kunnen worden opgepikt zonder dat rekening wordt gehouden met de urgentie/volgorde van een rij, kan het transformatieproces procesbatches maken met een hogere mate van parallellisme (optimalisatie gebaseerd op verwerking buiten bestelling). Maar als de transformatie tijdstempels moet respecteren of belangrijkheidsvolgorde moet wijzigen, moeten de API voor gegevenstoegang of ETL-toolplanner/aanroeping ervoor zorgen dat batches waar mogelijk niet buiten de bestelling worden verwerkt.

## Uitstel

Uitstel is een proces waarbij de inputgegevens nog niet volledig genoeg zijn om naar downstreamprocessen te worden verzonden, maar in de toekomst bruikbaar kunnen zijn. Clients zullen hun individuele tolerantie voor gegevensramen voor toekomstige matching tegenover de kosten van verwerking bepalen om hun beslissing om gegevens te reserveren en opnieuw te verwerken in de volgende transformatieuitvoering te informeren, in de hoop dat het op een bepaald tijdstip in het bewaarvenster kan worden verrijkt en in overeenstemming gebracht/vastgemaakt. Deze cyclus loopt tot de rij voldoende is verwerkt of te groot wordt geacht om te blijven investeren in. Elke herhaling genereert uitgestelde gegevens die een superset zijn van alle uitgestelde gegevens in vorige herhalingen.

Het Platform van de Ervaring van Adobe identificeert momenteel geen uitgestelde gegevens, zodat moeten de cliëntimplementaties zich op de ETL en de handconfiguraties van Dataset baseren om een andere dataset in Platform te creëren die de brondataset weerspiegelt die kan worden gebruikt om uitgestelde gegevens te houden. In dit geval zijn uitgestelde gegevens vergelijkbaar met momentopnamegegevens. Bij elke uitvoering van de ETL-transformatie worden de brongegevens verenigd met uitgestelde gegevens en verzonden voor verwerking.

## Changelog

| Datum | Handeling | Beschrijving |
| ---- | ------ | ----------- |
| 2019-01-19 | Eigenschap &quot;fields&quot; uit gegevenssets verwijderd | Datasets bevatten eerder een eigenschap &quot;fields&quot; die een kopie van het schema bevatte. Deze mogelijkheid mag niet meer worden gebruikt. Als de eigenschap &quot;fields&quot; wordt gevonden, moet deze worden genegeerd en wordt in plaats daarvan &quot;ObservedSchema&quot; of &quot;schemaRef&quot; gebruikt. |
| 2019-03-15 | &quot;schemaRef&quot;-eigenschap toegevoegd aan gegevenssets | Het &quot;schemaRef&quot;bezit van een dataset bevat URI die naar het XDM schema verwijst waarop de dataset gebaseerd is en vertegenwoordigt alle potentiële gebieden die door de dataset zouden kunnen worden gebruikt. |
| 2019-03-15 | Alle eindgebruikersidentificatoren wijzen de eigenschap &quot;identityMap&quot; toe | De &quot;identityMap&quot;is een inkapseling van alle unieke herkenningstekens van een onderwerp, zoals identiteitskaart van CRM, ECID, of identiteitskaart van het loyaliteitsprogramma Deze kaart wordt gebruikt door de Dienst [van de](../identity-service/home.md) Identiteit om alle bekende en anonieme identiteiten van een onderwerp op te lossen, die één enkele identiteitsgrafiek voor elke eindgebruiker vormen. |
| 2019-05-30 | EOL en verwijder &quot;schema&quot;bezit uit datasets | De dataset &quot;schema&quot;bezit verstrekte een verwijzingsverbinding aan het schema gebruikend het afgekeurde `/xdms` eindpunt in Catalog API. Dit is vervangen door een &quot;schemaRef&quot;die &quot;id&quot;, &quot;versie&quot;, en &quot;contentType&quot;van het schema zoals die in de nieuwe Registratie API van het Schema van verwijzingen wordt voorzien. |