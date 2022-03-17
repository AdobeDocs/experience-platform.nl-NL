---
title: Adobe Experience Platform Web SDK - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK kunt gebruiken om de mogelijkheden van het Platform in uw website te integreren.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 71857ffc5e671f4d9a0502fb95d89d30fdec1f15
workflow-type: tm+mt
source-wordcount: '622'
ht-degree: 0%

---

# Overzicht Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van Adobe Experience Cloud kunnen communiceren met de verschillende services in de [!DNL Experience Cloud] via het Adobe Experience Platform Edge Network. Naast de JavaScript-bibliotheek is er een [tagextensie](./extension/web-sdk-extension-configuration.md) om met uw configuraties van SDK van het Web te helpen.

**Voor een geleidelijke gids aan vestiging SDK van het Web met markeringen en het verzenden van gegevens naar de oplossingen gelieve te zien [Zelfstudie Adobe Experience Cloud implementeren met Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en)**

## Beleef de rand

[!DNL Adobe Experience Platform Web SDK] maakt deel uit van de verzameling waaruit Experience Edge bestaat. Experience Edge bestaat uit drie technologieën:

* **[!DNL Adobe Experience Platform Web SDK]:** Een JavaScript SDK en tagextensie om de implementatie aanzienlijk te vereenvoudigen [!DNL Adobe] technologieën
* **Adobe Experience Platform Mobile SDK:** Een uitbreiding van de mobiele SDK van v5 zodat klanten de nieuwe implementatiemethode kunnen gebruiken
* **[!DNL Adobe Experience Platform Edge Network]:** Een globaal verdeeld netwerk van servers die een nieuwe methodologie om toelaten op te stellen [!DNL Adobe] producten

De [!DNL Adobe Experience Edge] is een nieuw kader voor gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen.

[!DNL Adobe Experience Edge] biedt één geconsolideerde SDK voor elk kanaal (JavaScript, Mobiel, Server-kant), dat gegevens verzendt naar een gemeenschappelijk Adobe-domein (`adobedc.net`) en ontvangt één enkele nuttige lading voor gegevens en ervaringslevering.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdiensten het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te nemen en op te stellen.  Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Verhoogt de snelheid van innovatie
* Creeert duurzame concurrerende voordelen voor klanten van Adobe

Met één enkel geconsolideerd randsysteem kunnen klanten hun reclame-, marketing- of personalisatiecampagnes op alle kanalen als een geïntegreerde ervaring beheren.  Het staat [!DNL Adobe] om de diensten met lagere totale kosten van eigendom voor klanten te leveren.  Het helpt ook de snelheid van productinnovatie te verhogen door de rand in real time pluggable te maken en toe te staan [!DNL Adobe] en zijn klanten om nieuwe mogelijkheden en klant-bepaalde logica aan dat real time systeem sneller toe te voegen.

## Video-overzicht

De volgende video geeft een overzicht van de Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## SDK&#39;s vervangen door Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK vervangt de volgende SDK&#39;s:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Dit is niet alleen een omslag rond bestaande bibliotheken. Het is een volledige herschrijving. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om de [!DNL Experience Cloud] en [open bron](https://github.com/adobe/alloy).

Naast een nieuwe bibliotheek, is er een nieuw eindpunt dat de HTTP- verzoeken aan de oplossingen van Adobe stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen stuurde AT.js een vraag naar Adobe Target, zond DIL.js een vraag naar Adobe Audience Manager, en tenslotte stuurde AppMeasurement.js een vraag naar Adobe Analytics. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een halen [!DNL Target] ervaring, gegevens verzenden naar [!DNL Audience Manager]en geef de gegevens door aan Adobe Experience Platform in één aanroep.

De volgende video demonstreert Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network] in actie. Het videovoorbeeld gebruikt één enkele vraag aan Adobe die gegevens naar verzendt [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], en [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148?quality=12&learn=on)

Dit product ontwikkelt zich voortdurend en groeit om steeds meer gebruiksgevallen te ondersteunen. Als u de nieuwste ontwikkelingen wilt bijhouden en wilt zien wat wij op dit moment steunen, raadpleegt u de [pagina met ondersteunde gebruiksgevallen](https://github.com/orgs/adobe/projects/18/views/1).
