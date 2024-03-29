---
keywords: Experience Platform;thuis;populaire onderwerpen;ETL;etl;etl integraties;ETL-integratie
solution: Experience Platform
title: Ontwikkeling van ETL-integratie voor Adobe Experience Platform
description: De ETL-integratiehandleiding beschrijft algemene stappen voor het maken van krachtige, veilige connectors voor Experience Platform en het opnemen van gegevens in Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: b80d8349fc54a955ebb3362d67a482d752871420
workflow-type: tm+mt
source-wordcount: '3978'
ht-degree: 0%

---

# Ontwikkeling van ETL-integratie voor Adobe Experience Platform

De ETL-integratiehandleiding beschrijft algemene stappen voor het maken van krachtige, veilige connectors voor [!DNL Experience Platform] en gegevens opnemen in [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [Verificatie en autorisatie voor Experience Platform-API&#39;s](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Deze handleiding bevat ook voorbeeld-API-aanroepen die moeten worden gebruikt bij het ontwerpen van een ETL-connector, met koppelingen naar documentatie die elke aanroep omschrijft [!DNL Experience Platform] de dienst, en het gebruik van zijn API, meer in detail.

Er is een voorbeeldintegratie beschikbaar op [!DNL GitHub] via de [ETL Ecosystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) onder de [!DNL Apache] Licentieversie 2.0.

## Workflow

Het volgende workflowdiagram biedt een overzicht op hoog niveau voor de integratie van Adobe Experience Platform-componenten met een ETL-toepassing en -aansluiting.

![](images/etl.png)

## Adobe Experience Platform-componenten

Er zijn veelvoudige Experience Platform componenten betrokken bij ETL schakelaarintegratie. In de volgende lijst worden verschillende belangrijke componenten en functies beschreven:

- **Adobe Identity Management System (IMS)** - Biedt een framework voor verificatie van Adobe-services.
- **IMS-organisatie** - Een onderneming die producten en diensten in eigendom kan hebben of in licentie kan geven en toegang kan verlenen tot haar leden.
- **IMS-gebruiker** - leden van een IMS-organisatie. De relatie Organisatie met gebruiker is veel te veel.
- **[!DNL Sandbox]** - Een virtuele partitie één [!DNL Platform] bijvoorbeeld om toepassingen voor digitale ervaringen te helpen ontwikkelen en te ontwikkelen.
- **Gegevensdetectie** - Registreert de metagegevens van opgenomen en getransformeerde gegevens in [!DNL Experience Platform].
- **[!DNL Data Access]** - Biedt gebruikers een interface om toegang te krijgen tot hun gegevens in [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Pushgegevens naar [!DNL Experience Platform] with [!DNL Data Ingestion] API&#39;s.
- **[!DNL Schema Registry]** - Definieert en slaat schema op dat de structuur van gegevens beschrijft waarin gegevens moeten worden gebruikt [!DNL Experience Platform].

## Aan de slag met [!DNL Experience Platform] API&#39;s

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben aan met succes vraag aan [!DNL Experience Platform] API&#39;s.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de conventies die worden gebruikt in documentatie voor voorbeeld-API-aanroepen raadpleegt u de sectie over [voorbeeld-API-aanroepen lezen](../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] gids voor probleemoplossing.

### Waarden verzamelen voor vereiste koppen

Om vraag te maken aan [!DNL Platform] API&#39;s, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste kopteksten in alle [!DNL Experience Platform] API-aanroepen, zoals hieronder wordt getoond:

- Toestemming: houder `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle verzoeken aan [!DNL Platform] API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over sandboxen in [!DNL Platform], zie de [overzichtsdocumentatie van sandbox](../sandboxes/home.md).

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Algemene gebruikersstroom

Om te beginnen, registreert een gebruiker ETL in [!DNL Experience Platform] gebruikersinterface (UI) en leidt datasets voor opname gebruikend een standaardschakelaar of een duw-dienst schakelaar.

In UI, leidt de gebruiker tot de outputdataset door een datasetschema te selecteren. De keuze van het schema hangt af van het type gegevens (record- of tijdreeks) waarin de gegevens worden opgenomen [!DNL Platform]. Door op het lusje van Schema binnen UI te klikken, zal de gebruiker alle beschikbare schema&#39;s, met inbegrip van het gedragstype kunnen bekijken dat het schema steunt.

In ETL zal de gebruiker beginnen hun toewijzingstransformaties te ontwerpen nadat de aangewezen verbinding (gebruikend hun geloofsbrieven) wordt gevormd. Er wordt aangenomen dat het ETL-gereedschap al [!DNL Experience Platform] geïnstalleerde connectors (proces niet gedefinieerd in deze integratiegids).

Mockups voor een voorbeeld van een ETL-tool en -workflow zijn beschikbaar in de [ETL-workflow](./workflow.md). Hoewel de ETL-gereedschappen verschillende indelingen kunnen hebben, zijn de meeste toepassingen beschikbaar voor vergelijkbare functies.

>[!NOTE]
>
>De ETL-aansluiting moet een tijdstempelfilter opgeven waarmee de datum voor het invoeren van gegevens en verschuiving (d.w.z. Het venster waarvoor gegevens moeten worden gelezen). Het ETL-hulpmiddel moet het gebruik van deze twee parameters in deze of een andere relevante interface ondersteunen. In Adobe Experience Platform worden deze parameters toegewezen aan beschikbare datums (indien aanwezig) of vastgelegde datums in het batchobject van de gegevensset.

### Lijst met gegevenssets weergeven

Gebruikend de bron van gegevens voor afbeelding, kan een lijst van alle beschikbare datasets worden gehaald gebruikend [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

U kunt één API-verzoek indienen om alle beschikbare gegevenssets weer te geven (bijvoorbeeld `GET /dataSets`), met best practices om queryparameters op te nemen die de grootte van de reactie beperken.

In gevallen waarin volledige gegevenssetinformatie wordt gevraagd, kan de antwoordlading voorbij 3 GB in grootte bereiken, die algemene prestaties kan vertragen. Daarom zal het gebruiken van vraagparameters om slechts de informatie te filtreren nodig maken [!DNL Catalog] efficiëntere zoekopdrachten.

#### Filteren op List

Wanneer het filtreren van reacties, kunt u veelvoudige filters in één enkele vraag gebruiken door parameters met een ampersand (`&`). Sommige queryparameters accepteren door komma&#39;s gescheiden lijsten met waarden, zoals het filter &quot;Eigenschappen&quot; in de voorbeeldaanvraag hieronder.

[!DNL Catalog] de reacties worden automatisch gemeten volgens gevormde grenzen, nochtans kan de &quot;grens&quot;vraagparameter worden gebruikt om de beperkingen aan te passen en het aantal teruggekeerde voorwerpen te beperken. Vooraf geconfigureerd [!DNL Catalog] de responsgrenzen zijn :

- Als er geen limietparameter is opgegeven, is het maximumaantal objecten per antwoordlading 20.
- De algemene limiet voor alle andere [!DNL Catalog] query&#39;s zijn 100 objecten.
- Voor datasetvragen, als observableSchema wordt gevraagd gebruikend de parameter van de eigenschappenvraag, is het maximumaantal teruggekeerde datasets 20.
- Ongeldige limietparameters (inclusief `limit=0`) wordt voldaan aan een HTTP 400-fout met een overzicht van de juiste bereiken.
- Als limieten of verschuivingen als queryparameters worden doorgegeven, hebben ze voorrang op de parameters die als kopteksten worden doorgegeven.

De parameters van de vraag worden behandeld meer in detail in [Overzicht van Catalog Service](../catalog/home.md).

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
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Raadpleeg de [Overzicht van Catalog Service](../catalog/home.md) voor gedetailleerde voorbeelden van hoe te om vraag te maken aan [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Antwoord**

De reactie omvat drie (`limit=3`) datasets met de &quot;name&quot;, &quot;description&quot; en &quot;schemaRef&quot;, zoals aangegeven door de `properties` queryparameter.

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

Het &quot;schemaRef&quot;bezit van een dataset bevat URI die het XDM schema van verwijzingen voorzien waarop de dataset gebaseerd is. Het XDM-schema (&quot;schemaRef&quot;) vertegenwoordigt alle potentiële velden die door de dataset kunnen worden gebruikt, niet noodzakelijkerwijs de velden die worden gebruikt (zie &quot;observableSchema&quot; hieronder).

Het XDM-schema is het schema dat u gebruikt wanneer u de gebruiker een lijst moet geven met alle beschikbare velden waarnaar kan worden geschreven.

De eerste &quot;schemaRef.id&quot;-waarde in het vorige reactieobject (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) is een URI die verwijst naar een specifiek XDM-schema in het dialoogvenster [!DNL Schema Registry]. Het schema kan worden teruggewonnen door een raadpleging (GET) verzoek aan het [!DNL Schema Registry] API.

>[!NOTE]
>
>De eigenschap &quot;schemaRef&quot; vervangt de nu afgekeurde eigenschap &quot;schema&quot;. Als &quot;schemaRef&quot;van de dataset afwezig is of geen waarde bevat, zult u de aanwezigheid van een &quot;schema&quot;bezit moeten controleren. Dit kan worden gedaan door &quot;schemaRef&quot; te vervangen door &quot;schema&quot; in het dialoogvenster `properties` vraagparameter in de vorige vraag. Meer informatie over de eigenschap &quot;schema&quot; vindt u in het gedeelte [Eigenschap DataSet &quot;schema&quot;](#dataset-schema-property-deprecated---eol-2019-05-30) de volgende sectie.

**API-indeling**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Verzoek**

In de aanvraag wordt de gecodeerde URL gebruikt `id` URI van het schema (de waarde van het kenmerk &quot;schemaRef.id&quot;) en vereist de header Accept.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

De responsindeling is afhankelijk van het type Accept-header dat in de aanvraag wordt verzonden. Voor opzoekverzoeken is ook een `version` worden opgenomen in de koptekst Accepteren. In de volgende tabel worden de beschikbare kopteksten voor zoekopdrachten geaccepteerd:

| Accepteren | Beschrijving |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Aanvragen, titels, id&#39;s en versies van lijsten (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs en allOf opgelost, heeft titels en beschrijvingen |
| `application/vnd.adobe.xed+json; version={major version}` | Onbewerkt met $ref en alles, heeft titels en beschrijvingen |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Onbewerkt met $ref en alles, geen titels of beschrijvingen |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs en allOf opgelost, geen titels of beschrijvingen |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs en alle opgeloste, omschrijvingen inbegrepen |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` en `application/vnd.adobe.xed-full+json; version={major version}` Dit zijn de meest gebruikte Accepteer koppen. `application/vnd.adobe.xed-id+json` heeft de voorkeur voor het aanbieden van bronnen in de [!DNL Schema Registry] aangezien alleen de titel, id en version worden geretourneerd. `application/vnd.adobe.xed-full+json; version={major version}` heeft de voorkeur voor het weergeven van een specifieke bron (aan de hand van de id), aangezien deze alle velden (genest onder &quot;eigenschappen&quot;) retourneert, evenals titels en beschrijvingen.

**Antwoord**

Het JSON-schema dat wordt geretourneerd, beschrijft de structuur en veldniveaugegevens (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, enz.) van de gegevens, geserialiseerd als JSON. Als het gebruiken van een rangschikkingsformaat buiten JSON voor opname (zoals Parquet of Scala), [Handleiding voor het schemaregister](../xdm/tutorials/create-schema-api.md) bevat een tabel met het gewenste JSON-type (&quot;meta:xdmType&quot;) en de bijbehorende representatie in andere indelingen.

Samen met deze lijst, [!DNL Schema Registry] De Gids van de ontwikkelaar bevat diepgaande voorbeelden van alle mogelijke vraag die kan worden gemaakt gebruikend [!DNL Schema Registry] API.

### De eigenschap &quot;schema&quot; van de gegevensset (VEROUDERD - EOL 2019-05-30)

Datasets kunnen een eigenschap &quot;schema&quot; bevatten die nu is vervangen en tijdelijk beschikbaar blijft voor achterwaartse compatibiliteit. Bijvoorbeeld een lijst (GET) verzoek gelijkend op eerder gemaakt, waar &quot;schema&quot;werd vervangen &quot;schema&quot;in `properties` De vraagparameter, zou het volgende kunnen terugkeren:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Als het &quot;schema&quot;bezit van een dataset wordt bevolkt, wijst dit erop dat het schema afgekeurd is `/xdms` schema en, indien ondersteund, de ETL-connector de waarde in de eigenschap &quot;schema&quot; moet gebruiken met de `/xdms` eindpunt (een afgekeurd eindpunt in het [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/)) om het oudere schema op te halen.

**API-indeling**

```http
GET /catalog/{"schema" property without the "@"}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/xdms/context/person?expansion=xdm" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

>[!NOTE]
>
>Een optionele queryparameter, `expansion=xdm`, geeft de API de opdracht om schema&#39;s waarnaar wordt verwezen, volledig uit te breiden en in line te zetten. Dit kunt u doen wanneer u een lijst met alle mogelijke velden aan de gebruiker presenteert.

**Antwoord**

Vergelijkbaar met de stappen voor [gegevenssetschema weergeven](#view-dataset-schema), bevat de reactie een JSON-schema dat de structuur en de informatie op veldniveau van de gegevens beschrijft, geserialiseerd als JSON.

>[!NOTE]
>
>Wanneer het &quot;schema&quot;gebied leeg is of volledig afwezig, zou de schakelaar het &quot;schemaRef&quot;gebied moeten lezen en gebruiken [Schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/) zoals getoond in vorige stappen aan [een gegevenssetschema weergeven](#view-dataset-schema).

### De eigenschap &quot;observableSchema&quot;

De eigenschap &quot;observableSchema&quot; van een dataset heeft een JSON-structuur die overeenkomt met die van het XDM-schema JSON. Het &quot;observableSchema&quot; bevat de velden die aanwezig waren in de binnenkomende invoerbestanden. Gegevens schrijven naar [!DNL Experience Platform], is een gebruiker niet vereist om elk gebied van het doelschema te gebruiken. In plaats daarvan moeten ze alleen die velden leveren die worden gebruikt.

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

De ETL-toepassing kan een mogelijkheid bieden om gegevens voor te vertonen ([&quot;Figuur 8&quot;in het ETL- Werkschema](./workflow.md)). De API voor gegevenstoegang biedt verschillende opties voor het voorvertonen van gegevens.

Aanvullende informatie, waaronder stapsgewijze instructies voor het voorvertonen van gegevens met behulp van de API voor gegevenstoegang, vindt u in de [zelfstudie over gegevenstoegang](../data-access/tutorials/dataset-data.md).

### Krijg datasetdetails gebruikend de &quot;eigenschappen&quot;vraagparameter

Zoals u in de bovenstaande stappen kunt zien bij [een lijst met gegevenssets weergeven](#view-list-of-datasets)kunt u &quot;bestanden&quot; aanvragen met de queryparameter &quot;eigenschappen&quot;.

U kunt verwijzen naar de [Overzicht van Catalog Service](../catalog/home.md) voor gedetailleerde informatie over het vragen van datasets en beschikbare reactiefilters.

**API-indeling**

```http
GET /catalog/dataSets?limit={value}&properties={value}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets?limit=1&properties=files" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

**Antwoord**

De reactie zal één dataset omvatten (`limit=1`) met de eigenschap &quot;files&quot;.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSetFiles?dataSetId=5bf479a6a8c862000050e3c7"
  }
}
```

### Gegevenssetbestanden weergeven met het kenmerk &quot;files&quot;

U kunt ook een verzoek van de GET gebruiken om dossierdetails te halen gebruikend het &quot;dossiers&quot;attribuut.

**API-indeling**

```http
GET /catalog/dataSets/{DATASET_ID}/views/{VIEW_ID}/files
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/5bf479a6a8c862000050e3c7/views/5bf479a654f52014cfffe7f1/files" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwoord**

De reactie omvat identiteitskaart van het Dossier van de Dataset als top-level bezit, met dossierdetails bevat binnen het voorwerp van identiteitskaart van het Dossier van de Dataset.

```json
{
    "194e89b976494c9c8113b968c27c1472-1": {
        "batchId": "194e89b976494c9c8113b968c27c1472",
        "dataSetViewId": "5bf479a654f52014cfffe7f1",
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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
        "imsOrg": "{ORG_ID}",
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

De id&#39;s van het gegevenssetbestand die in de vorige reactie zijn geretourneerd, kunnen worden gebruikt in een GET-verzoek om meer bestandsgegevens op te halen via de [!DNL Data Access] API.

De [gegevenstoegangsoverzicht](../data-access/home.md) bevat informatie over het gebruik van de [!DNL Data Access] API.

**API-indeling**

```http
GET /export/files/{DATASET_FILE_ID}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
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

De eigenschap &quot;href&quot; kan worden gebruikt om voorvertoningsgegevens op te halen via de [[!DNL Data Access API]](../data-access/home.md).

**API-indeling**

```http
GET /export/files/{FILE_ID}?path={FILE_NAME}.{FILE_FORMAT}
```

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/ea40946ac03140ec8ac4f25da360620a-1?path=samplefile.parquet" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Het antwoord op het bovenstaande verzoek bevat een voorvertoning van de inhoud van het bestand.

Meer informatie over de [!DNL Data Access] API, met inbegrip van gedetailleerde verzoeken en reacties, is beschikbaar in [gegevenstoegangsoverzicht](../data-access/home.md).

### &quot;fileDescription&quot; ophalen uit gegevensset

De bestemmingscomponent als output van getransformeerde gegevens, zal de Ingenieur van Gegevens een Dataset van de Output kiezen ([&quot;Figuur 12&quot;in het ETL- Werkschema](workflow.md)). Het XDM-schema is gekoppeld aan de uitvoergegevensset. De te schrijven gegevens worden geïdentificeerd door het kenmerk &quot;fileDescription&quot; van de gegevenssetentiteit van de API&#39;s voor gegevensdetectie. Deze informatie kan worden opgehaald met een dataset-id (`{DATASET_ID}`). De eigenschap &quot;fileDescription&quot; in het JSON-antwoord geeft de gevraagde informatie.

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
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
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

Gegevens worden geschreven naar [!DNL Experience Platform] met de [Batchverwerking-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  Gegevens schrijven is een asynchroon proces. Wanneer gegevens naar Adobe Experience Platform worden geschreven, wordt alleen een batch gemaakt en gemarkeerd als een succes nadat de gegevens volledig zijn geschreven.

Gegevens in [!DNL Experience Platform] moet worden geschreven in de vorm van Parquet-bestanden.

## Uitvoeringsfase

Wanneer de uitvoering start, leest de connector (zoals gedefinieerd in de broncomponent) de gegevens van [!DNL Experience Platform] met de [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/). Het transformatieproces leest de gegevens voor een bepaald tijdbereik. Intern, zal het partijen brondatasets vragen. Tijdens het vragen, zal het een geparameterized (het rollen voor tijdreeksgegevens, of stijgende gegevens) begindatum en lijstdatasetdossiers voor die partijen gebruiken, en begint verzoeken om gegevens voor die datasetdossiers te doen.

### Voorbeeldtransformaties

De [ETL-testtransformaties](./transformations.md) Het document bevat een aantal voorbeeldtransformaties, waaronder identiteitsbeheer en gegevenstypetoewijzingen. Gebruik deze transformaties ter referentie.

### Gegevens lezen van [!DNL Experience Platform]

Met de [[!DNL Catalog API]](https://www.adobe.io/experience-platform-apis/references/catalog/), kunt u alle batches ophalen tussen een opgegeven begin- en eindtijd en ze sorteren op de volgorde waarin ze zijn gemaakt.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Details over het filteren van batches vindt u in de [Zelfstudie over gegevenstoegang](../data-access/tutorials/dataset-data.md).

### Bestanden ophalen uit een batch

Als u de id hebt voor de batch die u zoekt (`{BATCH_ID}`), is het mogelijk om een lijst van dossiers terug te winnen die tot een specifieke partij behoren via [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/).  Nadere bijzonderheden hierover zijn te vinden in het [[!DNL Data Access] zelfstudie](../data-access/tutorials/dataset-data.md).

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Bestanden openen met bestands-id

De unieke id van een bestand gebruiken (`{FILE_ID`), [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) U kunt de specifieke details van het bestand openen, zoals de naam, grootte in bytes en een koppeling om het bestand te downloaden.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

De reactie kan naar één bestand of naar een map verwijzen. De details over elk kunnen in worden gevonden [[!DNL Data Access] zelfstudie](../data-access/tutorials/dataset-data.md).

### Bestandsinhoud openen

De [[!DNL Data Access API]](https://www.adobe.io/experience-platform-apis/references/data-access/) kan worden gebruikt om tot de inhoud van een specifiek dossier toegang te hebben. Om de inhoud op te halen, wordt een verzoek van de GET ingediend gebruikend de waarde die voor wordt teruggekeerd `_links.self.href` wanneer u een bestand opent met de bestands-id.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Het antwoord op deze aanvraag bevat de inhoud van het bestand. Voor meer informatie, met inbegrip van details over reactiepaginering, zie [Hoe kan ik-gegevens opvragen via API voor gegevenstoegang](../data-access/tutorials/dataset-data.md) zelfstudie.

### Records voor schemaconformiteit valideren

Wanneer gegevens worden geschreven, kunnen gebruikers ervoor kiezen om gegevens te valideren volgens de validatieregels die in het XDM-schema zijn gedefinieerd. Meer informatie over schemavalidatie vindt u in de [ETL Ecosystem Integration Reference Code on [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Als u de referentie-implementatie gebruikt die u kunt vinden op [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md)kunt u schemavalidatie in deze implementatie inschakelen met de eigenschap system `-DenableSchemaValidation=true`.

Validatie kan worden uitgevoerd voor logische XDM-typen, met kenmerken zoals `minLength` en `maxlength` voor tekenreeksen, `minimum` en `maximum` voor gehele getallen en meer. De [Handleiding voor ontwikkelaars van de API voor schemaregister](../xdm/api/getting-started.md) bevat een tabel met een overzicht van de XDM-typen en de eigenschappen die voor validatie kunnen worden gebruikt.

>[!NOTE]
>
>De minimum- en maximumwaarden voor de verschillende `integer` De typen zijn de MIN- en MAX-waarden die het type ondersteunt, maar deze waarden kunnen verder worden beperkt tot de minimum- en maximumwaarden die u kiest.

### Een batch maken

Zodra de gegevens worden verwerkt, zal het hulpmiddel ETL de gegevens terug schrijven naar [!DNL Experience Platform] met de [Batchverwerking-API](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Voordat gegevens kunnen worden toegevoegd aan een gegevensset, moet deze worden gekoppeld aan een batch die later wordt geüpload naar een specifieke gegevensset.

**Verzoek**

```SHELL
curl -X POST "https://platform.adobe.io/data/foundation/import/batches" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -d '{
        "datasetId":"{DATASET_ID}"
      }'
```

Meer informatie over het maken van een batch, inclusief voorbeeldaanvragen en reacties vindt u in het dialoogvenster [Overzicht van inname in batch](../ingestion/batch-ingestion/overview.md).

### Schrijven naar gegevensset

Nadat een nieuwe partij met succes tot stand is gebracht, kunnen de dossiers dan aan een specifieke dataset worden geupload. U kunt meerdere bestanden in een batch plaatsen totdat deze worden gepromoot. Bestanden kunnen worden geüpload met de API voor het uploaden van kleine bestanden. Als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden, kunt u de API voor het uploaden van grote bestanden gebruiken. Meer informatie over het gebruik van zowel het uploaden van grote als kleine bestanden vindt u in het gedeelte [Overzicht van inname in batch](../ingestion/batch-ingestion/overview.md).

**Verzoek**

Gegevens in [!DNL Experience Platform] moet worden geschreven in de vorm van Parquet-bestanden.

```shell
curl -X PUT "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}/dataSets/{DATASET_ID}/files/{FILE_NAME}.parquet" \
  -H "accept: application/json" \
  -H "x-gw-ims-org-id:{ORG_ID}" \
  -H "Authorization:Bearer ACCESS_TOKEN" \
  -H "x-api-key: API_KEY" \
  -H "content-type: application/octet-stream" \
  --data-binary "@{FILE_PATH_AND_NAME}.parquet"
```

### Batchupload voltooien

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Door dit te doen, [!DNL Catalog] Invoer &quot;DataSetFile&quot; wordt gemaakt voor de voltooide bestanden en is gekoppeld aan de gegenereerde batch. De [!DNL Catalog] batch wordt vervolgens gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd om de beschikbare gegevens in te voeren.

De gegevens worden eerst op de halteplaats op Adobe Experience Platform geland en vervolgens na catalogisering en validatie naar de uiteindelijke locatie verplaatst. De partijen zullen als succesvol worden gemerkt zodra alle gegevens naar een permanente plaats worden verplaatst.

**Verzoek**

```shell
curl -X POST "https://platform.adobe.io/data/foundation/import/batches/{BATCH_ID}?action=COMPLETE" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

Als dit lukt, retourneert de reactie HTTP Status 200 OK en is de hoofdtekst van de reactie leeg.

Het ETL-hulpmiddel zorgt ervoor dat de tijdstempel van de brongegevensset(s) wordt genoteerd wanneer de gegevens worden gelezen.

Bij de volgende transformatie-uitvoering, waarschijnlijk door planning of aanroeping van de gebeurtenis, zal ETL beginnen om de gegevens van eerder-bewaarde timestamp en alle gegevens te vragen die door:gaan.

### Laatste batchstatus ophalen

Voordat u nieuwe taken uitvoert met het gereedschap ETL, moet u controleren of de laatste batch is voltooid. De [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) een batchspecifieke optie biedt die de details van de desbetreffende partijen bevat.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Antwoord**

Nieuwe taken kunnen worden gepland als de vorige batch-&quot;status&quot;-waarde &quot;success&quot; is, zoals hieronder wordt getoond:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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

Een individuele partijstatus kan door worden teruggewonnen [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) door een verzoek tot GET in te dienen met de `{BATCH_ID}`. De `{BATCH_ID}` gebruikt zou het zelfde zijn als identiteitskaart terugkwam toen de partij werd gecreeerd.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie - geslaagd**

De volgende reactie laat een &quot;succes&quot; zien:

```json
"{BATCH_ID}": {
    "imsOrg": "{ORG_ID}",
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
    "imsOrg": "{ORG_ID}",
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

Hiertoe gebruiken de gegevensbeheerders van de client de [!DNL Platform] UI om de batches met beschadigde gegevens te verwijderen. Vervolgens zal de ETL waarschijnlijk opnieuw moeten worden uitgevoerd, zodat de ETL met correcte gegevens kan worden gerepareerd. Als de bron zelf corrupte gegevens had, zal de gegevensingenieur/beheerder de bronpartijen moeten verbeteren en de gegevens (of in Adobe Experience Platform of via schakelaars ETL) opnieuw opnemen.

Gebaseerd op het type van gegevens die worden geproduceerd, zal het de keus van de gegevensingenieur zijn om één enkele partij of alle partijen uit bepaalde datasets te verwijderen. Gegevens worden verwijderd/gearchiveerd volgens [!DNL Experience Platform] richtsnoeren.

Het is waarschijnlijk een scenario dat de functionaliteit ETL om gegevens te zuiveren belangrijk zal zijn.

Zodra het leegmaken is voltooid, moeten de clientbeheerders Adobe Experience Platform opnieuw configureren om de verwerking voor kernservices opnieuw te starten vanaf het moment dat de batches worden verwijderd.

## Gelijktijdige batchverwerking

Naar eigen goeddunken van de klant kunnen gegevensbeheerders/engineers besluiten gegevens op sequentiële wijze of op gelijktijdige wijze te extraheren, te transformeren en te laden, afhankelijk van de kenmerken van een bepaalde gegevensset. Dit wordt ook gebaseerd op het geval waarin de client de getransformeerde gegevens gebruikt.

Bijvoorbeeld, als de cliënt aan een updatable persistentieopslag voortduurt en de opeenvolging of de orde van gebeurtenissen belangrijk is, kan de cliënt banen met opeenvolgende transformaties strikt moeten verwerken ETL.

In andere gevallen kunnen gegevens in de vorm van een out-of-order worden verwerkt door downstreamtoepassingen/processen die intern worden gesorteerd met een opgegeven tijdstempel. In die gevallen kunnen parallelle ETL-transformaties levensvatbaar zijn om de verwerkingstijd te verbeteren.

Voor bronbatches is dit weer afhankelijk van de voorkeur van de klant en de beperking van de consument. Als de brongegevens parallel kunnen worden opgepikt zonder dat rekening wordt gehouden met de urgentie/volgorde van een rij, kan het transformatieproces procesbatches maken met een hogere mate van parallellisme (optimalisatie gebaseerd op verwerking buiten bestelling). Maar als de transformatie tijdstempels moet respecteren of belangrijkheidsvolgorde moet wijzigen, moeten de API voor gegevenstoegang of ETL-toolplanner/aanroeping ervoor zorgen dat batches waar mogelijk niet buiten de bestelling worden verwerkt.

## Uitstel

Uitstel is een proces waarbij de inputgegevens nog niet volledig genoeg zijn om naar downstreamprocessen te worden verzonden, maar in de toekomst bruikbaar kunnen zijn. Clients zullen hun individuele tolerantie voor gegevensramen voor toekomstige matching tegenover de kosten van verwerking bepalen om hun beslissing om gegevens te reserveren en opnieuw te verwerken in de volgende transformatieuitvoering te informeren, in de hoop dat het op een bepaald tijdstip in het bewaarvenster kan worden verrijkt en in overeenstemming gebracht/vastgemaakt. Deze cyclus loopt tot de rij voldoende is verwerkt of te groot wordt geacht om te blijven investeren in. Elke herhaling genereert uitgestelde gegevens die een superset zijn van alle uitgestelde gegevens in vorige herhalingen.

Adobe Experience Platform identificeert momenteel geen uitgestelde gegevens, zodat de cliëntimplementaties op de ETL en de handconfiguraties van Dataset moeten vertrouwen om een andere dataset in te leiden [!DNL Platform] het weerspiegelen van de brondataset die kan worden gebruikt om uitgestelde gegevens te houden. In dit geval zijn uitgestelde gegevens vergelijkbaar met momentopnamegegevens. Bij elke uitvoering van de ETL-transformatie worden de brongegevens verenigd met uitgestelde gegevens en verzonden voor verwerking.

## Changelog

| Datum | Actie | Beschrijving |
| ---- | ------ | ----------- |
| 2019-01-19 | Eigenschap &quot;fields&quot; uit gegevenssets verwijderd | Datasets bevatten eerder een eigenschap &quot;fields&quot; die een kopie van het schema bevatte. Deze mogelijkheid mag niet meer worden gebruikt. Als de eigenschap &quot;fields&quot; wordt gevonden, moet deze worden genegeerd en wordt in plaats daarvan &quot;ObservedSchema&quot; of &quot;schemaRef&quot; gebruikt. |
| 2019-03-15 | &quot;schemaRef&quot;-eigenschap toegevoegd aan gegevenssets | Het &quot;schemaRef&quot;bezit van een dataset bevat URI die naar het XDM schema verwijst waarop de dataset gebaseerd is en vertegenwoordigt alle potentiële gebieden die door de dataset zouden kunnen worden gebruikt. |
| 2019-03-15 | Alle eindgebruikersidentificatoren wijzen de eigenschap &quot;identityMap&quot; toe | De &quot;identityMap&quot;is een inkapseling van alle unieke herkenningstekens van een onderwerp, zoals identiteitskaart van CRM, ECID, of identiteitskaart van het loyaliteitsprogramma Deze kaart wordt gebruikt door [[!DNL Identity Service]](../identity-service/home.md) om alle bekende en anonieme identiteiten van een onderwerp op te lossen, en één identiteitsgrafiek voor elke eindgebruiker te vormen. |
| 2019-05-30 | EOL en verwijder &quot;schema&quot;bezit uit datasets | De dataset &quot;schema&quot;bezit verstrekte een verwijzingsverbinding aan het schema gebruikend afgekeurd `/xdms` in de [!DNL Catalog] API. Dit is vervangen door een &quot;schemaRef&quot;die &quot;id&quot;, &quot;versie&quot;, en &quot;contentType&quot;van het schema zoals die in het nieuwe wordt van verwijzingen voorzien [!DNL Schema Registry] API. |
