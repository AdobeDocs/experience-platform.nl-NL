---
title: Adobe Experience Platform Web SDK - Overzicht
description: Leer hoe u de Adobe Experience Platform Web SDK kunt gebruiken om de mogelijkheden van het Platform in uw website te integreren.
keywords: Adobe Experience Platform Web SDK;Platform Web SDK;Web SDK;edge;Visitor.js;AppMeasurement.js;AT.js;DIL.js;web sdk;SDK;web SDK;Launch;launch
exl-id: 1348144a-7d25-4c27-bc40-3daee2f043a6
source-git-commit: 00801465435133fce29002c8bd0f2256745ba2c2
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%

---

# Overzicht Adobe Experience Platform Web SDK {#overview}

Adobe Experience Platform Web SDK is een JavaScript-bibliotheek aan de clientzijde waarmee klanten van Adobe Experience Cloud kunnen communiceren met de verschillende services in de [!DNL Experience Cloud] via het Adobe Experience Platform Edge Network. Naast de JavaScript-bibliotheek is er een [tagextensie](./extension/web-sdk-extension-configuration.md) om met uw configuraties van SDK van het Web te helpen.

Voor een geleidelijke gids aan vestiging SDK van het Web met markeringen en het verzenden van gegevens naar de oplossingen gelieve te zien [Zelfstudie Adobe Experience Cloud implementeren met Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html?lang=en).

>[!IMPORTANT]
>
>Dit product ontwikkelt zich voortdurend en groeit om steeds meer gebruiksgevallen te ondersteunen. Als u de nieuwste ontwikkelingen wilt bijhouden en wilt zien wat wij op dit moment steunen, raadpleegt u de [pagina met ondersteunde gebruiksgevallen](https://github.com/orgs/adobe/projects/18/views/1).

## Adobe Experience Edge

[!DNL Adobe Experience Platform Web SDK] maakt deel uit van de verzameling die de [!DNL Adobe Experience Edge]. [!DNL Experience Edge] bestaat uit de volgende technologieën:

* **[[!DNL Adobe Experience Platform Web SDK]](#overview):** Een JavaScript SDK en tagextensie om de implementatie aanzienlijk te vereenvoudigen [!DNL Adobe] technologieën.
* **[[!DNL Adobe Experience Platform Mobile SDK]](https://aep-sdks.gitbook.io/docs/getting-started/overview):** Een uitbreiding van de mobiele SDK van v5 zodat klanten de nieuwe implementatiemethode kunnen gebruiken
* **[[!DNL Adobe Experience Platform Edge Network]](../server-api/overview.md):** Een globaal verdeeld netwerk van servers die een nieuwe methodologie om toelaten op te stellen [!DNL Adobe] producten

De [!DNL Adobe Experience Edge] is een nieuw kader voor gegevensverzameling met lage latentie, pluggable computergebruik en snelle gegevensactivering op alle adresseerbare kanalen.

[!DNL Adobe Experience Edge] biedt één geconsolideerde SDK voor elk kanaal (JavaScript, Mobiel, Server-kant), dat gegevens verzendt naar een gemeenschappelijk Adobe-domein (`adobedc.net`) en ontvangt één enkele nuttige lading voor gegevens en ervaringslevering.

Aan de serverzijde, maken een verenigde randgateway en een gemeenschappelijk kader van de platformdiensten het gemakkelijk om nieuwe mogelijkheden in deze real-time gegevensverwerkingsomgeving op te nemen en op te stellen.  Deze architectuur:

* Vermindert klantentijd aan waarde
* Beëindigt de behoefte aan &quot;punt&quot;integratie
* Verbetert de prestaties in vergelijking met de oude bibliotheken
* Lagere kosten
* Verhoogt de snelheid van innovatie
* Creeert duurzame concurrerende voordelen voor klanten van Adobe

Met één enkel geconsolideerd randsysteem kunnen klanten hun reclame-, marketing- of personalisatiecampagnes op alle kanalen als een geïntegreerde ervaring beheren. Het staat [!DNL Adobe] om de diensten met lagere totale kosten van eigendom voor klanten te leveren.  Het helpt ook de snelheid van productinnovatie te verhogen door de rand in real time pluggable te maken en toe te staan [!DNL Adobe] en zijn klanten om nieuwe mogelijkheden en klant-bepaalde logica aan dat real time systeem sneller toe te voegen.

## Video-overzicht {#video}

De volgende video geeft een overzicht van de Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network].

>[!VIDEO](https://video.tv.adobe.com/v/34141?quality=12&learn=on)

## Bibliotheken die worden vervangen door de Web SDK {#sdks}

De SDK van het Web is niet alleen een omslag rond bestaande bibliotheken. Het is een volledig nieuwe bibliotheek, die vanaf de grond is geschreven om functies van bestaande bibliotheken te integreren. Het doel is een einde te maken aan de uitdagingen waarbij tags in de juiste volgorde moeten worden afgevuurd, inconsistentie met bibliotheekversieproblemen en een beter beheer van afhankelijkheden. Het is een nieuwe manier om de [!DNL Experience Cloud] en [open bron](https://github.com/adobe/alloy).

De SDK van het Web vervangt de volgende SDK&#39;s:

* Visitor.js
* AppMeasurement.js
* AT.js
* DIL.js

Naast een nieuwe bibliotheek, is er een nieuw eindpunt dat de HTTP- verzoeken aan de oplossingen van Adobe stroomlijnt. Vóór, stuurde Visitor.js een blokkerende vraag naar de dienst van bezoekersidentiteitskaart, toen stuurde AT.js een vraag naar Adobe Target, zond DIL.js een vraag naar Adobe Audience Manager, en tenslotte stuurde AppMeasurement.js een vraag naar Adobe Analytics. Deze nieuwe bibliotheek en eindpunt kunnen een identiteitskaart terugwinnen, een halen [!DNL Target] ervaring, gegevens verzenden naar [!DNL Audience Manager]en geef de gegevens door aan Adobe Experience Platform in één aanroep.

De volgende video demonstreert Adobe Experience Platform [!DNL Web SDK] en Adobe Experience Platform [!DNL Edge Network] in actie. Het videovoorbeeld gebruikt één enkele vraag aan Adobe die gegevens naar verzendt [!DNL Experience Platform], [!DNL Analytics], [!DNL Audience Manager], en [!DNL Target].

>[!VIDEO](https://video.tv.adobe.com/v/34148)

## Migreren van bestaande bibliotheken naar Web SDK {#migrating-to-web-sdk}

Om uw migratie vanaf om het even welk [bestaande bibliotheken](#sdks) naar Web SDK, biedt Adobe een gestroomlijnd verbeteringspad, dat u toestaat om elke individuele pagina van uw website aan Web SDK te migreren, zonder de behoefte om uw volledige website in één keer te migreren.

Dit betekent dat u Web SDK op een pagina kunt gebruiken en de bestaande bibliotheken op de andere pagina&#39;s kunt verlaten, tot u hen eveneens kunt migreren.

### at.js aan de migratieoverwegingen van SDK van het Web {#considerations}

Voordat u pagina&#39;s migreert die [!DNL at.js] aan Web SDK, zorg ervoor om de volgende de configuratieopties van SDK van het Web toe te laten. Zo blijft het bezoekersprofiel behouden tijdens het navigeren vanaf pagina&#39;s met [!DNL at.js ] naar pagina&#39;s die Web SDK gebruiken.

* [` idMigrationEnabled`](fundamentals/configuring-the-sdk.md#id-migration-enabled)
* [` targetMigrationEnabled`](fundamentals/configuring-the-sdk.md#targetMigrationEnabled)


>[!IMPORTANT]
>
>De volgende functies van het Doel worden niet ondersteund bij het migreren van at.js naar Web SDK:
> * [Aanbiedingen omleiden](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en)
> * [CNAME en ondersteuning voor andere domeinen](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/?lang=en)


Na het migreren van at.js aan Web SDK, zou u moeten verwijderen `targetMigrationEnabled` van uw configuratie.



