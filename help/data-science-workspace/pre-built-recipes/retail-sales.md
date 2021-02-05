---
keywords: Experience Platform;winkelrecept;Data Science Workspace;populaire onderwerpen;recepten;prebuild recept
solution: Experience Platform
title: Recipe detailhandel
topic: overview
description: Met het recept voor detailhandel kunt u de verkoopprognose voor alle winkels die gedurende een bepaalde periode worden ingezaaid, voorspellen. Met een accuraat voorspellingsmodel zou de detailhandelaar de relatie tussen vraag en prijsbeleid kunnen vinden en geoptimaliseerde prijsbeslissingen kunnen nemen om verkoop en inkomsten te maximaliseren.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '585'
ht-degree: 0%

---


# Detailhandelrecept

Met het recept voor detailhandel kunt u de verkoopprognose voor alle winkels die gedurende een bepaalde periode worden ingezaaid, voorspellen. Met een accuraat voorspellingsmodel zou de detailhandelaar de relatie tussen vraag en prijsbeleid kunnen vinden en geoptimaliseerde prijsbeslissingen kunnen nemen om verkoop en inkomsten te maximaliseren.

Het volgende document zal vragen zoals beantwoorden:
* Voor wie is dit recept gebouwd?
* Wat doet dit recept?
* Hoe begin ik?

## Voor wie is dit recept gebouwd?

Een detailhandelaar staat voor vele uitdagingen om concurrerend te blijven op de huidige markt. Uw merk probeert de jaarlijkse verkoop voor uw merk in de detailhandel te verhogen, maar er zijn veel beslissingen om uw bedrijfskosten te minimaliseren. Te veel levering verhoogt voorraadkosten terwijl te weinig levering het risico verhoogt om klanten aan andere merken te verliezen. Moet u de komende maanden meer voorraad bestellen? Hoe bepaalt u de optimale prijs voor uw producten om wekelijkse verkoopdoelstellingen te handhaven?

## Wat doet dit recept?

In het recept Verkoopprognose voor detailhandel wordt machinaal leren gebruikt om verkooptrends te voorspellen. Het recept doet dit door gebruik te maken van de rijkdom aan historische detailhandelsgegevens en een aangepast algoritme voor het stimuleren van het regressorleren van machines om de verkoop een week van tevoren te voorspellen. Het model maakt gebruik van de aankoopgeschiedenis in het verleden en is standaard ingesteld op vooraf bepaalde configuratieparameters die zijn bepaald door onze Data Scientists om de voorspellende nauwkeurigheid te verbeteren.

## Hoe begin ik?

U kunt beginnen door dit [leerprogramma](../jupyterlab/create-a-recipe.md) te volgen.

Deze zelfstudie gaat over het maken van het recept voor detailhandel in een Jupyter-laptop en het gebruik van de laptop voor het recept-workflow om het recept in Adobe Experience Platform te maken.

## Gegevensschema

Dit recept gebruikt [XDM schema&#39;s](../../xdm/schema/field-dictionary.md) om de gegevens te modelleren. Het schema dat voor dit recept wordt gebruikt wordt hieronder getoond:

| Veldnaam | Type |
--- | ---
| date | Tekenreeks |
| winkel | Geheel |
| storeType | Tekenreeks |
| wekelijkseVerkoop | Getal |
| storeSize | Geheel |
| temperatuur | Getal |
| RegionalFuelPrice | Getal |
| markeren | Getal |
| cpi | Getal |
| werkloosheid | Getal |
| isHoliday | Boolean |


## Algorithm

Eerst, wordt de trainingsdataset in het *DSWRetailSales* schema geladen. Vanaf hier wordt het model getraind met behulp van een [algoritme voor het verhogen van het verloop](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Bij het verhogen van het verloop wordt ervan uitgegaan dat zwakke studenten (een die minstens iets beter is dan een willekeurige kans) een opvolging van studenten kunnen vormen die zich richten op het verbeteren van de zwakheden van de vorige leerling. Samen kunnen ze worden gebruikt om een krachtig voorspellend model te maken.

Het proces omvat drie elementen: een verliesfunctie, een zwakke leerling en een additief model.

De verliesfunctie verwijst naar een maat van hoe goed een voorspellingsmodel doet in termen van het kunnen voorspellen van het verwachte resultaat - de minste vierkantsregressie wordt in dit recept gebruikt.

Bij het verhogen van het verloop wordt een beslissingsstructuur gebruikt als de zwakke leerling. Normaal gesproken worden structuren met een beperkt aantal lagen, knooppunten en splitsingen gebruikt om ervoor te zorgen dat de leerling zwak blijft.

Ten slotte wordt een additief model gebruikt. Na het berekenen van het verlies met de verliesfunctie wordt de boom die het verlies vermindert gekozen en gewogen om het modelleren van de lastigste waarnemingen te verbeteren. De productie van de gewogen boom wordt vervolgens toegevoegd aan de bestaande reeks bomen om de uiteindelijke productie van het model te verbeteren - de hoeveelheid van de toekomstige verkoop.