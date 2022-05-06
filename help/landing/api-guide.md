---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;api-handleiding;platform-api-handleiding;inleiding tot platform;ontwikkelaarshandleiding
solution: Experience Platform
title: Aan de slag met Adobe Experience Platform API's
topic-legacy: api guide
description: Adobe Experience Platform biedt API-services die nauw met elkaar zijn verbonden. Deze handleiding bevat informatie over de beschikbare services, vereiste headers voor CRUD-bewerkingen, foutberichten, Postman-verzamelingen en voorbeeld-API-aanroepen.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '1379'
ht-degree: 0%

---

# Aan de slag met Adobe Experience Platform API&#39;s

Adobe Experience Platform is ontwikkeld volgens een &quot;API first&quot;-filosofie. Met Platform-API&#39;s kunt u via programmacode elementaire CRUD-bewerkingen (Maken, Lezen, Bijwerken, Verwijderen) uitvoeren op gegevens, zoals het configureren van berekende kenmerken, het openen van gegevens/entiteiten, het exporteren van gegevens, het verwijderen van overbodige gegevens of batches en meer.

De APIs voor elke dienst van het Experience Platform delen allen de zelfde reeks authentificatiekopballen en gebruiken gelijkaardige syntaxis voor hun verrichtingen CRUD. In de volgende handleiding worden de stappen beschreven die nodig zijn om aan de slag te gaan met Platform-API&#39;s.

## Verificatie en kopteksten

Om met succes vraag aan Platform eindpunten te maken, moet u voltooien [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en). Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Sandbox-header

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Aanvragen voor Platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over sandboxen in Platform raadpleegt u de [overzichtsdocumentatie van sandbox](../sandboxes/home.md).

### Koptekst van inhoudstype

Alle verzoeken met een nuttige lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een omvatten `Content-Type` header. Accepteerde waarden zijn specifiek voor elk API-eindpunt. Als een specifieke `Content-Type` waarde is nodig voor een eindpunt, zal zijn waarde in de voorbeeld API verzoeken worden getoond die door worden verstrekt [API-handleidingen voor afzonderlijke Platforms](#api-guides).

## Grondbeginselen van Experience Platform API

Adobe Experience Platform API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen, zodat de bronnen van Platforms effectief kunnen worden beheerd.

Ga voor meer informatie over de onderliggende API-technologieën die door het Platform worden gebruikt, zoals bijvoorbeeld JSON-schemaobjecten, naar de [Grondbeginselen van Experience Platform API](api-fundamentals.md) hulplijn.

## Postman-verzamelingen voor Experience Platform-API&#39;s

Postman is een samenwerkingsplatform voor API-ontwikkeling waarmee u omgevingen kunt instellen met vooraf ingestelde variabelen, API-verzamelingen kunt delen, CRUD-aanvragen kunt stroomlijnen en nog veel meer. De meeste Platform API diensten hebben de inzamelingen van Postman die kunnen worden gebruikt om bij het maken van API vraag te helpen.

Ga voor meer informatie over Postman, zoals hoe u een omgeving kunt instellen, een lijst met beschikbare verzamelingen en hoe u verzamelingen kunt importeren naar de [Platform Postman-documentatie](postman.md).

## API-voorbeeldaanroepen lezen {#sample-api}

De aanvraagindelingen zijn afhankelijk van de Platform-API die wordt gebruikt. De beste manier om te leren hoe te om uw API vraag te structureren is door samen met de voorbeelden te volgen die in de documentatie voor de bepaalde dienst van het Platform worden verstrekt u gebruikt.

De documentatie voor [!DNL Experience Platform] toont voorbeeld API vraag op twee verschillende manieren. Eerst, wordt de vraag voorgesteld in zijn **API-indeling**, een malplaatjevertegenwoordiging die slechts de verrichting (GET, POST, PUT, PATCH, DELETE) en het eindpunt toont die (bijvoorbeeld `/global/classes`). Sommige malplaatjes tonen ook de plaats van variabelen helpen illustreren hoe een vraag zou moeten worden geformuleerd, zoals `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

De vraag wordt dan getoond als cURL bevelen in a **Verzoek**, die de vereiste headers en het volledige &#39;basispad&#39; bevat die nodig zijn om te kunnen communiceren met de API. Het basispad moet vooraf aan alle eindpunten worden toegevoegd. Bijvoorbeeld: `/global/classes` eindpunt wordt `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. U zult het formaat van API/verzoekpatroon door de documentatie zien, en zal naar verwachting de volledige weg gebruiken die in het voorbeeldverzoek wordt getoond wanneer het maken van uw eigen vraag aan Platform APIs.

### Voorbeeld-API-aanvraag

Hier volgt een voorbeeld-API-aanvraag die de indeling weergeeft die u in de documentatie zult tegenkomen.

**API-indeling**

De API-indeling toont de bewerking (GET) en het eindpunt dat wordt gebruikt. Variabelen worden aangegeven met accolades (in dit geval: `{CONTAINER_ID}`).

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
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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

De [Handleiding voor het oplossen van problemen met Platforms](troubleshooting.md#errors-and-troubleshooting) verstrekt een lijst van fouten die u wanneer het gebruiken van om het even welke dienst van het Experience Platform kunt ontmoeten.

Voor het oplossen van problemengidsen op de individuele diensten van het Platform, zie [servicemap voor probleemoplossing](troubleshooting.md#service-troubleshooting-directory).

Voor meer informatie over specifieke eindpunten in Platform APIs, met inbegrip van vereiste kopballen en aanvraaginstanties, gelieve te zien [API-hulplijnen voor Platform](#api-guides).

## API-hulplijnen voor Platform {#api-guides}

| API-handleiding | Beschrijving |
| --- | --- |
| [[!DNL Access Control] API-handleiding](.././access-control/api/getting-started.md) | De [!DNL Access Control] Het API-eindpunt kan het huidige beleid ophalen dat van kracht is voor een gebruiker op bepaalde bronnen binnen een opgegeven sandbox. Alle andere toegangsbeheermogelijkheden worden verstrekt door [Adobe Admin Console](https://adminconsole.adobe.com/). |
| [Handleiding voor inname van batch-API](.././ingestion/batch-ingestion/api-overview.md) | De Adobe Experience Platform [!DNL Data Ingestion] Met API kunt u gegevens als batchbestanden in het Platform opnemen. Gegevens die worden opgenomen kunnen de profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket), of gegevens zijn die met een bekend schema in de Registratie van het Schema (XDM) in overeenstemming zijn. |
| [[!DNL Catalog Service] API-handleiding](.././catalog/api/getting-started.md) | De [!DNL Catalog Service] Met API kunnen ontwikkelaars metagegevens voor gegevenssets beheren in Adobe Experience Platform. Dit omvat gegevenslocaties, verwerkingsfasen, fouten die tijdens de verwerking zijn opgetreden en gegevensrapporten. |
| [[!DNL Data Access] API-handleiding](.././data-access/api.md) | De [!DNL Data Access] API staat ontwikkelaars toe om informatie over ingebedde datasets binnen Experience Platform terug te winnen. Hiertoe behoren het openen en downloaden van gegevenssetbestanden, het ophalen van koptekstgegevens, het opgeven van mislukte en opvolgende batches en het downloaden van voorvertoningen van CSV-/Parquet-bestanden. |
| [[!DNL Dataset Service] API-handleiding](.././data-governance/labels/dataset-api.md) | Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API voor catalogusservice die metagegevens van gegevenssets beheert. |
| [[!DNL Identity Service] API-handleiding](.././identity-service/api/getting-started.md) | De [!DNL Identity Service] Met API kunnen ontwikkelaars de identificatie van uw klanten op verschillende apparaten, meerdere kanalen en vrijwel realtime beheren met behulp van identiteitsgrafieken in Adobe Experience Platform. |
| [[!DNL Observability Insights] API-handleiding](.././observability/api/overview.md) | [!DNL Observability Insights] is een RESTful API die ontwikkelaars toestaat om zeer belangrijke waarneembaarheidsmetriek in Adobe Experience Platform bloot te stellen. Deze cijfers verstrekken inzichten in de gebruiksstatistieken van het Platform, gezondheid-controles voor de diensten van het Platform, historische tendensen, en prestatiesindicatoren voor diverse functies van het Platform. |
| [[!DNL Policy Service] API-handleiding](.././data-governance/api/overview.md) <br> (Gegevensbeheer) | De [!DNL Policy Service] Met API kunt u labels en beleidsregels voor gegevensgebruik maken en beheren om te bepalen welke marketingacties kunnen worden uitgevoerd tegen gegevens die bepaalde labels voor gegevensgebruik bevatten. Als u labels wilt toepassen op gegevenssets en velden, raadpleegt u de [[!DNL Dataset Service] API](.././data-governance/labels/dataset-api.md) hulplijn |
| [[!DNL Privacy Service] API-handleiding](.././privacy-service/api/getting-started.md) | De [!DNL Privacy Service] Met API kunnen ontwikkelaars hun verzoeken om toegang tot of verwijdering van hun persoonlijke gegevens in Experience Cloud-toepassingen maken en beheren, in overeenstemming met de wettelijke privacyregels. |
| [[!DNL Query Service] API-handleiding](.././query-service/api/getting-started.md) | De [!DNL Query Service] Met API kunnen ontwikkelaars hun Adobe Experience Platform-gegevens opvragen met behulp van standaard SQL. |
| [[!DNL Real-time Customer Profile] API-handleiding](.././profile/api/overview.md) | Met de realtime-API voor klantprofiel kunnen ontwikkelaars profielgegevens verkennen en ermee werken, zoals het weergeven van profielen, het maken en bijwerken van samenvoegbeleid, het exporteren of samplen van profielgegevens en het verwijderen van profielgegevens die niet langer vereist zijn of die bij fout zijn toegevoegd. |
| [Handleiding voor sandbox-API](.././sandboxes/api/getting-started.md) | Met de sandbox-API kunnen ontwikkelaars via programmacode geïsoleerde virtuele sandboxomgevingen in Adobe Experience Platform beheren. |
| [[!DNL Schema Registry] API-handleiding](.././xdm/api/overview.md) <br> (XDM) | De [!DNL Schema Registry] Met API kunnen ontwikkelaars programmatisch alle schema&#39;s en gerelateerde XDM-bronnen (Experience Data Model) in Adobe Experience Platform beheren. |
| [[!DNL Segmentation Service] API-handleiding](.././segmentation/api/overview.md) | De [!DNL Segmentation Service] Met API kunnen ontwikkelaars segmentatiebewerkingen in Adobe Experience Platform programmatisch beheren. Dit omvat het bouwen van segmenten en het produceren van publiek van uw gegevens van het Profiel van de Klant in real time. |
| [[!DNL Sensei Machine Learning] API-handleiding](.././data-science-workspace/api/getting-started.md) <br> (Werkruimte voor gegevenswetenschap) | De [!DNL Sensei Machine Learning] API verstrekt een mechanisme voor gegevenswetenschappers om machine het leren (ML) diensten van het algoritme op het instappen, experimenteren, en aan de dienstplaatsing te organiseren en te beheren. |

Voor meer informatie over specifieke eindpunten en verrichtingen beschikbaar voor elke dienst, gelieve te zien [API-naslagdocumentatie](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O.

## Volgende stappen

In dit document zijn de vereiste kopteksten, beschikbare hulplijnen en een voorbeeld-API-aanroep geïntroduceerd. Nu u de vereiste koptekstwaarden hebt om API-aanroepen uit te voeren op Adobe Experience Platform, selecteert u een API-eindpunt dat u wilt verkennen in het dialoogvenster [Tabel met Platform-API-hulplijnen](#api-guides).

Voor antwoorden op veelgestelde vragen raadpleegt u de [Handleiding voor het oplossen van problemen met Platforms](troubleshooting.md).

Als u een Postman-omgeving wilt instellen en de beschikbare Postman-verzamelingen wilt verkennen, raadpleegt u de [Platform Postman-handleiding](postman.md).
