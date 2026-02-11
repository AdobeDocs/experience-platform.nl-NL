---
title: Opmerkingen bij de release Adobe Experience Platform Web SDK
description: De nieuwste aanvullende informatie voor de Adobe Experience Platform Web SDK.
keywords: Adobe Experience Platform Web SDK;Experience Platform Web SDK;Web SDK;release notes;
exl-id: efd4e866-6a27-4bd5-af83-4a97ca8adebd
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '2673'
ht-degree: 5%

---


# Opmerkingen bij de release Web SDK

In dit document worden de opmerkingen bij de release voor de Adobe Experience Platform Web SDK besproken.
Voor de recentste versienota&#39;s op de de markeringsuitbreiding van SDK van het Web, zie de [&#x200B; nota&#39;s van de de marktextensie van SDK van het Web &#x200B;](/help/tags/extensions/client/web-sdk/web-sdk-ext-release-notes.md).

## Versie 2.31.0 - 9 februari 2026

**Nieuwe functies**

- De beschikbaarheid van `"oneTimeAnalyticsReferrer"` is toegevoegd aan de array met tekenreeksen van [`context`](commands/configure/context.md) .
- De Brand Concierge-component toegevoegd.
- `meta.queueTimeMillis` toegevoegd aan netwerkverzoek om de tijd tussen het maken van de gebeurtenis en de verzonden tijd op te nemen.
- De capaciteit om de identiteitskaart voort te zetten zodat kan het met verdere vraag worden bevolkt.

**Bevestigingen en verbeteringen**

- De `aria-label` en `name` attributen worden nu overwogen in [&#x200B; automatische verbindingsinzameling &#x200B;](commands/configure/clickcollectionenabled.md).
- Probleem verholpen waarbij een mogelijk ras kon worden hersteld met integratie van identiteitskaarten.
- Probleem verholpen waarbij tijdstempel niet was opgenomen in `streamingMedia` .
- Probleem verholpen waarbij aangepaste code-acties slechts eenmaal werden uitgevoerd.

## Versie 2.30.0 - 24 september 2025

**Nieuwe functies**

- Extra ondersteuning voor het weergeven van pushmeldingen.

## Versie 2.29.0 - 4 september 2025

**Nieuwe functies**

- Toegevoegde ondersteuning voor het verzamelen van Adobe Advertisement Data voor Adobe Journey Analytics
- Extra ondersteuning voor het opnemen van gegevens van pushabonnementen in gebruikersprofielen.

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij gedeelten met configuratieoverschrijvingen werden samengevoegd in plaats van vervangen.
- Probleem verholpen waarbij verzameling koppelingen de volledige documentinhoud als naam van de koppeling verzendt.
- Probleem verholpen waarbij bepaalde voorstellen niet opnieuw konden worden weergegeven.

## Versie 2.28.1 - vrijdag 31 juli 2025

**Bevestigingen en verbeteringen**

- Probleem verholpen waardoor aangepaste builds niet konden worden uitgevoerd.

## Versie 2.28.0 - vrijdag 24 juli 2025

**Nieuwe functies**

- Toegevoegde ondersteuning voor Adobe Journey Optimizer-regels voor ongeschiktheid.

**Bevestigingen en verbeteringen**

- Oplossing een fout in de [&#x200B; Tracker van Analytics van Media &#x200B;](commands/getmediaanalyticstracker.md) waar het `length` bezit van het media voorwerp verkeerd erkende ongeldige gegevenstypes.
- Verbeterde [&#x200B; fout behandeling van het 0&rbrace; identiteitsbeheer &lbrace;om belofteverwervingen behoorlijk te verwerken wanneer de identiteitsraadpleging ontbreekt.](../use-cases/identity/id-overview.md)
- Oplossing voor een probleem waarbij personalisatie-inhoud met HTML-inhoudsitems niet werd gerenderd met een fout die betrekking had op een ontbrekende `renderStatusHandler` .
- Vaste activiteitenkaart [&#x200B; inzameling URL &#x200B;](commands/configure/clickcollectionenabled.md) om niet-HTTP URLs behoorlijk te behandelen.

**Bekende kwesties**

- Het [&#x200B; douane bouwt &#x200B;](/help/collection/js/install/create-custom-build.md) proces gebruikend `npx @adobe/alloy` werkt momenteel niet zoals verwacht in versie 2.28.0. Alle componenten zijn inbegrepen in de geproduceerde bouwstijl, ongeacht de geselecteerde modules. Dit probleem heeft geen invloed op het standaard JavaScript-bestand dat beschikbaar is op de CDN. Er wordt een correctie uitgevoerd.

## Versie 2.27.0 - woensdag 20 mei 2025

**Bevestigingen en verbeteringen**

- Probleem verholpen met in-app berichten waarbij de aangepaste opmaak niet correct werd toegepast.
- De indeling van de gebeurtenisgeschiedenis is gewijzigd. Hierdoor worden in-app berichten en inhoudskaarten opnieuw weergegeven terwijl de oude historiegegevens worden verwijderd.
- Oplossing een kwestie waar de voorstellen in de gebruiksgevallen van het KUUROORD opnieuw zouden worden toegepast.
- Probleem verholpen met klikken op volgen op schaduw-DOM-elementen.

## Versie 2.26.0 - 5 maart 2025

**Nieuwe functies**

- U kunt nu het Web SDK NPM-pakket gebruiken om aangepaste Web SDK-builds te maken en alleen de bibliotheekcomponenten te selecteren die u nodig hebt. Dit leidt tot een vermindering van de bibliotheekgrootte en geoptimaliseerde laadtijden. Zie de documentatie op hoe te [&#x200B; tot een douaneSDK van het Web leiden gebruikend het pakket NPM &#x200B;](install/create-custom-build.md).
- De opdracht [`getIdentity`](commands/getidentity.md) leest de ECID nu automatisch rechtstreeks vanuit het `kndctr` -identiteitscookie. Als u `getIdentity` aanroept met de naamruimte `ECID` en er al een identiteitscookie is, vraagt Web SDK de Edge Network niet langer om de identiteit op te halen. Het leest nu de identiteit uit het cookie.

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij met `getIdentity` -opdrachten de identiteit niet werd geretourneerd nadat een `collect` -aanroep was verzonden.
- Probleem verholpen waarbij het omleiden van inhoud tot flikkering leidde voordat de omleiding plaatsvond.

## Versie 2.25.0 - vrijdag 23 januari 2025

**Vaste en verbeteringen**

- Validatie van opties toegevoegd aan de opdracht `setDebug` .
- Er is een waarschuwing toegevoegd tijdens het configureren van een functie `onBeforeLinkClickSend` of een koppelingskwalificatie voor downloadkoppelingen wanneer de functie voor klikken is uitgeschakeld.
- Probleem verholpen waarbij gerenderde voorstellingen niet waren opgenomen in weergavemeldingen.

**Nieuwe functies**

- Implementeerde een fallback naar het geconfigureerde Edge-domein wanneer cookies van derden zijn ingeschakeld en aanvragen naar adobedc.demdex.net worden geblokkeerd.

## Versie 2.24.1 - zaterdag 6 december 2024

**Vaste en verbeteringen**

- Oplossing van een gebiedsdeelkwestie met betrekking tot [&#x200B; de Motor van de Regels van Adobe Experience Platform &#x200B;](https://github.com/adobe/aepsdk-rulesengine-typescript/), die fouten in sommige klantenintegratie veroorzaakte. SDK van het Web vereist nu [&#x200B; versie 2.0.3 van de Motor van de Regels van 0&rbrace; Adobe Experience Platform of later.](https://github.com/adobe/aepsdk-rulesengine-typescript/)

## Versie 2.24.0 - vrijdag 31 oktober 2024

**Nieuwe functies**

- [&#x200B; DataStream treedt met voeten &#x200B;](/help/datastreams/overrides.md) wordt nu gesteund wanneer het beginnen van media zittingen.

- Toegevoegde steun voor de reactietekenen van Adobe Target in de [`onContentRendering`](monitoring-hooks.md#onContentRendering) controlehaak.

**Bevestigingen en verbeteringen**

- Wanneer meerdere in-app berichten worden geretourneerd, wordt alleen de berichten met de hoogste prioriteit weergegeven. De andere bestanden worden opgenomen als onderdrukt.
- Lege gegevensstroomoverschrijvingen worden niet meer naar de Edge Network verzonden, waardoor potentiële conflicten met de routeringsconfiguraties aan de serverzijde worden verminderd.
- De naam van de volgende logboekberichtcomponentnamen is gewijzigd, zodat deze kunnen worden uitgelijnd met andere Adobe SDK&#39;s:
   - `DecisioningEngine` is hernoemd naar `RulesEngine`
   - `LegacyMediaAnalytics` is hernoemd naar `MediaAnalyticsBridge`
   - `Privacy` is hernoemd naar `Consent`
- Oplossing voor een fout die optrad wanneer standaardinhoudsitems werden gerenderd via [`applyPropositions`](commands/applypropositions.md) .
- Oplossing voor een CSS-fout in Adobe Target-acties voor verplaatsen en vergroten of verkleinen.
- De `machineLearning` -toets is verwijderd uit [`sendEvent`](commands/sendevent/overview.md) -reacties.

## Versie 2.23.0 - 19 september 2024

**Nieuwe functies**

- Toegevoegde steun voor het verzoeken van [&#x200B; identiteitskaart van de KERN &#x200B;](/help/collection/use-cases/identity/id-overview.md) in het [&#x200B; getIdentity &#x200B;](commands/getidentity.md) bevel.

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij cookies niet correct werden geschreven wanneer de Web SDK lokaal werd uitgevoerd.

## Versie 2.2.2.0 - 22 augustus 2024

**Nieuwe functies**

- Toegevoegde ondersteuning voor knuppels voor personalisatie-controle.

**Bevestigingen en verbeteringen**

- Ondersteuning voor Internet Explorer is verwijderd. Hierdoor wordt de gzip-grootte van de bibliotheek met 9% verminderd.
- Probleem verholpen waarbij de gegevens van de link activity map niet werden geïnitialiseerd toen de `onInstanceConfigured` monitorhaak werd aangeroepen.
- Probleem verholpen waarbij de doelen van cookies niet waren ingesteld op het juiste pad.
- Probleem met klant verholpen met aanroep naar has.
- Vaste een kwestie waar een ongeldige url coderen in de `adobe_mc` parameter [&#x200B; sendEvent &#x200B;](commands/sendevent/overview.md) vraag veroorzaakte om te ontbreken.

## Versie 2.21.1 - vrijdag 18 juli 2024

**Bevestigingen en verbeteringen**

- Oplossing voor een constructiefout bij gebruik van NPM-bibliotheek.

## Versie 2.21.0 - woensdag 16 juli 2024

**Nieuwe functies**

- Toegevoegde ondersteuning voor het automatisch bijhouden van propositieinteractie.
- Een aangepast constructiescript met een `alloy.js` -bestand toegevoegd.
- Verbeterde klikinzameling met ActivityMap en gebeurtenis groeperende steun.

## Versie 2.20.0 - woensdag 21 mei 2024

**Nieuwe functies**

- Toegevoegde steun voor [&#x200B; Streaming de Inzameling van Media &#x200B;](commands/configure/streamingmedia.md).

**Bevestigingen en verbeteringen**

- Het probleem waarbij de standaardinhoud werd verborgen door het voorverborgen fragment, is opgelost door een fout te voorkomen toen de toestemming werd geweigerd.

## Versie 2.19.2 - donderdag 10 januari 2024

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij identiteitsfouten andere fouten maskeerden en identiteitsfouten veranderden in waarschuwingen.
- Probleem verholpen waarbij de onderzijde van pagina-aanroepen nooit zouden worden verzonden wanneer de bovenkant van de pagina-aanroep was ingesteld op `renderDecisions` `false` .
- Probleem verholpen waarbij Web SDK geen interdomein-identiteiten kon lezen als er meerdere `adobe_mc` query-tekenreeksparameters waren.

## Versie 2.19.1 - zaterdag 10 november 2023

**Bevestigingen en verbeteringen**

- Probleem verholpen waarbij de array proposities die door `sendEvent` aanroepen werd geretourneerd, altijd leeg was.

## Versie 2.19.0 - donderdag 1 november 2023

**Nieuwe functies**

- Extra ondersteuning voor het renderen van berichten in de app van Adobe Journey Optimizer.
- Toegevoegde steun voor [&#x200B; bovenkant en bodem van paginagebeurtenissen &#x200B;](../use-cases/personalization/top-bottom-page-events.md).
- Optie [`defaultPersonalizationEnabled`](commands/sendevent/personalization.md) toegevoegd aan de opdracht `sendEvent` om het opvragen van het bereik en het standaardoppervlak voor de hele pagina te besturen.

**Bevestigingen en verbeteringen**

- Gecombineerde verpersoonlijkingsvertoningsgebeurtenissen samen wanneer het teruggeven van veelvoudige types van verpersoonlijking.
- Probleem verholpen waarbij de weergavenamen van toepassingen van één pagina hoofdlettergevoelig waren.
- Probleem verholpen met gepersonaliseerde aanbod-kiezers voor schaduwDOM.

## Versie 2.18.0 - dinsdag 31 juli 2023

**Nieuwe functies**

- Toegevoegde steun voor [&#x200B; per-bevel treedt van datastream identiteitskaart &#x200B;](/help/datastreams/overrides.md) met voeten.

**Bevestigingen en verbeteringen**

- Afsluitkoppelingen kwamen niet in aanmerking omdat het domein deel uitmaakte van een query. Dit probleem is nu opgelost.
- `edgeConfigId` vervangen door `datastreamId` in de Web SDK-configuratie.

## Versie 2.17.0 - donderdag 17 mei 2023

**Bevestigingen en verbeteringen**

- SDK van het Web codeert nu de het koekjesbestemmingswaarden van Audience Manager, gelijkend op [&#x200B; Data Integration Library (DIL) &#x200B;](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html).

## Versie 2.16.0 - 25 april 2023

**Nieuwe functies**

- Toegevoegde steun voor [&#x200B; datastream configuratie treedt met voeten &#x200B;](/help/datastreams/overrides.md).

## Versie 2.15.0 - 30 maart 2023

**Nieuwe functies**

- Toegevoegde ondersteuning voor [`onBeforeLinkClickSend`](commands/configure/onbeforelinkclicksend.md) link click callback.
- Extra ondersteuning voor Adobe Journey Optimizer klik tracking.

**Bevestigingen en verbeteringen**

- De koppelingsverzameling bevat nu de naam van de koppeling en het bezoekersgebied.
- Fout met betrekking tot console verwijderd voor mislukte URL-doelen.

## Versie 2.14.0 - donderdag 25 januari 2023

- (Beta) Extra ondersteuning voor Adobe Journey Optimizer-oppervlakken en -voorstellingen.

**Bevestigingen en verbeteringen**

- Probleem verholpen met aangepaste code-acties voor Adobe Target VEC waarbij de code op een andere locatie werd geïnjecteerd dan met [!DNL at.js] .
- Probleem verholpen waarbij in sommige randgevallen de koptekst van de &quot;referentie&quot; niet correct was ingesteld bij aanvragen bij de Edge Network.
- Vaste een kwestie waar [&#x200B; de wenk van de gebruikersagent &#x200B;](../use-cases/client-hints.md) eigenschappen aan een onjuist type konden worden geplaatst.
- Correctie van een probleem waarbij `placeContext.localTime` niet overeenkwam met het schema.

## Versie 2.13.1 - vrijdag 13 oktober 2022

- Probleem verholpen waarbij bezoekersmigratie niet werkt als window.Visitor na het configureren wordt gedefinieerd. Dit is vooral een probleem wanneer u met Adobe-tags werkt.
- Probleem verholpen waarbij `device.screenWidth` en `device.screenHeight` in sommige omgevingen als tekenreeksen werden gevuld.

## Versie 2.13.0 - 28 september 2022

**Nieuwe functies**

- Extra ondersteuning voor Volledige migratie van pagina naar pagina. Het Adobe Target-profiel blijft nu behouden wanneer een bezoeker zich tussen de pagina&#39;s at.js en Web SDK verplaatst.
- Toegevoegde configureerbare steun voor [&#x200B; high entropy gebruiker-Agent de Hints van de Cliënt &#x200B;](../use-cases/client-hints.md).
- Extra ondersteuning voor de opdracht [`applyResponse`](commands/applyresponse.md) . Dit laat hybride verpersoonlijking via [&#x200B; Edge Network API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/api/) toe.
- Koppelingen in de QA-modus werken nu op meerdere pagina&#39;s.

**Bevestigingen en verbeteringen**

- Correctie van een probleem waarbij de gegevens voor bijhouden van koppelingen niet werden bijgewerkt nadat de functie voor het bijhouden van koppelingen was uitgeschakeld.
- Bijgewerkte opdrachten om een validatiefout te genereren wanneer onbekende opties worden opgegeven.
- De eigenschap `_experience.decisioning.propositionEventType` wordt nu gevuld wanneer automatisch weergave- en interactiepersonalisatie-gebeurtenissen worden verzonden.
- Toegevoegde gedupliceerde naamruimtevalidatie voor de opdracht `getIdentity` .
- Toegevoegde gedupliceerde validatie van beslissingsbereik voor de opdracht `sendEvent` .

## Versie 2.12.0 - donderdag 29 juni 2022

- Wijzig de aanvragen aan de Edge Network om de `cluster` cookie locatiehint te gebruiken als onderdeel van de URL. Dit zorgt ervoor dat gebruikers die hun locatie wijzigen (bijvoorbeeld via een VPN of rijden met mobiele apparaten, enz.), halverwege de sessie dezelfde kant op gaan en hetzelfde personalisatieprofiel hebben.
- Hiermee worden de geconfigureerde functies in de opdrachtreactie van getLibraryInfo gerenderd.

## Versie 2.11.0 - dinsdag 13 juni 2022

**Nieuwe functies**

- U kunt nu nauwkeuriger persoonlijke ervaringen bieden door gebruikers-id&#39;s te delen tussen mobiele apps en mobiele webinhoud, en tussen domeinen. Zie [&#x200B; specifieke documentatie &#x200B;](../use-cases/identity/id-sharing.md) om meer te leren.
- U kunt nu een array met voorstellingen van [!DNL Adobe Target] renderen of uitvoeren in toepassingen van één pagina, zonder de analytische meetgegevens te verhogen. Dit vermindert rapportagefouten en vergroot de nauwkeurigheid van de analyse. Zie [&#x200B; specifieke documentatie &#x200B;](../use-cases/personalization/rendering-personalization-content.md) om meer te leren.
- Extra informatie toegevoegd aan de opdracht `getLibraryInfo` , inclusief beschikbare opdrachten en de uiteindelijke configuratie voor de instantie.

**Bevestigingen en verbeteringen**

- Bijgewerkte cookie-instellingen die moeten worden gebruikt `sameSite="none"` en `secure` markering op [!DNL HTTPS] pagina&#39;s.
- Correctie van een probleem waarbij gepersonaliseerde inhoud niet correct werd toegepast bij gebruik van de pseudo-kiezer van `eq` .
- Correctie van een probleem waarbij `localTimezoneOffset` de validatie van Experience Platform kon mislukken.

## Versie 2.10.1 - woensdag 3 mei 2022

- Probleem verholpen waarbij meerdere permanente iframes werden gemaakt voor id-syncs en segmentdoelen.

## Versie 2.10.0 - 22 april 2022

- Gebruik een blijvend iframe voor alle ID syncs en segmentbestemmingen.
- Probleem verholpen waarbij samengevoegde metrische profielen werden gedupliceerd in het `sendEvent` resultaat.

## Versie 2.9.0 - 10 maart 2022

- Extra ondersteuning voor het bijhouden van Adobe Target-ervaringen van [!DNL control (default)] .
- De gebeurtenis view-change is geoptimaliseerd voor toepassingen op één pagina. Het weergavebericht wordt nu opgenomen in de gebeurtenis view-change wanneer persoonlijke ervaringen worden weergegeven.
- Waarschuwing van console is verwijderd als er geen `eventType` aanwezig is.
- Probleem verholpen waarbij de eigenschap `propositions` alleen werd geretourneerd van een `sendEvent` -opdracht wanneer er ervaringen werden opgevraagd of opgehaald uit de cache. De eigenschap `propositions` wordt nu altijd gedefinieerd als een array.
- Probleem verholpen waarbij verborgen containers niet werden weergegeven als er een fout was geretourneerd door de Edge Network.
- Probleem verholpen waarbij de interactieve gebeurtenissen niet in Adobe Target werden meegeteld. Dit probleem is opgelost door de weergavenaam toe te voegen aan de XDM op web.webPageDetails.viewName.
- Los gebroken documentatiekoppelingen in consoleberichten op.

## Versie 2.8.0 - donderdag 19 januari 2022

- Ondersteuning voor schaduw-DOM-kiezers voor personalisatie.
- Naam gewijzigd in gebeurtenistypen voor personalisatie. (`display` en `click` worden `decisioning.propositionDisplay` en `decisioning.propositionInteract`)
- Probleem verholpen waarbij HTML-aanbiedingen met inline scripttags de scripttags twee keer aan de pagina toevoegden, ook al werd het script slechts één keer uitgevoerd.

## Versie 2.7.0 - woensdag 26 oktober 2021

- Maak aanvullende informatie van de Edge Network beschikbaar in de geretourneerde waarde van `sendEvent` , inclusief `inferences` en `destinations` . Het formaat van deze eigenschappen kan veranderen aangezien deze eigenschappen momenteel als deel van een Beta uitrollen.

## Versie 2.6.4 - 7 september 2021

- Probleem verholpen waarbij de volledige `head` -inhoud werd vervangen door HTML Adobe Target-handelingen die waren ingesteld op het `head` -element. Stel nu HTML-handelingen in die worden toegepast op het element `head` , en die worden gewijzigd in HTML toevoegen.

## Versie 2.6.3 - 16 augustus 2021

- Probleem verholpen waarbij objecten die niet voor openbaar gebruik zijn bedoeld, werden blootgesteld via de opgeloste belofte van de opdracht `configure` .

## Versie 2.6.2 - 4 augustus 2021

- Probleem verholpen waarbij een waarschuwing over de afschrijving van `result.decisions` (opgegeven door de opdracht `sendEvent` ) zou worden geregistreerd bij de console, zelfs als de eigenschap `result.decisions` niet werd benaderd. Er wordt geen waarschuwing geregistreerd wanneer de eigenschap `result.decisions` wordt benaderd, maar de eigenschap is nog steeds afgekeurd.

## Versie 2.6.1 - vrijdag 29 juli 2021

- Probleem verholpen waarbij het renderen van een app-weergave van één pagina zonder inhoud voor personalisatie een fout zou opleveren en de belofte die door de opdracht `sendEvent` is geretourneerd, zou worden afgewezen.

## Versie 2.6.0 - woensdag 27 juli 2021

- Verstrekt meer verpersoonlijkingsinhoud in de `sendEvent` opgeloste belofte, met inbegrip van de reactietekenen van Adobe Target. Wanneer de opdracht `sendEvent` wordt uitgevoerd, wordt een promise geretourneerd die uiteindelijk wordt opgelost met een `result` -object dat informatie bevat die van de server is ontvangen. Eerder bevatte dit resultaatobject een eigenschap met de naam `decisions` . Deze eigenschap `decisions` is vervangen. Er is een nieuwe eigenschap, `propositions` , toegevoegd. Deze nieuwe eigenschap biedt klanten toegang tot meer personalisatie-inhoud, inclusief reactietokens.

## Versie 2.5.0 - juni 2021

- Toegevoegde ondersteuning voor aanpassingsmogelijkheden.
- Automatisch verzamelde viewport breedten en hoogten die negatieve waarden zijn zullen niet meer naar de server worden verzonden.
- Wanneer een gebeurtenis wordt geannuleerd door `false` vanuit een `onBeforeEventSend` callback te retourneren, wordt nu een bericht geregistreerd.
- Probleem verholpen waarbij specifieke onderdelen van XDM-gegevens die bestemd waren voor één gebeurtenis, waren opgenomen in meerdere gebeurtenissen.

## Versie 2.4.0 - maart 2021

- SDK kan nu als [&#x200B; NPM pakket &#x200B;](install/npm.md) worden geïnstalleerd.
- Toegevoegde steun voor een `out` optie wanneer [&#x200B; vormend standaardtoestemming &#x200B;](commands/configure/defaultconsent.md), die alle gebeurtenissen laat vallen tot de toestemming wordt ontvangen (de bestaande `pending` optie maakt gebeurtenissen een rij en verzendt hen zodra de toestemming wordt ontvangen).
- De callback van [`onBeforeEventSend`](commands/configure/onbeforeeventsend.md) kan nu worden gebruikt om te voorkomen dat een gebeurtenis wordt verzonden.
- Er wordt nu een XDM-schemaveldgroep gebruikt in plaats van `meta.personalization` bij het verzenden van gebeurtenissen over gepersonaliseerde inhoud die wordt gerenderd of waarop wordt geklikt.
- De opdracht [`getIdentity`](commands/getidentity.md) retourneert nu de id van het randgebied naast de identiteit.
- Waarschuwingen en fouten die van de server zijn ontvangen, zijn verbeterd en worden op een geschiktere manier afgehandeld.
- Toegevoegde ondersteuning voor de Adobe-standaard Goedkeuring 2.0 voor de opdracht [`setConsent`](commands/setconsent.md) .
- Wanneer u de voorkeuren voor toestemming ontvangt, worden deze gehasht en lokaal opgeslagen voor een geoptimaliseerde integratie tussen CMP&#39;s, Experience Platform Web SDK en Experience Platform Edge Network. Als u toestemmingsvoorkeur verzamelt, moedigen wij u nu aan om `setConsent` op elke paginading te roepen.
- Twee [&#x200B; controlerende haken &#x200B;](https://github.com/adobe/alloy/wiki/Monitoring-Hooks), `onCommandResolved` en `onCommandRejected`, zijn toegevoegd.
- Bug Fix: de gebeurtenissen van het de interactiebericht van Personalization zouden dubbele informatie over de zelfde activiteit bevatten wanneer een gebruiker aan een nieuwe single-page toepassingsmening, terug naar de originele mening navigeerde, en een element in aanmerking voor omzetting klikte.
- Opgeloste problemen: als voor de eerste gebeurtenis die door de SDK wordt verzonden `documentUnloading` is ingesteld op `true` , [`sendBeacon` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Navigator/sendBeacon) , wordt de gebeurtenis verzonden, wat resulteert in een fout met betrekking tot een identiteit die niet wordt vastgesteld.

## Versie 2.3.0 - november 2020

- Nonce-ondersteuning toegevoegd om een strenger beleid voor inhoudsbeveiliging mogelijk te maken.
- Extra ondersteuning voor personalisatie voor toepassingen van één pagina.
- Verbeterde compatibiliteit met andere JavaScript-code op de pagina die mogelijk `window.console` -API&#39;s overschrijft.
- Bug Fix: `sendBeacon` werd niet gebruikt toen `documentUnloading` was ingesteld op `true` of wanneer de koppelingenklikken automatisch werden bijgehouden.
- Bug Fix: Een koppeling wordt niet automatisch bijgehouden als het ankerelement HTML-inhoud bevat.
- Bug Fix: Bepaalde browserfouten die een alleen-lezen `message` eigenschap bevatten, zijn niet correct verwerkt, waardoor een andere fout aan de klant wordt gemeld.
- Bug Fix: Als de SDK binnen een iframe wordt uitgevoerd, treedt een fout op als de HTML-pagina van het iframe zich in een ander subdomein bevindt dan de HTML-pagina van het bovenliggende venster.

## Versie 2.2.0 - oktober 2020

- Bug Fix: Het Opt-in-object blokkeerde Web SDK om aanroepen uit te voeren wanneer `idMigrationEnabled` `true` is.
- Bug Fix: Maak het Web SDK zich bewust van verzoeken die verpersoonlijkingsaanbiedingen zouden moeten terugkeren om een het flikkeren kwestie te verhinderen.

## Versie 2.1.0 - augustus 2020

- Verwijder de opdracht `syncIdentity` en ondersteun het doorgeven van die id&#39;s in de opdracht `sendEvent` .
- Ondersteuning voor IAB 2.0 Consent Standard.
- Ondersteuning voor het doorgeven van aanvullende id&#39;s in de opdracht `setConsent` .
- Ondersteuning voor het overschrijven van de opdracht `datasetId` in de opdracht `sendEvent` .
- Steun die Hooks controleert ([&#x200B; las meer &#x200B;](https://github.com/adobe/alloy/wiki/Monitoring-Hooks))
- Geef `environment: browser` door in de contextgegevens van de implementatiedetails.
