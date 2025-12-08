---
title: Overzicht van de Web SDK JavaScript-bibliotheek
description: Gegevens verzenden naar de Adobe Experience Platform Edge Network met JavaScript.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f932e9868e84cf8abdaa6cf0b2da5bac837234d
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# Overzicht van de Web SDK JavaScript-bibliotheek

**SDK van het Web van Adobe Experience Platform** is een cliënt-kant bibliotheek van JavaScript die u toestaat om gegevens naar Adobe Experience Platform Edge Network te verzenden. Deze gids documenteert de de bibliotheek van SDK van het Web JavaScript (`alloy.js`) implementatiepad, met inbegrip van kernconcepten, installatie, configuratie, en bevelen. Voor de de markeringsuitbreiding van SDK van het Web in UI van de Inzameling van Gegevens, zie de [&#x200B; de markeringsuitbreiding van SDK van het Web &#x200B;](/help/tags/extensions/client/web-sdk/overview.md).

Het Web SDK verzendt gegevens op een oplossing-agnostische manier (XDM) naar Experience Platform Edge Network, die dan de gegevens aan oplossing-specifieke formaten en bestemmingen in real time in kaart brengt en het verzendt.

## Experience Platform Edge Network {#edge-network}

De Adobe Experience Platform Edge Network biedt gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen. Het biedt één geconsolideerde SDK voor web, mobiel, en server-zijkanalen, die gegevens naar een gemeenschappelijk domein van Adobe (`adobedc.net`) verzenden en één enkele lading voor gegevens en ervaringslevering ontvangen.

Op de server-kant, vereenvoudigen een verenigde randgateway en een gemeenschappelijk kader van de platformdienst de plaatsing van nieuwe mogelijkheden, terwijl het verstrekken van de volgende voordelen:

* verkort de tijd van de klant aan waarde;
* de noodzaak van &quot;point&quot;-integratie te beëindigen;
* Verbetering van de prestaties in vergelijking met de oude bibliotheken;
* verlaging van de exploitatiekosten;
* de innovatiesnelheid verhogen;
* Aanhoudende concurrentievoordelen voor Adobe-klanten.

Met een geconsolideerd Edge-systeem kunt u reclame-, marketing- en personalisatiecampagnes op alle kanalen beheren. Dit verlaagt de totale eigendomskosten en ondersteunt verschillende gegevenstypen, zodat u uw gegevensmodel kunt toewijzen voor gebruik met meerdere Experience Cloud-producten.

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotheken die worden vervangen door de Web SDK {#sdks}

De Web SDK is een geheel nieuwe opensource-bibliotheek waarin functies van bestaande bibliotheken kunnen worden geïntegreerd. Er worden problemen opgelost met de volgorde waarin de tags worden geactiveerd, inconsistenties in de versie en het beheer van afhankelijkheden, waardoor een manier wordt geboden om veel Experience Cloud-producten te implementeren. Web SDK vervangt gegevensinzameling voor de volgende diensten:

* Adobe Experience Platform Visitor ID-service (`Visitor.js`)
* Adobe Analytics (`AppMeasurement.js`)
* Adobe Target (`AT.js`)
* Adobe Audience Manager (`DIL.js`)
* Adobe Media Analytics
* Adobe Advertising

Het introduceert ook een nieuw eindpunt dat HTTP- verzoeken aan de oplossingen van Adobe stroomlijnt. Eerder, waren de veelvoudige vraag nodig voor elke bibliotheek van de gegevensinzameling. Met één aanroep kan nu een id worden opgehaald, een [!DNL Target] -ervaring worden opgehaald, gegevens worden verzonden naar [!DNL Audience Manager] en gegevens worden doorgegeven aan Adobe Experience Platform.

## Migreren van bestaande bibliotheken naar Web SDK {#migrating-to-web-sdk}

Adobe biedt een gestroomlijnd upgradepad om de migratie van bestaande bibliotheken naar de Web SDK te vereenvoudigen. U kunt elke pagina van uw website afzonderlijk migreren zonder dat u de gehele site tegelijk hoeft te migreren. U kunt de Web SDK op sommige pagina&#39;s gebruiken terwijl de bestaande bibliotheken op anderen blijven, die voor een geleidelijke overgang toestaan.
