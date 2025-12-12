---
title: Builds
description: Leer meer over het concept van builds en hoe ze binnen Adobe Experience Platform werken.
exl-id: af899282-aa2d-4395-8dbd-18d91be3f041
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '746'
ht-degree: 0%

---

# Builds

Een build is de set bestanden met alle code die op het clientapparaat wordt uitgevoerd.

Het is een samenstelling van de veranderingen u binnen uw bibliotheek specificeerde, evenals alles die is voorgelegd, goedgekeurd, of gepubliceerd vóór het.

De build bestaat uit code-bestanden aan de clientzijde die naar elkaar verwijzen. Deze bestanden worden geleverd op de hostlocatie via de omgeving en host die u voor de bibliotheek hebt gekozen. De code die u op uw site implementeert, verwijst naar dezelfde locatie, zodat de bestanden kunnen worden geladen wanneer een gebruiker toegang verkrijgt tot uw site of toepassing.

## Bestandsinhoud

Een bibliotheek definieert een discrete set tagbronnen (extensies, regels en gegevenselementen) die in de bibliotheek moeten worden opgenomen.

Een bouwstijl bevat alle modulecode (die door de uitbreidingsontwikkelaars wordt verstrekt) en de configuratie (ingegaan door u) die nodig is om de middelen te aandrijven bevat binnen de bibliotheek. Bijvoorbeeld, als een uitbreiding acties verstrekt die niet binnen uw regels worden gebruikt, dan is de code om die acties uit te voeren niet bevat binnen de bouwstijl.

Builds worden verdeeld in het hoofdbibliotheekbestand en mogelijk veel kleinere bestanden. In de insluitcode wordt naar het hoofdbibliotheekbestand verwezen en tijdens runtime op de pagina geladen. Het bevat:

* De regelengine
* Alle extensieconfiguraties
* Alle code en configuratie van gegevenselement
* Alle code en configuratie van regelgebeurtenissen
* Alle voorwaardencode en configuratie
* De code en de configuratie van de gebeurtenis voor om het even welke regels die Bibliotheek Geladen of Pagina onderaan als gebeurtenis hebben (aangezien wij weten wij dat onmiddellijk zullen nodig hebben).

De kleinere bestanden bevatten code en configuratie voor afzonderlijke handelingen die naar wens op de pagina worden geladen. Wanneer een Regel wordt teweeggebracht en zijn Voorwaarden worden geëvalueerd zodat de Acties moeten worden uitgevoerd, worden de noodzakelijke code en de configuratie voor die specifieke actie teruggewonnen van één van de kleinere dossiers. Dit betekent dat alleen de code die nodig is om de vereiste handelingen uit te voeren, ooit op de pagina wordt geladen, waardoor de hoofdbibliotheek zo klein mogelijk wordt.

## Bestandsindeling

De standaardbestandsindeling voor builds is een pakket bestanden met alle vereiste code voor extensies, gegevenselementen en regels die op de gewenste manier worden uitgevoerd.

In bepaalde gevallen hebt u echter de voorkeur aan een zip-archief van de bestanden in plaats van aan het uitvoerbare bestand met code op de client. Bijvoorbeeld, zou u een archief kunnen willen tot stand brengen als u uw bouwstijl zelf host en de bouwstijl in een andere plaatsing wilt gebruiken. Als u iets opgeeft in het zelfgehoste pad naar het bibliotheekveld, kunt u uw omgeving opslaan. Samen met uw nieuwe code, wordt een verbinding aan de gearchiveerde download beschikbaar. Nadat de bibliotheek is gemaakt, kunt u een zip-bestand naar Akamai implementeren en dit downloaden van `assets.adobedtm.com/...` .

>[!NOTE]
>
>Er bestaat niets op die locatie totdat u een build maakt.

Ongeacht de bestandsindeling wordt de build altijd geleverd op de locatie die door de gastheer is opgegeven.

Om een bouwstijl te voltooien, selecteer een bibliotheek en selecteer de optie van de Bouwstijl die op dat niveau van het het publiceren proces beschikbaar is (Bouwstijl voor Ontwikkeling, Bouwstijl voor het Opvoeren, etc.

## Miniatuur

Minificatie verlaagt de bandbreedtekosten en verbetert de snelheid door gegevens te verwijderen die niet vereist zijn voor uitvoering vanuit een bestand.

Om de prestaties te verbeteren, minimaliseert Experience Platform alles, waaronder:

* De hoofdtagbibliotheek
* Modulecode die door extensieontwikkelaars is opgegeven als onderdeel van een extensie
* Aangepaste code verstrekt door Experience Platform-gebruikers

>[!NOTE]
>
>Als de modulecode en de aangepaste code al zijn geminiateerd, wordt deze door Experience Platform opnieuw geminificeerd. Deze tweede minificatie biedt geen extra voordelen, maar het veroorzaakt geen schade en maakt Experience Platform minder complex en eenvoudiger te onderhouden.

Alle gegeven code aan de clientzijde verwijst naar de geminificeerde versie van de code. Dit wordt weergegeven in de bestandsnamen die de standaardnaamgevingsconventie voor geminificeerde bestanden volgen:

`launch-%environment_id%.min.js`

Als u de niet-geminiaterde code wilt zien, verwijdert u .min uit de bestandsnaam:

`launch-%environment_id%.js`

Als een extensieontwikkelaar geminificeerde code met de extensie levert, biedt Experience Platform geen niet-geminiateerde code in de niet-geminiateerde build. Op dezelfde manier als een gebruiker van Experience Platform geminificeerde code in een doos van de douanecode zet, wordt die code nog geminiatuurd in niet-geminiateerde bouwstijlen. Experience Platform maakt niets uit.

Voor meer informatie over minificatie, zie [&#x200B; dit stapelpadartikel &#x200B;](https://blog.stackpath.com/glossary/minification/).

Wanneer het uitvoeren van een bouwstijl zal het eerst de niet-geminiateerde bibliotheek construeren, dan de volledige bibliotheek in één keer minieme.
