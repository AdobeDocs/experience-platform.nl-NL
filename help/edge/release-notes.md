---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: De recentste versienota's voor het Web SDK van Adobe Experience Platform.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 207fdd6d8a8dc27fa89798999734ba820f30fd54
workflow-type: tm+mt
source-wordcount: '1169'
ht-degree: 0%

---


# Aanvullende informatie

In dit document worden de releaseopmerkingen voor de Adobe Experience Platform Web SDK besproken.
Voor de recentste versienota&#39;s op de de markeringsuitbreiding van SDK van het Web, zie [Opmerkingen bij de release Web SDK-tag](extension/web-sdk-ext-release-notes.md).

## Versie 2.11.0 - 13 juni 2022

**Nieuwe functies**

* U kunt nu nauwkeuriger persoonlijke ervaringen bieden door gebruikers-id&#39;s te delen tussen mobiele apps en mobiele webinhoud, en tussen domeinen. Zie de [speciale documentatie](identity/id-sharing.md) voor meer informatie.
* U kunt nu een array met voorstellingen renderen of uitvoeren vanuit [!DNL Adobe Target] in toepassingen van één pagina, zonder de analytische meetgegevens te verhogen. Dit vermindert rapportagefouten en vergroot de nauwkeurigheid van de analyse. Zie de [speciale documentatie](personalization/rendering-personalization-content.md#applypropositions) voor meer informatie.
* Aanvullende informatie toegevoegd aan de `getLibraryInfo` bevel met inbegrip van beschikbare bevelen en de definitieve configuratie voor de instantie.

**Oplossingen en verbeteringen**

* Bijgewerkte cookie-instellingen die moeten worden gebruikt `sameSite="none"` en `secure` markering op [!DNL HTTPS] pagina&#39;s.
* Correctie van een probleem waarbij gepersonaliseerde inhoud niet correct werd toegepast tijdens het gebruik van het dialoogvenster `eq` pseudo-kiezer.
* Probleem verholpen waarbij `localTimezoneOffset` kan de validatie van het Experience Platform niet voltooien.

## Versie 2.10.1 - 3 mei 2022

* Probleem verholpen waarbij meerdere permanente iframes werden gemaakt voor id-syncs en segmentdoelen.

## Versie 2.10.0 - 22 april 2022

* Gebruik een blijvend iframe voor alle ID syncs en segmentbestemmingen.
* Oplossing voor een probleem waarbij samengevoegde metrische profielen werden gedupliceerd in het dialoogvenster `sendEvent` resultaat.

## Versie 2.9.0 - 10 maart 2022

* Toegevoegde ondersteuning voor tekstspatiëring [!DNL control (default)] Adobe Target ervaart.
* De gebeurtenis view-change is geoptimaliseerd voor toepassingen op één pagina. Het weergavebericht wordt nu opgenomen in de gebeurtenis view-change wanneer persoonlijke ervaringen worden weergegeven.
* Waarschuwing van console is verwijderd als dit niet het geval is `eventType` aanwezig is.
* Het probleem waarbij de `propositions` eigenschap is alleen geretourneerd door een `sendEvent` gebruiken wanneer ervaringen zijn opgevraagd of opgehaald uit de cache. De `propositions` eigenschap wordt nu altijd gedefinieerd als een array.
* Probleem verholpen waarbij verborgen containers niet werden weergegeven als er een fout was geretourneerd van Adobe Experience Edge.
* Probleem verholpen waarbij de interactieve gebeurtenissen niet in Adobe Target werden meegeteld. Dit probleem is opgelost door de weergavenaam toe te voegen aan de XDM op web.webPageDetails.viewName.
* Los gebroken documentatiekoppelingen in consoleberichten op.

## Versie 2.8.0 - 19 januari 2022

* Ondersteuning voor schaduw-DOM-kiezers voor personalisatie.
* Naam gewijzigd in gebeurtenistypen voor personalisatie. (`display` en `click` worden `decisioning.propositionDisplay` en `decisioning.propositionInteract`)
* Probleem verholpen waarbij HTML-aanbiedingen met inlinescripttags de scripttags twee keer aan de pagina hebben toegevoegd, ook al werd het script slechts één keer uitgevoerd.

## Versie 2.7.0 - 26 oktober 2021

* Maak aanvullende informatie van Experience Edge beschikbaar in de geretourneerde waarde van `sendEvent`, met inbegrip van `inferences` en `destinations`. Het formaat van deze eigenschappen kan veranderen aangezien deze eigenschappen momenteel als deel van een Bèta rollen. Zie voor meer informatie [Gebeurtenissen bijhouden.](fundamentals/tracking-events.md)

## Versie 2.6.4 - 7 september 2021

* Probleem verholpen waarbij ingestelde HTML Adobe Target-acties werden toegepast op de `head` element vervangt het gehele `head` inhoud. Stel nu HTML-handelingen in die worden toegepast op de `head` -element wordt gewijzigd en voegt HTML toe.

## Versie 2.6.3 - 16 augustus 2021

* Probleem verholpen waarbij objecten die niet voor openbaar gebruik bestemd waren, werden blootgesteld via de opgeloste belofte van de `configure` gebruiken.

## Versie 2.6.2 - 4 augustus 2021

* Probleem verholpen waarbij een waarschuwing over de afgekeurde versie van `result.decisions` (verstrekt door de `sendEvent` bevel) zou aan de console worden geregistreerd zelfs wanneer `result.decisions` eigenschap werd niet benaderd. Er wordt geen waarschuwing geregistreerd wanneer u het dialoogvenster opent `result.decisions` eigenschap, maar de eigenschap is nog steeds afgekeurd.

## Versie 2.6.1 - 29 juli 2021

* Probleem verholpen waarbij het renderen van de personalisatie voor een app-weergave van één pagina zonder personalisatie-inhoud een fout zou veroorzaken en de belofte zou doen terugkomen van de app. Dit probleem is nu opgelost. `sendEvent` te verwerpen opdracht.

## Versie 2.6.0 - 27 juli 2021

* Verstrekt meer verpersoonlijkingsinhoud in `sendEvent` opgelost belofte, inclusief Adobe Target response tokens. Wanneer de `sendEvent` bevel wordt uitgevoerd, wordt een belofte teruggegeven, die uiteindelijk met een wordt opgelost `result` object met informatie die van de server is ontvangen. Eerder bevatte dit resultaatobject een eigenschap met de naam `decisions`. Dit `decisions` eigenschap is vervangen. Een nieuwe eigenschap, `propositions`, is toegevoegd. Deze nieuwe eigenschap biedt klanten toegang tot meer personalisatie-inhoud, waaronder [reactietokens](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/accessing-response-tokens.html).

## Versie 2.5.0 - juni 2021

* Toegevoegde ondersteuning voor aanpassingsmogelijkheden.
* Automatisch verzamelde viewport breedten en hoogten die negatieve waarden zijn zullen niet meer naar de server worden verzonden.
* Wanneer een gebeurtenis wordt geannuleerd door terug te keren `false` van een `onBeforeEventSend` callback, wordt een bericht nu geregistreerd.
* Probleem verholpen waarbij specifieke onderdelen van XDM-gegevens die bestemd waren voor één gebeurtenis, waren opgenomen in meerdere gebeurtenissen.

## Versie 2.4.0 - maart 2021

* De SDK kan nu [geïnstalleerd als npm-pakket](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/installing-the-sdk.html).
* Extra ondersteuning voor een `out` optie wanneer [standaardgoedkeuring configureren](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#default-consent), waardoor alle gebeurtenissen worden gestopt totdat toestemming is ontvangen (de bestaande `pending` de optie vormt gebeurtenissen een rij en verzendt hen zodra de toestemming wordt ontvangen).
* De [onBeforeEventSend callback](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html#onbeforeeventsend) kan nu worden gebruikt om te voorkomen dat een gebeurtenis wordt verzonden.
* Gebruikt nu een XDM-schemaveldgroep in plaats van `meta.personalization` wanneer het verzenden van gebeurtenissen over gepersonaliseerde inhoud die wordt teruggegeven of geklikt.
* De [getIdentity, opdracht](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html#retrieving-the-visitor-id) retourneert nu de id van het randgebied naast de identiteit.
* Waarschuwingen en fouten die van de server zijn ontvangen, zijn verbeterd en worden op een geschiktere manier afgehandeld.
* Extra ondersteuning voor [Adobe 2](https://experienceleague.adobe.com/docs/experience-platform/edge/consent/supporting-consent.html?communicating-consent-preferences-via-the-adobe-standard).
* De voorkeur van de toestemming, wanneer ontvangen, wordt gehakt en in lokale opslag voor een geoptimaliseerde integratie onder CMPs, het Web SDK van het Platform, en het Netwerk van de Rand van het Platform opgeslagen. Als u toestemmingsvoorkeur verzamelt, moedigen wij u nu aan om te roepen `setConsent` op elke pagina die wordt geladen.
* Twee [toezicht op haken](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` en `onCommandRejected`, zijn toegevoegd.
* Opgeloste problemen: Gebeurtenissen voor persoonlijke interactiemeldingen bevatten dubbele informatie over dezelfde activiteit wanneer een gebruiker naar een nieuwe app-weergave van één pagina navigeert, teruggaat naar de oorspronkelijke weergave en op een element klikt dat in aanmerking komt voor conversie.
* Opgeloste problemen: Als de eerste gebeurtenis die door de SDK is verzonden `documentUnloading` instellen op `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) wordt gebruikt om de gebeurtenis te verzenden, wat resulteert in een fout betreffende een identiteit die niet wordt vastgesteld.

## Versie 2.3.0 - november 2020

* Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
* Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
* Verbeterde compatibiliteit met andere JavaScript-code op de pagina die mogelijk wordt overschreven `window.console` API&#39;s.
* Opgeloste problemen: `sendBeacon` niet werd gebruikt toen `documentUnloading` is ingesteld op `true` of wanneer de koppeling kliks automatisch is bijgehouden.
* Opgeloste problemen: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
* Opgeloste problemen: Bepaalde browserfouten die alleen-lezen bevatten `message` eigenschap is niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
* Opgeloste problemen: Als de SDK in een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe zich in een ander subdomein bevindt dan de HTML-pagina van het bovenliggende venster.

## Versie 2.2.0 - oktober 2020

* Opgeloste problemen: Het object Opt-in blokkeerde het openen van aanroepen wanneer `idMigrationEnabled` is `true`.
* Opgeloste problemen: Alloy bewust maken van verzoeken die de aanbiedingen van de verpersoonlijking zouden moeten terugkeren om een flikkerende kwestie te verhinderen.

## Versie 2.1.0 - augustus 2020

* Verwijder de `syncIdentity` opdracht en ondersteuning voor het doorgeven van die id&#39;s in het dialoogvenster `sendEvent` gebruiken.
* Ondersteuning voor IAB 2.0 Consent Standard.
* Ondersteuning voor het doorgeven van aanvullende id&#39;s in het dialoogvenster `setConsent` gebruiken.
* Ondersteuning voor het overschrijven van de `datasetId` in de `sendEvent` gebruiken.
* Ondersteuningslantmonitoren ([Meer informatie](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Voldoende `environment: browser` in de implementatie de contextgegevens.
