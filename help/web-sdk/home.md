---
title: Adobe Experience Platform Web Software Development Kit (SDK) - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK gebruikt om de mogelijkheden van het platform in uw website te integreren.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 58cd6300307881c3de7c52e07c401bf2ed908517
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 1%

---


# Adobe Experience Platform Web SDK {#overview}

>[!IMPORTANT]
>
>Eind april 2024 zal de SDK van het Web van Adobe Experience Platform steun voor alle versies van Internet Explorer verwijderen.

De Adobe Experience Platform Web Software Development Kit (SDK) is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud via het Adobe Experience Platform Edge Network kunnen communiceren met hun services.

De Adobe biedt twee methodes aan om Web SDK uit te voeren:

* De [Web SDK-tagextensie](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Bekijk de zelfstudie over hoe u [Adobe Experience Cloud implementeren met Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) voor meer informatie .
* Handmatige implementatie met de Web SDK JavaScript-bibliotheek.

Deze gebruikershandleiding bevat instructies voor het werken met de oplossingen voor Experiencen Cloud via zowel de Web SDK JavaScript-bibliotheek als de tagextensie, indien van toepassing.

## Experience Platform Edge Network {#edge-network}

De SDK van het Web van de Experience Platform maakt deel uit van een inzameling van hulpmiddelen die omhoog het Netwerk van de Rand van Adobe Experience Platform maken.

Het Edge-netwerk bestaat uit de volgende onderdelen:

* **[Experience Platform Web SDK](#overview):** Een JavaScript-bibliotheek en een tagextensie waarmee u de implementatie van Adobe-technologieën kunt vereenvoudigen.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/home/):** Een uitbreiding op de mobiele SDK van v5 waarmee u de nieuwe implementatiemethodologie kunt gebruiken.
* **[Edge Network Server-API](../server-api/overview.md):** Een API aan de serverzijde die u voor diverse gegevensinzameling, verpersoonlijking, reclame en marketing gebruiksgevallen kunt gebruiken. De server-API kan worden gebruikt op servers, IoT-apparaten, set-top boxes en verschillende andere apparaten.

Het Edge-netwerk is een raamwerk voor gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen. Het verstrekt één enkele geconsolideerde SDK voor elk kanaal (Web, mobiel, server-kant), die gegevens naar een gemeenschappelijk domein van de Adobe (`adobedc.net`) en ontvangt één enkele terugverdientijd voor gegevens en ervaringslevering.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdienst het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te stellen. Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Versnelt innovatie
* Creeert duurzame concurrentievoordelen voor Adobe klanten

Met één geconsolideerd randsysteem kunt u uw reclame-, marketing- of personalisatiecampagnes op alle kanalen beheren als een geïntegreerde ervaring. Het staat ook Adobe toe om de diensten met lagere totale kosten van eigendom voor klanten te leveren. Het randsysteem wordt ontworpen om de meeste soorten gegevens aan te passen, toestaand u om uw eigen gegevensmodel in kaart te brengen dat door veelvoudige producten van de Experience Cloud moet worden opgenomen.

## Video-overzicht {#video}

Bekijk de onderstaande video voor een overzicht van de Adobe Experience Platform [!DNL Web SDK] en de [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotheken die worden vervangen door de Web SDK {#sdks}

De Web SDK is niet alleen een omslag rond bestaande bibliotheken. Het is een nieuwe bibliotheek, die vanaf de grond is geschreven om functies van bestaande bibliotheken te integreren. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om de [!DNL Experience Cloud] en [open bron](https://github.com/adobe/alloy).

De SDK van het Web vervangt de volgende SDK&#39;s:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Naast een nieuwe bibliotheek, is er een nieuw eindpunt dat de HTTP- verzoeken aan Adobe oplossingen stroomlijnt. Voor, `Visitor.js` verzond een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen `AT.js` een oproep naar Adobe Target heeft gestuurd, `DIL.js` heeft Adobe Audience Manager gebeld en uiteindelijk `AppMeasurement.js` heeft Adobe Analytics gebeld. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een halen [!DNL Target] ervaring, gegevens verzenden naar [!DNL Audience Manager]en geef de gegevens door aan Adobe Experience Platform in één aanroep.

De volgende video demonstreert Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network] in actie. Het videovoorbeeld gebruikt één enkele vraag aan Adobe die gegevens naar verzendt [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], en [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migreren van bestaande bibliotheken naar Web SDK {#migrating-to-web-sdk}

Om uw migratie vanaf om het even welk [bestaande bibliotheken](#sdks) naar Web SDK, biedt de Adobe een gestroomlijnd verbeteringspad aan. Met dit pad kunt u elke afzonderlijke pagina van uw website migreren naar de SDK van het web zonder dat u uw gehele website tegelijk hoeft te migreren. U kunt de SDK van het Web op een bepaalde pagina gebruiken terwijl de bestaande bibliotheken op andere pagina&#39;s verblijven. Zodra u klaar bent, kunt u die andere pagina&#39;s ook migreren.

### Migratie van `AT.js` naar Web SDK-overwegingen {#considerations}

Voordat u pagina&#39;s migreert die `AT.js` aan Web SDK, zorg ervoor om de volgende de configuratieopties van SDK van het Web toe te laten. Met deze opties blijft het bezoekersprofiel behouden tijdens het navigeren vanaf pagina&#39;s met `AT.js` naar pagina&#39;s die Web SDK gebruiken.

* [` idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [` targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>De volgende functies van het Doel worden niet ondersteund bij het migreren van at.js naar Web SDK:
>
>* [Aanbiedingen omleiden](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME en ondersteuning voor andere domeinen](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Na het migreren van `AT.js` aan de SDK van het Web, verwijder `targetMigrationEnabled` van uw configuratie.
