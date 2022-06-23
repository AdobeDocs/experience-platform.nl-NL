---
keywords: Experience Platform;home;populaire onderwerpen;API-foutcodes;API-foutcode;API voor foutcode;API voor foutcodes;API-aanvraagfout;API-probleemoplossing;API-fout
solution: Experience Platform
title: Adobe Experience Platform - Veelgestelde vragen en handleiding voor probleemoplossing
description: Vind antwoorden op vaak gestelde vragen en een gids voor het oplossen van problemen gemeenschappelijke fouten in Experience Platform.
landing-page-description: Vind antwoorden op vaak gestelde vragen en een gids voor het oplossen van problemen gemeenschappelijke fouten in Experience Platform.
topic-legacy: getting started
type: Documentation
exl-id: 3e6d29aa-2138-421b-8bee-82b632962c01
source-git-commit: da3e93f6c10c89c173fff786604ef844f56081be
workflow-type: tm+mt
source-wordcount: '1851'
ht-degree: 1%

---

# [!DNL Platform] Veelgestelde vragen en handleiding voor probleemoplossing

Dit document bevat antwoorden op veelgestelde vragen over Adobe Experience Platform en een gids voor probleemoplossing op hoog niveau voor algemene fouten die in een [!DNL Experience Platform] API. Voor het oplossen van problemengidsen op individueel [!DNL Platform] de diensten, zie [servicemap voor probleemoplossing](#service-troubleshooting-directory) hieronder.

## Veelgestelde vragen {#faq}

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over Adobe Experience Platform.

## Wat is [!DNL Experience Platform] API&#39;s? {#what-are-experience-platform-apis}

[!DNL Experience Platform] biedt veelvoudige RESTful APIs aan die HTTP- verzoeken aan toegang gebruiken [!DNL Platform] middelen. Deze dienst APIs elk stelt veelvoudige eindpunten bloot, en staat u toe om verrichtingen aan lijst (GET), raadpleging (GET) uit te voeren, (PUT en/of PATCH), en (DELETE) middelen uit te geven. Voor meer informatie over specifieke eindpunten en verrichtingen beschikbaar voor elke dienst, gelieve te zien [API-naslagdocumentatie](https://www.adobe.com/go/platform-api-reference-en) op Adobe I/O.

## Hoe kan ik een API-aanvraag opmaken? {#how-do-i-format-an-api-request}

De aanvraagindelingen variëren afhankelijk van [!DNL Platform] API die wordt gebruikt. De beste manier om te leren hoe te om uw API vraag te structureren is door samen met de voorbeelden te volgen die in de documentatie voor specifiek worden verstrekt [!DNL Platform] service die u gebruikt.

Voor meer informatie over het opmaken van API-aanvragen raadpleegt u de gids Platform API aan de slag [voorbeeld-API-aanroepen lezen](./api-guide.md#sample-api) sectie.

## Wat is mijn IMS-organisatie? {#what-is-my-ims-organization}

Een IMS-organisatie is een Adobe-representatie van een klant. Om het even welke vergunning gegeven Adobe oplossingen zijn geïntegreerd met deze klantenorganisatie. Wanneer een IMS-organisatie [!DNL Experience Platform], kan het toegang toewijzen aan ontwikkelaars. De IMS-organisatie-id (`x-gw-ims-org-id`) staat voor de organisatie waarvoor een API-aanroep moet worden uitgevoerd en is daarom vereist als header in alle API-aanvragen. Deze id is te vinden via de [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui): in de **Integraties** tabblad, navigeert u naar de **Overzicht** sectie voor een bepaalde integratie om de id onder te zoeken **Client Credentials**. Voor een geleidelijke analyse van hoe te voor authentiek te verklaren in [!DNL Platform], zie de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en).

## Waar kan ik mijn API-sleutel vinden? {#where-can-i-find-my-api-key}

Een API-sleutel is vereist als een header in alle API-aanvragen. Het kan via [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Binnen de console, op de **Integraties** tabblad, navigeert u naar de **Overzicht** voor een specifieke integratie, vindt u de sleutel onder **Client Credentials**. Voor een geleidelijke analyse van hoe te voor authentiek te verklaren om [!DNL Platform], zie de [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en).

## Hoe krijg ik een toegangstoken? {#how-do-i-get-an-access-token}

Toegangstempens zijn vereist in de machtigingheader van alle API-aanroepen. Ze kunnen worden gegenereerd met behulp van een `curl` gebruiken, op voorwaarde dat u toegang hebt tot een integratie voor een IMS-organisatie. Toegangstokens zijn slechts geldig gedurende 24 uur, waarna een nieuw teken moet worden geproduceerd om verder te gebruiken API. Voor details bij het produceren van toegangstokens, zie [verificatiezelfstudie](https://www.adobe.com/go/platform-api-authentication-en).

## Hoe gebruik ik queryparameters? {#how-do-i-user-query-parameters}

Sommige [!DNL Platform] API-eindpunten accepteren queryparameters om specifieke informatie te zoeken en de resultaten in de reactie te filteren. De parameters van de vraag worden toegevoegd aan verzoekwegen met een vraagteken (`?`), gevolgd door een of meer queryparameters met de indeling `paramName=paramValue`. Wanneer het combineren van veelvoudige parameters in één enkele vraag, moet u ampersand (`&`) om afzonderlijke parameters te scheiden. Het volgende voorbeeld toont aan hoe een verzoek dat veelvoudige vraagparameters gebruikt in de documentatie wordt vertegenwoordigd.

Voorbeelden van veelgebruikte queryparameters zijn:

```http
GET /tenant/schemas?orderby=title
GET /datasets?limit=36&start=10
GET /batches?createdAfter=1559775880000&orderBy=desc:created
```

Voor gedetailleerde informatie over welke vraagparameters voor de specifieke dienst of een eindpunt beschikbaar zijn, te herzien gelieve de dienst-specifieke documentatie.

## Hoe kan ik een JSON-veld aangeven dat moet worden bijgewerkt in een PATCH-verzoek? {#how-do-i-indicate-a-json-field-to-update-in-a-patch-request}

Veel PATCH-bewerkingen in [!DNL Platform] APIs-gebruik [JSON-aanwijzer](https://tools.ietf.org/html/rfc6901) tekenreeksen die JSON-eigenschappen aangeven die moeten worden bijgewerkt. Deze worden meestal opgenomen in aanvraagladingen die [JSON Patch](https://tools.ietf.org/html/rfc6902) gebruiken. Zie de [Handleiding voor API-basisbeginselen](api-fundamentals.md) voor gedetailleerde informatie over de vereiste syntaxis voor deze technologieën.

## Mag ik Postman gebruiken om vraag te maken aan [!DNL Platform] API&#39;s? {#how-do-i-use-postman-to-make-calls-to-platform-apis}

[Postman](https://www.postman.com/) is een nuttig hulpmiddel om vraag aan RESTful APIs te visualiseren. De [Aan de slag-handleiding voor Platform-API](api-guide.md) bevat een video en instructies voor het importeren van Postman-verzamelingen. Bovendien wordt een lijst van de inzamelingen van Postman voor elke dienst verstrekt.

## Wat zijn de systeemvereisten voor [!DNL Platform]? {#what-are-the-system-requirements-for-platform}

Afhankelijk van of u de UI of API gebruikt, zijn de volgende systeemvereisten van toepassing:

**Voor bewerkingen op basis van UI:**
- Een moderne, standaard webbrowser. De nieuwste versie van [!DNL Chrome] wordt aanbevolen, huidige en vorige grote introducties van [!DNL Firefox], [!DNL Internet Explorer]en Safari worden ook ondersteund.
   - Elke keer dat een nieuwe hoofdversie wordt uitgebracht, [!DNL Platform] start met ondersteuning van de meest recente versie terwijl de ondersteuning voor de derde meest recente versie wordt stopgezet.
- Voor alle browsers moeten cookies en JavaScript zijn ingeschakeld.

**Voor API- en ontwikkelaarsinteracties:**
- Een ontwikkelomgeving voor REST-, streaming- en WebHaak-integratie.

## Fouten en problemen oplossen {#errors-and-troubleshooting}

Hieronder volgt een lijst met fouten die u kunt tegenkomen bij het gebruik van [!DNL Experience Platform] service. Voor het oplossen van problemengidsen op individueel [!DNL Platform] de diensten, zie [servicemap voor probleemoplossing](#service-troubleshooting-directory) hieronder.

## API-statuscodes {#api-status-codes}

De volgende statuscodes kunnen worden gevonden op elk [!DNL Experience Platform] API. Elk artikel heeft verschillende oorzaken en daarom zijn de toelichtingen in deze paragraaf algemeen van aard. Voor meer informatie over specifieke fouten in afzonderlijke [!DNL Platform] de diensten, gelieve te zien [servicemap voor probleemoplossing](#service-troubleshooting-directory) hieronder.

| Statuscode | Beschrijving | Mogelijke oorzaken |
|--- | --- | ---|
| 400 | Ongeldig verzoek | Het verzoek is onjuist samengesteld, bevat geen sleutelinformatie en/of bevat een onjuiste syntaxis. |
| 401 | Verificatie mislukt | De aanvraag heeft geen verificatiecontrole doorstaan. Uw toegangstoken ontbreekt of is ongeldig. Zie de [OAuth-tokenfouten](#oauth-token-is-missing) voor meer informatie hieronder. |
| 403 | Verboden | De bron is gevonden, maar u hebt niet de juiste referenties om deze te bekijken. |
| 404 | Niet gevonden | De gevraagde bron is niet gevonden op de server. De bron is mogelijk verwijderd of het gevraagde pad is onjuist ingevoerd. |
| 500 | Interne serverfout | Dit is een serverfout. Als u vele gelijktijdige vraag maakt, kunt u de API grens bereiken en moet uw resultaten filtreren. (Zie de [!DNL Catalog Service] Subhandleiding voor API-ontwikkelaars ingeschakeld [filteren, gegevens](../catalog/api/filter-data.md) voor meer informatie.) Wacht even voordat u uw verzoek opnieuw probeert en neem contact op met de beheerder als het probleem zich blijft voordoen. |

## Koptekstfouten aanvragen {#request-header-errors}

Alle API-aanroepen in [!DNL Platform] specifieke aanvraagheaders vereisen. Om te zien welke kopballen voor de individuele diensten worden vereist, gelieve te zien [API-naslagdocumentatie](https://www.adobe.com/go/platform-api-reference-en). Als u de waarden voor de vereiste verificatieheaders wilt vinden, raadpleegt u de [Zelfstudie verificatie](https://www.adobe.com/go/platform-api-authentication-en). Als een van deze headers ontbreekt of ongeldig is bij het aanroepen van een API, kunnen de volgende fouten optreden.

### OAuth-token ontbreekt {#oauth-token-is-missing}

```json
{
    "error_code": "403010",
    "message": "Oauth token is missing."
}
```

Dit foutbericht wordt weergegeven wanneer een `Authorization` header ontbreekt in een API-aanvraag. Zorg ervoor dat de machtigingheader is opgenomen met een geldig toegangstoken voordat u het opnieuw probeert.

### OAuth-token is niet geldig {#oauth-token-is-not-valid}

```json
{
    "error_code": "401013",
    "message": "Oauth token is not valid"
}
```

Dit foutbericht wordt weergegeven wanneer het toegangstoken in het dialoogvenster `Authorization` header is not valid. Controleer of het token correct is ingevoerd, of [een nieuw token genereren](https://www.adobe.com/go/platform-api-authentication-en) in de Adobe I/O Console.

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

Dit foutbericht wordt weergegeven wanneer de waarde van de opgegeven API-sleutelheader (`x-api-key`) is ongeldig. Controleer of u de sleutel correct hebt ingevoerd voordat u het opnieuw probeert. Als u de API-sleutel niet kent, kunt u deze vinden in het dialoogvenster [Adobe I/O-console](https://console.adobe.io): in de **Integraties** tabblad, navigeert u naar de **Overzicht** sectie voor een specifieke integratie om de API-sleutel onder te zoeken **Client Credentials**.

### Ontbrekende koptekst {#missing-header}

```json
{
    "error_code": "400003",
    "message": "Missing header"
}
```

Dit foutbericht wordt weergegeven als een IMS org-header (`x-gw-ims-org-id`) ontbreekt in een API-aanvraag. Zorg ervoor dat de koptekst is opgenomen in de id van uw IMS-organisatie voordat u het opnieuw probeert.

### Profiel is niet geldig {#profile-is-not-valid}

```json
{
    "error_code": "403025",
    "message": "Profile is not valid"
}
```

Dit foutbericht wordt weergegeven wanneer de gebruiker of de Adobe I/O-integratie (geïdentificeerd door de [toegangstoken](#how-do-i-get-an-access-token) in de `Authorization` header) heeft geen recht om te bellen naar [!DNL Experience Platform] API&#39;s voor de IMS Org die worden geleverd in het dialoogvenster `x-gw-ims-org-id` header. Controleer of u de juiste id voor uw IMS-organisatie in de koptekst hebt opgegeven voordat u het opnieuw probeert. Als u uw organisatie-id niet kent, kunt u deze vinden in de [Adobe I/O-console](https://console.adobe.io): in de **Integraties** tabblad, navigeert u naar de **Overzicht** sectie voor een specifieke integratie om de id onder te zoeken **Client Credentials**.

### Fout bij vernieuwen van tag {#refresh-etag-error}

```json
{
"errorMessage":"Supplied version=[\\\\\\\"a200a2a3-0000-0200-0000-123178f90000\\\\\\\"] does not match the current version on entity=[\\\\\\\"a200cdb2-0000-0200-0000-456179940000\\\\\\\"]"
}
```

U kunt een etiketfout ontvangen als een verandering op om het even welke bron of bestemmingsentiteit zoals stroom, verbinding, bronschakelaar, of doelverbinding door een andere API bezoeker werd aangebracht. Vanwege de niet-overeenkomende versie wordt de wijziging die u wilt aanbrengen, niet toegepast op de laatste versie van de entiteit.

Als u dit wilt verhelpen, moet u de entiteit opnieuw ophalen, ervoor zorgen dat de wijzigingen compatibel zijn met de nieuwe versie van de entiteit en vervolgens de nieuwe tag in het dialoogvenster `If-Match` en tot slot de API-aanroep.

### Geldig inhoudstype niet opgegeven {#valid-content-type-not-specified}

```json
{
    "type": "/placeholder/type/uri",
    "status": 400,
    "title": "BadRequestError",
    "detail": "A valid content-type must be specified"
}
```

Dit foutbericht wordt weergegeven wanneer een POST-, PUT- of PATCH-aanvraag ongeldig is of ontbreekt `Content-Type` header. Zorg ervoor dat de koptekst is opgenomen in de aanvraag en dat de waarde ervan `application/json`.

### Gebruikersgebied ontbreekt {#user-region-is-missing}

```json
{
    "error_code": "403027",
    "message": "User region is missing"
}
```

Dit foutbericht wordt weergegeven in een van de twee onderstaande gevallen:
- Wanneer een onjuiste of onjuist gevormde IMS Org-header (`x-gw-ims-org-id`) wordt doorgegeven in een API-aanvraag. Zorg ervoor dat de juiste id van uw IMS-organisatie is opgenomen voordat u het opnieuw probeert.
- Wanneer uw account (weergegeven door de opgegeven verificatiereferenties) niet is gekoppeld aan een productprofiel voor Experience Platform. Voer de volgende stappen uit [toegangsreferenties genereren](./api-authentication.md#authentication-for-each-session) in de Platform API-verificatiezelfstudie om Platform toe te voegen aan uw account en uw verificatiegegevens dienovereenkomstig bij te werken.

## Servicemap voor probleemoplossing {#service-troubleshooting-directory}

Hieronder volgt een lijst met probleemoplossingsgidsen en API-naslagdocumentatie voor [!DNL Experience Platform] API&#39;s. Elke het oplossen van problemengids verstrekt antwoorden op vaak gestelde vragen en oplossingen aan problemen die specifiek zijn voor individueel [!DNL Platform] diensten. De API verwijzingsdocumenten verstrekken een uitvoerige gids aan alle beschikbare eindpunten voor elke dienst, en tonen de instanties van de steekproefaanvraag, reacties, en foutencodes die u kunt ontvangen.

| Service | API-referentie | Problemen oplossen |
| --- | --- | --- |
| Toegangsbeheer | [API voor toegangsbeheer](https://www.adobe.io/experience-platform-apis/references/access-control/) | [Handleiding voor probleemoplossing bij toegangsbeheer](../access-control/troubleshooting-guide.md) |
| Adobe Experience Platform-gegevensinscriptie | [[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/) | [Handleiding voor het oplossen van problemen met inslikken](../ingestion/batch-ingestion/troubleshooting.md)<br><br>[Handleiding voor het oplossen van problemen bij het streamen](../ingestion/streaming-ingestion/troubleshooting.md) |
| Adobe Experience Platform Data Science Workspace | [[!DNL Sensei Machine Learning API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/sensei-ml-api.yaml) | [[!DNL Data Science Workspace] gids voor problemen](../data-science-workspace/troubleshooting-guide.md) |
| Adobe Experience Platform Data Governance | [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) |  |
| Adobe Experience Platform Identity Service | [[!DNL Identity Service API]](https://www.adobe.io/experience-platform-apis/references/identity-service) | [[!DNL Identity Service] gids voor problemen](../identity-service/troubleshooting-guide.md) |
| Adobe Experience Platform Query Service | [[!DNL Query Service API]](https://www.adobe.io/experience-platform-apis/references/query-service/) | [[!DNL Query Service] gids voor problemen](../query-service/troubleshooting-guide.md) |
| Adobe Experience Platform-segmentatie | [[!DNL Segmentation API]](https://www.adobe.io/experience-platform-apis/references/segmentation/) |
| [!DNL Catalog Service] | [[!DNL Catalog Service API]](https://www.adobe.io/experience-platform-apis/references/catalog/) |  |
| [!DNL Experience Data Model] (XDM) | [[!DNL Schema Registry API]](https://www.adobe.io/experience-platform-apis/references/schema-registry/) | [[!DNL XDM System] Veelgestelde vragen en handleiding voor probleemoplossing](../xdm/troubleshooting-guide.md) |
| [!DNL Flow Service] ([!DNL Sources] en [!DNL Destinations]) | [[!DNL Flow Service API]](https://www.adobe.io/experience-platform-apis/references/flow-service/) |  |
| [!DNL Real-time Customer Profile] | [[!DNL Real-time Customer Profile API]](https://www.adobe.com/go/profile-apis-en) | [[!DNL Profile] gids voor problemen](../profile/troubleshooting.md) |
| Sandboxen | [Sandbox-API](https://www.adobe.io/experience-platform-apis/references/sandbox) | [Richtlijnen voor het oplossen van problemen met sandboxen](../sandboxes/troubleshooting-guide.md) |
