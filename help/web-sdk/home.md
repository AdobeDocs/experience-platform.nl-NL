---
title: Adobe Experience Platform Web Software Development Kit (SDK) - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK gebruikt om de mogelijkheden van het platform in uw website te integreren.
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 2bf9c7ada9fd223df92b5cc9b1415f20705c2042
workflow-type: tm+mt
source-wordcount: '600'
ht-degree: 1%

---

# Adobe Experience Platform Web SDK {#overview}

De Adobe Experience Platform Web SDK is een client-side JavaScript-bibliotheek waarmee Adobe Experience Cloud-klanten via de Adobe Experience Platform-Edge Network kunnen communiceren met hun services.

U kunt SDK van het Web op twee manieren uitvoeren:

* De [ de markeringsuitbreiding van SDK van het Web ](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Zie het leerprogramma op hoe te [ Adobe Experience Cloud met Web SDK ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) voor meer informatie uitvoeren.
* Handmatige implementatie die de [ bibliotheek van SDK van het Web SDK JavaScript ](install/library.md) gebruikt.

Deze handleiding bevat instructies voor het werken met oplossingen voor Experiencen Cloud met zowel de Web SDK JavaScript-bibliotheek als de tagextensie.

## Edge Network Experience Platform {#edge-network}



De SDK van het Web van de Experience Platform maakt deel uit van de Edge Network van Adobe Experience Platform, die omvat:

* **[SDK van het Web van het Experience Platform](#overview)**: Een bibliotheek en markeringsuitbreiding van JavaScript voor het vereenvoudigen van de plaatsing van de technologie van de Adobe.
* **[Experience Platform Mobiele SDK ](https://developer.adobe.com/client-sdks/home/)**: Een uitbreiding aan v5 mobiele SDK voor de nieuwe plaatsingsmethodologie.
* **[Edge Network API](../server-api/overview.md)**: Een server-kant API voor gegevensinzameling, verpersoonlijking, reclame, en marketing gebruiksgevallen. U kunt het op servers, apparaten IoT, reeks-hoogste dozen, en andere apparaten gebruiken.

De Edge Network biedt gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen. Het biedt één geconsolideerde SDK voor Web, mobiel, en server-zijkanalen aan, die gegevens naar een gemeenschappelijk domein van de Adobe (`adobedc.net`) verzenden en één enkele lading voor gegevens en ervaringslevering ontvangen.

Op de server-kant, vereenvoudigen een verenigde randgateway en een gemeenschappelijk kader van de platformdienst de plaatsing van nieuwe mogelijkheden, terwijl het verstrekken van de volgende voordelen:

* verkort de tijd van de klant aan waarde;
* de noodzaak van &quot;point&quot;-integratie te beëindigen;
* Verbetering van de prestaties in vergelijking met de oude bibliotheken;
* verlaging van de exploitatiekosten;
* de innovatiesnelheid verhogen;
* Het creëren van duurzame concurrentievoordelen voor Adobe klanten.

Met een geconsolideerd Edge-systeem kunt u reclame-, marketing- en personalisatiecampagnes op alle kanalen beheren. Het vermindert de totale kosten van eigendom en steunt diverse gegevenstypes, toelatend u om uw gegevensmodel voor gebruik met de veelvoudige producten van het Experience Cloud in kaart te brengen.

## Video-overzicht {#video}

Bekijk de onderstaande video voor een overzicht van de Adobe Experience Platform [!DNL Web SDK] en de [!DNL Edge Network] .

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotheken die worden vervangen door de Web SDK {#sdks}

De SDK van het Web is een nieuwe, open-bronbibliotheek die van kras wordt gebouwd om functionaliteit van bestaande bibliotheken te integreren. Het richt kwesties met markering het ontsteken orde, versie inconsistenties, en gebiedsdeelbeheer, die een nieuwe, [ open bron ](https://github.com/adobe/alloy) manier aanbieden om [!DNL Experience Cloud] uit te voeren.

De Web SDK vervangt:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Het introduceert ook een nieuw eindpunt dat HTTP- verzoeken aan Adobe oplossingen stroomlijnt. Eerder waren meerdere aanroepen nodig voor `Visitor.js` , `AT.js` , `DIL.js` en `AppMeasurement.js` . Met één aanroep kan nu een id worden opgehaald, een [!DNL Target] -ervaring worden opgehaald, gegevens worden verzonden naar [!DNL Audience Manager] en gegevens worden doorgegeven aan Adobe Experience Platform.

Bekijk de onderstaande video om Adobe Experience Platform [!DNL Web SDK] en [!DNL Edge Network] in actie te zien, met behulp van één aanroep om gegevens naar [!DNL Experience Platform] , [!DNL Analytics] , [!DNL Audience Manager] en [!DNL Target] te verzenden.

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migreren van bestaande bibliotheken naar Web SDK {#migrating-to-web-sdk}

De Adobe biedt een gestroomlijnde verbeteringsweg aan om uw migratie van om het even welke [ bestaande bibliotheken ](#sdks) aan Web SDK te vereenvoudigen. U kunt elke pagina van uw website afzonderlijk migreren zonder dat u de gehele site tegelijk hoeft te migreren. U kunt de SDK van het Web op sommige pagina&#39;s gebruiken terwijl de bestaande bibliotheken op anderen blijven, die voor een geleidelijke overgang toestaan.

### Overwegingen bij het migreren van `AT.js` naar Web SDK {#considerations}

Voordat u pagina&#39;s migreert met `AT.js` naar Web SDK, schakelt u de volgende Web SDK-configuratieopties in om ervoor te zorgen dat het bezoekersprofiel behouden blijft wanneer u tussen pagina&#39;s navigeert.

* [` idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [` targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)

>[!IMPORTANT]
>
>De volgende doelfuncties worden niet ondersteund bij het migreren van `at.js` naar Web SDK:
>
>* [ Redirect aanbiedingen ](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [ CNAME en dwars-domeinsteun ](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Nadat u van `AT.js` naar de SDK van het Web hebt gemigreerd, verwijdert u de optie `targetMigrationEnabled` uit uw configuratie.
