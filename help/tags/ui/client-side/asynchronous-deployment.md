---
title: Asynchrone implementatie
description: Leer hoe u Adobe Experience Platform-tagbibliotheken asynchroon op uw website kunt implementeren.
exl-id: ed117d3a-7370-42aa-9bc9-2a01b8e7794e
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1001'
ht-degree: 0%

---

# Asynchrone implementatie {#asynchronous-deployment}

>[!CONTEXTUALHELP]
>id="platform_tags_asynchronous_deployment"
>title="Asynchrone implementatie"
>abstract="Als deze optie is ingeschakeld, zal de browser bij het parseren van deze scripttag beginnen met het laden van het JavaScript-bestand, maar in plaats van te wachten tot de bibliotheek is geladen en uitgevoerd, de rest van het document blijven parseren en renderen. Dit kan de prestaties van webpagina&#39;s verbeteren, maar heeft belangrijke gevolgen voor de manier waarop bepaalde regels worden uitgevoerd. Raadpleeg de documentatie voor meer informatie."

Prestaties en het niet blokkeren van de implementatie van de JavaScript-bibliotheken die onze producten vereisen, worden steeds belangrijker voor Adobe Experience Cloud-gebruikers. Gereedschappen zoals [[!DNL Google PageSpeed] &#x200B;](https://developers.google.com/speed/pagespeed/insights/) raden gebruikers aan hun manier van implementatie van de Adobe-bibliotheken op hun site te wijzigen. In dit artikel wordt uitgelegd hoe u de Adobe JavaScript-bibliotheken asynchroon kunt gebruiken.

## Synchroon versus asynchroon

### Synchrone implementatie

Bibliotheken worden vaak synchroon geladen in de tag `<head>` van een pagina. Bijvoorbeeld:

```markup
<script src="example.js"></script>
```

Standaard parseert de browser het document en bereikt deze regel. Vervolgens haalt de browser het JavaScript-bestand op van de server. De browser wacht tot het bestand is geretourneerd, parseert het bestand en voert het uit. Tot slot wordt de rest van het HTML-document nog steeds geparseerd.

Als de parser de tag `<script>` tegenkomt voordat zichtbare inhoud wordt gerenderd, wordt de weergave van de inhoud vertraagd. Als het JavaScript-bestand dat wordt geladen niet absoluut noodzakelijk is om inhoud aan uw gebruikers weer te geven, hebt u uw bezoekers onnodig gevraagd om op inhoud te wachten. Hoe groter de bibliotheek, des te langer de vertraging.  Daarom markeren benchmarkgereedschappen voor websiteprestaties zoals [!DNL Google PageSpeed] of [!DNL Lighthouse] vaak synchroon geladen scripts.

Tagbeheerbibliotheken kunnen snel groter worden als u veel tags moet beheren.

### Asynchrone implementatie

U kunt elke bibliotheek asynchroon laden door een `async` -kenmerk toe te voegen aan de `<script>` -tag. Bijvoorbeeld:

```markup
<script src="example.js" async></script>
```

Dit geeft aan de browser aan dat wanneer deze scripttag wordt geparseerd, de browser moet beginnen met het laden van het JavaScript-bestand. In plaats van te wachten tot de bibliotheek is geladen en uitgevoerd, moet de browser de rest van het document blijven parseren en renderen.

## Overwegingen bij asynchrone implementatie

Zoals hierboven beschreven, pauzeert de browser bij synchrone implementaties het parseren en renderen van de pagina terwijl de Adobe Experience Platform-tagbibliotheek wordt geladen en uitgevoerd. Bij asynchrone implementaties parseert en rendert de browser de pagina terwijl de bibliotheek wordt geladen. Er moet rekening worden gehouden met de variabiliteit van het tijdstip waarop de tagbibliotheek kan zijn geladen ten opzichte van het parseren en renderen van pagina&#39;s.

Ten eerste, omdat de tagbibliotheek al kan worden geladen voordat of nadat de onderkant van de pagina is geparseerd en uitgevoerd, moet u `_satellite.pageBottom()` niet meer aanroepen vanuit de paginacode (`_satellite` is pas beschikbaar nadat de bibliotheek is geladen). Dit wordt verklaard in [&#x200B; Lading de markeringen inbedden asynchroon code &#x200B;](#loading-the-tags-embed-code-asynchronously).

Ten tweede kan de tagbibliotheek klaar zijn met laden voor of nadat de [`DOMContentLoaded` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) browser-gebeurtenis (DOM Ready) is opgetreden.

Wegens deze twee punten, is het de moeite waard om aan te tonen hoe de [&#x200B; Geladen Bibliotheek &#x200B;](../../extensions/client/core/overview.md#library-loaded-page-top), [&#x200B; Onderkant van de Pagina &#x200B;](../../extensions/client/core/overview.md#page-bottom), [&#x200B; Klaar DOM &#x200B;](../../extensions/client/core/overview.md#page-bottom), en [&#x200B; Venster &#x200B;](../../extensions/client/core/overview.md#window-loaded) gebeurtenistypen van de de uitbreidingsfunctie van de Kern wanneer het laden van een markeringsbibliotheek asynchroon.

Als de eigenschap tag de volgende vier regels bevat:

* Regel A: gebruikt het bibliotheekgeladen gebeurtenistype
* Regel B: gebruikt het gebeurtenistype Pagina onder
* Regel C: gebruikt het DOM Klaar gebeurtenistype
* Regel D: gebruikt het gebeurtenistype Window Loaded

Ongeacht wanneer het laden van de tagbibliotheek is voltooid, worden alle regels gegarandeerd uitgevoerd en worden ze in de volgende volgorde uitgevoerd:

Regel A → Regel B → Regel C → Regel D

Hoewel de volgorde altijd wordt gehandhaafd, kunnen sommige regels direct worden uitgevoerd wanneer de tagbibliotheek klaar is met laden, terwijl andere later wellicht worden uitgevoerd. Het volgende gebeurt wanneer de tagbibliotheek klaar is met laden:

1. Regel A wordt onmiddellijk uitgevoerd.
1. Als de browsergebeurtenis `DOMContentLoaded` (DOM Ready) al heeft plaatsgevonden, worden de regels B en C direct uitgevoerd. Anders, worden Regel B en Regel C uitgevoerd later wanneer de [`DOMContentLoaded` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/Events/DOMContentLoaded) browser gebeurtenis voorkomt.
1. Als de [`load` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/Events/load) browser gebeurtenis (Venster Geladen) reeds voorkwam, wordt Regel D uitgevoerd onmiddellijk. Anders, zal Regel D later worden uitgevoerd wanneer de [`load` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/Events/load) browser gebeurtenis voorkomt. Merk op dat als u de markeringsbibliotheek volgens de instructies hebt geïnstalleerd, de markeringsbibliotheek *altijd* klaar is ladend alvorens de [`load` &#x200B;](https://developer.mozilla.org/en-US/docs/Web/Events/load) browser gebeurtenis voorkomt.

Houd rekening met het volgende wanneer u deze principes toepast op uw eigen website:

* **een regel die de Bibliotheek Geladen gebeurtenistype gebruikt zou kunnen uitvoeren alvorens uw gegevenslaag volledig wordt geladen.** Dit kan ertoe leiden dat de handelingen van de regel worden uitgevoerd met ontbrekende gegevens omdat de gegevens nog niet beschikbaar waren op de pagina. Deze soorten kwesties kunnen worden verlicht door uw regelconfiguratie aan te passen. Als voorbeeld, in plaats van het hebben van een regel die door het Bibliotheek Geladen gebeurtenistype wordt teweeggebracht, kon u in plaats daarvan het gebeurtenistype van de Gebeurtenis van de Douane of van de Vraag gebruiken die door uw paginacode worden teweeggebracht zodra uw gegevenslaag het laden beëindigt.
* **het de gebeurtenistype van de Onderkant van de Pagina verstrekt met name geen waarde wanneer de bibliotheek asynchroon wordt geladen.** Overweeg in plaats daarvan de Bibliotheek Geladen, Klaar DOM, Venster Geladen, of andere gebeurtenistypen.

Als u dingen die uit orde voorkomen ziet, is het waarschijnlijk dat u sommige timingkwesties hebt om door te werken. De plaatsingen die nauwkeurige timing vereisen zouden gebeurtenisluisteraars en het gebeurtenistype van de Gebeurtenis van de Douane of Directe Vraag kunnen moeten gebruiken om hun implementaties robuuster en consistenter te maken.

## De ingesloten code van tags asynchroon laden

De markeringen verstrekken een knevel om asynchrone lading aan te zetten wanneer het creëren van inbedcode wanneer u een [&#x200B; milieu &#x200B;](../publishing/environments.md) vormt. U kunt het asynchrone laden ook zelf configureren:

1. Voeg een asynchroon kenmerk toe aan de tag `<script>` om het script asynchroon te laden.

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

   Deze code vertelt Experience Platform dat de parser van de browser de bodem van de pagina heeft bereikt. Het is waarschijnlijk dat tags niet voor deze tijd zijn geladen en uitgevoerd, dus het aanroepen van `_satellite.pageBottom()` resulteert in een fout en het gebeurtenistype Pagina onder werkt mogelijk niet zoals verwacht.
