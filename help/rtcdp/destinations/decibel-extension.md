---
title: Decibel-extensie
seo-title: Decibel-extensie
description: De Decibel uitbreiding is een analysebestemming in het Platform van de Gegevens van de Klant van Adobe in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
seo-description: De Decibel uitbreiding is een analysebestemming in het Platform van de Gegevens van de Klant van Adobe in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
translation-type: tm+mt
source-git-commit: a251d843401d2f092e368a4cdac217171fa4687f
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 2%

---


# [!DNL Decibel] extension {#decibel-extension}

## Overzicht {#overview}

Implementeer snel en naadloos [!DNL Decibel] op uw wegeigenschappen. De extra geavanceerde configuraties kunnen ook met regels worden opgesteld gebruikend acties die door de uitbreiding ter beschikking worden gesteld.

[!DNL Decibel] is een analytische uitbreiding in het Platform van de Gegevens van de Klant van de Adobe in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van [Adobe](https://exchange.adobe.com/experiencecloud.details.100913.html).

Deze bestemming is een Experience Platform Launch uitbreiding. Voor meer informatie over hoe de uitbreidingen van de Lancering in Adobe in real time CDP werken, zie het overzicht [van de uitbreidingen van het](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Decibel-extensie](assets/decibel-extension.png)


## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de [!DNL Destinations] catalogus voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot Experience Platform Launch nodig. Experience Platform Launch wordt aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot Launch en vraag hen om u de machtiging **[!UICONTROL manage_properties]** te verlenen, zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De [!DNL Decibel] extensie installeren:

1. In de [Adobe in real time CDP interface](http://platform.adobe.com/), ga naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configureren]** in de rechterrail. Als de **[!UICONTROL Configure]** controle grayed is, mist u de toestemming **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).
4. Selecteer in het venster **[!UICONTROL Selecteer beschikbare]** starteigenschap de eigenschap Launch waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in Launch. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de documentatie bij Starten.
5. Met de workflow gaat u naar Start om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie de [Decibel uitbreidingspagina](https://exchange.adobe.com/experiencecloud.details.100913.html) op de Uitwisseling van Adobe.

U kunt de extensie ook rechtstreeks in de interface [](https://launch.adobe.com/)Experience Platform Launch installeren. Zie [Een nieuwe extensie](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) toevoegen in de documentatie bij Starten.


## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen in Launch.

In Launch kunt u regels instellen voor geïnstalleerde extensies om gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de interface Launch.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt CDP-interface in realtime van Adobe nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kies de installatieworkflow zoals beschreven in de extensie [](#install-extension) Installeren om de extensie te starten en te configureren of te verwijderen.

Zie [Extensies upgraden](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de documentatie bij Starten voor een upgrade van de extensie.



