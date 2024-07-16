---
keywords: Experience Platform;home;populaire onderwerpen;API-foutcodes;API-foutcode;API voor foutcode;API voor foutcodes;API-aanvraagfout;API-probleemoplossing;API-fout
solution: Experience Platform
title: Adobe Experience Platform - Veelgestelde vragen en handleiding voor probleemoplossing
description: Vind antwoorden op veelgestelde vragen en een handleiding voor het oplossen van veelvoorkomende problemen in Experience Platform.
landing-page-description: Vind antwoorden op veelgestelde vragen en een handleiding voor het oplossen van veelvoorkomende problemen in Experience Platform.
short-description: Vind antwoorden op veelgestelde vragen en een handleiding voor het oplossen van veelvoorkomende problemen in Experience Platform.
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: 81f570f8e5401624ccac74696b2323252a4de0a9
workflow-type: tm+mt
source-wordcount: '1812'
ht-degree: 3%

---

# [!DNL Platform] Handleiding Veelgestelde vragen en problemen oplossen

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform en een gids voor probleemoplossing op hoog niveau voor algemene fouten die kunnen worden aangetroffen in elke [!DNL Experience Platform] -API. Voor het oplossen van problemengidsen op de individuele [!DNL Platform] diensten, zie de [ folder van het de dienstoplossen van problemen ](#service-troubleshooting-directory) hieronder.

## Veelgestelde vragen {#faq}

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Adobe Experience Platform.

## Wat zijn [!DNL Experience Platform] API&#39;s? {#what-are-experience-platform-apis}

[!DNL Experience Platform] biedt meerdere RESTful-API&#39;s die HTTP-aanvragen gebruiken om toegang te krijgen tot [!DNL Platform] -bronnen. Deze dienst APIs elk stelt veelvoudige eindpunten bloot, en staat u toe om verrichtingen aan lijst (GET), raadpleging (GET) uit te voeren, (PUT en/of PATCH), en (DELETE) middelen uit te geven. Voor meer informatie over specifieke eindpunten en verrichtingen beschikbaar voor elke dienst, gelieve te zien de [ documentatie van de Verwijzing API ](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O.

## Hoe kan ik een API-aanvraag opmaken? {#how-do-i-format-an-api-request}

De aanvraagindelingen variëren afhankelijk van de [!DNL Platform] API die wordt gebruikt. De beste manier om te leren hoe te om uw API vraag te structureren is door naast de voorbeelden te volgen die in de documentatie voor de bepaalde [!DNL Platform] dienst worden verstrekt u gebruikt.

Voor meer informatie bij het formatteren van API verzoeken, gelieve te bezoeken Platform API begonnen gids [ lezend steekproefAPI vraag ](./api-guide.md#sample-api) sectie.

## Wat is mijn organisatie? {#what-is-my-ims-organization}

Een organisatie is een Adobe vertegenwoordiging van een klant. Om het even welke vergunning gegeven oplossingen van de Adobe zijn geïntegreerd met deze klantenorganisatie. Wanneer een organisatie [!DNL Experience Platform] mag gebruiken, kan zij toegang toewijzen aan ontwikkelaars. De organisatie-id (`x-gw-ims-org-id`) vertegenwoordigt de organisatie waarvoor een API-aanroep moet worden uitgevoerd en is daarom vereist als een header in alle API-aanvragen. Deze identiteitskaart kan door [ Adobe Developer Console ](https://www.adobe.com/go/devs_console_ui) worden gevonden: in het **3} lusje van de Integraties {, navigeer aan de** sectie van het Overzicht **voor om het even welke bijzondere integratie om identiteitskaart onder** de Geloofsbrieven van de Cliënt **te vinden.** Voor een geleidelijke analyse van hoe te in [!DNL Platform] voor authentiek te verklaren, zie het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en).

## Waar kan ik mijn API-sleutel vinden? {#where-can-i-find-my-api-key}

Een API-sleutel is vereist als een header in alle API-aanvragen. Het kan door [ Adobe Developer Console ](https://www.adobe.com/go/devs_console_ui) worden gevonden. Binnen de console, op het **lusje van de Integraties**, navigeer aan de **sectie van het Overzicht** voor een specifieke integratie en u zult de sleutel onder **Credentials van de Cliënt** vinden. Voor een geleidelijke analyse van hoe te om aan [!DNL Platform] voor authentiek te verklaren, zie het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en).

## Hoe krijg ik een toegangstoken? {#how-do-i-get-an-access-token}

Toegangstempens zijn vereist in de machtigingheader van alle API-aanroepen. Ze kunnen worden gegenereerd met behulp van een CURL-opdracht, op voorwaarde dat u toegang hebt tot een integratie voor een organisatie. Toegangstokens zijn slechts geldig gedurende 24 uur, waarna een nieuw teken moet worden geproduceerd om verder te gebruiken API. Voor details bij het produceren van toegangstokens, zie het [ authentificatieleerprogramma ](https://www.adobe.com/go/platform-api-authentication-en).

## Hoe gebruik ik queryparameters? {#how-do-i-user-query-parameters}

Sommige API-eindpunten van [!DNL Platform] accepteren queryparameters om specifieke informatie te zoeken en de resultaten in de reactie te filteren. De parameters van de vraag worden toegevoegd aan verzoekwegen met een vraagteken (`?`) symbool, dat door één of meerdere vraagparameters wordt gevolgd gebruikend het formaat `paramName=paramValue`. Wanneer het combineren van veelvoudige parameters in één enkele vraag, moet u ampersand (`&`) gebruiken om individuele parameters te scheiden. Het volgende voorbeeld toont aan hoe een verzoek dat veelvoudige vraagparameters gebruikt in de documentatie wordt vertegenwoordigd.

Voorbeelden van veelgebruikte queryparameters zijn:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Voor gedetailleerde informatie over welke vraagparameters voor de specifieke dienst of een eindpunt beschikbaar zijn, te herzien gelieve de dienst-specifieke documentatie.

## Hoe kan ik een JSON-veld aangeven dat moet worden bijgewerkt in een PATCH-verzoek? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Vele verrichtingen van de PATCH in [!DNL Platform] APIs gebruiken [ JSON ](https://tools.ietf.org/html/rfc6901) koorden van de Aanwijzer om op eigenschappen te wijzen JSON om bij te werken. Deze zijn typisch inbegrepen in verzoeklading gebruikend [ JSON formaat van het Reparatie ](https://tools.ietf.org/html/rfc6902). Zie de [ API grondbeginselen gids ](api-fundamentals.md) voor gedetailleerde informatie over vereiste syntaxis voor deze technologieën.

## Kan ik Postman gebruiken om oproepen te doen naar [!DNL Platform] API&#39;s? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[ Postman ](https://www.postman.com/) is een nuttig hulpmiddel om vraag aan RESTful APIs te visualiseren. De [ Platform API die begonnen gids ](api-guide.md) wordt van start bevat een video en instructies voor het invoeren van de inzamelingen van Postman. Bovendien wordt een lijst van de inzamelingen van Postman voor elke dienst verstrekt.

## Wat zijn de systeemvereisten voor [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Afhankelijk van of u de UI of API gebruikt, zijn de volgende systeemvereisten van toepassing:

**voor op UI gebaseerde verrichtingen:**
- Een moderne, standaard webbrowser. Hoewel de nieuwste versie van [!DNL Chrome] wordt aanbevolen, worden huidige en vorige grote releases van [!DNL Firefox] , [!DNL Internet Explorer] en Safari ook ondersteund.
   - Elke keer dat een nieuwe hoofdversie wordt uitgebracht, ondersteunt [!DNL Platform] de meest recente versie terwijl de ondersteuning voor de derde meest recente versie wordt stopgezet.
- Alle browsers moeten cookies hebben en JavaScript ingeschakeld.

**voor API en ontwikkelaarinteractie:**
- Een ontwikkelomgeving voor REST-, streaming- en WebHaak-integratie.

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Hieronder volgt een lijst met fouten die kunnen optreden bij het gebruik van een [!DNL Experience Platform] -service. Voor het oplossen van problemengidsen op de individuele [!DNL Platform] diensten, zie de [ folder van het de dienstoplossen van problemen ](#service-troubleshooting-directory) hieronder.

## API-statuscodes {#api-status-codes}

De volgende statuscodes kunnen worden gevonden op elke [!DNL Experience Platform] -API. Elk artikel heeft verschillende oorzaken en daarom zijn de toelichtingen in deze paragraaf algemeen van aard. Voor meer details betreffende specifieke fouten in de individuele [!DNL Platform] diensten, te zien gelieve de [ folder van het de dienstoplossen van problemen ](#service-troubleshooting-directory) hieronder.

| Statuscode | Beschrijving | Mogelijke oorzaken |
|--- | --- | ---|
| 400 | Ongeldig verzoek | Het verzoek is onjuist samengesteld, bevat geen sleutelinformatie en/of bevat een onjuiste syntaxis. |
| 401 | Verificatie mislukt | De aanvraag heeft geen verificatiecontrole doorstaan. Uw toegangstoken ontbreekt of is ongeldig. Zie de [ symbolische fouten van het type OAuth ](#oauth-token-is-missing) hieronder voor meer details. |
| 403 | Verboden | De bron is gevonden, maar u hebt niet de juiste referenties om deze te bekijken. <br> Een waarschijnlijke oorzaak van deze fout is dat u niet de vereiste [ toegangsbeheertoestemmingen ](/help/access-control/home.md) zou kunnen hebben om tot het middel toegang te hebben of uit te geven. Lees hoe te [ krijgt de noodzakelijke op attribuut-gebaseerde toegangsbeheertoestemmingen ](/help/landing/api-authentication.md#get-abac-permissions) om Platform APIs te gebruiken. </p> |
| 404 | Niet gevonden | De gevraagde bron is niet gevonden op de server. De bron is mogelijk verwijderd of het gevraagde pad is onjuist ingevoerd. |
| 500 | Interne serverfout | Dit is een serverfout. Als u vele gelijktijdige vraag maakt, kunt u de API grens bereiken en moet uw resultaten filtreren. (Zie de [!DNL Catalog Service] sub-gids van de de ontwikkelaarsgids van API op [ het filtreren gegevens ](../catalog/api/filter-data.md) om meer te leren.) Wacht even voordat u uw verzoek opnieuw probeert en neem contact op met de beheerder als het probleem zich blijft voordoen. |

## Koptekstfouten aanvragen {#request-header-errors}

Voor alle API-aanroepen in [!DNL Platform] zijn specifieke aanvraagheaders vereist. Om te zien welke kopballen voor de individuele diensten worden vereist, gelieve te zien de [ documentatie van de Verwijzing API ](https://www.adobe.com/go/platform-api-reference-en). Om de waarden voor de vereiste authentificatiekopballen te vinden, zie het [ leerprogramma van de Authentificatie ](https://www.adobe.com/go/platform-api-authentication-en). Als een van deze headers ontbreekt of ongeldig is bij het aanroepen van een API, kunnen de volgende fouten optreden.

### OAuth-token ontbreekt {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Dit foutbericht wordt weergegeven wanneer een `Authorization` -header ontbreekt in een API-aanvraag. Zorg ervoor dat de machtigingheader is opgenomen met een geldig toegangstoken voordat u het opnieuw probeert.

### OAuth-token is niet geldig {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Dit foutbericht wordt weergegeven wanneer het toegangstoken in de header van `Authorization` niet geldig is. Zorg ervoor dat het teken correct is ingegaan, of [ produceert een nieuw teken ](https://www.adobe.com/go/platform-api-authentication-en) in de Console van Adobe I/O.

### API-sleutel is vereist {#api-key-is-required}

```json
{
    "error_code": "403000",
    "message": "Api Key is required"
}
```

Dit foutbericht wordt weergegeven wanneer een API-sleutelheader (`x-api-key`) ontbreekt in een API-aanvraag. Zorg ervoor dat de header is opgenomen met een geldige API-sleutel voordat u het opnieuw probeert.

### API-sleutel is ongeldig {#api-key-is-invalid}

```json
{
    "error_code": "403003",
    "message": "Api Key is invalid"
}
```

Dit foutbericht wordt weergegeven wanneer de waarde van de opgegeven API-sleutelheader (`x-api-key`) ongeldig is. Controleer of u de sleutel correct hebt ingevoerd voordat u het opnieuw probeert. Als u uw API sleutel niet kent, kunt u het in de [ Console van de Adobe I/O ](https://console.adobe.io) vinden: in het **3} lusje van de Integraties {, navigeer aan de** sectie van het Overzicht **voor een specifieke integratie om de API sleutel onder** Credentials van de Cliënt te vinden **.**

### Ontbrekende koptekst {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Dit foutbericht wordt weergegeven wanneer een organisatiekoptekst (`x-gw-ims-org-id`) ontbreekt in een API-aanvraag. Zorg ervoor dat de koptekst is opgenomen in de id van uw organisatie voordat u het opnieuw probeert.

### Profiel is niet geldig {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Dit foutenbericht toont wanneer de gebruiker of de integratie van de Adobe I/O (die door het [ toegangstoken ](#how-do-i-get-an-access-token) in de `Authorization` kopbal wordt geïdentificeerd) niet gerechtigd is om vraag aan [!DNL Experience Platform] APIs voor de organisatie te maken die in de `x-gw-ims-org-id` kopbal wordt verstrekt. Zorg ervoor dat u de juiste id voor uw organisatie hebt opgegeven in de koptekst voordat u het opnieuw probeert. Als u uw organisatieidentiteitskaart niet kent, kunt u het in de [ Console van de Adobe I/O ](https://console.adobe.io) vinden: in het **3} lusje van Integraties {, navigeer aan de** sectie van het Overzicht **voor een specifieke integratie om identiteitskaart onder** de Referenties van de Cliënt **te vinden.**

### Fout bij vernieuwen van tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

U kunt een etiketfout ontvangen als een verandering op om het even welke bron of bestemmingsentiteit zoals stroom, verbinding, bronschakelaar, of doelverbinding door een andere API bezoeker werd aangebracht. Vanwege de niet-overeenkomende versie wordt de wijziging die u wilt aanbrengen, niet toegepast op de laatste versie van de entiteit.

Om dit op te lossen, moet u de entiteit opnieuw halen, ervoor zorgen dat uw veranderingen met nieuwe versie van de entiteit compatibel zijn, dan plaats het nieuwe etiket in de `If-Match` kopbal, en maak tot slot de API vraag.

### Geldig inhoudstype niet opgegeven {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Dit foutbericht wordt weergegeven wanneer een POST-, PUT- of PATCH-aanvraag een ongeldige of ontbrekende `Content-Type` header heeft. Zorg ervoor dat de koptekst in de aanvraag is opgenomen en dat de waarde ervan `application/json` is.

### Gebruikersgebied ontbreekt {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Dit foutbericht wordt weergegeven in een van de twee onderstaande gevallen:
- Wanneer een onjuiste of misvormde kopbal van organisatieID (`x-gw-ims-org-id`) in een API verzoek wordt overgegaan. Zorg ervoor dat de juiste id van uw organisatie is opgenomen voordat u het opnieuw probeert.
- Wanneer uw account (weergegeven door de opgegeven verificatiereferenties) niet is gekoppeld aan een productprofiel voor Experience Platform. Volg de stappen op [ het produceren van toegangsgeloofsbrieven ](./api-authentication.md#authentication-for-each-session) in het de authentificatieleerprogramma van het Platform API om Platform aan uw rekening toe te voegen en uw authentificatiegeloofsbrieven dienovereenkomstig bij te werken.

## Servicemap voor problemen {#service-troubleshooting-directory}

Hieronder volgt een lijst met probleemoplossingsgidsen en API-naslagdocumentatie voor [!DNL Experience Platform] API&#39;s. Elke gids voor probleemoplossing biedt antwoorden op veelgestelde vragen en oplossingen voor problemen die specifiek zijn voor afzonderlijke [!DNL Platform] -services. De API verwijzingsdocumenten verstrekken een uitvoerige gids aan alle beschikbare eindpunten voor elke dienst, en tonen de instanties van de steekproefaanvraag, reacties, en foutencodes die u kunt ontvangen.

| Service | API-naslag | Problemen oplossen |
| --- | --- | --- |
| Toegangsbeheer | [ controle API van de Toegang ](https://www.adobe.io/experience-platform-apis/references/access-control/) | [ de gids van het de controleoplossen van problemenoplossing van de Toegang ](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform-gegevensinscriptie | [[!DNL Batch Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/batch-ingestion/) | [ het oplossen van problemengids van de Inname van de Partij ](../ingestion/batch-ingestion/troubleshooting.md) |
| Adobe Experience Platform-gegevensinscriptie | [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/) | [ Streaming het oplossen van problemengids van de Inname ](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace]  het oplossen van problemengids ](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform Data Governance | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service]  het oplossen van problemengids ](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service]  het oplossen van problemengids ](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform-segmentatie | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System]  Veelgestelde vragen en het oplossen van problemengids ](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] en [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-Time Customer Profile] | [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile]  het oplossen van problemengids ](../profile/troubleshooting.md) |
| Sandboxes | [ Sandbox API ](https://www.adobe.io/experience-platform-apis/references/sandbox) | [ het oplossen van problemengids van Sandboxes ](../sandboxes/troubleshooting-guide.md) |
