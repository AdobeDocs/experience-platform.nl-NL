---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: De nieuwste aanvullende informatie voor de Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;release notes;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 0%

---


# Aanvullende informatie

In dit document worden de releaseopmerkingen voor de Adobe Experience Platform Web SDK besproken.
Voor de recentste versienota&#39;s op de de markeringsuitbreiding van SDK van het Web, zie [Opmerkingen bij de release Web SDK-tag](../tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Versie 2.19.2 - 10 januari 2024

**Oplossingen en verbeteringen**

* Probleem verholpen waarbij identiteitsfouten andere fouten maskeerden en identiteitsfouten veranderden in waarschuwingen.
* Probleem verholpen waarbij de onderzijde van de paginanummers nooit zou worden verzonden als er een bovenzijde van de paginanroep was met `renderDecisions` instellen op `false`.
* Probleem verholpen waarbij Web SDK geen interdomein-identiteiten kon lezen als er meerdere waren. Dit probleem is nu opgelost. `adobe_mc` querytekenreeksparameters.

## Versie 2.19.1 - 10 november 2023

**Oplossingen en verbeteringen**

* Probleem verholpen waarbij de array proposities werd geretourneerd van `sendEvent` de vraag was altijd leeg.

## Versie 2.19.0 - 1 november 2023

**Nieuwe functies**

* Extra ondersteuning voor het renderen van berichten in de app van Adobe Journey Optimizer.
* Extra ondersteuning voor [boven- en onderzijde van paginagebeurtenissen](use-cases/top-bottom-page-events.md).
* Toegevoegd [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) aan de `sendEvent` gebruiken om het opvragen van het bereik en het standaardoppervlak voor de hele pagina te besturen.

**Oplossingen en verbeteringen**

* Gecombineerde verpersoonlijkingsvertoningsgebeurtenissen samen wanneer het teruggeven van veelvoudige types van verpersoonlijking.
* Probleem verholpen waarbij de weergavenamen van toepassingen van één pagina hoofdlettergevoelig waren.
* Probleem verholpen met gepersonaliseerde aanbod-kiezers voor schaduwDOM.

## Versie 2.18.0 - 31 juli 2023

**Nieuwe functies**

* Extra ondersteuning voor [per-opdracht overschrijvingen van de gegevensstroom-id](../datastreams/overrides.md).

**Oplossingen en verbeteringen**

* Afsluitkoppelingen kwamen niet in aanmerking omdat het domein deel uitmaakte van een query. Dit probleem is nu opgelost.
* Vervangen `edgeConfigId` ten gunste van `datastreamId` in de configuratie van Web SDK.

## Versie 2.17.0 - 17 mei 2023

**Oplossingen en verbeteringen**

* De SDK van het Web codeert nu de bestemmingswaarden van het koekje van de Audience Manager, gelijkend op [Data Integration Library (DIL)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html).

## Versie 2.16.0 - 25 april 2023

**Nieuwe functies**

* Extra ondersteuning voor [gegevensstroomconfiguratie overschrijft](../datastreams/overrides.md).

## Versie 2.15.0 - 30 maart 2023

**Nieuwe functies**

* Extra ondersteuning voor [`onBeforeLinkClickSend`](/help/web-sdk/commands/configure/onbeforelinkclicksend.md) koppeling klikken op callback.
* Extra ondersteuning voor Adobe Journey Optimizer klik tracking.

**Oplossingen en verbeteringen**

* De koppelingsverzameling bevat nu de naam van de koppeling en het bezoekersgebied.
* Fout met betrekking tot console verwijderd voor mislukte URL-doelen.

## Versie 2.14.0 - 25 januari 2023

* (bèta) Extra ondersteuning voor Adobe Journey Optimizer-oppervlakken en -voorstellingen.

**Oplossingen en verbeteringen**

* Probleem verholpen met aangepaste code-acties voor Adobe Target VEC waarbij de code op een andere locatie werd geïnjecteerd dan met [!DNL at.js].
* Probleem verholpen waarbij de koptekst van de &quot;referentie&quot; in sommige randgevallen niet correct was ingesteld bij aanvragen bij het Edge-netwerk.
* Probleem verholpen waarbij [client-tip voor gebruikersagent](/help/web-sdk/use-cases/client-hints.md) eigenschappen kunnen op een onjuist type worden ingesteld.
* Probleem verholpen waarbij `placeContext.localTime` komt niet overeen met het schema.

## Versie 2.13.1 - 13 oktober 2022

* Probleem verholpen waarbij bezoekersmigratie niet werkt als window.Visitor na het configureren wordt gedefinieerd. Dit is vooral een probleem wanneer u met Adobe-tags werkt.
* Probleem verholpen waarbij `device.screenWidth` en `device.screenHeight` werden in sommige omgevingen als tekenreeksen gevuld.

## Versie 2.13.0 - 28 september 2022

**Nieuwe functies**

* Extra ondersteuning voor [Volledige migratie pagina voor pagina](home.md#migrating-to-web-sdk). Het Adobe Target-profiel blijft nu behouden wanneer een bezoeker zich tussen de pagina&#39;s at.js en Web SDK verplaatst.
* Toegevoegde configureerbare ondersteuning voor [hoge entropgebruiker-Agent de wenken van de Cliënt](/help/web-sdk/use-cases/client-hints.md).
* Extra ondersteuning voor de [`applyResponse`](/help/web-sdk/commands/applyresponse.md) gebruiken. Hierdoor is een hybride personalisatie mogelijk via de [Edge Network Server-API](../server-api/overview.md).
* Koppelingen in de QA-modus werken nu op meerdere pagina&#39;s.

**Oplossingen en verbeteringen**

* Correctie van een probleem waarbij de gegevens voor bijhouden van koppelingen niet werden bijgewerkt nadat de functie voor het bijhouden van koppelingen was uitgeschakeld.
* Bijgewerkte opdrachten om een validatiefout te genereren wanneer onbekende opties worden opgegeven.
* De `_experience.decisioning.propositionEventType` Deze eigenschap wordt nu gevuld wanneer automatisch weergave- en interactiepitalisatiegebeurtenissen worden verzonden.
* Toegevoegde gedupliceerde naamruimtevalidatie voor de `getIdentity` gebruiken.
* Toegevoegde gedupliceerde validatie van beslissingsbereik voor de `sendEvent` gebruiken.

## Versie 2.12.0 - 29 juni 2022

* Verander de verzoeken aan het Netwerk van de Rand om het `cluster` de locatie van de cookie als onderdeel van de URL. Dit zorgt ervoor dat gebruikers die hun locatie wijzigen (bijvoorbeeld via een VPN of rijden met mobiele apparaten, enz.), halverwege de sessie dezelfde kant op gaan en hetzelfde personalisatieprofiel hebben.
* Hiermee worden de geconfigureerde functies in de opdrachtreactie van getLibraryInfo gerenderd.

## Versie 2.11.0 - 13 juni 2022

**Nieuwe functies**

* U kunt nu nauwkeuriger persoonlijke ervaringen bieden door gebruikers-id&#39;s te delen tussen mobiele apps en mobiele webinhoud, en tussen domeinen. Zie de [speciale documentatie](identity/id-sharing.md) voor meer informatie.
* U kunt nu een array met voorstellingen renderen of uitvoeren vanuit [!DNL Adobe Target] in toepassingen van één pagina, zonder de analytische meetgegevens te verhogen. Dit vermindert rapportagefouten en vergroot de nauwkeurigheid van de analyse. Zie de [speciale documentatie](personalization/rendering-personalization-content.md#applypropositions) voor meer informatie.
* Aanvullende informatie toegevoegd aan de `getLibraryInfo` bevel met inbegrip van beschikbare bevelen en de definitieve configuratie voor de instantie.

**Oplossingen en verbeteringen**

* Te gebruiken bijgewerkte cookie-instellingen `sameSite="none"` en `secure` markering op [!DNL HTTPS] pagina&#39;s.
* Correctie van een probleem waarbij gepersonaliseerde inhoud niet correct werd toegepast tijdens het gebruik van de `eq` pseudo-kiezer.
* Probleem verholpen waarbij `localTimezoneOffset` kan de validatie van het Experience Platform niet voltooien.

## Versie 2.10.1 - 3 mei 2022

* Probleem verholpen waarbij meerdere permanente iframes werden gemaakt voor id-syncs en segmentdoelen.

## Versie 2.10.0 - 22 april 2022

* Gebruik een blijvend iframe voor alle ID syncs en segmentbestemmingen.
* Oplossing voor een probleem waarbij samengevoegde metrische profielen werden gedupliceerd in de `sendEvent` resultaat.

## Versie 2.9.0 - 10 maart 2022

* Toegevoegde ondersteuning voor tekstspatiëring [!DNL control (default)] Adobe Target ervaart.
* De gebeurtenis view-change is geoptimaliseerd voor toepassingen op één pagina. Het weergavebericht wordt nu opgenomen in de gebeurtenis view-change wanneer persoonlijke ervaringen worden weergegeven.
* Waarschuwing van console is verwijderd als dit niet het geval is `eventType` aanwezig is.
* Het probleem waarbij de `propositions` eigenschap is alleen geretourneerd door een `sendEvent` gebruiken wanneer ervaringen zijn opgevraagd of opgehaald uit de cache. De `propositions` eigenschap wordt nu altijd gedefinieerd als een array.
* Probleem verholpen waarbij verborgen containers niet werden weergegeven als er een fout was geretourneerd van het Edge-netwerk.
* Probleem verholpen waarbij de interactieve gebeurtenissen niet in Adobe Target werden meegeteld. Dit probleem is opgelost door de weergavenaam toe te voegen aan de XDM op web.webPageDetails.viewName.
* Los gebroken documentatiekoppelingen in consoleberichten op.

## Versie 2.8.0 - 19 januari 2022

* Ondersteuning voor schaduw-DOM-kiezers voor personalisatie.
* Naam gewijzigd in gebeurtenistypen voor personalisatie. (`display` en `click` worden `decisioning.propositionDisplay` en `decisioning.propositionInteract`)
* Probleem verholpen waarbij HTML-aanbiedingen met inlinescripttags de scripttags twee keer aan de pagina hebben toegevoegd, ook al werd het script slechts één keer uitgevoerd.

## Versie 2.7.0 - 26 oktober 2021

* Maak extra informatie van het Netwerk van de Rand in de terugkeerwaarde van bloot `sendEvent`, inclusief `inferences` en `destinations`. Het formaat van deze eigenschappen kan veranderen aangezien deze eigenschappen momenteel als deel van een Bèta rollen.

## Versie 2.6.4 - 7 september 2021

* Probleem verholpen waarbij ingestelde HTML Adobe Target-acties werden toegepast op de `head` element vervangt het gehele `head` inhoud. Stel nu HTML-handelingen in die worden toegepast op de `head` -element wordt gewijzigd en voegt HTML toe.

## Versie 2.6.3 - 16 augustus 2021

* Probleem verholpen waarbij objecten die niet voor openbaar gebruik bestemd waren, werden blootgesteld via de opgeloste belofte van de `configure` gebruiken.

## Versie 2.6.2 - 4 augustus 2021

* Probleem verholpen waarbij een waarschuwing over de afgekeurde versie van `result.decisions` (verstrekt door de `sendEvent` bevel) zou aan de console worden geregistreerd zelfs wanneer `result.decisions` eigenschap werd niet benaderd. Er wordt geen waarschuwing geregistreerd wanneer u het dialoogvenster opent `result.decisions` eigenschap, maar de eigenschap is nog steeds vervangen.

## Versie 2.6.1 - 29 juli 2021

* Probleem verholpen waarbij het renderen van de personalisatie voor een app-weergave van één pagina zonder personalisatie-inhoud een fout zou veroorzaken en de belofte zou doen terugkomen van de `sendEvent` te verwerpen opdracht.

## Versie 2.6.0 - 27 juli 2021

* Verstrekt meer verpersoonlijkingsinhoud in `sendEvent` opgelost belofte, inclusief Adobe Target response tokens. Wanneer de `sendEvent` bevel wordt uitgevoerd, wordt een belofte teruggegeven, die uiteindelijk met een wordt opgelost `result` object met informatie die van de server is ontvangen. Eerder bevatte dit resultaatobject een eigenschap met de naam `decisions`. Dit `decisions` eigenschap is vervangen. Een nieuwe eigenschap, `propositions`, is toegevoegd. Deze nieuwe eigenschap biedt klanten toegang tot meer personalisatie-inhoud, waaronder [reactietokens](/help/web-sdk/personalization/adobe-target/accessing-response-tokens.md).

## Versie 2.5.0 - juni 2021

* Toegevoegde ondersteuning voor aanpassingsmogelijkheden.
* Automatisch verzamelde viewport breedten en hoogten die negatieve waarden zijn zullen niet meer naar de server worden verzonden.
* Wanneer een gebeurtenis wordt geannuleerd door terug te keren `false` van een `onBeforeEventSend` callback, wordt een bericht nu geregistreerd.
* Probleem verholpen waarbij specifieke onderdelen van XDM-gegevens die bestemd waren voor één gebeurtenis, waren opgenomen in meerdere gebeurtenissen.

## Versie 2.4.0 - maart 2021

* De SDK kan nu als een [NPM-pakket](/help/web-sdk/install/npm.md).
* Extra ondersteuning voor een `out` optie wanneer [standaardgoedkeuring configureren](/help/web-sdk/commands/configure/defaultconsent.md), waardoor alle gebeurtenissen worden gestopt totdat toestemming is ontvangen (de bestaande `pending` de optie vormt gebeurtenissen een rij en verzendt hen zodra de toestemming wordt ontvangen).
* De [`onBeforeEventSend`](/help/web-sdk/commands/configure/onbeforeeventsend.md) callback kan nu worden gebruikt om te voorkomen dat een gebeurtenis wordt verzonden.
* Gebruikt nu een XDM-schemaveldgroep in plaats van `meta.personalization` wanneer het verzenden van gebeurtenissen over gepersonaliseerde inhoud die wordt teruggegeven of geklikt.
* De [`getIdentity`](/help/web-sdk/commands/getidentity.md) retourneert nu de id van het randgebied naast de identiteit.
* Waarschuwingen en fouten die van de server zijn ontvangen, zijn verbeterd en worden op een geschiktere manier afgehandeld.
* Toegevoegde ondersteuning voor de norm Goedkeuring 2.0 van de Adobe voor de [`setConsent`](/help/web-sdk/commands/setconsent.md) gebruiken.
* De voorkeur van de toestemming, wanneer ontvangen, wordt gehakt en in lokale opslag voor een geoptimaliseerde integratie onder CMPs, het Web SDK van het Platform, en het Netwerk van de Rand van het Platform opgeslagen. Als u toestemmingsvoorkeur verzamelt, moedigen wij u nu aan om te roepen `setConsent` op elke pagina die wordt geladen.
* Twee [toezicht op haken](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` en `onCommandRejected`, zijn toegevoegd.
* Bug Fix: de gebeurtenissen van het de interactiebericht van de Personalisatie zouden dubbele informatie over de zelfde activiteit bevatten wanneer een gebruiker aan een nieuwe single-page toepassingsmening, terug naar de originele mening navigeerde, en een element in aanmerking voor omzetting klikte.
* Bug Fix: als de eerste gebeurtenis die door de SDK is verzonden `documentUnloading` instellen op `true`, [`sendBeacon`](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) wordt gebruikt om de gebeurtenis te verzenden, wat resulteert in een fout betreffende een identiteit die niet wordt vastgesteld.

## Versie 2.3.0 - november 2020

* Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
* Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
* Verbeterde compatibiliteit met andere JavaScript-code op de pagina die mogelijk wordt overschreven `window.console` API&#39;s.
* Opgeloste problemen: `sendBeacon` niet werd gebruikt toen `documentUnloading` is ingesteld op `true` of wanneer de koppeling kliks automatisch is bijgehouden.
* Bug Fix: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
* Bug Fix: Certain browser errors containing a read-only `message` eigenschap is niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
* Bug Fix: Als de SDK binnen een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe afkomstig is uit een ander subdomein dan de HTML van het bovenliggende venster.

## Versie 2.2.0 - oktober 2020

* Bug Fix: Het Opt-in voorwerp blokkeerde Web SDK om vraag te maken wanneer `idMigrationEnabled` is `true`.
* Bug Fix: Maak Web SDK zich van verzoeken bewust die verpersoonlijkingsaanbiedingen zouden moeten terugkeren om een het flikkeren kwestie te verhinderen.

## Versie 2.1.0 - augustus 2020

* Verwijder de `syncIdentity` opdracht en ondersteuning voor het doorgeven van die id&#39;s in het dialoogvenster `sendEvent` gebruiken.
* Ondersteuning voor IAB 2.0 Consent Standard.
* Ondersteuning voor het doorgeven van aanvullende id&#39;s in het dialoogvenster `setConsent` gebruiken.
* Ondersteuning voor het overschrijven van de `datasetId` in de `sendEvent` gebruiken.
* Support Monitoring Hooks ([Meer informatie](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
* Voldoende `environment: browser` in de implementatie de contextgegevens.
