---
keywords: Experience Platform;thuis;populaire onderwerpen;ETL;etl;etl integraties;ETL-integratie
solution: Experience Platform
title: Ontwikkeling van ETL-integratie voor Adobe Experience Platform
topic: overview
description: De ETL-integratiehandleiding beschrijft algemene stappen voor het maken van krachtige, veilige connectors voor Experience Platform en het opnemen van gegevens in het Platform.
translation-type: tm+mt
source-git-commit: a489ab248793a063295578943ad600d8eacab6a2
workflow-type: tm+mt
source-wordcount: '4143'
ht-degree: 0%

---


# Ontwikkeling van ETL-integratie voor Adobe Experience Platform

In de ETL-integratiehandleiding worden algemene stappen beschreven voor het maken van krachtige, veilige connectors voor [!DNL Experience Platform] en het opnemen van gegevens in [!DNL Platform].


- [[!DNL Catalog]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)
- [[!DNL Data Access]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml)
- [[!DNL Data Ingestion]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)
- [Verificatie en autorisatie voor Experience Platform-API&#39;s](https://www.adobe.com/go/platform-api-authentication-en)
- [[!DNL Schema Registry]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml)

Deze handleiding bevat ook voorbeeld-API-aanroepen die moeten worden gebruikt bij het ontwerpen van een ETL-connector, met koppelingen naar documentatie waarin elke [!DNL Experience Platform]-service wordt beschreven en waarin meer in detail wordt ingegaan op het gebruik van de bijbehorende API.

Een voorbeeldintegratie is beschikbaar op [!DNL GitHub] via [ETL Ecosystem Integration Reference Code](https://github.com/adobe/acp-data-services-etl-reference) onder [!DNL Apache] License Version 2.0.

## Workflow

Het volgende workflowdiagram biedt een overzicht op hoog niveau voor de integratie van Adobe Experience Platform-componenten met een ETL-toepassing en -aansluiting.

![](images/etl.png)

## Adobe Experience Platform-componenten

Er zijn veelvoudige Experience Platform componenten betrokken bij ETL schakelaarintegratie. In de volgende lijst worden verschillende belangrijke componenten en functies beschreven:

- **Adobe Identity Management System (IMS)** : biedt een framework voor verificatie van Adobe-services.
- **IMS-organisatie** : een organisatie die producten en diensten kan bezitten of in licentie kan geven en toegang kan verlenen tot haar leden.
- **IMS-gebruiker** : leden van een IMS-organisatie. De relatie Organisatie met gebruiker is veel te veel.
- **[!DNL Sandbox]** - Een virtuele partitie die één  [!DNL Platform] instantie vormt, om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.
- **Gegevensdetectie** : neemt de metagegevens van opgenomen en getransformeerde gegevens op in  [!DNL Experience Platform].
- **[!DNL Data Access]** - Biedt gebruikers een interface om toegang te krijgen tot hun gegevens in  [!DNL Experience Platform].
- **[!DNL Data Ingestion]** - Past gegevens aan  [!DNL Experience Platform] met  [!DNL Data Ingestion] APIs.
- **[!DNL Schema Registry]** - Definieert en slaat schema op dat de structuur van gegevens beschrijft waarin gegevens moeten worden gebruikt  [!DNL Experience Platform].

## Aan de slag met [!DNL Experience Platform] API&#39;s

De volgende secties verstrekken extra informatie die u zult moeten kennen of hebben aan hand om met succes vraag aan [!DNL Experience Platform] APIs te maken.

### API-voorbeeldaanroepen lezen

Deze gids verstrekt voorbeeld API vraag om aan te tonen hoe te om uw verzoeken te formatteren. Dit zijn paden, vereiste kopteksten en correct opgemaakte ladingen voor aanvragen. Voorbeeld-JSON die wordt geretourneerd in API-reacties, wordt ook verschaft. Voor informatie over de overeenkomsten die in documentatie voor steekproefAPI vraag worden gebruikt, zie de sectie over [hoe te om voorbeeld API vraag](../landing/troubleshooting.md#how-do-i-format-an-api-request) in [!DNL Experience Platform] het oplossen van problemengids te lezen.

### Waarden verzamelen voor vereiste koppen

Als u [!DNL Platform] API&#39;s wilt aanroepen, moet u eerst de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en) voltooien. Het voltooien van de zelfstudie over verificatie biedt de waarden voor elk van de vereiste headers in alle API-aanroepen [!DNL Experience Platform], zoals hieronder wordt getoond:

- Autorisatie: Drager `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Alle bronnen in [!DNL Experience Platform] zijn geïsoleerd naar specifieke virtuele sandboxen. Alle aanvragen voor [!DNL Platform] API&#39;s vereisen een header die de naam van de sandbox opgeeft waarin de bewerking plaatsvindt:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Raadpleeg de documentatie [sandbox-overzicht](../sandboxes/home.md) voor meer informatie over sandboxen in [!DNL Platform].

Alle verzoeken die een nuttige lading (POST, PUT, PATCH) bevatten vereisen een extra kopbal:

- Inhoudstype: application/json

## Algemene gebruikersstroom

Om te beginnen, registreert een gebruiker ETL in het [!DNL Experience Platform] gebruikersinterface (UI) en leidt datasets voor opname gebruikend een standaardschakelaar of een duw-dienst schakelaar.

In UI, leidt de gebruiker tot de outputdataset door een datasetschema te selecteren. De keuze van het schema hangt af van het type gegevens (record- of tijdreeks) dat in [!DNL Platform] wordt ingevoerd. Door op het lusje van Schema binnen UI te klikken, zal de gebruiker alle beschikbare schema&#39;s, met inbegrip van het gedragstype kunnen bekijken dat het schema steunt.

In ETL zal de gebruiker beginnen hun toewijzingstransformaties te ontwerpen nadat de aangewezen verbinding (gebruikend hun geloofsbrieven) wordt gevormd. Er wordt aangenomen dat [!DNL Experience Platform]-connectors al zijn geïnstalleerd (proces niet gedefinieerd in deze integratiegids).

In de [ETL-workflow](./workflow.md) zijn modellen voor een voorbeeld-ETL-tool en -workflow opgenomen. Hoewel de ETL-gereedschappen verschillende indelingen kunnen hebben, zijn de meeste toepassingen beschikbaar voor vergelijkbare functies.

>[!NOTE]
>
>De ETL-aansluiting moet een tijdstempelfilter opgeven waarmee de datum voor het invoeren van gegevens en verschuiving (d.w.z. het venster waarvoor gegevens moeten worden gelezen) wordt aangegeven. Het ETL-hulpmiddel moet het gebruik van deze twee parameters in deze of een andere relevante interface ondersteunen. In Adobe Experience Platform worden deze parameters toegewezen aan beschikbare datums (indien aanwezig) of vastgelegde datums in het batchobject van de gegevensset.

### Lijst met gegevenssets weergeven

Gebruikend de bron van gegevens voor afbeelding, kan een lijst van alle beschikbare datasets worden gehaald gebruikend [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

U kunt één API-verzoek indienen om alle beschikbare gegevenssets te bekijken (bijvoorbeeld `GET /dataSets`), met beste praktijken die zijn om vraagparameters te omvatten die de grootte van de reactie beperken.

In gevallen waarin volledige gegevenssetinformatie wordt gevraagd, kan de antwoordlading voorbij 3 GB in grootte bereiken, die algemene prestaties kan vertragen. Daarom zal het gebruiken van vraagparameters om slechts de benodigde informatie te filtreren [!DNL Catalog] vragen efficiënter maken.

#### Filteren op List

Wanneer het filtreren van reacties, kunt u veelvoudige filters in één enkele vraag gebruiken door parameters met een ampersand (`&`) te scheiden. Sommige queryparameters accepteren door komma&#39;s gescheiden lijsten met waarden, zoals het filter &quot;Eigenschappen&quot; in de voorbeeldaanvraag hieronder.

[!DNL Catalog] de reacties worden automatisch gemeten volgens gevormde grenzen, nochtans kan de &quot;grens&quot;vraagparameter worden gebruikt om de beperkingen aan te passen en het aantal teruggekeerde voorwerpen te beperken. De vooraf geconfigureerde [!DNL Catalog] responslimieten zijn:

- Als er geen limietparameter is opgegeven, is het maximumaantal objecten per antwoordlading 20.
- De globale grens voor alle andere [!DNL Catalog] vragen is 100 voorwerpen.
- Voor datasetvragen, als observableSchema wordt gevraagd gebruikend de parameter van de eigenschappenvraag, is het maximumaantal teruggekeerde datasets 20.
- Ongeldige limietparameters (met inbegrip van `limit=0`) worden voldaan aan een fout van HTTP 400 die juiste waaiers schetst.
- Als limieten of verschuivingen als queryparameters worden doorgegeven, hebben ze voorrang op de parameters die als kopteksten worden doorgegeven.

De parameters van de vraag worden behandeld meer in detail in [Overzicht van de Dienst van de Catalogus](../catalog/home.md).

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

Raadpleeg het [Overzicht van de catalogusservice](../catalog/home.md) voor gedetailleerde voorbeelden van het maken van aanroepen naar [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml).

**Antwoord**

De reactie omvat drie (`limit=3`) datasets die de &quot;naam&quot;, &quot;beschrijving&quot;, en &quot;schemaRef&quot;zoals die door `properties` vraagparameter wordt vermeld tonen.

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

De eerste &quot;schemaRef.id&quot;waarde in het vorige reactievoorwerp (`https://ns.adobe.com/{TENANT_ID}/schemas/274f17bc5807ff307a046bab1489fb18`) is URI die aan een specifiek schema XDM in [!DNL Schema Registry] richt. Het schema kan worden teruggewonnen door een raadpleging (GET) verzoek aan [!DNL Schema Registry] API te maken.

>[!NOTE]
>
>De eigenschap &quot;schemaRef&quot; vervangt de nu afgekeurde eigenschap &quot;schema&quot;. Als &quot;schemaRef&quot;van de dataset afwezig is of geen waarde bevat, zult u de aanwezigheid van een &quot;schema&quot;bezit moeten controleren. Dit zou kunnen worden gedaan door &quot;schemaRef&quot;met &quot;schema&quot;in de `properties` vraagparameter in de vorige vraag te vervangen. Meer details over het &quot;schema&quot;bezit zijn beschikbaar in [Dataset &quot;schema&quot;bezit](#dataset-schema-property-deprecated---eol-2019-05-30) sectie die volgt.

**API-indeling**

```http
GET /schemaregistry/tenant/schemas/{url encoded schemaRef.id}
```

**Verzoek**

Het verzoek gebruikt URL gecodeerd `id` URI van het schema (de waarde van het &quot;schemaRef.id&quot;attribuut) en vereist een Accept kopbal.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/https%3A%2F%2Fns.adobe.com%2F{TENANT_ID}%2Fschemas%2F274f17bc5807ff307a046bab1489fb18 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-full+json; version=1' \
```

De responsindeling is afhankelijk van het type Accept-header dat in de aanvraag wordt verzonden. Voor opzoekverzoeken moet ook een `version` worden opgenomen in de koptekst Accepteren. In de volgende tabel worden de beschikbare kopteksten voor zoekopdrachten geaccepteerd:

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
>`application/vnd.adobe.xed-id+json` en  `application/vnd.adobe.xed-full+json; version={major version}` zijn de meest gebruikte Accepteer kopteksten. `application/vnd.adobe.xed-id+json` heeft de voorkeur voor het aanbieden van resources in de  [!DNL Schema Registry] code, aangezien alleen de titel, id en versie worden geretourneerd. `application/vnd.adobe.xed-full+json; version={major version}` heeft de voorkeur voor het weergeven van een specifieke bron (aan de hand van de id), aangezien deze alle velden (genest onder &quot;eigenschappen&quot;) retourneert, evenals titels en beschrijvingen.

**Antwoord**

Het JSON-schema dat wordt geretourneerd, beschrijft de structuur en veldniveaugegevens (&quot;type&quot;, &quot;format&quot;, &quot;minimum&quot;, &quot;maximum&quot;, enz.) van de gegevens, met serienummering gecodeerd als JSON. Als het gebruiken van een rangschikkingsformaat buiten JSON voor opname (zoals Parquet of Scala), [de Gids van de Registratie van het Schema](../xdm/tutorials/create-schema-api.md) bevat een lijst die het gewenste type JSON (&quot;meta:xdmType&quot;) en zijn overeenkomstige vertegenwoordiging in andere formaten toont.

Samen met deze lijst, bevat de [!DNL Schema Registry] Gids van de Ontwikkelaar diepgaande voorbeelden van alle mogelijke vraag die kan worden gemaakt gebruikend [!DNL Schema Registry] API.

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

Als het &quot;schema&quot;bezit van een dataset wordt bevolkt, wijst dit erop dat het schema een afgekeurd `/xdms` schema is en, waar gesteund, zou de schakelaar ETL de waarde in het &quot;schema&quot;bezit met het `/xdms` eindpunt (een afgekeurd eindpunt in [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml)) moeten gebruiken om het erfenisschema terug te winnen.

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

>[!NOTE]
>
>Een facultatieve vraagparameter, `expansion=xdm`, vertelt API om volledig uit te breiden en in-lijn om het even welke referenced schema&#39;s. Dit kunt u doen wanneer u een lijst met alle mogelijke velden aan de gebruiker presenteert.

**Antwoord**

Gelijkaardig aan de stappen voor [het bekijken van datasetschema](#view-dataset-schema), bevat de reactie een schema JSON dat de structuur en gebied-vlakke informatie van de gegevens beschrijft, die als JSON in series worden vervaardigd.

>[!NOTE]
>
>Wanneer het &quot;schema&quot;gebied leeg is of volledig ontbreekt, zou de schakelaar het &quot;schemaRef&quot;gebied moeten lezen en [de Registratie API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van het Schema zoals aangetoond in de vorige stappen gebruiken om [een datasetschema](#view-dataset-schema) te bekijken.

### De eigenschap &quot;observableSchema&quot;

De eigenschap &quot;observableSchema&quot; van een dataset heeft een JSON-structuur die overeenkomt met die van het XDM-schema JSON. Het &quot;observableSchema&quot; bevat de velden die aanwezig waren in de binnenkomende invoerbestanden. Wanneer het schrijven van gegevens aan [!DNL Experience Platform], wordt een gebruiker vereist niet om elk gebied van het doelschema te gebruiken. In plaats daarvan moeten ze alleen die velden leveren die worden gebruikt.

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

De ETL-toepassing kan een mogelijkheid bieden om gegevens voor te vertonen ([&quot;Figuur 8&quot; in de ETL-workflow](./workflow.md)). De API voor gegevenstoegang biedt verschillende opties voor het weergeven van voorvertoningen van gegevens.

Aanvullende informatie, waaronder stapsgewijze instructies voor het voorvertonen van gegevens met behulp van de API voor gegevenstoegang, vindt u in de [zelfstudie voor gegevenstoegang](../data-access/tutorials/dataset-data.md).

### Krijg datasetdetails gebruikend de &quot;eigenschappen&quot;vraagparameter

Zoals aangetoond in de stappen hierboven aan [bekijk een lijst van datasets](#view-list-of-datasets), kunt u &quot;dossiers&quot;verzoeken gebruikend de &quot;eigenschappen&quot;vraagparameter.

U kunt naar [Overzicht van de Dienst van de Catalogus ](../catalog/home.md) voor gedetailleerde informatie over het vragen van datasets en beschikbare reactiefilters verwijzen.

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

U kunt ook een verzoek van de GET gebruiken om dossierdetails te halen gebruikend het &quot;dossiers&quot;attribuut.

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

De id&#39;s van het gegevenssetbestand die in de vorige reactie zijn geretourneerd, kunnen worden gebruikt in een GET-verzoek om meer bestandsgegevens op te halen via de API [!DNL Data Access].

Het [overzicht van de gegevenstoegang](../data-access/home.md) bevat details over hoe te om [!DNL Data Access] API te gebruiken.

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

De eigenschap &quot;href&quot; kan worden gebruikt om voorvertoningsgegevens op te halen via [[!DNL Data Access API]](../data-access/home.md).

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

Meer informatie over de [!DNL Data Access] API, inclusief gedetailleerde verzoeken en reacties, is beschikbaar in [overzicht van gegevenstoegang](../data-access/home.md).

### &quot;fileDescription&quot; ophalen uit gegevensset

De bestemmingscomponent als output van getransformeerde gegevens, zal de Ingenieur van Gegevens een Dataset van de Output ([&quot;Figuur 12&quot;in het ETL Werkschema](workflow.md)) kiezen. Het XDM-schema is gekoppeld aan de uitvoergegevensset. De te schrijven gegevens worden geïdentificeerd door het kenmerk &quot;fileDescription&quot; van de gegevenssetentiteit van de API&#39;s voor gegevensdetectie. Deze informatie kan worden opgehaald gebruikend een dataset identiteitskaart (`{DATASET_ID}`). De eigenschap &quot;fileDescription&quot; in het JSON-antwoord geeft de gevraagde informatie.

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

De gegevens worden naar [!DNL Experience Platform] geschreven met behulp van [Data Ingestie API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml).  Het schrijven van gegevens is een asynchroon proces. Wanneer gegevens naar Adobe Experience Platform worden geschreven, wordt alleen een batch gemaakt en gemarkeerd als een succes nadat de gegevens volledig zijn geschreven.

Gegevens in [!DNL Experience Platform] moeten worden geschreven in de vorm van Parquet-bestanden.

## Uitvoeringsfase

Wanneer de uitvoering start, leest de connector (zoals gedefinieerd in de broncomponent) de gegevens van [!DNL Experience Platform] met de [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml). Het transformatieproces leest de gegevens voor een bepaald tijdbereik. Intern, zal het partijen brondatasets vragen. Tijdens het vragen, zal het een geparameterized (het rollen voor tijdreeksgegevens, of stijgende gegevens) begindatum en lijstdatasetdossiers voor die partijen gebruiken, en begint verzoeken om gegevens voor die datasetdossiers te doen.

### Voorbeeldtransformaties

Het [voorbeeld ETL-transformaties](./transformations.md)-document bevat een aantal voorbeeldtransformaties, waaronder identiteitsbeheer en gegevenstypetoewijzingen. Gebruik deze transformaties ter referentie.

### Gegevens lezen van [!DNL Experience Platform]

Met de [[!DNL Catalog API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) kunt u alle batches tussen een opgegeven begintijd en eindtijd ophalen en sorteren op de volgorde waarin ze zijn gemaakt.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/catalog/batches?dataSet=DATASETID&createdAfter=START_TIMESTAMP&createdBefore=END_TIMESTAMP&sort=desc:created" \
  -H "Accept: application/json" \
  -H "Authorization:Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}"
```

Details over het filteren van batches vindt u in de [zelfstudie over gegevenstoegang](../data-access/tutorials/dataset-data.md).

### Bestanden ophalen uit een batch

Zodra u identiteitskaart voor de partij hebt u (`{BATCH_ID}`) zoekt, is het mogelijk om een lijst van dossiers terug te winnen die tot een specifieke partij via [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) behoren.  Details hiervoor zijn beschikbaar in de [[!DNL Data Access] zelfstudie](../data-access/tutorials/dataset-data.md).

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/batches/{BATCH_ID}/files" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-api-key : {API_KEY}"
```

### Bestanden openen met bestands-id

Met de unieke id van een bestand (`{FILE_ID`) kunt u [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) gebruiken om toegang te krijgen tot de specifieke details van het bestand, zoals de naam, grootte in bytes en een koppeling om het bestand te downloaden.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{FILE_ID}" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key : {API_KEY}"
```

De reactie kan naar één bestand of naar een map verwijzen. Details over elk kunnen in [[!DNL Data Access] tutorial](../data-access/tutorials/dataset-data.md) worden gevonden.

### Bestandsinhoud openen

De [[!DNL Data Access API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/data-access-api.yaml) kan worden gebruikt om tot de inhoud van een specifiek dossier toegang te hebben. Om de inhoud te halen, wordt een verzoek van de GET gemaakt gebruikend de waarde die voor `_links.self.href` wanneer het toegang tot van een dossier gebruikend dossier - identiteitskaart is teruggekeerd.

**Verzoek**

```shell
curl -X GET "https://platform.adobe.io/data/foundation/export/files/{DATASET_FILE_ID}?path=filename1.csv" \
  -H "Authorization: Bearer {ACCESS_TOKEN}" \
  -H "x-gw-ims-org-id: {IMS_ORG}" \
  -H "x-sandbox-name: {SANDBOX_NAME}" \
  -H "x-api-key: {API_KEY}"
```

Het antwoord op deze aanvraag bevat de inhoud van het bestand. Voor meer informatie, met inbegrip van details over reactiepaginering, zie [hoe te Gegevens van de Vraag via gegevenstoegang API](../data-access/tutorials/dataset-data.md) leerprogramma.

### Records voor schemaconformiteit valideren

Wanneer gegevens worden geschreven, kunnen gebruikers ervoor kiezen om gegevens te valideren volgens de validatieregels die in het XDM-schema zijn gedefinieerd. Meer informatie over schemabevestiging kan in [ETL de Code van de Verwijzing van de Integratie van het Ecosysteem op  [!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md#validation) worden gevonden.

Als u de verwijzingsimplementatie gebruikt die op [[!DNL GitHub]](https://github.com/adobe/experience-platform-etl-reference/blob/fd08dd9f74ae45b849d5482f645f859f330c1951/README.md) wordt gevonden, kunt u schemabevestiging in deze implementatie aanzetten gebruikend het systeembezit `-DenableSchemaValidation=true`.

Validatie kan worden uitgevoerd voor logische types XDM, gebruikend attributen zoals `minLength` en `maxlength` voor koorden, `minimum` en `maximum` voor gehelen, en meer. De [Handleiding voor ontwikkelaars van de API voor schemaregistratie](../xdm/api/getting-started.md) bevat een tabel met XDM-typen en de eigenschappen die voor validatie kunnen worden gebruikt.

>[!NOTE]
>
>De minimum en maximumwaarden die voor verschillende `integer` types worden verstrekt zijn de MIN en MAX waarden die het type kan steunen, maar deze waarden kunnen verder tot minimum en maximum van uw kiezen worden beperkt.

### Een batch maken

Nadat de gegevens zijn verwerkt, schrijft het hulpprogramma ETL de gegevens terug naar [!DNL Experience Platform] met de [Batch-inname-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml). Voordat gegevens kunnen worden toegevoegd aan een gegevensset, moet deze worden gekoppeld aan een batch die later wordt geüpload naar een specifieke gegevensset.

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

Details voor het maken van een batch, inclusief voorbeeldaanvragen en reacties, vindt u in het [Overzicht van de batchverwerking](../ingestion/batch-ingestion/overview.md).

### Schrijven naar gegevensset

Nadat een nieuwe partij met succes tot stand is gebracht, kunnen de dossiers dan aan een specifieke dataset worden geupload. U kunt meerdere bestanden in een batch plaatsen totdat deze worden gepromoot. Bestanden kunnen worden geüpload met de API voor het uploaden van kleine bestanden. als uw bestanden echter te groot zijn en de gatewaylimiet wordt overschreden, kunt u de API voor het uploaden van grote bestanden gebruiken. De details voor het gebruiken van zowel Groot als Klein Dossier uploaden kunnen in [Overzicht van de Ingestie van de Partij ](../ingestion/batch-ingestion/overview.md) worden gevonden.

**Verzoek**

Gegevens in [!DNL Experience Platform] moeten worden geschreven in de vorm van Parquet-bestanden.

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

Nadat alle bestanden naar de batch zijn geüpload, kan de batch worden gemarkeerd als voltooid. Door dit te doen, worden de [!DNL Catalog] &quot;DataSetFile&quot;ingangen gecreeerd voor de voltooide dossiers en met te verbinden genereert partij. De [!DNL Catalog] partij wordt dan duidelijk als succesvol, die stroomafwaartse stromen om de beschikbare gegevens in te voeren teweegbrengt.

De gegevens worden eerst op de halteplaats op Adobe Experience Platform geland en vervolgens na catalogisering en validatie naar de uiteindelijke locatie verplaatst. De partijen zullen als succesvol worden gemerkt zodra alle gegevens naar een permanente plaats worden verplaatst.

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

Bij de volgende transformatie-uitvoering, waarschijnlijk door planning of aanroeping van de gebeurtenis, zal ETL beginnen om de gegevens van eerder-bewaarde timestamp en alle gegevens te vragen die voorwaarts gaan.

### Laatste batchstatus ophalen

Voordat u nieuwe taken uitvoert met het gereedschap ETL, moet u controleren of de laatste batch is voltooid. [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) verstrekt een batch-specifieke optie die de details van de relevante partijen verstrekt.

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

Een individuele partijstatus kan door [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) worden teruggewonnen door een verzoek van de GET uit te geven gebruikend `{BATCH_ID}`. De gebruikte `{BATCH_ID}` zou het zelfde zijn als identiteitskaart terugkwam toen de partij werd gecreeerd.

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

Hiertoe gebruiken de gegevensbeheerders van de client de interface [!DNL Platform] om de batches met beschadigde gegevens te verwijderen. Vervolgens zal de ETL waarschijnlijk opnieuw moeten worden uitgevoerd, zodat de ETL met correcte gegevens kan worden gerepareerd. Als de bron zelf corrupte gegevens had, zal de gegevensingenieur/beheerder de bronpartijen moeten verbeteren en de gegevens (of in Adobe Experience Platform of via schakelaars ETL) opnieuw opnemen.

Gebaseerd op het type van gegevens die worden geproduceerd, zal het de keus van de gegevensingenieur zijn om één enkele partij of alle partijen uit bepaalde datasets te verwijderen. Gegevens worden verwijderd/gearchiveerd volgens de richtlijnen [!DNL Experience Platform].

Het is waarschijnlijk een scenario dat de functionaliteit ETL om gegevens te zuiveren belangrijk zal zijn.

Zodra het leegmaken is voltooid, moeten de clientbeheerders Adobe Experience Platform opnieuw configureren om de verwerking voor kernservices opnieuw te starten vanaf het moment dat de batches worden verwijderd.

## Gelijktijdige batchverwerking

Naar eigen goeddunken van de klant kunnen gegevensbeheerders/engineers besluiten gegevens op sequentiële wijze of op gelijktijdige wijze te extraheren, te transformeren en te laden, afhankelijk van de kenmerken van een bepaalde gegevensset. Dit wordt ook gebaseerd op het geval waarin de client de getransformeerde gegevens gebruikt.

Bijvoorbeeld, als de cliënt aan een updatable persistentieopslag voortduurt en de opeenvolging of de orde van gebeurtenissen belangrijk is, kan de cliënt banen met opeenvolgende transformaties strikt moeten verwerken ETL.

In andere gevallen kunnen gegevens in de vorm van een out-of-order worden verwerkt door downstreamtoepassingen/processen die intern worden gesorteerd met een opgegeven tijdstempel. In die gevallen kunnen parallelle ETL-transformaties levensvatbaar zijn om de verwerkingstijd te verbeteren.

Voor bronbatches is dit weer afhankelijk van de voorkeur van de klant en de beperking van de consument. Als de brongegevens parallel kunnen worden opgepikt zonder dat rekening wordt gehouden met de urgentie/volgorde van een rij, kan het transformatieproces procesbatches maken met een hogere mate van parallellisme (optimalisatie gebaseerd op verwerking buiten bestelling). Maar als de transformatie tijdstempels moet respecteren of belangrijkheidsvolgorde moet wijzigen, moeten de API voor gegevenstoegang of ETL-toolplanner/aanroeping ervoor zorgen dat batches waar mogelijk niet buiten de bestelling worden verwerkt.

## Uitstel

Uitstel is een proces waarbij de inputgegevens nog niet volledig genoeg zijn om naar downstreamprocessen te worden verzonden, maar in de toekomst bruikbaar kunnen zijn. Clients zullen hun individuele tolerantie voor gegevensramen voor toekomstige matching tegenover de kosten van verwerking bepalen om hun beslissing om gegevens te reserveren en opnieuw te verwerken in de volgende transformatieuitvoering te informeren, in de hoop dat het op een bepaald tijdstip in het bewaarvenster kan worden verrijkt en in overeenstemming gebracht/vastgemaakt. Deze cyclus loopt tot de rij voldoende is verwerkt of te groot wordt geacht om te blijven investeren in. Elke herhaling genereert uitgestelde gegevens die een superset zijn van alle uitgestelde gegevens in vorige herhalingen.

Adobe Experience Platform identificeert momenteel geen uitgestelde gegevens, zodat moeten de cliëntimplementaties zich op de ETL en de handconfiguraties van Dataset baseren om een andere dataset in [!DNL Platform] te creëren die de brondataset weerspiegelt die kan worden gebruikt om uitgestelde gegevens te houden. In dit geval zijn uitgestelde gegevens vergelijkbaar met momentopnamegegevens. Bij elke uitvoering van de ETL-transformatie worden de brongegevens verenigd met uitgestelde gegevens en verzonden voor verwerking.

## Changelog

| Datum | Actie | Beschrijving |
| ---- | ------ | ----------- |
| 2019-01-19 | Eigenschap &quot;fields&quot; uit gegevenssets verwijderd | Datasets bevatten eerder een eigenschap &quot;fields&quot; die een kopie van het schema bevatte. Deze mogelijkheid mag niet meer worden gebruikt. Als de eigenschap &quot;fields&quot; wordt gevonden, moet deze worden genegeerd en wordt in plaats daarvan &quot;ObservedSchema&quot; of &quot;schemaRef&quot; gebruikt. |
| 2019-03-15 | &quot;schemaRef&quot;-eigenschap toegevoegd aan gegevenssets | Het &quot;schemaRef&quot;bezit van een dataset bevat URI die naar het XDM schema verwijst waarop de dataset gebaseerd is en vertegenwoordigt alle potentiële gebieden die door de dataset zouden kunnen worden gebruikt. |
| 2019-03-15 | Alle eindgebruikersidentificatoren wijzen de eigenschap &quot;identityMap&quot; toe | De &quot;identityMap&quot;is een inkapseling van alle unieke herkenningstekens van een onderwerp, zoals identiteitskaart van CRM, ECID, of identiteitskaart van het loyaliteitsprogramma Deze kaart wordt gebruikt door [[!DNL Identity Service]](../identity-service/home.md) om alle bekende en anonieme identiteiten van een onderwerp op te lossen, die één enkele identiteitsgrafiek voor elke eindgebruiker vormen. |
| 2019-05-30 | EOL en verwijder &quot;schema&quot;bezit uit datasets | De dataset &quot;schema&quot;bezit verstrekte een verwijzingsverbinding aan het schema gebruikend het afgekeurde `/xdms` eindpunt in [!DNL Catalog] API. Dit is vervangen door een &quot;schemaRef&quot;die &quot;id&quot;, &quot;versie&quot;, en &quot;contentType&quot;van het schema zoals die in nieuwe [!DNL Schema Registry] API van verwijzingen voorzien. |