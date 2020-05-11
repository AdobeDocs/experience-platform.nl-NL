---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform - Veelgestelde vragen en handleiding voor probleemoplossing
topic: getting started
translation-type: tm+mt
source-git-commit: d9aa21a7439a6c40f6f51dfbdf5c7b3690c4593a
workflow-type: tm+mt
source-wordcount: '2001'
ht-degree: 0%

---


# Platform FAQ en het oplossen van problemengids

Dit document bevat antwoorden op veelgestelde vragen over het Adobe Experience Platform en een gids voor probleemoplossing op hoog niveau voor algemene fouten die kunnen optreden in elke API van het Experience Platform. Voor het oplossen van problemengidsen op de individuele diensten van het Platform, zie de [dienst het oplossen van problemenfolder](#service-troubleshooting-directory) hieronder.

## Veelgestelde vragen {#faq}

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over het Adobe Experience Platform.

## Wat zijn Experience Platform API&#39;s? {#what-are-experience-platform-apis}

Het Platform van de ervaring biedt veelvoudige RESTful APIs aan die HTTP- verzoeken om tot de middelen van het Platform gebruiken toegang te hebben. Deze dienst APIs elk stelt veelvoudige eindpunten bloot, en staat u toe om verrichtingen aan lijst (KRIJGEN), raadpleging (KRIJGEN) uit te voeren, (PLAATS en/of PATCH) middelen uit te geven, en te schrappen (VERWIJDEREN). Raadpleeg de [API-naslagdocumentatie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html) bij Adobe I/O voor meer informatie over specifieke eindpunten en bewerkingen die beschikbaar zijn voor elke service.

## Hoe kan ik een API-aanvraag opmaken? {#how-do-i-format-an-api-request}

De aanvraagindelingen zijn afhankelijk van de Platform-API die wordt gebruikt. De beste manier om te leren hoe te om uw API vraag te structureren is door samen met de voorbeelden te volgen die in de documentatie voor de bepaalde dienst van het Platform worden verstrekt u gebruikt.

### Voorbeeld-API-aanroepen lezen

De documentatie voor het Platform van de Ervaring toont voorbeeld API vraag op twee verschillende manieren. Eerst, wordt de vraag voorgesteld in zijn **API formaat**, een malplaatjevertegenwoordiging die slechts de verrichting (GET, POST, PUT, PATCH, DELETE) en het eindpunt toont dat (bijvoorbeeld, `/global/classes`) wordt gebruikt. Sommige malplaatjes tonen ook de plaats van variabelen helpen illustreren hoe een vraag zou moeten worden geformuleerd, zoals `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

De vraag wordt dan getoond als cURL bevelen in een **Verzoek**, die de noodzakelijke kopballen en volledige &quot;basisweg&quot;nodig omvat om met API met succes in wisselwerking te staan. Het basispad moet vooraf aan alle eindpunten worden toegevoegd. Het eerder vermelde `/global/classes` eindpunt wordt bijvoorbeeld `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. U zult het formaat van API/verzoekpatroon door de documentatie zien, en zal naar verwachting de volledige weg gebruiken die in het voorbeeldVerzoek wordt getoond wanneer het maken van uw eigen vraag aan Platform APIs.

### Voorbeeld-API-aanvraag

Hier volgt een voorbeeld-API-aanvraag die de indeling weergeeft die u in de documentatie zult tegenkomen.

**API-indeling**

Het API formaat toont de verrichting (KRIJGT) en het eindpunt dat wordt gebruikt. Variabelen worden aangegeven met accolades (in dit geval `{CONTAINER_ID}`).

```http
GET /{CONTAINER_ID}/classes
```

**Verzoek**

In deze voorbeeldaanvraag krijgen de variabelen van de API-indeling de werkelijke waarden in het aanvraagpad. Alle vereiste kopballen worden eveneens getoond, als of waarden van de steekproefkopbal of variabelen waar de gevoelige informatie (zoals veiligheidstekenen en toegangsidentiteitskaart) zou moeten worden omvat.

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

Raadpleeg de documentatie bij de [API-naslaggids](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)voor meer informatie over specifieke eindpunten in platform-API&#39;s, inclusief vereiste headers en aanvraagorganen.

## Wat is mijn IMS-organisatie? {#what-is-my-ims-organization}

Een IMS-organisatie is een Adobe-representatie van een klant. Alle Adobe-oplossingen met licentie zijn geïntegreerd met deze klantenorganisatie. Wanneer een IMS-organisatie recht heeft op Experience Platform, kan zij toegang toewijzen aan ontwikkelaars. De IMS-organisatie-id (`x-gw-ims-org-id`) vertegenwoordigt de organisatie waarvoor een API-aanroep moet worden uitgevoerd en is daarom vereist als een header in alle API-aanvragen. Deze id kunt u vinden via de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): in het lusje van **Integraties** , navigeer aan de sectie van het **Overzicht** voor om het even welke bepaalde integratie om identiteitskaart onder de Geloofsbrieven **van de** Cliënt te vinden. Voor een geleidelijke analyse van hoe te in Platform voor authentiek te verklaren, zie het [authentificatieleerprogramma](../tutorials/authentication.md).

## Waar kan ik mijn API-sleutel vinden? {#where-can-i-find-my-api-key}

Een API-sleutel is vereist als een header in alle API-aanvragen. U vindt deze via de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Binnen de console, op het lusje van **Integraties** , navigeer aan de sectie van het **Overzicht** voor een specifieke integratie en u zult de sleutel onder de Verantwoordelijkheden **van de** Cliënt vinden. Voor een geleidelijke analyse van hoe te om aan Platform voor authentiek te verklaren, zie het [authentificatieleerprogramma](../tutorials/authentication.md).

## Hoe krijg ik een toegangstoken? {#how-do-i-get-an-access-token}

Toegangstempens zijn vereist in de machtigingheader van alle API-aanroepen. Ze kunnen worden gegenereerd met een `curl` opdracht, op voorwaarde dat u toegang hebt tot een integratie voor een IMS-organisatie. Toegangstokens zijn slechts geldig gedurende 24 uur, waarna een nieuw teken moet worden geproduceerd om verder te gebruiken API. Voor details bij het produceren van toegangstokens, zie de [authentificatielutorial](../tutorials/authentication.md).

## Hoe gebruik ik queryparameters? {#how-do-i-user-query-parameters}

Sommige platform API eindpunten aanvaarden vraagparameters om van specifieke informatie de plaats te bepalen en de resultaten te filtreren die in de reactie zijn teruggekeerd. De parameters van de vraag worden toegevoegd aan verzoekwegen met een symbool van het vraagteken (`?`), dat door één of meerdere vraagparameters wordt gevolgd gebruikend het formaat `paramName=paramValue`. Wanneer het combineren van veelvoudige parameters in één enkele vraag, moet u ampersand (`&`) gebruiken om individuele parameters te scheiden. Het volgende voorbeeld toont aan hoe een verzoek dat veelvoudige vraagparameters gebruikt in de documentatie wordt vertegenwoordigd.

Voorbeelden van veelgebruikte queryparameters zijn:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Voor gedetailleerde informatie over welke vraagparameters voor de specifieke dienst of een eindpunt beschikbaar zijn, te herzien gelieve de dienst-specifieke documentatie.

## Hoe kan ik een JSON-veld aangeven dat moet worden bijgewerkt in een PATCH-verzoek? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Veel PATCH-bewerkingen in platform-API&#39;s gebruiken [JSON-aanwijzertekenreeksen](https://tools.ietf.org/html/rfc6901) om aan te geven dat de JSON-eigenschappen moeten worden bijgewerkt. Deze worden meestal opgenomen in de payloads voor aanvragen met de [JSON-indeling voor patches](https://tools.ietf.org/html/rfc6902) . Zie de handleiding [met grondbeginselen van de](api-fundamentals.md) API voor gedetailleerde informatie over vereiste syntaxis voor deze technologieën.

## Kan ik Postman gebruiken om vraag aan Platform APIs te maken? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.getpostman.com/) is een nuttig hulpmiddel om vraag aan RESTful APIs te visualiseren. In dit [artikel](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u Postman kunt instellen om automatisch verificatie uit te voeren en deze te gebruiken voor gebruik van de API&#39;s van het Experience Platform.

## Wat zijn de systeemvereisten voor Platform? {#what-are-the-system-requirements-for-platform}

Afhankelijk van of u de UI of API gebruikt, zijn de volgende systeemvereisten van toepassing:

**Voor bewerkingen op basis van UI:**
- Een moderne, standaard webbrowser. Hoewel de nieuwste versie van Chrome wordt aanbevolen, worden de huidige en vorige grote versies van Firefox, Internet Explorer en Safari ook ondersteund.
   - Telkens wanneer een nieuwe belangrijke versie wordt vrijgegeven, begint Platform steun de meest recente versie terwijl de steun voor de derde meest recente versie wordt gelaten vallen.
- Voor alle browsers moeten cookies en JavaScript zijn ingeschakeld.

**Voor API- en ontwikkelaarsinteracties:**
- Een ontwikkelomgeving voor REST-, streaming- en WebHaak-integratie.

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Hieronder volgt een lijst met fouten die u kunt tegenkomen bij het gebruik van een service van het Experience Platform. Voor het oplossen van problemengidsen op de individuele diensten van het Platform, zie de [dienst het oplossen van problemenfolder](#service-troubleshooting-directory) hieronder.

## API-statuscodes {#api-status-codes}

Op elke API van het Experience Platform kunnen de volgende statuscodes worden gevonden. Elk artikel heeft verschillende oorzaken en daarom zijn de toelichtingen in deze paragraaf algemeen van aard. Voor meer details betreffende specifieke fouten in de individuele diensten van het Platform, te zien gelieve de [dienst het oplossen van problemenfolder](#service-troubleshooting-directory) hieronder.

| Statuscode | Beschrijving | Mogelijke oorzaken |
--- | --- | ---
| 400 | Ongeldig verzoek | Het verzoek is niet correct samengesteld, bevat geen sleutelinformatie en/of bevat een onjuiste syntaxis. |
| 401 | Verificatie mislukt | De aanvraag heeft geen verificatiecontrole doorstaan. Uw toegangstoken ontbreekt of is ongeldig. Zie de [sectie voor tokenfouten](#oauth-token-is-missing) hieronder voor meer informatie. |
| 403 | Verboden | De bron is gevonden, maar u hebt niet de juiste referenties om deze te bekijken. |
| 404 | Niet gevonden | De gevraagde bron is niet gevonden op de server. De bron is mogelijk verwijderd of het gevraagde pad is onjuist ingevoerd. |
| 500 | Interne serverfout | Dit is een serverfout. Als u vele gelijktijdige vraag maakt, kunt u de API grens bereiken en moet uw resultaten filtreren. (Zie de subhandleiding voor ontwikkelaars van de Catalogusservice-API voor meer informatie over het [filteren van gegevens](../catalog/api/filter-data.md) .) Wacht even voordat u uw verzoek opnieuw probeert en neem contact op met de beheerder als het probleem zich blijft voordoen. |

## Koptekstfouten aanvragen {#request-header-errors}

Voor alle API-aanroepen in Platform zijn specifieke aanvraagheaders vereist. Raadpleeg de documentatie bij de [API-naslaggids](https://www.adobe.io/apis/experienceplatform/home/api-reference.html)voor informatie over de vereiste headers voor afzonderlijke services. Zie de zelfstudie [Verificatie voor](../tutorials/authentication.md)informatie over de waarden voor de vereiste verificatieheaders. Als een van deze headers ontbreekt of ongeldig is bij het aanroepen van een API, kunnen de volgende fouten optreden.

### OAuth-token ontbreekt {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Dit foutbericht wordt weergegeven wanneer een `Authorization` koptekst ontbreekt in een API-aanvraag. Zorg ervoor dat de machtigingheader is opgenomen met een geldig toegangstoken voordat u het opnieuw probeert.

### OAuth-token is niet geldig

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Dit foutbericht wordt weergegeven wanneer het toegangstoken in de `Authorization` koptekst niet geldig is. Controleer of het token correct is ingevoerd of [genereer een nieuw token](../tutorials/authentication.md) in de Adobe I/O-console.

### API-sleutel is vereist

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Dit foutbericht wordt weergegeven wanneer een API-sleutelheader (`x-api-key`) ontbreekt in een API-aanvraag. Zorg ervoor dat de header is opgenomen met een geldige API-sleutel voordat u het opnieuw probeert.

### API-sleutel is ongeldig

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Dit foutbericht wordt weergegeven wanneer de waarde van de opgegeven API-sleutelheader (`x-api-key`) ongeldig is. Controleer of u de sleutel correct hebt ingevoerd voordat u het opnieuw probeert. Als u de API-sleutel niet kent, vindt u deze in de [Adobe I/O-console](https://console.adobe.io): op het tabblad **Integraties** navigeert u naar de sectie **Overzicht** voor een specifieke integratie om de API-sleutel onder **Client Credentials** te vinden.


### Ontbrekende koptekst

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Dit foutbericht wordt weergegeven wanneer een IMS org-header (`x-gw-ims-org-id`) ontbreekt in een API-aanvraag. Zorg ervoor dat de koptekst is opgenomen in de id van uw IMS-organisatie voordat u het opnieuw probeert.

### Profiel is niet geldig

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Dit foutbericht wordt weergegeven wanneer de gebruiker of Adobe I/O-integratie (geïdentificeerd door het [toegangstoken](#how-do-i-get-an-access-token) in de `Authorization` koptekst) niet het recht heeft om aanroepen uit te voeren naar Experience Platform-API&#39;s voor de IMS-organisatie in de `x-gw-ims-org-id` koptekst. Controleer of u de juiste id voor uw IMS-organisatie in de koptekst hebt opgegeven voordat u het opnieuw probeert. Als u uw organisatie-id niet kent, vindt u deze in de [Adobe I/O-console](https://console.adobe.io): op het tabblad **Integraties** navigeert u naar de sectie **Overzicht** voor een specifieke integratie om de id onder **Client Credentials** te vinden.

### Geldig inhoudstype niet opgegeven

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Dit foutbericht wordt weergegeven wanneer een POST-, PUT- of PATCH-aanvraag een ongeldige of ontbrekende `Content-Type` koptekst heeft. Zorg ervoor dat de koptekst in de aanvraag is opgenomen en dat de waarde ervan `application/json`is.


## Servicemap voor probleemoplossing {#service-troubleshooting-directory}

Hieronder volgt een lijst met probleemoplossingsgidsen en API-naslagdocumentatie voor Experience Platform-API&#39;s. Elke het oplossen van problemengids verstrekt antwoorden op vaak gestelde vragen en oplossingen aan problemen die voor de individuele diensten van het Platform specifiek zijn. De API verwijzingsdocumenten verstrekken een uitvoerige gids aan alle beschikbare eindpunten voor elke dienst, en tonen de instanties van de steekproefaanvraag, reacties, en foutencodes die u kunt ontvangen.

| Service | API-referentie | Problemen oplossen |
--- | --- | ---
| Toegangsbeheer | [API voor toegangsbeheer](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Handleiding voor probleemoplossing bij toegangsbeheer](../access-control/troubleshooting-guide.md) |
| Catalogus | [Catalogusservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| Gegevensinname (batch) | [Data Ingestie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handleiding voor het oplossen van problemen met inslikken](../ingestion/batch-ingestion/troubleshooting.md) |
| Gegevensverwerking (streaming) | [Data Ingestie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handleiding voor het oplossen van problemen bij het streamen](../ingestion/streaming-ingestion/troubleshooting.md) |
| Werkruimte voor gegevenswetenschap | [API Sensei Machine Learning](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [Handleiding voor het oplossen van problemen in de Data Science Workspace](../data-science-workspace/troubleshooting-guide.md) |
| Etikettering en handhaving van gegevensgebruik (DULE) | [DULE Policy Service API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Experience Data Model (XDM) | [Schema-register-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [Handleiding Veelgestelde vragen over XDM-systemen en probleemoplossing](../xdm/troubleshooting-guide.md) |
| Identiteitsservice | [Identiteitsservice-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [Handleiding voor het oplossen van problemen met identiteitsservice](../identity-service/troubleshooting-guide.md) |
| Query-service | [Query Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [Handleiding voor het oplossen van problemen bij Query Service](../query-service/troubleshooting-guide.md) |
| Klantprofiel in realtime | [Real-time API voor klantprofiel](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) |  |
| Sandboxen | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Richtlijnen voor het oplossen van problemen met sandboxen](../sandboxes/troubleshooting-guide.md) |
| Segmentering | [Segmentatie-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |