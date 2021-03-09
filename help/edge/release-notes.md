---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: De recentste versienota's voor het Web SDK van Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;versie nota's;
translation-type: tm+mt
source-git-commit: b0e6d1f7cf7302bb3a7403bb18dfd8b7489d583e
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---


# Releaseopmerkingen

## Versie 2.4.0

* De SDK kan nu [worden geïnstalleerd als een npm-pakket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Toegevoegde steun voor een `out` optie wanneer [vormend standaardtoestemming](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), die alle gebeurtenissen laat vallen tot de toestemming wordt ontvangen (de bestaande `pending` optie vormt gebeurtenissen in de rij en verzendt hen zodra de toestemming wordt ontvangen).
* De [onBeforeEventSend callback](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kan nu worden gebruikt om te voorkomen dat een gebeurtenis wordt verzonden.
* Er wordt nu een XDM-mix gebruikt in plaats van `meta.personalization` bij het verzenden van gebeurtenissen over gepersonaliseerde inhoud die wordt gerenderd of waarop wordt geklikt.
* De [getIdentity opdracht](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) retourneert nu de id van het randgebied naast de identiteit.
* Waarschuwingen en fouten die van de server zijn ontvangen, zijn verbeterd en worden op een geschiktere manier afgehandeld.
* Toegevoegde steun [Adobe verzonden 2.0 norm](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* De voorkeur van de toestemming, wanneer ontvangen, wordt gehakt en in lokale opslag voor een geoptimaliseerde integratie onder CMPs, het Web SDK van het Platform, en het Netwerk van de Rand van het Platform opgeslagen. Als u toestemmingsvoorkeur verzamelt, moedigen wij u nu aan om `setConsent` op elke paginading te roepen.
* Er zijn twee [controlehaken](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` en `onCommandRejected` toegevoegd.
* Opgeloste problemen: Gebeurtenissen voor persoonlijke interactiemeldingen bevatten dubbele informatie over dezelfde activiteit wanneer een gebruiker naar een nieuwe app-weergave van één pagina navigeert, teruggaat naar de oorspronkelijke weergave en op een element klikt dat in aanmerking komt voor conversie.
* Opgeloste problemen: Als de eerste gebeurtenis die door de SDK wordt verzonden `documentUnloading` op `true` was ingesteld, zou [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) worden gebruikt om de gebeurtenis te verzenden, resulterend in een fout betreffende een identiteit die niet wordt gevestigd.

## Versie 2.3.0

* Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
* Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
* Verbeterde compatibiliteit met andere JavaScript-code op de pagina die wellicht API&#39;s van `window.console` overschrijft.
* Opgeloste problemen: `sendBeacon` werd niet gebruikt wanneer `documentUnloading` aan `true` werd geplaatst of wanneer de verbinding kliks automatisch werd gevolgd.
* Opgeloste problemen: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
* Opgeloste problemen: Bepaalde browserfouten met een alleen-lezen `message`-eigenschap zijn niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
* Opgeloste problemen: Als de SDK in een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe afkomstig is uit een ander subdomein dan de HTML-pagina van het bovenliggende venster.

## Versie 2.2.0

* Opgeloste problemen: Het Opt-in voorwerp blokkeerde Alloy om vraag te maken wanneer `idMigrationEnabled` `true` is.
* Opgeloste problemen: Alloy bewust maken van verzoeken die de aanbiedingen van de verpersoonlijking zouden moeten terugkeren om een flikkerende kwestie te verhinderen.

## Versie 2.1.0

* Verwijder het `syncIdentity` bevel en steun die die IDs in het `sendEvent` bevel overgaan.
* Ondersteuning voor IAB 2.0 Consent Standard.
* Ondersteuning voor het doorgeven van aanvullende id&#39;s in de opdracht `setConsent`.
* Ondersteuning voor het overschrijven van `datasetId` in de opdracht `sendEvent`.
* Ondersteuningslantmonitoren ([Meer informatie](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Geef `environment: browser` door in de contextgegevens van de implementatiedetails.
