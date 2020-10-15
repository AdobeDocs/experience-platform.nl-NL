---
title: Adobe Experience Platform Web SDK Help
seo-title: Adobe Experience Platform Web SDK Help
description: Leer wat Adobe Experience Platform Web SDK is en hoe deze kan worden gebruikt.
seo-description: klanten van de Adobe Experience Cloud in staat stellen te communiceren met de verschillende diensten in de Experience Cloud.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---


# Wat is Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van de Adobe Experience Cloud kunnen communiceren met de verschillende services in de [!DNL Experience Cloud] Adobe [!DNL Experience Platform Edge Network]. Naast de JavaScript-bibliotheek is er een extensie [voor](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) Experience Platforms Launch die u kunt helpen met uw Web SDK-configuraties.

## Beleef de rand

[!DNL Adobe Experience Platform Web SDK] maakt deel uit van de verzameling waaruit Experience Edge bestaat. Experience Edge bestaat uit drie technologieën:

* **[!DNL Adobe Experience Platform Web SDK]:** Een JavaScript SDK en [!DNL Experience Platform Launch] extensie voor een drastische vereenvoudiging van de implementatie van [!DNL Adobe] technologieën
* **Adobe Experience Platform Mobile SDK:** Een uitbreiding van de mobiele SDK van v5 zodat klanten de nieuwe implementatiemethode kunnen gebruiken
* **[!DNL Adobe Experience Platform Edge Network]:** Een globaal verdeeld netwerk van servers die een nieuwe methodologie toelaten om [!DNL Adobe] producten op te stellen

Het [!DNL Adobe Experience Edge] is een nieuw kader voor gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen.

[!DNL Adobe Experience Edge] biedt één geconsolideerde SDK voor elk kanaal (JavaScript, Mobiel, Server-kant), die gegevens naar een gemeenschappelijk Adobe-domein (`adobedc.net`) verzendt en één enkele nuttige lading voor gegevens en ervaringslevering ontvangt.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdiensten het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te nemen en op te stellen.  Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Verhoogt de snelheid van innovatie
* Creeert duurzame concurrerende voordelen voor klanten van Adobe

Met één enkel geconsolideerd randsysteem kunnen klanten hun reclame-, marketing- of personalisatiecampagnes op alle kanalen als een geïntegreerde ervaring beheren.  Het staat toe [!DNL Adobe] om de diensten met lagere totale kosten van eigendom voor klanten te leveren.  Het helpt ook de snelheid van productinnovatie verhogen door de rand in real time pluggable te maken en [!DNL Adobe] en zijn klanten toe te staan om nieuwe mogelijkheden en klant-bepaalde logica aan dat echt - tijdsysteem sneller toe te voegen.

## Video-overzicht

De volgende video geeft een overzicht van de Adobe Experience Platform [!DNL Web SDK] en [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK&#39;s vervangen door Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK vervangt de volgende SDK&#39;s:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dit is niet alleen een omslag rond bestaande bibliotheken. Het is een volledige herschrijving. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om de richtlijn uit te voeren [!DNL Experience Cloud] en het is een [open bron](https://github.com/adobe/alloy).

Naast een nieuwe bibliotheek, is er een nieuw eindpunt dat de HTTP- verzoeken aan de oplossingen van Adobe stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen stuurde AT.js een vraag naar Adobe Target, zond DIL.js een vraag naar Adobe Audience Manager, en tenslotte stuurde AppMeasurement.js een vraag naar Adobe Analytics. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een [!DNL Target] ervaring halen, gegevens verzenden naar [!DNL Audience Manager], en de gegevens tot Adobe Experience Platform in één enkele vraag overgaan.

De volgende video demonstreert de Adobe Experience Platform [!DNL Web SDK] en [!DNL Edge Network] in actie. Het videovoorbeeld gebruikt één enkele vraag aan Adobe die gegevens naar [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager]en [!DNL Target]verzendt.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

## Aan de slag

U wordt ten zeerste aangeraden de gids [Aan de slag uit te](consent/iab-tcf/with-launch.md) checken voor een korte zelfstudie over hoe u aan de slag kunt met Adobe Experience Platform Launch.

Dit product ontwikkelt zich voortdurend en groeit om steeds meer gebruiksgevallen te ondersteunen. Om de nieuwste ontwikkelingen bij te houden, bekijkt u ons [ondersteunde toetsenbord](https://github.com/adobe/alloy/projects/5). Wij houden dit bij met de gebruiksgevallen die wij momenteel steunen en de gevallen waarin wij aan het werk zijn om u in staat te stellen de beste beslissingen te nemen.

* **Gebruik nog niet ondersteunde gevallen:** Dit zijn gebruiksgevallen die op onze routekaart staan en die in de toekomst moeten worden ondersteund.
* **Gevallen worden gebruikt:** Dit zijn de gebruiksgevallen die het team momenteel aan de voltooiing voor versie werkt.
* **Gevallen voor ondersteund gebruik:** Dit zijn de gebruiksgevallen die worden ondersteund en vandaag werken.
* **Gebruik gevallen die we niet ondersteunen:** Dit zijn de gebruiksgevallen die we hebben besloten niet te steunen.
