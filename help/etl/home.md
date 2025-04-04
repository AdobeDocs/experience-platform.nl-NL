---
keywords: Experience Platform;home;populaire onderwerpen;ETL;etl;etl integratie;ETL-integratie
solution: Experience Platform
title: Ontwikkeling van ETL-integratie voor Adobe Experience Platform
description: In de ETL-integratiehandleiding worden algemene stappen beschreven voor het maken van krachtige, veilige connectors voor Experience Platform en het opnemen van gegevens in Experience Platform.
exl-id: 7d29b61c-a061-46f8-a31f-f20e4d725655
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '3978'
ht-degree: 0%

---

# Ontwikkeling van ETL-integratie voor Adobe Experience Platform

In de ETL-integratiehandleiding worden algemene stappen beschreven voor het maken van krachtige, veilige connectors voor [!DNL Experience Platform] en het opnemen van gegevens in [!DNL Experience Platform] .


- [[!DNL Catalog]](https://www.adobe.io/experience-platform-apis/references/catalog/)
- [[!DNL Data Access]](https://www.adobe.io/experience-platform-apis/references/data-access/)
- [[!DNL Batch Ingestion]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/)
- [[!DNL Streaming Ingestion]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)
- [ Authentificatie en Vergunning voor Experience Platform APIs ](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/experience-platform-apis/references/schema-registry/)

Deze handleiding bevat ook voorbeeld-API-aanroepen die moeten worden gebruikt bij het ontwerpen van een ETL-connector, met koppelingen naar documentatie die elke [!DNL Experience Platform] -service beschrijft en meer in detail het gebruik van de bijbehorende API.

Een steekproefintegratie is beschikbaar op [!DNL GitHub] via de [ Code van de Verwijzing van de Integratie van het Ecosysteem ETL ](https://github.com/adobe/acp-data-services-etl-reference) onder [!DNL Apache] Versie van de Vergunning 2.0.

## Workflow

Het volgende workflowdiagram biedt een overzicht op hoog niveau voor de integratie van Adobe Experience Platform-componenten met een ETL-toepassing en -aansluiting.

![](images/etl.png)

## Adobe Experience Platform-componenten

Er zijn veelvoudige Experience Platform componenten betrokken bij ETL schakelaarintegratie. In de volgende lijst worden verschillende belangrijke componenten en functies beschreven:

- **Adobe Identity Management Systeem (IMS)** - verstrekt kader voor authentificatie aan de diensten van Adobe.
- **IMS Organisatie** - een collectieve entiteit die producten en de diensten kan bezitten of vergunning geven en toegang tot zijn leden toestaan.
- **IMS Gebruiker** - leden van een organisatie IMS. De relatie Organisatie met gebruiker is veel te veel.
- **[!DNL Sandbox]** - Een virtuele partitie met één [!DNL Experience Platform] -instantie die u helpt bij het ontwikkelen en ontwikkelen van toepassingen voor digitale ervaringen.
- **Ontdekking van Gegevens** - registreert de meta-gegevens van ingebedde en getransformeerde gegevens in [!DNL Experience Platform].
- **[!DNL Data Access]** - Biedt gebruikers een interface voor toegang tot hun gegevens in [!DNL Experience Platform] .
- **[!DNL Data Ingestion]** - Past gegevens naar [!DNL Experience Platform] met [!DNL Data Ingestion] API&#39;s.
- **[!DNL Schema Registry]** - Definieert en slaat schema op dat de structuur van gegevens beschrijft die in [!DNL Experience Platform] moeten worden gebruikt.

## Aan de slag met [!DNL Experience Platform] API&#39;s

De volgende secties bevatten aanvullende informatie die u nodig hebt of die u zelf nodig hebt om aanroepen van [!DNL Experience Platform] API&#39;s te kunnen uitvoeren.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproef API vraag worden gebruikt, zie de sectie op [ hoe te om voorbeeld API vraag ](../landing/troubleshooting.md#how-do-i-format-an-api-request) in de [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Om vraag aan [!DNL Experience Platform] APIs te maken, moet u het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) eerst voltooien. Als u de zelfstudie over verificatie voltooit, krijgt u de waarden voor elk van de vereiste headers in alle API-aanroepen van [!DNL Experience Platform] , zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen naar [!DNL Experience Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Voor meer informatie over zandbakken in [!DNL Experience Platform], zie de [ documentatie van het zandbakoverzicht ](../sandboxes/home.md).

Alle verzoeken die een lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Algemene gebruikersstroom

Om te beginnen, registreert een gebruiker ETL in het [!DNL Experience Platform] gebruikersinterface (UI) en leidt datasets voor opname gebruikend een standaardschakelaar of een duw-dienst schakelaar.

In UI, leidt de gebruiker tot de outputdataset door een datasetschema te selecteren. De keuze van het schema hangt af van het type gegevens (record- of tijdreeks) dat in [!DNL Experience Platform] wordt opgenomen. Door op het lusje van Schema binnen UI te klikken, zal de gebruiker alle beschikbare schema&#39;s, met inbegrip van het gedragstype kunnen bekijken dat het schema steunt.

In ETL zal de gebruiker beginnen hun toewijzingstransformaties te ontwerpen nadat de aangewezen verbinding (gebruikend hun geloofsbrieven) wordt gevormd. Er wordt aangenomen dat voor het ETL-hulpprogramma al [!DNL Experience Platform] -connectors zijn geïnstalleerd (proces niet gedefinieerd in deze integratiegids).

Mockups voor een hulpmiddel en een werkschema van steekproefETL zijn verstrekt in het [ werkschema ETL ](./workflow.md). Hoewel de ETL-gereedschappen verschillende indelingen kunnen hebben, zijn de meeste toepassingen beschikbaar voor vergelijkbare functies.

>[!NOTE]
>
>De ETL-aansluiting moet een tijdstempelfilter opgeven waarmee de datum voor het invoeren van gegevens en verschuiving (d.w.z. Het venster waarvoor gegevens moeten worden gelezen). Het ETL-hulpmiddel moet het gebruik van deze twee parameters in deze of een andere relevante interface ondersteunen. In Adobe Experience Platform worden deze parameters toegewezen aan beschikbare datums (indien aanwezig) of vastgelegde datums in het batchobject van de gegevensset.

### Lijst met gegevenssets weergeven

Gebruikend de bron van gegevens voor afbeelding, kan een lijst van alle beschikbare datasets worden gehaald gebruikend [[!DNL Catalog API] ](https://www.adobe.io/experience-platform-apis/references/catalog/).

U kunt één enkele API verzoek uitgeven om alle beschikbare datasets (b.v. `GET /dataSets`) te bekijken, met beste praktijken die zijn om vraagparameters te omvatten die de grootte van de reactie beperken.

In gevallen waarin volledige gegevenssetinformatie wordt gevraagd, kan de antwoordlading voorbij 3 GB in grootte bereiken, die algemene prestaties kan vertragen. Daarom zal het gebruiken van vraagparameters om slechts de benodigde informatie te filtreren [!DNL Catalog] vragen efficiënter maken.

#### Filteren op List

Wanneer het filtreren van reacties, kunt u veelvoudige filters in één enkele vraag gebruiken door parameters met een ampersand (`&`) te scheiden. Sommige queryparameters accepteren door komma&#39;s gescheiden lijsten met waarden, zoals het filter &quot;Eigenschappen&quot; in de voorbeeldaanvraag hieronder.

[!DNL Catalog] de reacties worden automatisch gemeten volgens gevormde grenzen, nochtans kan de &quot;grens&quot;vraagparameter worden gebruikt om de beperkingen aan te passen en het aantal teruggekeerde voorwerpen te beperken. De vooraf geconfigureerde limiet voor de respons van [!DNL Catalog] is:

- Als er geen limietparameter is opgegeven, is het maximumaantal objecten per antwoordlading 20.
- De algemene limiet voor alle andere [!DNL Catalog] query&#39;s is 100 objecten.
- Voor datasetvragen, als observableSchema wordt gevraagd gebruikend de parameter van de eigenschappenvraag, is het maximumaantal teruggekeerde datasets 20.
- Ongeldige limietparameters (inclusief `limit=0`) worden gevonden met een HTTP 400-fout die juiste bereiken beschrijft.
- Als limieten of verschuivingen als queryparameters worden doorgegeven, hebben ze voorrang op de parameters die als kopteksten worden doorgegeven.

De parameters van de vraag worden behandeld in meer detail in het [ overzicht van de Dienst van de Catalogus ](../catalog/home.md).

**API formaat**

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

Gelieve te verwijzen naar het [ overzicht van de Dienst van de Catalogus ](../catalog/home.md) voor gedetailleerde voorbeelden van hoe te om vraag aan [[!DNL Catalog API] te maken ](https://www.adobe.io/experience-platform-apis/references/catalog/).

**Reactie**

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

Het &quot;schemaRef&quot;bezit van een dataset bevat URI die het XDM schema van verwijzingen voorzien waarop de dataset gebaseerd is. Het XDM-schema (&quot;schemaRef&quot;) vertegenwoordigt alle potentiële velden die door de dataset kunnen worden gebruikt, niet noodzakelijkerwijs de velden die worden gebruikt (zie &quot;observableSchema&quot; hieronder).

Het XDM-schema is het schema dat u gebruikt wanneer u de gebruiker een lijst moet geven met alle beschikbare velden waarnaar kan worden geschreven.

De eerste &quot;schemaRef.id&quot;waarde in het vorige reactievoorwerp (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) is URI die aan een specifiek schema XDM in [!DNL Schema Registry] richt. Het schema kan worden opgehaald door een opzoekaanvraag (GET) in te dienen bij de API van [!DNL Schema Registry] .

>[!NOTE]
>
>De eigenschap &quot;schemaRef&quot; vervangt de nu afgekeurde eigenschap &quot;schema&quot;. Als &quot;schemaRef&quot;van de dataset afwezig is of geen waarde bevat, zult u de aanwezigheid van een &quot;schema&quot;bezit moeten controleren. Dit zou kunnen worden gedaan door &quot;schemaRef&quot;met &quot;schema&quot;in de `properties` vraagparameter in de vorige vraag te vervangen. Meer details op het &quot;schema&quot;bezit zijn beschikbaar in de [ sectie van het Bezit van de Dataset &quot;schema&quot;dat volgt.](#dataset-schema-property-deprecated---eol-2019-05-30)

**API formaat**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Verzoek**

De aanvraag gebruikt de URL-gecodeerde `id` URI van het schema (de waarde van het kenmerk &quot;schemaRef.id&quot;) en vereist een Accept-header.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

De responsindeling is afhankelijk van het type Accept-header dat in de aanvraag wordt verzonden. Voor opzoekverzoeken moet ook een `version` worden opgenomen in de koptekst Accepteren. In de volgende tabel worden de beschikbare kopteksten voor zoekopdrachten geaccepteerd:

| Accepteren | Beschrijving |
| ------ | ----------- |
| `application/vnd.adobe.xed-id+json` | Aanvragen, titels, id&#39;s en versies van List (GET) |
| `application/vnd.adobe.xed-full+json; version={major version}` | $refs en allOf opgelost, heeft titels en beschrijvingen |
| `application/vnd.adobe.xed+json; version={major version}` | Onbewerkt met $ref en alles, heeft titels en beschrijvingen |
| `application/vnd.adobe.xed-notext+json; version={major version}` | Onbewerkt met $ref en alles, geen titels of beschrijvingen |
| `application/vnd.adobe.xed-full-notext+json; version={major version}` | $refs en allOf opgelost, geen titels of beschrijvingen |
| `application/vnd.adobe.xed-full-desc+json; version={major version}` | $refs en alle opgeloste, omschrijvingen inbegrepen |

>[!NOTE]
>
>`application/vnd.adobe.xed-id+json` en `application/vnd.adobe.xed-full+json; version={major version}` zijn de meestgebruikte Accepteerkoppen. `application/vnd.adobe.xed-id+json` heeft de voorkeur voor het weergeven van bronnen in de [!DNL Schema Registry] omdat alleen de titel, id en version worden geretourneerd. `application/vnd.adobe.xed-full+json; version={major version}` heeft de voorkeur voor het weergeven van een specifieke bron (aan de hand van de id), aangezien deze alle velden (genest onder &quot;eigenschappen&quot;) retourneert, evenals titels en beschrijvingen.

**Reactie**

Het JSON-schema dat wordt geretourneerd, beschrijft de structuur en veldniveauinformatie (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, enz.) van de gegevens, geserialiseerd als JSON. Als het gebruiken van een rangschikkingsformaat buiten JSON voor opname (zoals Parquet of Scala), bevat de [ Gids van de Registratie van het Schema ](../xdm/tutorials/create-schema-api.md) een lijst die het gewenste type JSON (&quot;meta:xdmType&quot;) en zijn overeenkomstige vertegenwoordiging in andere formaten tonen.

Samen met deze tabel bevat de [!DNL Schema Registry] Developer Guide diepgaande voorbeelden van alle mogelijke aanroepen die met de [!DNL Schema Registry] API kunnen worden uitgevoerd.

### De eigenschap &quot;schema&quot; van de gegevensset (VEROUDERD - EOL 2019-05-30)

Datasets kunnen een eigenschap &quot;schema&quot; bevatten die nu is vervangen en tijdelijk beschikbaar blijft voor achterwaartse compatibiliteit. Een aanbiedingsaanvraag (GET) die vergelijkbaar is met de eerder ingediende aanvraag, waarbij &quot;schema&quot; in de parameter `properties` is vervangen door &quot;schema&quot;, retourneert bijvoorbeeld het volgende:

```json
{
  "5ba9452f7de80400007fc52a": {
    "name": "Sample Dataset 1",
    "description": "Description of Sample Dataset 1.",
    "schema": "@/xdms/context/person"
  }
}
```

Als het &quot;schema&quot;bezit van een dataset wordt bevolkt, wijst dit erop dat het schema een afgekeurd `/xdms` schema is en, waar gesteund, zou de schakelaar ETL de waarde in het &quot;schema&quot;bezit met het `/xdms` eindpunt (een afgekeurd eindpunt in [[!DNL Catalog API] ](https://www.adobe.io/experience-platform-apis/references/catalog/)) moeten gebruiken om het erfenisschema terug te winnen.

**API formaat**

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
>Een optionele queryparameter, `expansion=xdm` , geeft de API de opdracht om schema&#39;s waarnaar wordt verwezen, volledig uit te breiden en in regel in te voeren. Dit kunt u doen wanneer u een lijst met alle mogelijke velden aan de gebruiker presenteert.

**Reactie**

Gelijkaardig aan de stappen voor [ het bekijken datasetschema ](#view-dataset-schema), bevat de reactie een schema JSON dat de structuur en gebied-vlakke informatie van de gegevens beschrijft, als JSON in series vervaardigd.

>[!NOTE]
>
>Wanneer het &quot;schema&quot;gebied leeg is of volledig afwezig, zou de schakelaar het &quot;schemaRef&quot;gebied moeten lezen en de [ Registratie API van het Schema ](https://www.adobe.io/experience-platform-apis/references/schema-registry/) zoals aangetoond in de vorige stappen gebruiken om [ een datasetschema ](#view-dataset-schema) te bekijken.

### De eigenschap &quot;observableSchema&quot;

De eigenschap &quot;observableSchema&quot; van een dataset heeft een JSON-structuur die overeenkomt met die van het XDM-schema JSON. Het &quot;observableSchema&quot; bevat de velden die aanwezig waren in de binnenkomende invoerbestanden. Wanneer u gegevens naar [!DNL Experience Platform] schrijft, hoeft een gebruiker niet elk veld in het doelschema te gebruiken. In plaats daarvan moeten ze alleen die velden leveren die worden gebruikt.

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

De toepassing ETL kan een vermogen aan voorproefgegevens ([ &quot;Figuur 8&quot;in het ETL- Werkschema verstrekken ](./workflow.md)). De API voor gegevenstoegang biedt verschillende opties voor het voorvertonen van gegevens.

De extra informatie, met inbegrip van geleidelijke begeleiding voor het voorvertonen van gegevens die API gebruiken van de gegevenstoegang, kan in het [ leerprogramma van de gegevenstoegang ](../data-access/tutorials/dataset-data.md) worden gevonden.

### Krijg datasetdetails gebruikend de &quot;eigenschappen&quot;vraagparameter

Zoals aangetoond in de stappen hierboven aan [ mening een lijst van datasets ](#view-list-of-datasets), kunt u &quot;dossiers&quot;verzoeken gebruikend de &quot;eigenschappen&quot;vraagparameter.

U kunt naar het [ overzicht van de Dienst van de Catalogus ](../catalog/home.md) voor gedetailleerde informatie over het vragen van datasets en beschikbare reactiefilters verwijzen.

**API formaat**

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

**Reactie**

De reactie zal één dataset (`limit=1`) omvatten die het &quot;dossiers&quot;bezit tonen.

```json
{
  "5bf479a6a8c862000050e3c7": {
    "files": "@/dataSetFiles?dataSetId=5bf479a6a8c862000050e3c7"
  }
}
```

### Gegevenssetbestanden weergeven met het kenmerk &quot;files&quot;

U kunt ook een GET-aanvraag gebruiken om bestandsgegevens op te halen met het kenmerk &quot;files&quot;.

**API formaat**

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

**Reactie**

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

De id&#39;s van het gegevensbestand die in de vorige reactie zijn geretourneerd, kunnen worden gebruikt in een GET-verzoek om meer bestandsgegevens op te halen via de [!DNL Data Access] API.

Het [ overzicht van de gegevenstoegang ](../data-access/home.md) bevat details op hoe te om [!DNL Data Access] API te gebruiken.

**API formaat**

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

**Reactie**

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

De eigenschap &quot;href&quot; kan worden gebruikt om voorvertoningsgegevens op te halen via de [[!DNL Data Access API]](../data-access/home.md) .

**API formaat**

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

Meer informatie over [!DNL Data Access] API, met inbegrip van gedetailleerde verzoeken en reacties, is beschikbaar in het [ overzicht van de gegevenstoegang ](../data-access/home.md).

### &quot;fileDescription&quot; ophalen uit gegevensset

De bestemmingscomponent als output van getransformeerde gegevens, zal de Ingenieur van Gegevens een Dataset van de Output ([ &quot;Figuur 12&quot;in het ETL- Werkschema ](workflow.md)) kiezen. Het XDM-schema is gekoppeld aan de uitvoergegevensset. De te schrijven gegevens worden geïdentificeerd door het kenmerk &quot;fileDescription&quot; van de gegevenssetentiteit van de API&#39;s voor gegevensdetectie. Deze informatie kan worden opgehaald gebruikend een dataset identiteitskaart (`{DATASET_ID}`). De eigenschap &quot;fileDescription&quot; in het JSON-antwoord geeft de gevraagde informatie.

**API formaat**

```shell
GET /catalog/dataSets/{DATASET_ID}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `{DATASET_ID}` | De `id` -waarde van de gegevensset waartoe u toegang probeert te krijgen. |

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/dataSets/59c93f3da7d0c00000798f68" \
-H "accept: application/json" \
-H "x-gw-ims-org-id: {ORG_ID}" \
-H "x-sandbox-name: {SANDBOX_NAME}" \
-H "Authorization: Bearer {ACCESS_TOKEN}" \
-H "x-api-key: {API_KEY}"
```

**Reactie**

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

De gegevens zullen aan [!DNL Experience Platform] worden geschreven gebruikend [ de Ingestie API van de Partij ](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/).  Gegevens schrijven is een asynchroon proces. Wanneer gegevens naar Adobe Experience Platform worden geschreven, wordt alleen een batch gemaakt en gemarkeerd als een succes nadat de gegevens volledig zijn geschreven.

Gegevens in [!DNL Experience Platform] moeten worden geschreven in de vorm van Parquet-bestanden.

## Uitvoeringsfase

Terwijl de uitvoering start, zal de connector (zoals gedefinieerd in de broncomponent) de gegevens lezen vanuit [!DNL Experience Platform] met behulp van [[!DNL Data Access API] ](https://www.adobe.io/experience-platform-apis/references/data-access/) . Het transformatieproces leest de gegevens voor een bepaald tijdbereik. Intern, zal het partijen brondatasets vragen. Tijdens het vragen, zal het een geparameterized (het rollen voor tijdreeksgegevens, of stijgende gegevens) begindatum en lijstdatasetdossiers voor die partijen gebruiken, en begint verzoeken om gegevens voor die datasetdossiers te doen.

### Voorbeeldtransformaties

Het [ de transformaties van steekproefETL ](./transformations.md) document bevat een aantal voorbeeldtransformaties, met inbegrip van identiteit behandeling en gegevens-type afbeeldingen. Gebruik deze transformaties ter referentie.

### Gegevens lezen uit [!DNL Experience Platform]

Gebruikend [[!DNL Catalog API] ](https://www.adobe.io/experience-platform-apis/references/catalog/), kunt u alle partijen tussen een gespecificeerde begintijd en eindtijd ophalen, en hen sorteren op de orde zij werden gecreeerd.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

De details op het filtreren van partijen kunnen in het [ leerprogramma van de Toegang van Gegevens ](../data-access/tutorials/dataset-data.md) worden gevonden.

### Bestanden ophalen uit een batch

Zodra u identiteitskaart voor de partij hebt u zoekt (`{BATCH_ID}`), is het mogelijk om een lijst van dossiers terug te winnen die tot een specifieke partij via [[!DNL Data Access API] behoren ](https://www.adobe.io/experience-platform-apis/references/data-access/).  De details voor het doen dit zijn beschikbaar in het [[!DNL Data Access]  leerprogramma ](../data-access/tutorials/dataset-data.md).

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

### Bestanden openen met bestands-id

Gebruikend unieke identiteitskaart van een dossier (`{FILE_ID`), [[!DNL Data Access API] ](https://www.adobe.io/experience-platform-apis/references/data-access/) kan worden gebruikt om tot de specifieke details van het dossier, met inbegrip van zijn naam, grootte in bytes, en een verbinding toegang te hebben om het te downloaden.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

De reactie kan naar één bestand of naar een map verwijzen. De details op elk kunnen in het [[!DNL Data Access]  leerprogramma ](../data-access/tutorials/dataset-data.md) worden gevonden.

### Bestandsinhoud openen

[[!DNL Data Access API] ](https://www.adobe.io/experience-platform-apis/references/data-access/) kan worden gebruikt om tot de inhoud van een specifiek dossier toegang te hebben. Om de inhoud op te halen, wordt een GET-aanvraag gedaan met de waarde die voor `_links.self.href` wordt geretourneerd wanneer een bestand wordt geopend met de bestands-id.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Het antwoord op deze aanvraag bevat de inhoud van het bestand. Voor meer informatie, met inbegrip van details op antwoordpaginering, zie [ hoe te Gegevens van de Vraag via de toegang API van de gegevenstoegang ](../data-access/tutorials/dataset-data.md) leerprogramma.

### Records voor schemaconformiteit valideren

Wanneer gegevens worden geschreven, kunnen gebruikers ervoor kiezen om gegevens te valideren volgens de validatieregels die in het XDM-schema zijn gedefinieerd. Meer informatie over schemabevestiging kan in de [ ETL Code van de Verwijzing van de Integratie van het Ecosysteem op  [!DNL GitHub] worden gevonden ](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation).

Als u de verwijzingsimplementatie gebruikt die op [[!DNL GitHub] wordt gevonden ](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md), kunt u schemabevestiging in deze implementatie aanzetten gebruikend het systeembezit `-DenableSchemaValidation=true`.

Validatie kan worden uitgevoerd voor logische XDM-typen, met kenmerken zoals `minLength` en `maxlength` voor tekenreeksen, `minimum` en `maximum` voor gehele getallen en meer. De [ de ontwikkelaarsgids van de Registratie van het Schema API ](../xdm/api/getting-started.md) bevat een lijst die types XDM en de eigenschappen schetst die voor bevestiging kunnen worden gebruikt.

>[!NOTE]
>
>De minimum- en maximumwaarden die voor verschillende `integer` -typen worden opgegeven, zijn de MIN- en MAX-waarden die door het type worden ondersteund, maar deze waarden kunnen verder worden beperkt tot de minimum- en maximumwaarden van uw keuze.

### Een batch maken

Zodra het gegeven wordt verwerkt, zal het hulpmiddel ETL de gegevens terug naar [!DNL Experience Platform] schrijven gebruikend [ de Ingestie API van de Partij ](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/). Voordat gegevens kunnen worden toegevoegd aan een gegevensset, moet deze worden gekoppeld aan een batch die later wordt geüpload naar een specifieke gegevensset.

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

De details voor het creëren van een partij, met inbegrip van steekproefverzoeken en reacties kunnen in het [ overzicht van de Opname van de Partij van de Partij ](../ingestion/batch-ingestion/overview.md) worden gevonden.

### Schrijven naar gegevensset

Nadat een nieuwe partij met succes tot stand is gebracht, kunnen de dossiers dan aan een specifieke dataset worden geupload. U kunt meerdere bestanden in een batch plaatsen totdat deze worden gepromoot. Bestanden kunnen worden geüpload met de API voor het uploaden van kleine bestanden. Als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden, kunt u de API voor het uploaden van grote bestanden gebruiken. De details voor het gebruiken van zowel Groot als Klein Dossier uploaden kunnen in het [ overzicht van de Opname van de Partij van de Partij ](../ingestion/batch-ingestion/overview.md) worden gevonden.

**Verzoek**

Gegevens in [!DNL Experience Platform] moeten worden geschreven in de vorm van Parquet-bestanden.

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

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Op deze manier worden de [!DNL Catalog] &quot;DataSetFile&quot;-items gemaakt voor de voltooide bestanden en gekoppeld aan de generatiebatch. De batch [!DNL Catalog] wordt vervolgens gemarkeerd als succesvol, waardoor stroomafwaartse stromen worden geactiveerd om de beschikbare gegevens in te voeren.

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

Voordat u nieuwe taken uitvoert met het gereedschap ETL, moet u controleren of de laatste batch is voltooid. [[!DNL Catalog Service API] ](https://www.adobe.io/experience-platform-apis/references/catalog/) verstrekt een batch-specifieke optie die de details van de relevante partijen verstrekt.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?limit=1&sort=desc:created" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie**

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

Een individuele partijstatus kan door [[!DNL Catalog Service API] ](https://www.adobe.io/experience-platform-apis/references/catalog/) worden teruggewonnen door een GET- verzoek uit te geven gebruikend `{BATCH_ID}`. De gebruikte `{BATCH_ID}` zou dezelfde zijn als de id die werd geretourneerd toen de batch werd gemaakt.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches/{BATCH_ID}" \
  -H "Accept: application/json" \
  -H "x-gw-ims-org-id: {ORG_ID}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key: {API_KEY}"
```

**Reactie - Succes**

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

**Reactie - Mislukking**

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

Hiertoe gebruiken de gegevensbeheerders van de client de gebruikersinterface van [!DNL Experience Platform] om de batches met beschadigde gegevens te verwijderen. Vervolgens zal de ETL waarschijnlijk opnieuw moeten worden uitgevoerd, zodat de ETL met correcte gegevens kan worden gerepareerd. Als de bron zelf corrupte gegevens had, zal de gegevensingenieur/beheerder de bronpartijen moeten verbeteren en de gegevens (of in Adobe Experience Platform of via schakelaars ETL) opnieuw opnemen.

Gebaseerd op het type van gegevens die worden geproduceerd, zal het de keus van de gegevensingenieur zijn om één enkele partij of alle partijen uit bepaalde datasets te verwijderen. Gegevens worden verwijderd/gearchiveerd volgens de [!DNL Experience Platform] richtlijnen.

Het is waarschijnlijk een scenario dat de functionaliteit ETL om gegevens te zuiveren belangrijk zal zijn.

Zodra het leegmaken is voltooid, moeten de clientbeheerders Adobe Experience Platform opnieuw configureren om de verwerking voor kernservices opnieuw te starten vanaf het moment dat de batches worden verwijderd.

## Gelijktijdige batchverwerking

Naar eigen goeddunken van de klant kunnen gegevensbeheerders/engineers besluiten gegevens op sequentiële wijze of op gelijktijdige wijze te extraheren, te transformeren en te laden, afhankelijk van de kenmerken van een bepaalde gegevensset. Dit wordt ook gebaseerd op het geval waarin de client de getransformeerde gegevens gebruikt.

Bijvoorbeeld, als de cliënt aan een updatable persistentieopslag voortduurt en de opeenvolging of de orde van gebeurtenissen belangrijk is, kan de cliënt banen met opeenvolgende transformaties strikt moeten verwerken ETL.

In andere gevallen kunnen gegevens in de vorm van een out-of-order worden verwerkt door downstreamtoepassingen/processen die intern worden gesorteerd met een opgegeven tijdstempel. In die gevallen kunnen parallelle ETL-transformaties levensvatbaar zijn om de verwerkingstijd te verbeteren.

Voor bronbatches is dit weer afhankelijk van de voorkeur van de klant en de beperking van de consument. Als de brongegevens parallel kunnen worden opgepikt zonder dat rekening wordt gehouden met de urgentie/volgorde van een rij, kan het transformatieproces procesbatches maken met een hogere mate van parallellisme (optimalisatie gebaseerd op verwerking buiten bestelling). Maar als de transformatie tijdstempels moet respecteren of belangrijkheidsvolgorde moet wijzigen, moeten de API voor gegevenstoegang of ETL-toolplanner/aanroeping ervoor zorgen dat batches waar mogelijk niet buiten de bestelling worden verwerkt.

## Uitstel

Uitstel is een proces waarbij de inputgegevens nog niet volledig genoeg zijn om naar downstreamprocessen te worden verzonden, maar in de toekomst bruikbaar kunnen zijn. Clients zullen hun individuele tolerantie voor gegevensramen voor toekomstige matching tegenover de kosten van verwerking bepalen om hun beslissing om gegevens te reserveren en opnieuw te verwerken in de volgende transformatieuitvoering te informeren, in de hoop dat het op een bepaald tijdstip in het bewaarvenster kan worden verrijkt en in overeenstemming gebracht/vastgemaakt. Deze cyclus loopt tot de rij voldoende is verwerkt of te groot wordt geacht om te blijven investeren in. Elke herhaling genereert uitgestelde gegevens die een superset zijn van alle uitgestelde gegevens in vorige herhalingen.

Adobe Experience Platform identificeert momenteel geen uitgestelde gegevens, zodat moeten de cliëntimplementaties zich op de ETL en de handconfiguraties van Dataset baseren om een andere dataset in [!DNL Experience Platform] te creëren die de brondataset weerspiegelt die kan worden gebruikt om uitgestelde gegevens te houden. In dit geval zijn uitgestelde gegevens vergelijkbaar met momentopnamegegevens. Bij elke uitvoering van de ETL-transformatie worden de brongegevens verenigd met uitgestelde gegevens en verzonden voor verwerking.

## Changelog

| Datum | Actie | Beschrijving |
| ---- | ------ | ----------- |
| 2019-01-19 | Eigenschap &quot;fields&quot; uit gegevenssets verwijderd | Datasets bevatten eerder een eigenschap &quot;fields&quot; die een kopie van het schema bevatte. Deze mogelijkheid mag niet meer worden gebruikt. Als de eigenschap &quot;fields&quot; wordt gevonden, moet deze worden genegeerd en wordt in plaats daarvan &quot;ObservedSchema&quot; of &quot;schemaRef&quot; gebruikt. |
| 2019-03-15 | &quot;schemaRef&quot;-eigenschap toegevoegd aan gegevenssets | Het &quot;schemaRef&quot;bezit van een dataset bevat URI die naar het XDM schema verwijst waarop de dataset gebaseerd is en vertegenwoordigt alle potentiële gebieden die door de dataset zouden kunnen worden gebruikt. |
| 2019-03-15 | Alle eindgebruikersidentificatoren wijzen de eigenschap &quot;identityMap&quot; toe | De &quot;identityMap&quot;is een inkapseling van alle unieke herkenningstekens van een onderwerp, zoals CRMID, ECID, of identiteitskaart van het loyaliteitsprogramma. Deze kaart wordt door [[!DNL Identity Service]](../identity-service/home.md) gebruikt om alle bekende en anonieme identiteiten van een onderwerp op te lossen en vormt één identiteitsgrafiek voor elke eindgebruiker. |
| 2019-05-30 | EOL en verwijder &quot;schema&quot;bezit uit datasets | De dataset &quot;schema&quot;bezit verstrekte een verwijzingsverbinding aan het schema gebruikend het afgekeurde `/xdms` eindpunt in [!DNL Catalog] API. Deze is vervangen door een &quot;schemaRef&quot; die de &quot;id&quot;, &quot;version&quot; en &quot;contentType&quot; van het schema biedt, zoals vermeld in de nieuwe [!DNL Schema Registry] API. |
