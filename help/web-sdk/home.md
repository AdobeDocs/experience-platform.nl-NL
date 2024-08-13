---
title: Adobe Experience Platform Web Software Development Kit (SDK) - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK gebruikt om de mogelijkheden van het platform in uw website te integreren.
source-git-commit: ac8bb272a8af26f90a866541d513e50bf2dfa8b0
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---


# Adobe Experience Platform Web SDK {#overview}

>[!IMPORTANT]
>
>Eind april 2024 zal de SDK van het Web van Adobe Experience Platform steun voor alle versies van Internet Explorer verwijderen.

De Adobe Experience Platform Web Software Development Kit (SDK) is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud via de Adobe Experience Platform-Edge Network kunnen communiceren met hun services.

De Adobe biedt twee methodes aan om Web SDK uit te voeren:

* De [ de markeringsuitbreiding van SDK van het Web ](../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md). Zie het leerprogramma op hoe te [ Adobe Experience Cloud met Web SDK ](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html) voor meer informatie uitvoeren.
* Handmatige implementatie met de Web SDK JavaScript-bibliotheek.

Deze gebruikershandleiding bevat instructies voor het werken met de oplossingen voor Experiencen Cloud via de Web SDK JavaScript-bibliotheek en de tagextensie, indien van toepassing.

## Edge Network Experience Platform {#edge-network}

De SDK van het Web van het Experience Platform maakt deel uit van een inzameling van hulpmiddelen die omhoog de Edge Network van Adobe Experience Platform maken.

De Edge Network bestaat uit de volgende onderdelen:

* **[SDK van het Web van het Experience Platform ](#overview):** een bibliotheek van JavaScript en een markeringsuitbreiding die u helpen de plaatsing van de technologieën van de Adobe vereenvoudigen.
* **[Experience Platform Mobiele SDK ](https://developer.adobe.com/client-sdks/home/):** Een uitbreiding aan v5 mobiele SDK die u toestaat om de nieuwe plaatsingsmethodologie te gebruiken.
* **[de Server API van de Edge Network ](../server-api/overview.md):** een server-kant API die u voor diverse gegevensinzameling, verpersoonlijking, reclame en marketing gebruiksgevallen kunt gebruiken. De server-API kan worden gebruikt op servers, IoT-apparaten, set-top boxes en verschillende andere apparaten.

De Edge Network is een kader voor het verzamelen van gegevens met lage latentie, pluggable gegevensverwerking, en snelle gegevensactivering over alle adresseerbare kanalen. Het verstrekt één enkele geconsolideerde SDK voor elk kanaal (Web, mobiel, server-kant), die gegevens naar een gemeenschappelijk domein van de Adobe (`adobedc.net`) verzendt en één enkele nuttige lading terug voor gegevens en ervaringslevering ontvangt.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdienst het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te stellen. Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Versnelt innovatie
* Creeert duurzame concurrentievoordelen voor Adobe klanten

Met één geconsolideerd randsysteem kunt u uw reclame-, marketing- of personalisatiecampagnes op alle kanalen beheren als een geïntegreerde ervaring. Het staat ook Adobe toe om de diensten met lagere totale kosten van eigendom voor klanten te leveren. Het randsysteem wordt ontworpen om de meeste soorten gegevens aan te passen, toestaand u om uw eigen gegevensmodel in kaart te brengen dat door veelvoudige producten van de Experience Cloud moet worden opgenomen.

## Video-overzicht {#video}

Bekijk de onderstaande video voor een overzicht van de Adobe Experience Platform [!DNL Web SDK] en de [!DNL Edge Network] .

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotheken die worden vervangen door de Web SDK {#sdks}

De Web SDK is niet alleen een omslag rond bestaande bibliotheken. Het is een nieuwe bibliotheek, die vanaf de grond is geschreven om functies van bestaande bibliotheken te integreren. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om [!DNL Experience Cloud] uit te voeren en het is [ open bron ](https://github.com/adobe/alloy).

De SDK van het Web vervangt de volgende SDK&#39;s:

* `Visitor.js`
* `AppMeasurement.js`
* `AT.js`
* `DIL.js`

Naast een nieuwe bibliotheek, is er een nieuw eindpunt dat de HTTP- verzoeken aan Adobe oplossingen stroomlijnt. Voor `Visitor.js` een blokkerende aanroep naar de bezoeker-id-service heeft verzonden, heeft `AT.js` een aanroep naar Adobe Target verzonden, heeft `DIL.js` een aanroep naar Adobe Audience Manager verzonden en heeft `AppMeasurement.js` ten slotte een aanroep naar Adobe Analytics verzonden. Deze nieuwe bibliotheek en eindpunt kunnen een id ophalen, een [!DNL Target] -ervaring ophalen, gegevens naar [!DNL Audience Manager] verzenden en de gegevens in één aanroep aan Adobe Experience Platform doorgeven.

In de volgende video worden Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network] in actie gedemonstreerd. In het videovoorbeeld wordt één aanroep naar Adobe gebruikt die gegevens verzendt naar [!DNL Experience Platform] , [!DNL Analytics] , [!DNL Audience Manager] en [!DNL Target] .

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migreren van bestaande bibliotheken naar Web SDK {#migrating-to-web-sdk}

Om uw migratie van om het even welke [ bestaande bibliotheken ](#sdks) aan Web SDK te vereenvoudigen, biedt de Adobe een gestroomlijnde verbeteringspad aan. Met dit pad kunt u elke afzonderlijke pagina van uw website migreren naar de SDK van het web zonder dat u uw gehele website tegelijk hoeft te migreren. U kunt de SDK van het Web op een bepaalde pagina gebruiken terwijl de bestaande bibliotheken op andere pagina&#39;s verblijven. Zodra u klaar bent, kunt u die andere pagina&#39;s ook migreren.

### Overwegingen bij het migreren van `AT.js` naar Web SDK {#considerations}

Alvorens pagina&#39;s te migreren die `AT.js` aan Web SDK gebruiken, zorg ervoor om de volgende de configuratieopties van SDK van het Web toe te laten. Met deze opties blijft het bezoekersprofiel behouden tijdens het navigeren van pagina&#39;s met `AT.js` naar pagina&#39;s met Web SDK.

* [` idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md)
* [` targetMigrationEnabled`](/help/web-sdk/commands/configure/targetmigrationenabled.md)


>[!IMPORTANT]
>
>De volgende functies van het Doel worden niet ondersteund bij het migreren van at.js naar Web SDK:
>
>* [ Redirect aanbiedingen ](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html)
>* [ CNAME en dwars-domeinsteun ](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/atjs-cookies.html)

Nadat u van `AT.js` naar de SDK van het Web hebt gemigreerd, verwijdert u de optie `targetMigrationEnabled` uit uw configuratie.
