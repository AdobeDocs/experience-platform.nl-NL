---
keywords: Experience Platform;home;popular topics;API error codes;API error code;error code API;error codes API;API request error;API troubleshooting;API error
solution: Experience Platform
title: Adobe Experience Platform - Veelgestelde vragen en handleiding voor probleemoplossing
description: Vind antwoorden op vaak gestelde vragen en een gids voor het oplossen van problemen gemeenschappelijke fouten in Experience Platform.
landing-page-description: Find answers to frequently asked questions and a guide for troubleshooting common errors in Experience Platform.
topic: getting started
type: Documentation
translation-type: tm+mt
source-git-commit: 72f60ef80a23f5ca4e70147ee6aa6027028fefd0
workflow-type: tm+mt
source-wordcount: '1954'
ht-degree: 1%

---


# [!DNL Platform] Veelgestelde vragen en handleiding voor probleemoplossing

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform en een gids voor probleemoplossing op hoog niveau voor algemene fouten die in een [!DNL Experience Platform] API kunnen worden aangetroffen. Voor het oplossen van problemengidsen op de individuele [!DNL Platform] diensten, zie de hieronder [dienst het oplossen van problemenfolder](#service-troubleshooting-directory) .

## Veelgestelde vragen {#faq}

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Adobe Experience Platform.

## Wat zijn API&#39; [!DNL Experience Platform] s? {#what-are-experience-platform-apis}

[!DNL Experience Platform] biedt veelvoudige RESTful APIs aan die HTTP- verzoeken om tot [!DNL Platform] middelen gebruiken. Deze dienst APIs elk stelt veelvoudige eindpunten bloot, en staat u toe om verrichtingen aan lijst (GET), raadpleging (GET) uit te voeren, (PUT en/of PATCH), en (DELETE) middelen uit te geven. Raadpleeg de [API-naslagdocumentatie](http://www.adobe.com/go/platform-api-reference-en) op Adobe I/O voor meer informatie over specifieke eindpunten en bewerkingen die voor elke service beschikbaar zijn.

## Hoe kan ik een API-aanvraag opmaken? {#how-do-i-format-an-api-request}

De aanvraagindelingen variëren afhankelijk van de gebruikte [!DNL Platform] API. De beste manier om te leren hoe te om uw API vraag te structureren is door samen met de voorbeelden te volgen die in de documentatie voor de bijzondere [!DNL Platform] dienst worden verstrekt u gebruikt.

### Voorbeeld-API-aanroepen lezen

De documentatie voor [!DNL Experience Platform] toont voorbeeld API vraag op twee verschillende manieren. Eerst, wordt de vraag voorgesteld in zijn **API formaat**, een malplaatjevertegenwoordiging die slechts de verrichting (GET, POST, PUT, PATCH, DELETE) toont en het eindpunt dat (bijvoorbeeld, `/global/classes`) wordt gebruikt. Sommige malplaatjes tonen ook de plaats van variabelen helpen illustreren hoe een vraag zou moeten worden geformuleerd, zoals `GET /{VARIABLE}/classes/{ANOTHER_VARIABLE}`.

De vraag wordt dan getoond als cURL bevelen in een **Verzoek**, die de noodzakelijke kopballen en volledige &quot;basisweg&quot;nodig omvat om met API met succes in wisselwerking te staan. Het basispad moet vooraf aan alle eindpunten worden toegevoegd. Het eerder vermelde `/global/classes` eindpunt wordt bijvoorbeeld `https://platform.adobe.io/data/foundation/schemaregistry/global/classes`. U zult het formaat van API/verzoekpatroon door de documentatie zien, en zal naar verwachting de volledige weg gebruiken die in het voorbeeldVerzoek wordt getoond wanneer het maken van uw eigen vraag aan Platform APIs.

### Voorbeeld-API-aanvraag

Hier volgt een voorbeeld-API-aanvraag die de indeling weergeeft die u in de documentatie zult tegenkomen.

**API-indeling**

De API-indeling toont de bewerking (GET) en het eindpunt dat wordt gebruikt. Variabelen worden aangegeven met accolades (in dit geval `{CONTAINER_ID}`).

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

Raadpleeg de [API-naslagdocumentatie](http://www.adobe.com/go/platform-api-reference-en)voor meer informatie over specifieke eindpunten in Platform-API&#39;s, inclusief vereiste headers en aanvraaginstanties.

## Wat is mijn IMS-organisatie? {#what-is-my-ims-organization}

Een IMS-organisatie is een Adobe-representatie van een klant. Om het even welke vergunning gegeven Adobe oplossingen zijn geïntegreerd met deze klantenorganisatie. Wanneer een IMS-organisatie gerechtigd is om toegang te verlenen [!DNL Experience Platform], kan zij toegang toewijzen aan ontwikkelaars. De IMS-organisatie-id (`x-gw-ims-org-id`) vertegenwoordigt de organisatie waarvoor een API-aanroep moet worden uitgevoerd en is daarom vereist als een header in alle API-aanvragen. Deze id kunt u vinden via de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): in het lusje van **Integraties** , navigeer aan de sectie van het **Overzicht** voor om het even welke bepaalde integratie om identiteitskaart onder de Geloofsbrieven **van de** Cliënt te vinden. Voor een geleidelijke analyse van hoe te voor authentiek te verklaren in [!DNL Platform], zie het [authentificatieleerprogramma](http://www.adobe.com/go/platform-api-authentication-en).

## Waar kan ik mijn API-sleutel vinden? {#where-can-i-find-my-api-key}

Een API-sleutel is vereist als een header in alle API-aanvragen. U vindt deze via de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Binnen de console, op het lusje van **Integraties** , navigeer aan de sectie van het **Overzicht** voor een specifieke integratie en u zult de sleutel onder de Verantwoordelijkheden **van de** Cliënt vinden. Voor een geleidelijke analyse van hoe te voor authentiek te verklaren aan [!DNL Platform], zie het [authentificatieleerprogramma](http://www.adobe.com/go/platform-api-authentication-en).

## Hoe krijg ik een toegangstoken? {#how-do-i-get-an-access-token}

Toegangstempens zijn vereist in de machtigingheader van alle API-aanroepen. Ze kunnen worden gegenereerd met een `curl` opdracht, op voorwaarde dat u toegang hebt tot een integratie voor een IMS-organisatie. Toegangstokens zijn slechts geldig gedurende 24 uur, waarna een nieuw teken moet worden geproduceerd om verder te gebruiken API. Voor details bij het produceren van toegangstokens, zie de [authentificatielutorial](http://www.adobe.com/go/platform-api-authentication-en).

## Hoe gebruik ik queryparameters? {#how-do-i-user-query-parameters}

Sommige [!DNL Platform] API eindpunten aanvaarden vraagparameters om van specifieke informatie de plaats te bepalen en de resultaten te filtreren die in de reactie zijn teruggekeerd. De parameters van de vraag worden toegevoegd aan verzoekwegen met een symbool van het vraagteken (`?`), dat door één of meerdere vraagparameters wordt gevolgd gebruikend het formaat `paramName=paramValue`. Wanneer het combineren van veelvoudige parameters in één enkele vraag, moet u ampersand (`&`) gebruiken om individuele parameters te scheiden. Het volgende voorbeeld toont aan hoe een verzoek dat veelvoudige vraagparameters gebruikt in de documentatie wordt vertegenwoordigd.

Voorbeelden van veelgebruikte queryparameters zijn:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Voor gedetailleerde informatie over welke vraagparameters voor de specifieke dienst of een eindpunt beschikbaar zijn, te herzien gelieve de dienst-specifieke documentatie.

## Hoe kan ik een JSON-veld aangeven dat moet worden bijgewerkt in een PATCH-verzoek? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Veel PATCH-bewerkingen in [!DNL Platform] API&#39;s gebruiken [JSON-aanwijzertekenreeksen](https://tools.ietf.org/html/rfc6901) om aan te geven dat de JSON-eigenschappen moeten worden bijgewerkt. Deze worden meestal opgenomen in de payloads voor aanvragen met de [JSON-indeling voor patches](https://tools.ietf.org/html/rfc6902) . Zie de handleiding [met grondbeginselen van de](api-fundamentals.md) API voor gedetailleerde informatie over vereiste syntaxis voor deze technologieën.

## Kan ik Postman gebruiken om aanroepen te maken naar [!DNL Platform] API&#39;s? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) is een nuttig hulpmiddel om vraag aan RESTful APIs te visualiseren. In dit [artikel](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wordt beschreven hoe u Postman kunt instellen om automatisch verificatie uit te voeren en deze te gebruiken voor het gebruik van API&#39; [!DNL Experience Platform] s.

## Wat zijn de systeemvereisten [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Afhankelijk van of u de UI of API gebruikt, zijn de volgende systeemvereisten van toepassing:

**Voor bewerkingen op basis van UI:**
- Een moderne, standaard webbrowser. Hoewel de nieuwste versie van [!DNL Chrome] wordt aanbevolen, worden de huidige en vorige grote releases van [!DNL Firefox], [!DNL Internet Explorer]en Safari ook ondersteund.
   - Telkens wanneer een nieuwe belangrijke versie wordt vrijgegeven, [!DNL Platform] begint steun de meest recente versie terwijl de steun voor de derde meest recente versie wordt gelaten vallen.
- Voor alle browsers moeten cookies en JavaScript zijn ingeschakeld.

**Voor API- en ontwikkelaarsinteracties:**
- Een ontwikkelomgeving voor REST-, streaming- en WebHaak-integratie.

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Hier volgt een lijst met fouten die u kunt tegenkomen bij het gebruik van een [!DNL Experience Platform] service. Voor het oplossen van problemengidsen op de individuele [!DNL Platform] diensten, zie de hieronder [dienst het oplossen van problemenfolder](#service-troubleshooting-directory) .

## API-statuscodes {#api-status-codes}

De volgende statuscodes kunnen worden gevonden op elke [!DNL Experience Platform] API. Elk artikel heeft verschillende oorzaken en daarom zijn de toelichtingen in deze paragraaf algemeen van aard. Raadpleeg de onderstaande map met [!DNL Platform] serviceproblemen voor meer informatie over specifieke fouten in afzonderlijke [services](#service-troubleshooting-directory) .

| Statuscode | Beschrijving | Mogelijke oorzaken |
--- | --- | ---
| 400 | Ongeldig verzoek | Het verzoek is onjuist samengesteld, bevat geen sleutelinformatie en/of bevat een onjuiste syntaxis. |
| 401 | Verificatie mislukt | De aanvraag heeft geen verificatiecontrole doorstaan. Uw toegangstoken ontbreekt of is ongeldig. Zie de [sectie voor tokenfouten](#oauth-token-is-missing) hieronder voor meer informatie. |
| 403 | Verboden | De bron is gevonden, maar u hebt niet de juiste referenties om deze te bekijken. |
| 404 | Niet gevonden | De gevraagde bron is niet gevonden op de server. De bron is mogelijk verwijderd of het gevraagde pad is onjuist ingevoerd. |
| 500 | Interne serverfout | Dit is een serverfout. Als u vele gelijktijdige vraag maakt, kunt u de API grens bereiken en moet uw resultaten filtreren. (Zie de subhandleiding voor [!DNL Catalog Service] API-ontwikkelaars voor [het filteren van gegevens](../catalog/api/filter-data.md) voor meer informatie.) Wacht even voordat u uw verzoek opnieuw probeert en neem contact op met de beheerder als het probleem zich blijft voordoen. |

## Koptekstfouten aanvragen {#request-header-errors}

Voor alle API-aanroepen zijn specifieke aanvraagheaders [!DNL Platform] vereist. Raadpleeg de documentatie bij de [API-naslaggids](http://www.adobe.com/go/platform-api-reference-en)voor informatie over de vereiste headers voor afzonderlijke services. Zie de zelfstudie [Verificatie voor](http://www.adobe.com/go/platform-api-authentication-en)informatie over de waarden voor de vereiste verificatieheaders. Als een van deze headers ontbreekt of ongeldig is bij het aanroepen van een API, kunnen de volgende fouten optreden.

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

Dit foutbericht wordt weergegeven wanneer het toegangstoken in de `Authorization` koptekst niet geldig is. Controleer of het token correct is ingevoerd of [genereer een nieuw token](http://www.adobe.com/go/platform-api-authentication-en) in de Adobe I/O-console.

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

Dit foutbericht wordt weergegeven wanneer de gebruiker of Adobe I/O-integratie (geïdentificeerd door het [toegangstoken](#how-do-i-get-an-access-token) in de `Authorization` koptekst) niet het recht heeft om aanroepen uit te voeren naar API&#39; [!DNL Experience Platform] s voor de IMS-organisatie die in de `x-gw-ims-org-id` koptekst is opgegeven. Controleer of u de juiste id voor uw IMS-organisatie in de koptekst hebt opgegeven voordat u het opnieuw probeert. Als u uw organisatie-id niet kent, vindt u deze in de [Adobe I/O-console](https://console.adobe.io): op het tabblad **Integraties** navigeert u naar de sectie **Overzicht** voor een specifieke integratie om de id onder **Client Credentials** te vinden.

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

Hieronder volgt een lijst met probleemoplossingsgidsen en API-naslagdocumentatie voor [!DNL Experience Platform] API&#39;s. Elke het oplossen van problemengids verstrekt antwoorden aan vaak gestelde vragen en oplossingen aan problemen die voor de individuele [!DNL Platform] diensten specifiek zijn. De API verwijzingsdocumenten verstrekken een uitvoerige gids aan alle beschikbare eindpunten voor elke dienst, en tonen de instanties van de steekproefaanvraag, reacties, en foutencodes die u kunt ontvangen.

| Service | API-referentie | Problemen oplossen |
| --- | --- | --- |
| Toegangsbeheer | [API voor toegangsbeheer](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/access-control.yaml) | [Handleiding voor probleemoplossing bij toegangsbeheer](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform-gegevensinscriptie | [[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml) | [Handleiding voor](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[het oplossen van problemen bij het opnemen van batterijenHandleiding voor het oplossen van problemen bij het opnemen van streaming](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] gids voor problemen](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform Data Governance | [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/id-service-api.yaml) | [[!DNL Identity Service] gids voor problemen](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/qs-api.yaml) | [[!DNL Query Service] gids voor problemen](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform-segmentatie | [[!DNL Segmentation API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/catalog.yaml) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) | [[!DNL XDM System] Veelgestelde vragen en handleiding voor probleemoplossing](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] en [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/flow-service.yaml) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml) | [[!DNL Profile] gids voor problemen](../profile/troubleshooting.md) |
| Sandboxen | [Sandbox-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sandbox-api.yaml) | [Richtlijnen voor het oplossen van problemen met sandboxen](../sandboxes/troubleshooting-guide.md) |

