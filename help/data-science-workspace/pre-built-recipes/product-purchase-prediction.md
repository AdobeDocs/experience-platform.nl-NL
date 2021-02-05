---
keywords: Experience Platform;product aankoop recept;Data Science Workspace;populaire onderwerpen;recepten;pre-build recept
solution: Experience Platform
title: Recipe voor productaankoopprognose
topic: overview
description: Met het product Purchase Prediction recipe kunt u de waarschijnlijkheid voorspellen van een bepaald type aankoopgebeurtenis van de klant, bijvoorbeeld een aankoop van een product.
translation-type: tm+mt
source-git-commit: f4095a90ff70e8d054bae4f3b0f884552ffd30df
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 2%

---


# Voorspelrecept voor productaankoop

Met het product Purchase Prediction recipe kunt u de waarschijnlijkheid voorspellen van een bepaald type aankoopgebeurtenis van de klant, bijvoorbeeld een aankoop van een product.

![](../images/pre-built-recipes/ppp_bigpicture.png)

Het volgende document zal vragen zoals beantwoorden:
* Voor wie is dit recept gebouwd?
* Wat doet dit recept?

## Voor wie is dit recept gebouwd?

Uw merk streeft ernaar de driemaandelijkse verkoop voor uw productlijn door efficiënte en gerichte bevorderingen aan uw klanten te bevorderen. Maar niet alle klanten zijn gelijk en u wilt de waarde van uw geld. Waarop richt u zich? Welke van uw klanten zeer waarschijnlijk zullen antwoorden zonder uw bevordering indringend te vinden? Hoe kunt u uw aanbiedingen aan elke klant aanpassen? Op welke kanalen moet u vertrouwen en wanneer moet u promoties sturen?

## Wat doet dit recept?

Het product Purchase Prediction recipe maakt gebruik van machinaal leren om het gedrag van klanten bij aankopen te voorspellen. Het doet dit door een aangepaste willekeurige bosclassificator en een twee-tiered Model van de Gegevens van de Ervaring (XDM) toe te passen om de waarschijnlijkheid van een koopgebeurtenis te voorspellen. Het model gebruikt inputgegevens die de informatie van het klantenprofiel en vroegere aankoopgeschiedenis omvatten en gebreken aan vooraf bepaalde configuratieparameters die door onze Wetenschappers van Gegevens worden bepaald om voorspellende nauwkeurigheid te verbeteren.

## Gegevensschema

Dit recept gebruikt [XDM schema&#39;s](../../xdm/home.md) om de gegevens te modelleren. Het schema dat voor dit recept wordt gebruikt wordt hieronder getoond:

| Veldnaam | Type |
--- | ---
| userId | Tekenreeks |
| genderRatio | Getal |
| ageY | Getal |
| ageM | Getal |
| optionEmail | Boolean |
| OptionMobile | Boolean |
| optinAddress | Boolean |
| gemaakt | Geheel |
| totalOrders | Getal |
| totalItems | Getal |
| orderDate1 | Getal |
| ShippingDate1 | Getal |
| totalPrice1 | Getal |
| tax1 | Getal |
| orderDate2 | Getal |
| ShippingDate2 | Getal |
| totalPrice2 | Getal |


## Algorithm

Eerst, wordt de trainingsdataset in het *schema ProductPrediction* geladen. Van hier, wordt het model getraind gebruikend een [willekeurige bosclassificator](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestClassifier.html). Random forest classifier is een type gecodeerd algoritme dat verwijst naar een algoritme dat meerdere algoritmen combineert om betere voorspellende prestaties te verkrijgen. Het idee achter het algoritme is dat de willekeurige bosclassificator veelvoudige besluitvormingsbomen bouwt en hen samenvoegt om een nauwkeurigere en stabielere voorspelling tot stand te brengen.

Dit proces begint met het maken van een reeks beslissingsstructuren die willekeurig subsets van trainingsgegevens selecteren. Daarna wordt het gemiddelde van de resultaten van elke beslissingsboom genomen.