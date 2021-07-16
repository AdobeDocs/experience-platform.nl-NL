---
title: Opmerkingen bij de release Common Analytics Plugins Extension
description: De meest recente release bevat de extensie Common Analytics Plugins in Adobe Experience Platform.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 6%

---

# Opmerkingen bij de release Common Analytics Plugins

## 20 mei 2021

### Common Analytics Plugins Extension 3.0.5

#### Opgeloste problemen

* getTimeParting werd niet correct geïnitialiseerd bij gebruik van de generieke initialiseringsactie. Dit probleem is nu opgelost.

## 26 maart 2021

### Common Analytics Plugins Extension 3.0.4

#### Opgeloste problemen

* getPageLoadTime stelde variabelen onjuist in op het vensterobject. Dit probleem is nu opgelost.
* Probleem verholpen waarbij getQueryParam ongedefinieerd werd geretourneerd in plaats van &quot;&quot; als queryParam niet aanwezig was in de queryreeks
* Probleem verholpen waarbij onjuiste versienummers werden weergegeven in de initialisatiehandeling

## 19 maart 2021

### Common Analytics Plugins Extension 3.0.2

#### Functies

* Alle plug-ins die automatisch worden bijgewerkt om versiegegevens op te nemen als contextgegevens
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

## 9 april 2020

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
* Probleem verholpen waarbij `getTimeSinceLastVisit` tweemaal verscheen in de initialiseringsactie

## 15 november 2019

### Common Analytics Plugins Extension 2.1.0

#### Opgeloste problemen

* Nieuwe insteekacties voor afzonderlijke insteekmodules ter ondersteuning van achterwaartse compatibiliteit
* Probleem verholpen met de `cleanStr`-plug-in
* Probleem verholpen met de `getResponsiveLayout`-plug-in
* Probleem verholpen met de `getPageName`-plug-in

#### Functies

* Versie-update voor `getTimeParting`
* Versie-update voor `numberSuite`
* Versie-update voor `getNewRepeat`
* Bijgewerkte documentatie voor alle plug-ins

## 30 oktober 2019

### Common Analytics Plugins Extension 2.0.3

#### Opgeloste problemen

* Probleem verholpen waarbij documentatiekoppelingen werden verbroken

## 11 oktober 2019

### Common Analytics Plugins Extension 2.0.2

#### Functies

* 15 plug-ins toegevoegd aan de extensie
* Nieuwe initialiseringsactie gemaakt om een betere implementatie te ondersteunen

## 11 juli 2019

### Common Analytics Plugins Extension 1.0.4

#### Functies

* Extensie is vrijgegeven met zeven plug-ins
* Afzonderlijke acties om elke insteekmodule te initialiseren
