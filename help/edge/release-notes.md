---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: De recentste versienota's voor het Web SDK van Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: e158b8129fe5afe71af48b7c64ca34b00e79965c
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# Aanvullende informatie

## Versie 2.6.0 - 27 juli 2021

* Verstrekt meer verpersoonlijkingsinhoud in de `sendEvent` opgeloste belofte, met inbegrip van de reactietekenen van Adobe Target. Wanneer de opdracht `sendEvent` wordt uitgevoerd, wordt een belofte geretourneerd die uiteindelijk wordt omgezet met een `result`-object dat informatie bevat die van de server is ontvangen. Dit resultaatobject bevat een eigenschap met de naam `decisions`. Deze eigenschap `decisions` is vervangen. Er is een nieuwe eigenschap toegevoegd, `propositions`. Deze nieuwe eigenschap biedt klanten toegang tot meer personalisatie-inhoud, inclusief reactietokens. Meer documentatie is binnenkort beschikbaar.

## Versie 2.5.0 - juni 2021

* Toegevoegde ondersteuning voor aanpassingsmogelijkheden.
* Automatisch verzamelde viewport breedten en hoogten die negatieve waarden zijn zullen niet meer naar de server worden verzonden.
* Wanneer een gebeurtenis wordt geannuleerd door `false` van een `onBeforeEventSend` callback terug te keren, wordt een bericht nu geregistreerd.
* Probleem verholpen waarbij specifieke onderdelen van XDM-gegevens die bestemd waren voor één gebeurtenis, waren opgenomen in meerdere gebeurtenissen.

## Versie 2.4.0 - maart 2021

* De SDK kan nu [worden geïnstalleerd als een npm-pakket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Toegevoegde steun voor een `out` optie wanneer [vormend standaardtoestemming](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), die alle gebeurtenissen laat vallen tot de toestemming wordt ontvangen (de bestaande `pending` optie vormt gebeurtenissen in de rij en verzendt hen zodra de toestemming wordt ontvangen).
* De [onBeforeEventSend callback](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kan nu worden gebruikt om te voorkomen dat een gebeurtenis wordt verzonden.
* Gebruikt nu een XDM-schemagebiedgroep in plaats van `meta.personalization` wanneer het verzenden van gebeurtenissen over gepersonaliseerde inhoud die wordt teruggegeven of geklikt.
* De [getIdentity opdracht](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) retourneert nu de id van het randgebied naast de identiteit.
* Waarschuwingen en fouten die van de server zijn ontvangen, zijn verbeterd en worden op een geschiktere manier afgehandeld.
* Toegevoegde steun [Adobe verzonden 2.0 norm](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* De voorkeur van de toestemming, wanneer ontvangen, wordt gehakt en in lokale opslag voor een geoptimaliseerde integratie onder CMPs, het Web SDK van het Platform, en het Netwerk van de Rand van het Platform opgeslagen. Als u toestemmingsvoorkeur verzamelt, moedigen wij u nu aan om `setConsent` op elke paginading te roepen.
* Er zijn twee [controlehaken](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` en `onCommandRejected` toegevoegd.
* Opgeloste problemen: Gebeurtenissen voor persoonlijke interactiemeldingen bevatten dubbele informatie over dezelfde activiteit wanneer een gebruiker naar een nieuwe app-weergave van één pagina navigeert, teruggaat naar de oorspronkelijke weergave en op een element klikt dat in aanmerking komt voor conversie.
* Opgeloste problemen: Als de eerste gebeurtenis die door de SDK wordt verzonden `documentUnloading` op `true` was ingesteld, zou [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) worden gebruikt om de gebeurtenis te verzenden, resulterend in een fout betreffende een identiteit die niet wordt gevestigd.

## Versie 2.3.0 - november 2020

* Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
* Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
* Verbeterde compatibiliteit met andere JavaScript-code op de pagina die wellicht API&#39;s van `window.console` overschrijft.
* Opgeloste problemen: `sendBeacon` werd niet gebruikt wanneer `documentUnloading` aan `true` werd geplaatst of wanneer de verbinding kliks automatisch werd gevolgd.
* Opgeloste problemen: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
* Opgeloste problemen: Bepaalde browserfouten met een alleen-lezen `message`-eigenschap zijn niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
* Opgeloste problemen: Als de SDK in een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe afkomstig is uit een ander subdomein dan de HTML-pagina van het bovenliggende venster.

## Versie 2.2.0 - oktober 2020

* Opgeloste problemen: Het Opt-in voorwerp blokkeerde Alloy om vraag te maken wanneer `idMigrationEnabled` `true` is.
* Opgeloste problemen: Alloy bewust maken van verzoeken die de aanbiedingen van de verpersoonlijking zouden moeten terugkeren om een flikkerende kwestie te verhinderen.

## Versie 2.1.0 - augustus 2020

* Verwijder het `syncIdentity` bevel en steun die die IDs in het `sendEvent` bevel overgaan.
* Ondersteuning voor IAB 2.0 Consent Standard.
* Ondersteuning voor het doorgeven van aanvullende id&#39;s in de opdracht `setConsent`.
* Ondersteuning voor het overschrijven van `datasetId` in de opdracht `sendEvent`.
* Ondersteuningslantmonitoren ([Meer informatie](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Geef `environment: browser` door in de contextgegevens van de implementatiedetails.
