---
title: Opmerkingen bij de release Common Analytics Plugins Extension
description: De meest recente release bevat de extensie Common Analytics Plugins in Adobe Experience Platform.
exl-id: 5ea4b709-4e21-4f5d-be99-e72e4889ed99
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 2%

---

# Opmerkingen bij de release Common Analytics Plugins

## zaterdag 3 juni 2022

### Common Analytics Plugins Extension 3.0.7

#### Functies

* Insteekmodules die cookies instellen, gebruiken nu de beveiligde markering

## donderdag 23 juni 2021

### Common Analytics Plugins Extension 3.0.6

#### Opgeloste problemen

* getPercentPageViewed werd afgebroken bij gebruik van speciale tekens. Dit probleem is nu opgelost.

## vrijdag 20 mei 2021

### Common Analytics Plugins Extension 3.0.5

#### Opgeloste problemen

* getTimeParting werd niet correct geïnitialiseerd bij gebruik van de generieke initialiseringsactie. Dit probleem is nu opgelost.

## zaterdag 26 maart 2021

### Common Analytics Plugins Extension 3.0.4

#### Opgeloste problemen

* getPageLoadTime stelde variabelen onjuist in op het vensterobject. Dit probleem is nu opgelost.
* Probleem verholpen waarbij getQueryParam ongedefinieerd werd geretourneerd in plaats van &quot;&quot; als queryParam niet aanwezig was in de queryreeks
* Probleem verholpen waarbij onjuiste versienummers werden weergegeven in de initialisatiehandeling

## zaterdag 19 maart 2021

### Common Analytics Plugins Extension 3.0.2

#### Functies

* Alle plug-ins die automatisch worden bijgewerkt, bevatten versiegegevens als contextgegevens
* Toegevoegde getPercentPageViewed-plug-in
* Gegevenselementen toegevoegd voor de volgende plug-ins
   * getGeoCoordinates
   * getNewRepeat
   * getPageName
   * getResponsiveLayout
   * getTimeParting
   * getTimeSinceLastVisit
   * getVisitDuration
   * getVisitNum
* Bijgewerkte stijlen

## vrijdag 9 april 2020

### Common Analytics Plugins Extension 2.2.0

#### Opgeloste problemen

* Vaste formulering in de verlengingsweergave

#### Functies

* Bijgewerkte documentatie in initialiseert actie

## 5 december 2019

### Common Analytics Plugins Extension 2.1.1

#### Opgeloste problemen

* Probleem verholpen waardoor compatibiliteit met versie 2.0.X met oudere versies werd voorkomen
* Documentkoppelingen wezen op onjuiste documentatie. Dit probleem is nu opgelost.
* Probleem verholpen waarbij `getTimeSinceLastVisit` twee keer werd weergegeven in de initialisatieactie. Dit probleem is nu opgelost.

## 15 november 2019

### Common Analytics Plugins Extension 2.1.0

#### Opgeloste problemen

* Nieuwe insteekacties voor afzonderlijke insteekmodules ter ondersteuning van achterwaartse compatibiliteit
* Probleem verholpen met de `cleanStr` -plug-in
* Probleem verholpen met de `getResponsiveLayout` -plug-in
* Probleem verholpen met de `getPageName` -plug-in

#### Functies

* Versie-update voor `getTimeParting`
* Versie-update voor `numberSuite`
* Versie-update voor `getNewRepeat`
* Bijgewerkte documentatie voor alle plug-ins

## donderdag 30 oktober 2019

### Common Analytics Plugins Extension 2.0.3

#### Opgeloste problemen

* Probleem verholpen waarbij documentatiekoppelingen werden verbroken

## zaterdag 11 oktober 2019

### Common Analytics Plugins Extension 2.0.2

#### Functies

* 15 plug-ins toegevoegd aan de extensie
* Nieuwe initialiseringsactie gemaakt om een betere implementatie te ondersteunen

## vrijdag 11 juli 2019

### Common Analytics Plugins Extension 1.0.4

#### Functies

* Extensie is vrijgegeven met zeven plug-ins
* Afzonderlijke acties om elke insteekmodule te initialiseren
