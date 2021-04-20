---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;api-handleiding;platform-api-handleiding;inleiding tot platform;ontwikkelaarshandleiding
solution: Experience Platform
title: Aan de slag met Adobe Experience Platform API's
topic: api guide
description: Adobe Experience Platform biedt API-services die nauw met elkaar zijn verbonden. Deze gids bevat informatie over de beschikbare diensten, vereiste kopballen voor verrichtingen CRUD, foutenmeldingen, de inzamelingen van Postman, en de vraag van steekproefAPI.
translation-type: tm+mt
source-git-commit: 85d2ae5ccf1b27baaafe839f1d3f00d588abe4fc
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 0%

---


# Aan de slag met Adobe Experience Platform API&#39;s

Adobe Experience Platform is ontwikkeld volgens een &quot;API first&quot;-filosofie. Met Platform-API&#39;s kunt u via programmacode elementaire CRUD-bewerkingen (Maken, Lezen, Bijwerken, Verwijderen) uitvoeren op gegevens, zoals het configureren van berekende kenmerken, het openen van gegevens/entiteiten, het exporteren van gegevens, het verwijderen van overbodige gegevens of batches en meer.

De APIs voor elke dienst van het Experience Platform delen allen de zelfde reeks authentificatiekopballen en gebruiken gelijkaardige syntaxis voor hun verrichtingen CRUD. In de volgende handleiding worden de stappen beschreven die nodig zijn om aan de slag te gaan met Platform-API&#39;s.

## Verificatie en kopteksten

Om met succes vraag aan Platform eindpunten te maken, wordt u vereist om [authentificatieleerprogramma](https://www.adobe.com/go/platform-api-authentication-en) te voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

### Sandbox-header

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Zie de [sandbox overzichtsdocumentatie](../sandboxes/home.md) voor meer informatie over sandboxen in Platform.

### Koptekst van inhoudstype

Alle verzoeken met een nuttige lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. Accepteerde waarden zijn specifiek voor elk API-eindpunt. Als een specifieke `Content-Type` waarde voor een eindpunt nodig is, zal zijn waarde in de voorbeeldAPI verzoeken worden getoond die door [API gidsen voor de individuele diensten van het Platform worden verstrekt](#api-guides).

## Grondbeginselen van Experience Platform API

Adobe Experience Platform API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen, zodat de bronnen van Platforms effectief kunnen worden beheerd.

Voor meer informatie over de onderliggende API technologieën gebruikt het Platform, met inbegrip van voorbeeld JSON schemavoorwerpen, bezoek [Experience Platform API fundamentals](api-fundamentals.md) gids.

## Postmanverzamelingen voor Experience Platform-API&#39;s

Postman is een samenwerkingsplatform voor API-ontwikkeling waarmee u omgevingen kunt instellen met vooraf ingestelde variabelen, API-verzamelingen kunt delen, CRUD-aanvragen kunt stroomlijnen en nog veel meer. De meeste Platform API diensten hebben de inzamelingen van Postman die kunnen worden gebruikt om bij het maken van API vraag te helpen.

Meer informatie over Postman met inbegrip van hoe te opstelling een milieu, een lijst van beschikbare inzamelingen, en hoe te om inzamelingen in te voeren, de [documentatie van Postman van het Platform](postman.md) te bezoeken.

## Voorbeeld-API-aanroepen lezen {#sample-api}

De aanvraagindelingen zijn afhankelijk van de Platform-API die wordt gebruikt. De beste manier om te leren hoe te om uw API vraag te structureren is door samen met de voorbeelden te volgen die in de documentatie voor de bepaalde dienst van het Platform worden verstrekt u gebruikt.

De documentatie voor [!DNL Experience Platform] toont voorbeeld API vraag op twee verschillende manieren. Eerst, wordt de vraag voorgesteld in zijn **API formaat**, een malplaatjevertegenwoordiging die slechts de verrichting (GET, POST, PUT, PATCH, DELETE) en het eindpunt toont die wordt gebruikt (bijvoorbeeld, `/global/classes`). Sommige malplaatjes tonen ook de plaats van variabelen helpen illustreren hoe een vraag, zoals `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}` zou moeten worden geformuleerd.

De vraag wordt dan getoond als cURL bevelen in **Verzoek**, die de noodzakelijke kopballen en volledige &quot;basisweg&quot;nodig omvat om met API met succes in wisselwerking te staan. Het basispad moet vooraf aan alle eindpunten worden toegevoegd. Het eerder vermelde `/global/classes`-eindpunt wordt bijvoorbeeld `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. U zult het formaat van API/verzoekpatroon door de documentatie zien, en zal naar verwachting de volledige weg gebruiken die in het voorbeeldverzoek wordt getoond wanneer het maken van uw eigen vraag aan Platform APIs.

### Voorbeeld-API-aanvraag

Hier volgt een voorbeeld-API-aanvraag die de indeling weergeeft die u in de documentatie zult tegenkomen.

**API-indeling**

De API-indeling toont de bewerking (GET) en het eindpunt dat wordt gebruikt. Variabelen worden aangegeven met accolades (in dit geval `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Verzoek**

In deze voorbeeldaanvraag krijgen de variabelen van de API-indeling de werkelijke waarden in het aanvraagpad. Bovendien, worden alle vereiste kopballen getoond als of waarden van de steekproefkopbal of variabelen waar de gevoelige informatie (zoals veiligheidstokens en toegangsIDs) zou moeten worden omvat.

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwoord**

De reactie illustreert wat u zou verwachten te ontvangen na een succesvolle vraag aan API, die op het verzoek wordt gebaseerd dat werd verzonden. Soms wordt de reactie afgebroken voor de ruimte, wat betekent dat u meer informatie of aanvullende informatie ziet voor de hoeveelheid die in het voorbeeld wordt weergegeven.

```json
{
    "results": [
        {
            "title": "XDM ExperienceEvent",
            "$id": "https://ns.adobe.com/xdm/context/experienceevent",
            "meta:altId": "_xdm.context.experienceevent",
            "version": "1"
        },
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile",
            "meta:altId": "_xdm.context.profile",
            "version": "1"
        }
    ],
    "_links": {}
}
```

## Foutberichten

De [gids voor het oplossen van problemenproblemen van Platforms](troubleshooting.md#errors-and-troubleshooting) verstrekt een lijst van fouten die u wanneer het gebruiken van om het even welke dienst van het Experience Platform kunt ontmoeten.

Raadpleeg de [servicemap](troubleshooting.md#service-troubleshooting-directory) voor informatie over het oplossen van problemen met hulplijnen voor individuele Platforms.

Voor meer informatie over specifieke eindpunten in Platform APIs, met inbegrip van vereiste kopballen en verzoekorganismen, te zien gelieve [Platform API gidsen](#api-guides).

## API-hulplijnen voor Platform {#api-guides}

| API-handleiding | Beschrijving |
| --- | --- |
| [[!DNL Access Control] API-handleiding](.././access-control/api/getting-started.md) | Het [!DNL Access Control] API eindpunt kan huidig beleid terugwinnen dat voor een gebruiker op bepaalde middelen binnen een gespecificeerde zandbak van kracht is. Alle andere toegangsbeheermogelijkheden worden verstrekt door [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Handleiding voor inname van batch-API](.././ingestion/batch-ingestion/api-overview.md) | Met de Adobe Experience Platform [!DNL Data Ingestion]-API kunt u gegevens als batchbestanden in het Platform invoeren. Gegevens die worden opgenomen kunnen de profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket), of gegevens zijn die met een bekend schema in de Registratie van het Schema (XDM) in overeenstemming zijn. |
| [[!DNL Catalog Service] API-handleiding](.././catalog/api/getting-started.md) | Met de API [!DNL Catalog Service] kunnen ontwikkelaars metagegevens van gegevenssets beheren in Adobe Experience Platform. Dit omvat gegevenslocaties, verwerkingsfasen, fouten die tijdens de verwerking zijn opgetreden en gegevensrapporten. |
| [[!DNL Data Access] API-handleiding](.././data-access/api.md) | Met de API [!DNL Data Access] kunnen ontwikkelaars informatie ophalen over ingesloten gegevenssets in Experience Platform. Hiertoe behoren het openen en downloaden van gegevenssetbestanden, het ophalen van koptekstgegevens, het opgeven van mislukte en opvolgende batches en het downloaden van voorvertoningen van CSV-/Parquet-bestanden. |
| [[!DNL Dataset Service] API-handleiding](.././data-governance/labels/dataset-api.md) | Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert. |
| [[!DNL Flow Service] API-handleiding](.././sources/tutorials/api/create-dataset-base-connection.md) <br>  (Bronnen en doelen) | De [!DNL Flow Service] API wordt gebruikt om uw gegevens van diverse bronnen te verzamelen en te centraliseren en wordt gebruikt om gegevens tot stand te brengen en te activeren aan diverse bestemmingen binnen Adobe Experience Platform. De service biedt een RESTful-API waarvan alle ondersteunde bronnen kunnen worden aangesloten. |
| [[!DNL Identity Service] API-handleiding](.././identity-service/api/getting-started.md) | Met de [!DNL Identity Service]-API kunnen ontwikkelaars de identificatie van uw klanten via verschillende apparaten, kanalen en vrijwel realtime beheren met behulp van identiteitsgrafieken in Adobe Experience Platform. |
| [[!DNL Observability Insights] API-handleiding](.././observability/api/overview.md) | [!DNL Observability Insights] is een RESTful API die ontwikkelaars toestaat om zeer belangrijke waarneembaarheidsmetriek in Adobe Experience Platform bloot te stellen. Deze cijfers verstrekken inzichten in de gebruiksstatistieken van het Platform, gezondheid-controles voor de diensten van het Platform, historische tendensen, en prestatiesindicatoren voor diverse functies van het Platform. |
| [[!DNL Policy Service] API-handleiding](.././data-governance/api/overview.md) <br>  (gegevensbeheer) | Met de API [!DNL Policy Service] kunt u labels en beleidsregels voor gegevensgebruik maken en beheren om te bepalen welke marketingacties kunnen worden uitgevoerd tegen gegevens die bepaalde labels voor gegevensgebruik bevatten. Om etiketten op datasets en gebieden toe te passen, verwijs naar [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) gids |
| [[!DNL Privacy Service] API-handleiding](.././privacy-service/api/getting-started.md) | Met de API [!DNL Privacy Service] kunnen ontwikkelaars hun verzoeken om toegang tot of verwijdering van hun persoonlijke gegevens in Experience Cloud-toepassingen maken en beheren, in overeenstemming met de wettelijke privacyregels. |
| [[!DNL Query Service] API-handleiding](.././query-service/api/getting-started.md) | Met de API [!DNL Query Service] kunnen ontwikkelaars hun Adobe Experience Platform-gegevens opvragen met behulp van standaard SQL. |
| [[!DNL Real-time Customer Profile] API-handleiding](.././profile/api/overview.md) | Met de realtime-API voor klantprofiel kunnen ontwikkelaars profielgegevens verkennen en ermee werken, zoals het weergeven van profielen, het maken en bijwerken van samenvoegbeleid, het exporteren of samplen van profielgegevens en het verwijderen van profielgegevens die niet langer vereist zijn of die bij fout zijn toegevoegd. |
| [Handleiding voor sandbox-API](.././sandboxes/api/getting-started.md) | Met de sandbox-API kunnen ontwikkelaars via programmacode geïsoleerde virtuele sandboxomgevingen in Adobe Experience Platform beheren. |
| [[!DNL Schema Registry] API-handleiding](.././xdm/api/overview.md) <br>  (XDM) | Met de API [!DNL Schema Registry] kunnen ontwikkelaars programmatisch alle schema&#39;s en gerelateerde XDM-bronnen (Experience Data Model) in Adobe Experience Platform beheren. |
| [[!DNL Segmentation Service] API-handleiding](.././segmentation/api/overview.md) | Met de API [!DNL Segmentation Service] kunnen ontwikkelaars segmentatiebewerkingen in Adobe Experience Platform programmatisch beheren. Dit omvat het bouwen van segmenten en het produceren van publiek van uw gegevens van het Profiel van de Klant in real time. |
| [[!DNL Sensei Machine Learning] API-handleiding](.././data-science-workspace/api/getting-started.md) <br>  (Data Science Workspace) | De [!DNL Sensei Machine Learning] API verstrekt een mechanisme voor gegevenswetenschappers om machine het leren (ML) diensten van algoritme op het instappen, experimenteren, en aan de dienstplaatsing te organiseren en te beheren. |

Raadpleeg de [API-naslagdocumentatie](http://www.adobe.com/go/platform-api-reference-en) op Adobe I/O voor meer informatie over specifieke eindpunten en bewerkingen die beschikbaar zijn voor elke service.

## Volgende stappen

In dit document zijn de vereiste kopteksten, beschikbare hulplijnen en een voorbeeld-API-aanroep geïntroduceerd. Nu u de vereiste kopbalwaarden hebt nodig om API vraag op Adobe Experience Platform te maken, selecteer een API eindpunt u van [Platform API gidsen lijst ](#api-guides) wenst te onderzoeken.

Raadpleeg de [handleiding voor het oplossen van Platforms](troubleshooting.md) voor antwoorden op veelgestelde vragen.

Als u een Postman-omgeving wilt instellen en de beschikbare Postman-collecties wilt verkennen, raadpleegt u de [Handleiding Postman Platform](postman.md).

