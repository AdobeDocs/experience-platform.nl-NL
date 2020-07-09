---
title: Help bij Adobe Experience Platform Web SDK
seo-title: Help bij Adobe Experience Platform Web SDK
description: Leer welke SDK van het Web van het Adobe Experience Platform is en hoe het kan worden gebruikt.
seo-description: klanten van de Adobe Experience Cloud in staat stellen te communiceren met de verschillende services in de Experience Cloud.
translation-type: tm+mt
source-git-commit: 9b8bddf39301cdc39bfa5370ef98d99434fc64f8
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# Wat is SDK van het Web van Adobe Experience Platform

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud via het Edge Network van het Adobe Experience Platform kunnen communiceren met de verschillende services in de Experience Cloud.

De volgende video geeft een overzicht van het Web SDK van het Adobe Experience Platform en het Netwerk van de Rand.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDKs die door het Web SDK van het Adobe Experience Platform wordt vervangen

SDK van het Web van het Adobe Experience Platform vervangt de volgende SDKs:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dit is niet alleen een omslag rond bestaande bibliotheken. Het is een volledige herschrijving. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om de Experience Cloud te implementeren en het is een [open bron](https://github.com/adobe/alloy).

Naast een nieuwe bibliotheek is er een nieuw eindpunt dat de HTTP-aanvragen naar Adobe-oplossingen stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen stuurde AT.js een vraag naar Adobe Target, stuurde DIL.js een vraag naar Adobe Audience Manager, en tenslotte stuurde AppMeasurement.js een vraag naar Adobe Analytics. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een [!DNL Target] ervaring halen, gegevens verzenden naar Audience Manager, en de gegevens tot het Adobe Experience Platform in één enkele vraag overgaan.

De volgende video toont SDK van het Web van het Adobe Experience Platform en het Netwerk van de Rand in actie. In het videovoorbeeld wordt één aanroep naar Adobe uitgevoerd die gegevens naar Experience Platform, Analytics, Audience Manager en Target verzendt.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)


## Aan de slag

We raden u ten zeerste aan onze gids [Aan de slag uit te](getting-started/quick-start-with-launch.md) checken voor een korte zelfstudie over hoe u aan de slag kunt met Adobe Launch.

Dit product ontwikkelt zich voortdurend en groeit om steeds meer gebruiksgevallen te ondersteunen. Om de nieuwste ontwikkelingen bij te houden, bekijkt u ons [ondersteunde toetsenbord](https://github.com/adobe/alloy/projects/5). Wij houden dit bij met de gebruiksgevallen die wij momenteel steunen en de gevallen waarin wij aan het werk zijn om u in staat te stellen de beste beslissingen te nemen.

* __Gebruik gevallen die nog niet worden ondersteund__ . Dit zijn gebruiksgevallen die op onze routekaart staan en in de toekomst worden ondersteund.
* __Gevallen van het gebruik Lopend__ - Dit zijn de gebruiksgevallen het team momenteel aan voltooiing voor versie werkt.
* __Ondersteunde gebruiksscenario__ &#39;s - Dit zijn de gebruiksgevallen die worden ondersteund en die vandaag de dag werken.
* __Gebruik gevallen die we niet ondersteunen__ . Dit zijn de gebruiksgevallen die we hebben besloten niet te ondersteunen.
