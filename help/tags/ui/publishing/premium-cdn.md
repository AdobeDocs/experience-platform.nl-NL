---
title: Premium CDN-ondersteuning voor tags
description: Leer over de premiumfunctie CDN voor tags en hoe u deze kunt gebruiken om uw inhoud in meerdere geografische regio's te leveren.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---

# Premium CDN-ondersteuning voor tags (bèta)

>[!IMPORTANT]
>
>De premiumfunctie CDN voor tags bevindt zich momenteel in de bètaversie en uw organisatie heeft mogelijk nog geen toegang tot deze functie. Deze documentatie kan worden gewijzigd.

Wanneer u een [Door Adobe beheerde host](./hosts/managed-by-adobe-host.md) om uw Adobe Experience Platform-tagelementen op uw website te leveren, worden deze elementen over de hele wereld verspreid via verschillende CDN&#39;s (Content Delivery Networks) voor een zo snel mogelijke downloadsnelheid. Er zijn echter bepaalde gebieden waarvoor alle website-elementen moeten worden gerepliceerd en gehost op een server in dat gebied.

Om dit te verklaren, verstrekken de markeringen in Experience Platform een premieCDN eigenschap die u toestaat om inhoud aan deze speciale gebieden te leveren.

Premium CDN-ondersteuning is een betaalde functie en moet door uw organisatie worden aangeschaft om deze in te schakelen en te gebruiken. Deze gids behandelt hoe te om deze eigenschap in de UI van de Inzameling van Gegevens te vormen en te gebruiken nadat het is gekocht.

## Premium-CDN inschakelen voor uw organisatie

Premium CDN is ingeschakeld op bedrijfsniveau. Zodra uw organisatie de premieCDN eigenschap heeft gekocht, zal een beheerder van Adobe voor uw bedrijf in de Inzameling van Gegevens UI toelaten.

## Tagbibliotheken opnieuw samenstellen en installeren met bijgewerkte insluitcodes

Als premium-CDN eenmaal is ingeschakeld, betekent dit niet dat de tagelementen direct worden gerepliceerd en klaar zijn voor gebruik in de nieuwe gebieden. Dit betekent alleen dat u nu kunt kiezen wanneer u zich aanmeldt voor deze functie.

>[!IMPORTANT]
>
>Bibliotheken die zijn gebouwd voordat de CDN van de premie wordt ingeschakeld, blijven functioneren zoals ze dat nu doen. Dit geldt ook voor bibliotheken die niet door Adobe worden beheerd, aangezien [gearchiveerde omgevingen](./environments.md#archive) alleen relatieve URL&#39;s gebruiken voor hun middelenpaden. Houd er rekening mee dat elke bibliotheek die u maakt en die niet door Adobe wordt beheerd, zich gedraagt alsof de premiumfunctie CDN niet is ingeschakeld nadat u premium CDN hebt ingeschakeld.

Nadat u de CDN-naam van de Premium hebt ingeschakeld en alle bibliotheken die u wilt gebruiken vanuit de nieuwe hostingsgebieden hebt herbouwd, kunt u de nieuwe insluitcodes van de hostingsgebieden ophalen om deze toe te voegen aan uw websites.

>[!NOTE]
>
>De insluitcode van de bibliotheek die onder de [!UICONTROL Standard] Het hostinggebied blijft ongewijzigd werken en eventuele insluitcodes voor de paginanummers boven en onder aan de pagina zijn al op uw websites aanwezig.

Ga naar **[!UICONTROL Environments]** pagina of bekijk de instructies voor het installeren van de omgeving in het bewerkingsscherm van de bibliotheek om de nieuwe insluitcodes te zoeken. Elk nieuw ondersteund hostinggebied wordt weergegeven na het [!UICONTROL Standard] hostingsgebied (wordt gebruikt voor gebieden in de wereld die zonder premium-CDN worden ondersteund). In de onderstaande screenshot ziet u een insluitcode voor de Chinese regio die het volgende gebruikt `.cn` als topdomein (TLD).

![Code insluiten voor de regio China](../../images/ui/publishing/premium-cdn/embed-codes.png)

Kies de juiste insluitcode voor de webpagina en plak deze in het dialoogvenster `<head>` -code van het document. Voor meer informatie over het gebruik van insluitcodes voor het installeren van tagbibliotheken raadpleegt u de [UI-gids voor omgevingen](./environments.md#installation).

## Volgende stappen

In deze handleiding wordt beschreven hoe u de premiumfunctie CDN voor de implementatie van tags kunt inschakelen en installeren. Raadpleeg voor meer informatie over het installeren en testen van tagbibliotheken op uw web en mobiele eigenschappen de [publicatieoverzicht](./overview.md).
