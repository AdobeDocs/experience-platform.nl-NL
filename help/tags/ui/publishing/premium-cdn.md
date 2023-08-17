---
title: Experience Platform-tags (China)
description: Leer meer over de Chinese functie voor tags (Experience Platform Tags) en hoe u deze kunt gebruiken om uw inhoud in meerdere geografische regio's te leveren.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Experience Platform-tags (China)

Wanneer u een [Door Adobe beheerde host](./hosts/managed-by-adobe-host.md) om uw Adobe Experience Platform-tagelementen op uw website te leveren, worden deze elementen over de hele wereld verspreid via verschillende CDN&#39;s (Content Delivery Networks) voor een zo snel mogelijke downloadsnelheid. Er zijn echter bepaalde gebieden waarvoor alle website-elementen moeten worden gerepliceerd en gehost op een server in dat gebied.

Om dit te verklaren, verstrekken de markeringen in Experience Platform een eigenschap van de Markeringen van het Experience Platform (China) die u toestaat om inhoud aan deze speciale gebieden te leveren.

Ondersteuning voor Experience Platform Tags (China) is een betaalde functie en moet worden aangeschaft door uw organisatie om deze functie in te schakelen en te gebruiken. Deze gids behandelt hoe te om deze eigenschap in de UI van het Experience Platform of UI van de Inzameling van Gegevens te vormen en te gebruiken nadat het is gekocht.

## Experience Platform Tags (China) inschakelen voor uw organisatie

Experience Platform Tags (China) worden ingeschakeld op bedrijfsniveau. Zodra uw organisatie de eigenschap van de Markeringen van het Experience Platform (China) heeft gekocht, zal een beheerder van de Adobe de eigenschap in UI voor uw bedrijf toelaten.

## Tagbibliotheken opnieuw samenstellen en installeren met bijgewerkte insluitcodes

Als Experience Platform Tags (China) is ingeschakeld, betekent dit niet dat de elementen van de tag direct worden gerepliceerd en klaar zijn voor gebruik in de nieuwe gebieden. Dit betekent alleen dat u nu kunt kiezen wanneer u zich aanmeldt voor deze functie.

>[!IMPORTANT]
>
>Bibliotheken die zijn gebouwd voordat tags in China zijn toegestaan, zullen net zo blijven functioneren als nu. Dit geldt ook voor bibliotheken die niet door Adobe worden beheerd, aangezien [gearchiveerde omgevingen](./environments.md#archive) alleen relatieve URL&#39;s gebruiken voor hun middelenpaden. Houd er rekening mee dat elke bibliotheek die u maakt en die niet door Adobe wordt beheerd, zich gedraagt alsof de functie Tags in China niet is ingeschakeld nadat u Experience Platform Tags (China) hebt ingeschakeld.

Als u tags hebt ingeschakeld in China en alle bibliotheken die u wilt gebruiken vanuit de nieuwe hostinggebieden opnieuw hebt samengesteld, kunt u de nieuwe insluitcodes van de hostingregio ophalen om deze toe te voegen aan uw websites.

>[!NOTE]
>
>De insluitcode van de bibliotheek die onder de [!UICONTROL Standard] Het hostinggebied blijft ongewijzigd werken en eventuele insluitcodes voor de paginanummers boven en onder aan de pagina zijn al op uw websites aanwezig.

Ga naar **[!UICONTROL Environments]** pagina of bekijk de instructies voor het installeren van de omgeving in het bewerkingsscherm van de bibliotheek om de nieuwe insluitcodes te zoeken. Elk nieuw ondersteund hostinggebied wordt weergegeven na het [!UICONTROL Standard] hostinggebied (wordt gebruikt voor gebieden in de wereld die zonder Experience Platform-tags (China) worden ondersteund). In de onderstaande screenshot ziet u een insluitcode voor de Chinese regio die het volgende gebruikt `.cn` als topdomein (TLD).

![Code insluiten voor de regio China](../../images/ui/publishing/premium-cdn/embed-codes.png)

Kies de juiste insluitcode voor de webpagina en plak deze in het dialoogvenster `<head>` -code van het document. Voor meer informatie over het gebruik van insluitcodes voor het installeren van tagbibliotheken raadpleegt u de [UI-gids voor omgevingen](./environments.md#installation).

## Volgende stappen

In deze handleiding wordt beschreven hoe u de functie Experience Platform Tags (China) voor de implementatie van tags kunt inschakelen en installeren. Raadpleeg voor meer informatie over het installeren en testen van tagbibliotheken op uw web en mobiele eigenschappen de [publicatieoverzicht](./overview.md).
