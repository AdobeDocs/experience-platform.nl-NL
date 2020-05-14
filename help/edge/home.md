---
title: Adobe Experience Platform Web SDK Help
seo-title: Adobe Experience Platform Web SDK Help
description: Leer wat Adobe Experience Platform Web SDK is en hoe deze kan worden gebruikt.
seo-description: klanten van de Adobe Experience Cloud in staat stellen te communiceren met de verschillende services in de Experience Cloud.
translation-type: tm+mt
source-git-commit: f06c90d6248071894bd9929fbe1150e30c8e7385
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%

---


# Wat is Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud via het Adobe Experience Platform Edge Network kunnen communiceren met de verschillende services in de Experience Cloud.

## SDK&#39;s vervangen door Adobe Experience Platform Web SDK

De volgende SDK&#39;s worden vervangen door de Adobe Experience Platform Web SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dit is niet alleen een omslag rond bestaande bibliotheken. Het is een volledige herschrijving. Het doel is een einde te maken aan uitdagingen waarbij tags in de juiste volgorde worden afgevuurd, inconsistentie met bibliotheekversioning en beter afhankelijkheidsbeheer. Het is een nieuwe manier om de Experience Cloud te implementeren en het is een [open source](https://github.com/adobe/alloy)

Naast een nieuwe bibliotheek is er een nieuw eindpunt dat de HTTP-aanvragen naar Adobe-oplossingen stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen AT.js een vraag naar Adobe Target verzond, stuurde DIL.js een vraag naar de Manager van het Publiek van Adobe, en tenslotte stuurde AppMeturement.js een vraag naar de Analytics van Adobe. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een ervaring van het Doel halen, gegevens verzenden naar de Manager van de Publiek, en de gegevens tot het Platform van de Ervaring van Adobe in één enkele vraag overgaan.

## Aan de slag

We raden u ten zeerste aan onze gids [Aan de slag uit te](getting-started/quick-start-with-launch.md) checken voor een korte zelfstudie over hoe u aan de slag kunt gaan.

Dit product ontwikkelt zich voortdurend en groeit om steeds meer gebruiksgevallen te ondersteunen. Om de laatste tijd op de hoogte te blijven, checken we ons [ondersteunde toetsenbord](https://github.com/adobe/alloy/projects/5)uit. Wij houden dit bij met de gebruiksgevallen die wij momenteel steunen en de gevallen waarin wij aan het werk zijn om u in staat te stellen de beste beslissingen te nemen.

* __Gebruik gevallen die nog niet worden ondersteund__ - zijn gebruiksgevallen die op onze routekaart staan en in de toekomst moeten worden afgehandeld.
* __Gevallen van het gebruik Lopend__ - Dit zijn de gebruiksgevallen het team momenteel aan voltooiing voor versie werkt.
* __Ondersteunde gebruiksscenario__ &#39;s - Dit zijn de gebruiksgevallen die worden ondersteund en die vandaag de dag werken.
* __Gebruik gevallen die we niet ondersteunen__ . Dit zijn de gebruiksgevallen die we hebben besloten niet te ondersteunen.
