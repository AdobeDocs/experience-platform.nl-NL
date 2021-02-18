---
title: Adobe Experience Platform Web SDK - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK kunt gebruiken om de mogelijkheden van het Platform in uw website te integreren.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---


# Overzicht Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van Adobe Experience Cloud via het Adobe Experience Platform Edge Network kunnen communiceren met de verschillende services in de [!DNL Experience Cloud]. Naast de bibliotheek JavaScript, is er [Experience Platform Launch uitbreiding](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/aep-extension/overview.html) om met uw configuraties van SDK van het Web te helpen.

## Beleef de rand

[!DNL Adobe Experience Platform Web SDK] maakt deel uit van de verzameling waaruit Experience Edge bestaat. Experience Edge bestaat uit drie technologieën:

* **[!DNL Adobe Experience Platform Web SDK]:** Een JavaScript SDK en  [!DNL Experience Platform Launch] uitbreiding voor een drastische vereenvoudiging van de implementatie van  [!DNL Adobe] technologieën
* **Adobe Experience Platform Mobile SDK:** een uitbreiding op de mobiele SDK van v5 waarmee klanten de nieuwe implementatiemethode kunnen gebruiken
* **[!DNL Adobe Experience Platform Edge Network]:** Een wereldwijd gedistribueerd netwerk van servers dat een nieuwe methode om  [!DNL Adobe] producten in te voeren mogelijk maakt

De [!DNL Adobe Experience Edge] is een nieuw kader voor het verzamelen van gegevens met lage latentie, pluggable gegevensverwerking en snelle gegevensactivering over alle adresseerbare kanalen.

[!DNL Adobe Experience Edge] biedt één geconsolideerde SDK voor elk kanaal (JavaScript, Mobiel, Server-kant), die gegevens naar een gemeenschappelijk Adobe-domein (`adobedc.net`) verzendt en één enkele nuttige lading voor gegevens en ervaringslevering ontvangt.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdiensten het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te nemen en op te stellen.  Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Verhoogt de snelheid van innovatie
* Creeert duurzame concurrerende voordelen voor klanten van Adobe

Met één enkel geconsolideerd randsysteem kunnen klanten hun reclame-, marketing- of personalisatiecampagnes op alle kanalen als een geïntegreerde ervaring beheren.  Hierdoor kunnen klanten services leveren met lagere totale eigendomskosten.  [!DNL Adobe]  Het helpt ook de snelheid van productinnovatie te verhogen door de rand in real time pluggable te maken en [!DNL Adobe] en zijn klanten toe te staan om nieuwe mogelijkheden en klant-bepaalde logica aan dat echt - tijdsysteem sneller toe te voegen.

## Video-overzicht

De volgende video geeft een overzicht van de Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK&#39;s vervangen door Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK vervangt de volgende SDK&#39;s:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dit is niet alleen een omslag rond bestaande bibliotheken. Het is een volledige herschrijving. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om [!DNL Experience Cloud] uit te voeren en het is [open bron](https://github.com/adobe/alloy).

Naast een nieuwe bibliotheek, is er een nieuw eindpunt dat de HTTP- verzoeken aan de oplossingen van Adobe stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen stuurde AT.js een vraag naar Adobe Target, zond DIL.js een vraag naar Adobe Audience Manager, en tenslotte stuurde AppMeasurement.js een vraag naar Adobe Analytics. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een [!DNL Target] ervaring halen, gegevens verzenden naar [!DNL Audience Manager], en de gegevens tot Adobe Experience Platform in één enkele vraag overgaan.

In de volgende video worden Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network] in actie gedemonstreerd. Het videovoorbeeld gebruikt één enkele vraag aan Adobe die gegevens naar [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], en [!DNL Target] verzendt.

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Dit product ontwikkelt zich voortdurend en groeit om steeds meer gebruiksgevallen te ondersteunen. Als u de nieuwste ontwikkelingen wilt bijhouden, bekijkt u ons [ondersteunde toetsenbord](https://github.com/adobe/alloy/projects/5). Wij houden dit bij met de gebruiksgevallen die wij momenteel steunen en de gevallen waarin wij aan het werk zijn om u in staat te stellen de beste beslissingen te nemen.

* **Gebruik nog niet ondersteunde gevallen:** dit zijn gebruiksgevallen die op onze routekaart staan en in de toekomst worden ondersteund.
* **Gebruiksgevallen in uitvoering:** Dit zijn de gebruiksgevallen die het team momenteel aan voltooiing voor versie werkt.
* **Gevallen voor ondersteund gebruik:** Dit zijn de gebruiksgevallen die worden ondersteund en die vandaag worden gebruikt.
* **Gebruik gevallen die we niet ondersteunen:** dit zijn de gebruiksgevallen die we hebben besloten niet te ondersteunen.
