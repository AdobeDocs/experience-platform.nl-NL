---
keywords: Experience Platform;home;populaire onderwerpen;Adobe Experience Platform;api-handleiding;platform-api-handleiding;inleiding tot platform;ontwikkelaarshandleiding
solution: Experience Platform
title: Aan de slag met Adobe Experience Platform API's
description: Adobe Experience Platform biedt API-services die nauw met elkaar zijn verbonden. Deze handleiding bevat informatie over de beschikbare services, vereiste headers voor CRUD-bewerkingen, foutberichten, Postman-verzamelingen en voorbeeld-API-aanroepen.
exl-id: a362bcb4-a908-43a8-abd3-0e1d21cb9117
source-git-commit: c728d63c22593ca56999dd0bb6679dea7de0e00a
workflow-type: tm+mt
source-wordcount: '1405'
ht-degree: 0%

---

# Aan de slag met Adobe Experience Platform API&#39;s

Adobe Experience Platform is ontwikkeld volgens een &quot;API first&quot;-filosofie. Met platform-API&#39;s kunt u via programmacode elementaire CRUD-bewerkingen (Maken, Lezen, Bijwerken, Verwijderen) uitvoeren op gegevens, zoals het configureren van berekende kenmerken, het openen van gegevens/entiteiten, het exporteren van gegevens, het verwijderen van overbodige gegevens of batches en meer.

De APIs voor elke dienst van het Experience Platform delen allen de zelfde reeks authentificatiekopballen en gebruiken gelijkaardige syntaxis voor hun verrichtingen CRUD. In de volgende handleiding worden de stappen beschreven die nodig zijn om aan de slag te gaan met platform-API&#39;s.

## Verificatie en kopteksten

Om vraag aan de eindpunten van het Platform met succes te maken, wordt u vereist om het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en) te voltooien. Het voltooien van de autorisatiezelfstudie biedt de waarden voor elk van de vereiste headers in Experience Platform API-aanroepen, zoals hieronder wordt getoond:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

### Sandbox-header

Alle bronnen in Experience Platform zijn geïsoleerd naar specifieke virtuele sandboxen. Verzoeken aan platform-API&#39;s vereisen een header die de naam aangeeft van de sandbox waarin de bewerking plaatsvindt:

- `x-sandbox-name: {SANDBOX_NAME}`

Voor meer informatie over zandbakken in Platform, zie de [ documentatie van het zandbakoverzicht ](../sandboxes/home.md).

### Koptekst van inhoudstype

Alle verzoeken met een lading in het verzoeklichaam (zoals POST, PUT, en de vraag van PATCH) moeten een `Content-Type` kopbal omvatten. Accepteerde waarden zijn specifiek voor elk API-eindpunt. Als een specifieke `Content-Type` waarde voor een eindpunt nodig is, zal zijn waarde in de voorbeeld API verzoeken worden getoond die door de [ worden verstrekt API gidsen voor de individuele diensten van het Platform ](#api-guides).

## Grondbeginselen van Experience Platform API

Adobe Experience Platform API&#39;s maken gebruik van verschillende onderliggende technologieën en syntaxis die belangrijk zijn om te begrijpen, zodat de resources van het platform effectief kunnen worden beheerd.

Meer over het onderliggende API technologiegebruik van het Platform, met inbegrip van voorbeeld JSON schemavoorwerpen leren, bezoek de [ Experience Platform API fundamentals ](api-fundamentals.md) gids.

## Postman-verzamelingen voor Experience Platform-API&#39;s

Postman is een samenwerkingsplatform voor API-ontwikkeling waarmee u omgevingen kunt instellen met vooraf ingestelde variabelen, API-verzamelingen kunt delen, CRUD-aanvragen kunt stroomlijnen en nog veel meer. De meeste Platform API-services hebben Postman-verzamelingen die kunnen worden gebruikt om te helpen bij het maken van API-aanroepen.

Meer over Postman met inbegrip van leren hoe te opstelling een milieu, een lijst van beschikbare inzamelingen, en hoe te om inzamelingen in te voeren, bezoek de [ documentatie van Postman van het Platform ](postman.md).

## API-voorbeeldaanroepen lezen {#sample-api}

De aanvraagindelingen zijn afhankelijk van de Platform-API die wordt gebruikt. De beste manier om te leren hoe te om uw API vraag te structureren is door samen met de voorbeelden te volgen die in de documentatie voor de bepaalde dienst van het Platform worden verstrekt u gebruikt.

In de documentatie voor [!DNL Experience Platform] worden op twee verschillende manieren voorbeeld-API-aanroepen weergegeven. Eerst, wordt de vraag voorgesteld in zijn **API formaat**, een malplaatjevertegenwoordiging die slechts de verrichting (GET, POST, PUT, PATCH, DELETE) en het eindpunt toont dat (bijvoorbeeld, `/global/classes`) wordt gebruikt. Sommige malplaatjes tonen ook de plaats van variabelen helpen illustreren hoe een vraag, zoals `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}` zou moeten worden geformuleerd.

De vraag wordt dan getoond als cURL bevelen in a **Verzoek**, die de noodzakelijke kopballen en volledige &quot;basisweg&quot;nodig omvat om met API met succes in wisselwerking te staan. Het basispad moet vooraf aan alle eindpunten worden toegevoegd. Het bovengenoemde `/global/classes` -eindpunt wordt bijvoorbeeld `https://platform.adobe.io/data/foundation/schemaregistry/global/classes` . U zult het formaat van API/verzoekpatroon door de documentatie zien, en zal naar verwachting de volledige weg gebruiken die in het voorbeeldverzoek wordt getoond wanneer het maken van uw eigen vraag aan Platform APIs.

### Voorbeeld-API-aanvraag

Hieronder ziet u een voorbeeld-API-aanvraag die de indeling weergeeft die u in de documentatie zult tegenkomen.

**API formaat**

De API-indeling toont de bewerking (GET) en het eindpunt dat wordt gebruikt. Variabelen worden aangegeven met accolades (in dit geval `{CONTAINER_ID}` ).

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

**Reactie**

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

De [ het oplossen van problemengids van het Platform ](troubleshooting.md#errors-and-troubleshooting) verstrekt een lijst van fouten die u wanneer het gebruiken van om het even welke dienst van het Experience Platform kunt ontmoeten.

Voor het oplossen van problemengidsen op de individuele diensten van het Platform, zie de [ folder van het de dienstoplossen van problemen ](troubleshooting.md#service-troubleshooting-directory).

Voor meer informatie over specifieke eindpunten in Platform APIs, met inbegrip van vereiste kopballen en verzoekorganismen, gelieve te zien de [ gidsen van het Platform API ](#api-guides).

## Platform API-hulplijnen {#api-guides}

| API-handleiding | Beschrijving |
| --- | --- |
| [[!DNL Access Control]  API gids ](.././access-control/api/getting-started.md) | Het API-eindpunt van [!DNL Access Control] kan het huidige beleid ophalen dat van kracht is voor een gebruiker op bepaalde bronnen binnen een opgegeven sandbox. Alle andere mogelijkheden van de toegangscontrole worden verstrekt door [ Adobe Admin Console ](https://adminconsole.adobe.com/). |
| [ Gids van de Inname van de Partij API ](.././ingestion/batch-ingestion/api-overview.md) | Met de Adobe Experience Platform [!DNL Data Ingestion] -API kunt u gegevens als batchbestanden in Platform opnemen. Gegevens die worden opgenomen kunnen de profielgegevens van een vlak dossier in een systeem van CRM (zoals een dossier van het Pakket), of gegevens zijn die met een bekend schema in de Registratie van het Schema (XDM) in overeenstemming zijn. |
| [[!DNL Catalog Service]  API gids ](.././catalog/api/getting-started.md) | Met de API van [!DNL Catalog Service] kunnen ontwikkelaars metagegevens van gegevenssets beheren in Adobe Experience Platform. Dit omvat gegevenslocaties, verwerkingsfasen, fouten die tijdens de verwerking zijn opgetreden en gegevensrapporten. |
| [[!DNL Data Access]  API gids ](.././data-access/api.md) | Met de API van [!DNL Data Access] kunnen ontwikkelaars informatie ophalen over ingesloten gegevenssets binnen het Experience Platform. Hiertoe behoren het openen en downloaden van gegevenssetbestanden, het ophalen van koptekstgegevens, het opgeven van mislukte en opvolgende batches en het downloaden van voorvertoningen van CSV-/Parquet-bestanden. |
| [[!DNL Dataset Service]  API gids ](.././data-governance/labels/dataset-api.md) | Met de Dataset Service API kunt u gebruikslabels voor gegevenssets toepassen en bewerken. Deze klasse maakt deel uit van de mogelijkheden van de Adobe Experience Platform-gegevenscatalogus, maar staat los van de API van de Catalogusservice die metagegevens van gegevenssets beheert. |
| [[!DNL Edge Network Server]  API gids ](../server-api/overview.md) | [!DNL Edge Network Server API] kan voor een verscheidenheid van gegevensinzameling, verpersoonlijking, reclame en marketing gebruiksgevallen worden gebruikt. [!DNL Server API] kan op servers, [!DNL IoT] apparaten, reeks-hoogste dozen, en een verscheidenheid van andere apparaten worden gebruikt. |
| [[!DNL Identity Service]  API gids ](.././identity-service/api/getting-started.md) | Met de API van [!DNL Identity Service] kunnen ontwikkelaars de identificatie van uw klanten via verschillende apparaten, kanalen en in de buurt van realtime beheren met behulp van identiteitsgrafieken in Adobe Experience Platform. |
| [[!DNL Observability Insights]  API gids ](.././observability/api/overview.md) | [!DNL Observability Insights] is een RESTful API die ontwikkelaars toestaat om zeer belangrijke waarneembaarheidsmetriek in Adobe Experience Platform bloot te stellen. Deze metriek verstrekt inzicht in het gebruiksstatistieken van het Platform, gezondheid-controles voor de diensten van het Platform, historische tendensen, en prestatiesindicatoren voor diverse functies van het Platform. |
| [[!DNL Policy Service]  API gids ](.././data-governance/api/overview.md) <br> (het Beheer van Gegevens) | Met de API van [!DNL Policy Service] kunt u labels en beleidsregels voor gegevensgebruik maken en beheren om te bepalen welke marketingacties kunnen worden uitgevoerd tegen gegevens die bepaalde labels voor gegevensgebruik bevatten. Om etiketten op datasets en gebieden toe te passen, verwijs naar [[!DNL Dataset Service]  API ](.././data-governance/labels/dataset-api.md) gids |
| [[!DNL Privacy Service]  API gids ](.././privacy-service/api/getting-started.md) | Met de API van [!DNL Privacy Service] kunnen ontwikkelaars klantverzoeken maken en beheren om toegang te krijgen tot of gegevens te verwijderen uit verschillende Experiencen Cloud, in overeenstemming met de wettelijke privacyregels. |
| [[!DNL Query Service]  API gids ](.././query-service/api/getting-started.md) | Met de API van [!DNL Query Service] kunnen ontwikkelaars hun Adobe Experience Platform-gegevens opvragen met behulp van standaard SQL. |
| [[!DNL Real-Time Customer Profile]  API gids ](.././profile/api/overview.md) | Met de realtime-API voor klantprofiel kunnen ontwikkelaars profielgegevens verkennen en ermee werken, zoals het weergeven van profielen, het maken en bijwerken van samenvoegbeleid, het exporteren of samplen van profielgegevens en het verwijderen van profielgegevens die niet langer vereist zijn of die bij fout zijn toegevoegd. |
| [ zandbak API gids ](.././sandboxes/api/getting-started.md) | Met de sandbox-API kunnen ontwikkelaars via programmacode geïsoleerde virtuele sandboxomgevingen in Adobe Experience Platform beheren. |
| [[!DNL Schema Registry]  API gids ](.././xdm/api/overview.md) <br> (XDM) | Met de API van [!DNL Schema Registry] kunnen ontwikkelaars programmatisch alle schema&#39;s en gerelateerde XDM-bronnen (Experience Data Model) in Adobe Experience Platform beheren. |
| [[!DNL Segmentation Service]  API gids ](.././segmentation/api/overview.md) | Met de API van [!DNL Segmentation Service] kunnen ontwikkelaars segmentatiebewerkingen in Adobe Experience Platform programmatisch beheren. Dit omvat het bouwen van segmenten en het produceren van publiek van uw gegevens van het Profiel van de Klant in real time. |
| [[!DNL Sensei Machine Learning]  API gids ](.././data-science-workspace/api/getting-started.md) <br> (de Wetenschap van Gegevens Workspace) | De API van [!DNL Sensei Machine Learning] verstrekt een mechanisme voor gegevenswetenschappers om machine het leren (ML) diensten van algoritme op het instappen, experimenteren, en aan de dienstplaatsing te organiseren en te beheren. |

Voor meer informatie over specifieke eindpunten en verrichtingen beschikbaar voor elke dienst, gelieve te zien de [ API verwijzingsdocumentatie ](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O.

## Volgende stappen

In dit document zijn de vereiste kopteksten, beschikbare hulplijnen en een voorbeeld-API-aanroep geïntroduceerd. Nu u de vereiste kopbalwaarden nodig hebt om API vraag op Adobe Experience Platform te maken, selecteer een API eindpunt u van de [ lijst van de gidsen van het Platform API ](#api-guides) wenst te onderzoeken.

Voor antwoorden op vaak gestelde vragen, verwijs naar de [ het oplossen van problemengids van het Platform ](troubleshooting.md).

Om opstelling een milieu van Postman en de beschikbare inzamelingen van Postman te onderzoeken, verwijs naar de [ gids van Postman van het Platform ](postman.md).
