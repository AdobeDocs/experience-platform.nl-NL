---
keywords: Experience Platform;kleinhandelsrecept;Data Science Workspace;populaire onderwerpen;recepten;prebuild recept
solution: Experience Platform
title: Recipe detailhandel
description: Met het recept voor detailhandel kunt u de verkoopprognose voor alle winkels die gedurende een bepaalde periode worden ingezaaid, voorspellen. Met een accuraat voorspellingsmodel zou de detailhandelaar de relatie tussen vraag en prijsbeleid kunnen vinden en geoptimaliseerde prijsbeslissingen kunnen nemen om verkoop en inkomsten te maximaliseren.
exl-id: ff01fcd1-fca6-4957-8470-a974fd1520aa
source-git-commit: 5d98dc0cbfaf3d17c909464311a33a03ea77f237
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---

# Detailhandelrecept

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft.
>
>Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Met het recept voor detailhandel kunt u de verkoopprognose voor alle winkels die gedurende een bepaalde periode worden ingezaaid, voorspellen. Met een accuraat voorspellingsmodel zou de detailhandelaar de relatie tussen vraag en prijsbeleid kunnen vinden en geoptimaliseerde prijsbeslissingen kunnen nemen om verkoop en inkomsten te maximaliseren.

Het volgende document zal vragen zoals beantwoorden:
* Voor wie is dit recept gebouwd?
* Wat doet dit recept?
* Hoe begin ik?

## Voor wie is dit recept gebouwd?

Een detailhandelaar staat voor vele uitdagingen om concurrerend te blijven op de huidige markt. Uw merk probeert de jaarlijkse verkoop voor uw merk in de detailhandel te verhogen, maar er zijn veel beslissingen om uw bedrijfskosten tot een minimum te beperken. Te veel levering verhoogt voorraadkosten terwijl te weinig levering het risico verhoogt om klanten aan andere merken te verliezen. Moet u voor de komende maanden meer voorraad bestellen? Hoe bepaal je de optimale prijs voor je producten om de wekelijkse verkoopdoelen te handhaven?

## Wat doet dit recept?

Het Retail Sales Forecasting-recept maakt gebruik van machine learning om trends in de verkoop te voorspellen. Het recept doet dit door gebruik te maken van de rijkdom aan historische detailhandelsgegevens en een aangepast gradient boosting regresor machine learning algoritme om de verkoop een week van tevoren te voorspellen. Het model maakt gebruik van eerdere aankoopgeschiedenis en van vooraf bepaalde configuratieparameters die door onze Data Scientists zijn bepaald om voorspellende nauwkeurigheid te verbeteren.

## Hoe ga ik aan de slag?

U kunt begonnen worden door dit [&#x200B; leerprogramma &#x200B;](../jupyterlab/create-a-model.md) te volgen.

Deze zelfstudie gaat over het maken van het recept voor detailhandel in een Jupyter-laptop en het gebruik van de laptop voor het recept-workflow om het recept in Adobe Experience Platform te maken.

## Gegevensschema

Dit recept gebruikt [&#x200B; schema&#39;s XDM &#x200B;](../../xdm/schema/field-dictionary.md) om de gegevens te modelleren. Het schema dat voor dit recept wordt gebruikt wordt hieronder getoond:

| Veldnaam | Type |
| --- | --- |
| date | String |
| winkel | Geheel |
| storeType | Tekenreeks |
| wekelijkseVerkoop | Getal |
| storeSize | Geheel |
| temperatuur | Getal |
| RegionalFuelPrice | Getal |
| markdown | Getal |
| cpi | Getal |
| werkloosheid | Getal |
| isHoliday | Boolean |


## Algorithm

Eerst, wordt de opleidingsdataset in het *DSWRetailSales* schema geladen. Van hier, wordt het model getraind gebruikend a [&#x200B; gradiënt die regressoralgoritme opvoert &#x200B;](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html). Bij het verhogen van het verloop wordt ervan uitgegaan dat zwakke studenten (een die minstens iets beter is dan een willekeurige kans) een opvolging van studenten kunnen vormen die zich richten op het verbeteren van de zwakheden van de vorige leerling. Samen kunnen ze worden gebruikt om een krachtig voorspellend model te maken.

Het proces bestaat uit drie elementen: een verliesfunctie, een zwakke leerling en een additief model.

De verliesfunctie verwijst naar een maat van hoe goed een voorspellingsmodel doet in termen van het kunnen voorspellen van het verwachte resultaat - minst kwadratenregressie wordt in dit recept gebruikt.

Bij verloopboosting wordt een beslissingsstructuur gebruikt als de zwakke student. Normaal gesproken worden bomen met een beperkt aantal lagen, knooppunten en splitsingen gebruikt om ervoor te zorgen dat de student zwak blijft.

Ten slotte wordt een additief model gebruikt. Na het berekenen van het verlies met de verliesfunctie wordt de boom die het verlies vermindert gekozen en gewogen om de moeilijker waarneming beter te modelleren. De productie van de gewogen boom wordt vervolgens toegevoegd aan de bestaande reeks bomen om de uiteindelijke productie van het model te verbeteren - hoeveelheid van de toekomstige verkoop.
