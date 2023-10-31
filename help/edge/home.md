---
title: Adobe Experience Platform Web Software Development Kit (SDK) - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK gebruikt om de mogelijkheden van het platform in uw website te integreren.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 1%

---

# Overzicht van Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web Software Development Kit (SDK) is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud via het Adobe Experience Platform Edge Network kunnen communiceren met hun services. De Adobe biedt twee methodes aan om Web SDK uit te voeren:

* Handmatige implementatie met `alloy.js`. Deze gebruikershandleiding bevat documentatie voor deze implementatiemethode.
* De [Web SDK-tagextensie](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Zie [Zelfstudie Adobe Experience Cloud implementeren met Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) voor meer informatie .

## Experience Platform Edge Network

De SDK van het Web van de Experience Platform maakt deel uit van een inzameling van hulpmiddelen die omhoog het Netwerk van de Rand van Adobe Experience Platform maken. Het Edge-netwerk bestaat uit de volgende onderdelen:

* **[Experience Platform Web SDK](#overview):** Een JavaScript SDK en tagextensie om de implementatie van Adobe-technologieën aanzienlijk te vereenvoudigen.
* **[Experience Platform Mobile SDK](https://developer.adobe.com/client-sdks/documentation/):** Een uitbreiding van de mobiele SDK van v5 zodat klanten de nieuwe implementatiemethode kunnen gebruiken
* **[Experience Platform Edge Network Server-API](../server-api/overview.md):** Een API die kan worden gebruikt voor diverse gevallen van gegevensverzameling, personalisatie, reclame en marketing. De server-API kan worden gebruikt op servers, IoT-apparaten, set-top boxes en diverse andere apparaten.

Het Edge-netwerk is een raamwerk voor gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen. Het verstrekt één enkele geconsolideerde SDK voor elk kanaal (JavaScript, Mobiel, server-kant), dat gegevens naar een gemeenschappelijk domein van de Adobe verzendt (`adobedc.net`) en ontvangt één enkele terugverdientijd voor gegevens en ervaringslevering.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdienst het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te stellen. Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Versnelt innovatie
* Creeert duurzame concurrentievoordelen voor Adobe klanten

Met één geconsolideerd Edge-systeem kunnen klanten hun reclame-, marketing- of personalisatiecampagnes op alle kanalen als een geïntegreerde ervaring beheren. Het staat ook Adobe toe om de diensten met lagere totale kosten van eigendom voor klanten te leveren. Het randsysteem wordt ontworpen om de meeste soorten gegevens aan te passen, toestaand u om uw eigen gegevensmodel in kaart te brengen dat door veelvoudige producten van de Experience Cloud moet worden opgenomen.

## Video-overzicht {#video}

De volgende video geeft een overzicht van de Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network].

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

* [` idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [` targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>De volgende functies van het Doel worden niet ondersteund bij het migreren van at.js naar Web SDK:
>
>* [Aanbiedingen omleiden](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [CNAME en ondersteuning voor andere domeinen](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Na het migreren van `AT.js` aan de SDK van het Web, verwijder `targetMigrationEnabled` van uw configuratie.
