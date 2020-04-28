---
title: Adobe Experience Platform Web SDK Help
seo-title: Adobe Experience Platform Web SDK Help
description: Leer wat Adobe Experience Platform Web SDK is en hoe deze kan worden gebruikt.
seo-description: klanten van de Adobe Experience Cloud in staat stellen te communiceren met de verschillende services in de Experience Cloud.
translation-type: tm+mt
source-git-commit: 5027ae2cd083631d7122346796ef93572c129d3f

---


# (bètaversie) Wat is de Adobe Experience Platform Web SDK

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud via het Adobe Experience Platform Edge Network kunnen communiceren met de verschillende services in de Experience Cloud.

## SDK&#39;s vervangen door Adobe Experience Platform Web SDK

De volgende SDK&#39;s worden vervangen door de Adobe Experience Platform Web SDK:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dit is niet alleen een omslag rond bestaande bibliotheken. Het is een volledige herschrijving. Het doel is een einde te maken aan uitdagingen waarbij tags in de juiste volgorde worden afgevuurd, inconsistentie met bibliotheekversioning en beter afhankelijkheidsbeheer. Het is een nieuwe manier om de Experience Cloud te implementeren.

Naast een nieuwe bibliotheek is er een nieuw eindpunt dat de HTTP-aanvragen naar Adobe-oplossingen stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen AT.js een vraag naar Adobe Target verzond, stuurde DIL.js een vraag naar de Manager van het Publiek van Adobe, en tenslotte stuurde AppMeturement.js een vraag naar de Analytics van Adobe. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een ervaring van het Doel halen, gegevens verzenden naar de Manager van de Publiek, en de gegevens tot het Platform van de Ervaring van Adobe in één enkele vraag overgaan.