---
title: Adobe Experience Platform Web Software Development Kit (SDK) - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK kunt gebruiken om Experience Platform-mogelijkheden te integreren in uw website.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK {#overview}

De Adobe Experience Platform Web SDK is een client-side JavaScript-bibliotheek waarmee Adobe Experience Cloud-klanten via Adobe Experience Platform Edge Network kunnen communiceren met hun services.

U kunt SDK van het Web op twee manieren uitvoeren:

* De [&#x200B; de markeringsuitbreiding van SDK van het Web &#x200B;](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Zie het leerprogramma op hoe te [&#x200B; Adobe Experience Cloud met het Web SDK &#x200B;](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=nl-NL) voor meer informatie uitvoeren.
* Handmatige implementatie die de [&#x200B; bibliotheek van SDK van het Web JavaScript &#x200B;](install/library.md) gebruikt.

Deze handleiding bevat instructies voor het werken met Experience Cloud-oplossingen met zowel de Web SDK JavaScript-bibliotheek als de tagextensie.

## Experience Platform Edge Network {#edge-network}



De Experience Platform Web SDK maakt deel uit van de Adobe Experience Platform Edge Network, die het volgende omvat:

* **[Experience Platform Web SDK](#overview)**: Een bibliotheek en markeringsuitbreiding van JavaScript voor het vereenvoudigen van de technologieplaatsing van Adobe.
* **[Experience Platform Mobile SDK &#x200B;](https://developer.adobe.com/client-sdks/home/)**: Een uitbreiding aan v5 mobiele SDK voor de nieuwe plaatsingsmethodologie.
* **[Edge Network API &#x200B;](https://developer.adobe.com/data-collection-apis/docs/api/)**: Een server-kant API voor gegevensinzameling, verpersoonlijking, reclame, en marketing gebruiksgevallen. U kunt het op servers, apparaten IoT, reeks-hoogste dozen, en andere apparaten gebruiken.

De Edge Network biedt gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen. Het biedt één geconsolideerde SDK voor web, mobiel, en server-zijkanalen, die gegevens naar een gemeenschappelijk domein van Adobe (`adobedc.net`) verzenden en één enkele lading voor gegevens en ervaringslevering ontvangen.

Op de server-kant, vereenvoudigen een verenigde randgateway en een gemeenschappelijk kader van de platformdienst de plaatsing van nieuwe mogelijkheden, terwijl het verstrekken van de volgende voordelen:

* verkort de tijd van de klant aan waarde;
* de noodzaak van &quot;point&quot;-integratie te beëindigen;
* Verbetering van de prestaties in vergelijking met de oude bibliotheken;
* verlaging van de exploitatiekosten;
* de innovatiesnelheid verhogen;
* Aanhoudende concurrentievoordelen voor Adobe-klanten.

Met een geconsolideerd Edge-systeem kunt u reclame-, marketing- en personalisatiecampagnes op alle kanalen beheren. Dit verlaagt de totale eigendomskosten en ondersteunt verschillende gegevenstypen, zodat u uw gegevensmodel kunt toewijzen voor gebruik met meerdere Experience Cloud-producten.

## Video-overzicht {#video}

Bekijk de onderstaande video voor een overzicht van de Adobe Experience Platform [!DNL Web SDK] en de [!DNL Edge Network] .

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotheken die worden vervangen door de Web SDK {#sdks}

De Web SDK is een nieuwe, open-bronbibliotheek die van kras wordt gebouwd om functionaliteit van bestaande bibliotheken te integreren. Het richt kwesties met markering het ontsteken orde, versie inconsistenties, en gebiedsdeelbeheer, die een nieuwe, [&#x200B; open bron &#x200B;](https://github.com/adobe/alloy) manier aanbieden om [!DNL Experience Cloud] uit te voeren.

De Web SDK vervangt:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Het introduceert ook een nieuw eindpunt dat HTTP- verzoeken aan de oplossingen van Adobe stroomlijnt. Eerder waren meerdere aanroepen nodig voor `Visitor.js` , `AT.js` , `DIL.js` en `AppMeasurement.js` . Met één aanroep kan nu een id worden opgehaald, een [!DNL Target] -ervaring worden opgehaald, gegevens worden verzonden naar [!DNL Audience Manager] en gegevens worden doorgegeven aan Adobe Experience Platform.

Bekijk de onderstaande video om Adobe Experience Platform [!DNL Web SDK] en [!DNL Edge Network] in actie te zien, met behulp van één aanroep om gegevens naar [!DNL Experience Platform] , [!DNL Analytics] , [!DNL Audience Manager] en [!DNL Target] te verzenden.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migreren van bestaande bibliotheken naar Web SDK {#migrating-to-web-sdk}

Adobe biedt een gestroomlijnde verbeteringsweg aan om uw migratie van om het even welke [&#x200B; bestaande bibliotheken &#x200B;](#sdks) aan Web SDK te vereenvoudigen. U kunt elke pagina van uw website afzonderlijk migreren zonder dat u de gehele site tegelijk hoeft te migreren. U kunt de Web SDK op sommige pagina&#39;s gebruiken terwijl de bestaande bibliotheken op anderen blijven, die voor een geleidelijke overgang toestaan.

### Overwegingen bij het migreren van `AT.js` naar Web SDK {#considerations}

Voordat u pagina&#39;s migreert met `AT.js` naar Web SDK, schakelt u de volgende Web SDK-configuratieopties in om ervoor te zorgen dat het bezoekersprofiel behouden blijft wanneer u tussen pagina&#39;s navigeert.

* [` idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [` targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>De volgende doelfuncties worden niet ondersteund bij het migreren van `at.js` naar Web SDK:
>
>* [&#x200B; Redirect aanbiedingen &#x200B;](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=nl-NL)
>* [&#x200B; CNAME en dwars-domeinsteun &#x200B;](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html?lang=nl-NL)

Nadat u van `AT.js` naar de Web SDK hebt gemigreerd, verwijdert u de optie `targetMigrationEnabled` uit de configuratie.
