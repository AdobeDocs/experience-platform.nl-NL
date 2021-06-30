---
keywords: Experience Platform;profiel;realtime klantprofiel;problemen;API;verenigd profiel;verenigd profiel;verenigd;profiel;rtcp;XDM-grafieken
title: Algemene toegankelijkheidsfuncties in Platform
topic-legacy: guide
type: Documentation
description: Meer informatie over de algemene toegankelijkheidsfuncties die door Adobe Experience Platform worden ondersteund, zoals toetsenbordnavigatie, kleurenpaletten en contrast, en ondersteuning voor ondersteunende hulpmiddelen.
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 1%

---


# Toegankelijkheidsfuncties in Experience Platform

Adobe Experience Platform streeft ernaar alle individuen toegankelijke en inclusieve functies te bieden, inclusief gebruikers die werken met hulpprogramma&#39;s zoals spraakherkenningssoftware en schermlezers. In dit document worden de algemene toegankelijkheidsfuncties beschreven die door het Platform worden ondersteund, zoals toetsenbordnavigatie, semantische structuur, voldoende contrast tussen voorgrondelementen en achtergrondelementen en ondersteuning voor ondersteunende hulpmiddelen.

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

![Een blauwe rand rondom een geselecteerd element om aan te geven dat focus is toegepast.](images/profile-overview-tab.png)

## Kleurenpaletten en contrast

Experience Platform streeft naar [WCAG 2.1 AA](https://www.w3.org/TR/WCAG/)-conformiteit, inclusief vereisten voor kleurcontrast. De gebruikersinterface van het Experience Platform biedt voldoende contrast in de toepassing voor een toegankelijke weergave voor gebruikers met een laag gezichtsvermogen of een laag kleurfalen.

![Het kleurenpalet en het contrast aanwezig op de homepage van de interface van het Experience Platform.](images/homepage.png)

## Veldvalidatie vereist

Wanneer u gegevens toevoegt, schema&#39;s maakt of segmenten definieert, worden vereiste velden zowel visueel, met een sterretje naast het tekstlabel van een veld als programmatisch aangegeven. Deze velden activeren validatie wanneer u ongeldige gegevens in velden invoert en bij het opslaan. Als een vereist veld de validatie niet doorgeeft, wordt dit veld rood weergegeven met een foutpictogram en verschijnt ook een schriftelijke beschrijving van het probleem dat moet worden gecorrigeerd.

![Een close-up van een vereist veld waarvoor de validatie niet is geslaagd. Het veld wordt rood weergegeven en er is een foutpictogram aanwezig.](images/field-validation.png)