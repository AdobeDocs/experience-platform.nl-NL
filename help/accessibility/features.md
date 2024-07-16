---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd;profiel;rtcp;XDM-grafieken
title: Algemene toegankelijkheidsfuncties in platform
type: Documentation
description: Meer informatie over de algemene toegankelijkheidsfuncties die door Adobe Experience Platform worden ondersteund, zoals toetsenbordnavigatie, kleurenpaletten en contrast, en ondersteuning voor ondersteunende hulpmiddelen.
exl-id: 4b7e2f2b-af51-4376-8a63-16c921cc7135
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '481'
ht-degree: 0%

---

# Toegankelijkheidsfuncties in Experience Platform

Adobe Experience Platform streeft ernaar alle individuen toegankelijke en inclusieve functies te bieden, inclusief gebruikers die werken met hulpprogramma&#39;s zoals spraakherkenningssoftware en schermlezers. In dit document worden de algemene toegankelijkheidsfuncties beschreven die door Platform worden ondersteund, zoals toetsenbordnavigatie, semantische structuur, voldoende contrast tussen voorgrondelementen en achtergrondelementen en ondersteuning voor ondersteunende hulpmiddelen.

## Hulptechnologieën

Gebruikers met een handicap vertrouwen vaak op hardware en software, ook wel hulptechnologieën genoemd, om toegang te krijgen tot digitale inhoud en om softwareproducten te gebruiken. Adobe Experience Platform ondersteunt verschillende typen ondersteunende hulpmiddelen (AT), zoals schermlezers, zoomen en spraakherkenningssoftware, door de best practices voor toegankelijkheid te volgen, zoals het gebruik van semantische code, tekstequivalenten, labels en ARIA, waar nodig. Interactieve elementen binnen het gebruikersinterface van het Experience Platform (UI) gebruiken overeenkomstige etiketten, toegankelijke namen, en rollen die zowel hun doel als hun huidige staat identificeren. Zo zorgt u ervoor dat ondersteunende hulpmiddelen, zoals schermlezers, de labels en andere informatie voor gebruikers kunnen lezen, zodat ze gemakkelijk met de besturingselementen van de toepassing kunnen werken.

## Toegankelijkheid toetsenbord

Experience Platform streeft ernaar volledige toetsenbordtoegankelijkheid te ondersteunen.

De volgende navigatie-elementen vergemakkelijken de toegankelijkheid:
* De sleutel van het Lusje beweegt zich tussen elementen UI, secties, en menugroepen.
* Pijltoetsen worden verplaatst binnen menugroepen om focus in te stellen op afzonderlijke actieve elementen.
* Shift + Tab wordt achterwaarts door de tabvolgorde verplaatst.
* Met de toetsen Return (Enter) en Spatiebalk activeert u geselecteerde items.
* De escape-toets (ESC) fungeert als een cancel-knop om een dialoogvenster te sluiten als deze aanwezig is.
* Experience Platform geeft een blauwe rand rond een geselecteerd element weer om een duidelijke indicatie te geven van welk UI-element momenteel focus heeft.

![ een blauwe grens die rond een geselecteerd element verschijnt om erop te wijzen dat de nadruk wordt toegepast.](images/profile-overview-tab.png)

## Kleurenpaletten en contrast

Het Experience Platform streeft voor [ WCAG 2.1 a ](https://www.w3.org/TR/WCAG/) conformiteit, met inbegrip van vereisten voor kleurencontrast na. De gebruikersinterface van het Experience Platform biedt voldoende contrast in de toepassing voor een toegankelijke weergave voor gebruikers met een laag gezichtsvermogen of een laag kleurfalen.

![ het kleurenpalet en het contrast aanwezig op de homepage van Experience Platform UI.](images/homepage.png)

## Veldvalidatie vereist

Wanneer u gegevens toevoegt, schema&#39;s maakt of segmenten definieert, worden vereiste velden zowel visueel, met een sterretje naast het tekstlabel van een veld als programmatisch aangegeven. Deze velden activeren validatie wanneer u ongeldige gegevens in velden invoert en bij het opslaan. Als een vereist veld de validatie niet doorgeeft, wordt dit veld rood weergegeven met een foutpictogram en verschijnt ook een schriftelijke beschrijving van het probleem dat moet worden gecorrigeerd.

![ een close-up van een vereist gebied dat bevestiging niet heeft overgegaan. Het veld wordt rood weergegeven en er is een foutpictogram aanwezig.](images/field-validation.png)
