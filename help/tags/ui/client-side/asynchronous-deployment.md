---
title: Asynchrone implementatie
description: Leer hoe u Adobe Experience Platform-tagbibliotheken asynchroon op uw website kunt implementeren.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 0%

---

# Asynchrone implementatie {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Asynchrone implementatie"
>abstract="Als deze optie is ingeschakeld en de browser het JavaScript-bestand laadt wanneer deze scripttag wordt geparseerd, maar niet wacht tot de bibliotheek is geladen en uitgevoerd, blijft de rest van het document parseren en renderen. Dit kan de prestaties van webpagina&#39;s verbeteren, maar heeft belangrijke gevolgen voor de manier waarop bepaalde regels worden uitgevoerd. Raadpleeg de documentatie voor meer informatie."

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Prestaties en niet-blokkerende implementatie van de JavaScript-bibliotheken die vereist zijn voor onze producten, worden steeds belangrijker voor Adobe Experience Cloud-gebruikers. Gereedschappen zoals [[!DNL Google PageSpeed]](https://developers.google.com/speed/pagespeed/insights/) adviseren dat de gebruikers veranderen zij hoe zij de bibliotheken van de Adobe op hun plaats opstellen. In dit artikel wordt uitgelegd hoe u de Adobe JavaScript-bibliotheken asynchroon kunt gebruiken.

## Synchroon versus asynchroon

### Synchrone implementatie

Bibliotheken worden vaak synchroon geladen in het dialoogvenster `<head>` -tag van een pagina. Bijvoorbeeld:

```markup
<script src="example.js"></script>
```

Standaard parseert de browser het document en bereikt deze regel. Vervolgens haalt de browser het JavaScript-bestand op van de server. De browser wacht tot het bestand is geretourneerd, parseert het bestand en voert het uit. Tot slot wordt de rest van het HTML-document nog steeds geparseerd.

Als de parser de `<script>` -tag voordat zichtbare inhoud wordt gerenderd, wordt de weergave van de inhoud vertraagd. Als het JavaScript-bestand dat wordt geladen niet absoluut noodzakelijk is om inhoud aan uw gebruikers weer te geven, hebt u uw bezoekers onnodig gevraagd om op inhoud te wachten. Hoe groter de bibliotheek, des te langer de vertraging.  Daarom zijn benchmarktools voor websiteprestaties zoals [!DNL Google PageSpeed] of [!DNL Lighthouse] worden geladen scripts vaak synchroon gemarkeerd.

Tagbeheerbibliotheken kunnen snel groter worden als u veel tags moet beheren.

### Asynchrone implementatie

U kunt elke bibliotheek asynchroon laden door een `async` aan de `<script>` tag. Bijvoorbeeld:

```markup
<script src="example.js" async></script>
```

Dit geeft aan de browser aan dat wanneer deze scripttag wordt geparseerd, de browser moet beginnen met het laden van het JavaScript-bestand. In plaats van te wachten tot de bibliotheek is geladen en uitgevoerd, moet de browser de rest van het document blijven parseren en renderen.

## Overwegingen bij asynchrone implementatie

Zoals hierboven beschreven, pauzeert de browser bij synchrone implementaties het parseren en renderen van de pagina terwijl de Adobe Experience Platform-tagbibliotheek wordt geladen en uitgevoerd. Bij asynchrone implementaties parseert en rendert de browser de pagina terwijl de bibliotheek wordt geladen. Er moet rekening worden gehouden met de variabiliteit van het tijdstip waarop de tagbibliotheek kan zijn geladen ten opzichte van het parseren en renderen van pagina&#39;s.

Ten eerste, omdat de tagbibliotheek kan zijn geladen voor- of nadat de onderkant van de pagina is geparseerd en uitgevoerd, moet u niet langer bellen `_satellite.pageBottom()` uit uw paginacode (`_satellite` zijn pas beschikbaar nadat de bibliotheek is geladen). Dit wordt uitgelegd in [De ingesloten code van tags asynchroon laden](#loading-the-tags-embed-code-asynchronously).

Ten tweede kan de tagbibliotheek klaar zijn met laden voor of na de [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) Er is een browsergebeurtenis (DOM Ready) opgetreden.

Vanwege deze twee punten is het de moeite waard om te laten zien hoe de [Bibliotheek geladen](../../extensions/client/core/overview.md#library-loaded-page-top), [Pagina onder](../../extensions/client/core/overview.md#page-bottom), [gereed voor DOM](../../extensions/client/core/overview.md#page-bottom), en [Venster geladen](../../extensions/client/core/overview.md#window-loaded) gebeurtenistypen van de functie Core bij het asynchroon laden van een tagbibliotheek.

Als de eigenschap tag de volgende vier regels bevat:

* Regel A: gebruikt het bibliotheekgeladen gebeurtenistype
* Regel B: gebruikt het gebeurtenistype Pagina onder
* Regel C: gebruikt het DOM Ready-gebeurtenistype
* Regel D: gebruikt het gebeurtenistype Window Loaded

Ongeacht wanneer het laden van de tagbibliotheek is voltooid, worden alle regels gegarandeerd uitgevoerd en worden ze in de volgende volgorde uitgevoerd:

Regel A → Lijn B → Lijn C → Lijn D

Hoewel de volgorde altijd wordt gehandhaafd, kunnen sommige regels direct worden uitgevoerd wanneer de tagbibliotheek klaar is met laden, terwijl andere later wellicht worden uitgevoerd. Het volgende gebeurt wanneer de tagbibliotheek klaar is met laden:

1. Regel A wordt onmiddellijk uitgevoerd.
1. Als de `DOMContentLoaded` De browsergebeurtenis (DOM Ready) is al opgetreden, de regels B en C worden onmiddellijk uitgevoerd. Anders, worden de Lijn B en Lijn C uitgevoerd later wanneer [`DOMContentLoaded`](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) browsergebeurtenis.
1. Als de [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) browsergebeurtenis (Venster geladen) heeft zich al voorgedaan, Regel D wordt onmiddellijk uitgevoerd. Anders wordt Regel D later uitgevoerd wanneer [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) browsergebeurtenis. Let erop dat als u de tagbibliotheek volgens de instructies hebt geïnstalleerd, de tagbibliotheek *altijd* wordt geladen voordat de [`load`](https://developer.mozilla.org/en-US/docs/Web/Events/load) browsergebeurtenis.

Houd rekening met het volgende wanneer u deze principes toepast op uw eigen website:

* **Een regel die gebruikmaakt van het gebeurtenistype Bibliotheek Geladen kan worden uitgevoerd voordat de gegevenslaag volledig is geladen.**  Dit kan ertoe leiden dat de handelingen van de regel met ontbrekende gegevens worden uitgevoerd omdat de gegevens nog niet beschikbaar op de pagina waren. Deze soorten kwesties kunnen worden verlicht door uw regelconfiguratie aan te passen. Als voorbeeld, in plaats van het hebben van een regel die door het Bibliotheek Geladen gebeurtenistype wordt teweeggebracht, kon u in plaats daarvan het gebeurtenistype van de Gebeurtenis van de Douane of van de Vraag gebruiken die door uw paginacode worden teweeggebracht zodra uw gegevenslaag het laden beëindigt.
* **Het gebeurtenistype Pagina onder biedt niet in het bijzonder waarde wanneer de bibliotheek asynchroon wordt geladen.**  Overweeg in plaats daarvan de geladen bibliotheek, DOM Ready, Window Loaded of andere gebeurtenistypen.

Als u dingen die uit orde voorkomen ziet, is het waarschijnlijk dat u sommige timingkwesties hebt om door te werken. De plaatsingen die nauwkeurige timing vereisen zouden gebeurtenisluisteraars en het gebeurtenistype van de Gebeurtenis van de Douane of Directe Vraag kunnen moeten gebruiken om hun implementaties robuuster en consistenter te maken.

## De ingesloten code van tags asynchroon laden

Tags bieden een schakeloptie om het asynchroon laden van een insluitcode in te schakelen wanneer u een [milieu](../publishing/environments.md). U kunt het asynchrone laden ook zelf configureren:

1. Voeg een asynchroon attribuut aan toe `<script>` -tag om het script asynchroon te laden.

   Voor de tags die code insluiten, betekent dit dat u de volgende code wijzigt:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js"></script>
   ```

   op dit punt:

   ```markup
   <script src="//www.yoururl.com/launch-EN1a3807879cfd4acdc492427deca6c74e.min.js" async></script>
   ```

1. Verwijder alle code die u eerder onder aan de tag hebt toegevoegd:

   ```markup
   <script type="text/javascript">_satellite.pageBottom();</script>
   ```

   Deze code vertelt Platform dat de browser parser de bodem van de pagina heeft bereikt. Het is waarschijnlijk dat tags niet voor deze tijd zijn geladen en uitgevoerd en daarom `_satellite.pageBottom()` resulteert in een fout en het gebeurtenistype Pagina onder zich gedraagt zich mogelijk niet zoals verwacht.
