---
keywords: gtag;google gtag;google extension;google gtag extension;GTAG
title: Google-tag-extensie
seo-title: Google-tag-extensie
description: De Google-tagextensie is een advertentiebestemming in Real-time Customer Data Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
seo-description: De Google-tagextensie is een advertentiebestemming in Real-time Customer Data Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
translation-type: tm+mt
source-git-commit: 0232acdc64019b9d93888e8137ef9bc8e114779b
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 2%

---


# Google-tag-extensie {#gtag-advertising-extension}

## Overzicht {#overview}

Laad Google&#39;s `gtag.js` in uw site om gebeurtenisgegevens naar [!DNL Google Analytics], Google Ads en [!DNL Google Marketing Platform]. Met deze extensie voegt u alleen de tagcode toe aan uw site. U moet andere Google-extensies gebruiken om gebeurtenissen en handelingen toe te voegen die gtag gebruiken.

Google-tag is een advertentie-extensie in Real-time Customer Data Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van [Adobe](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Dit doel is een Adobe Experience Platform Launch-extensie. Voor meer informatie over hoe de uitbreidingen van de Lancering van het Platform in Adobe in real time CDP werken, zie het overzicht [van de uitbreidingen van](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Adobe Experience Platform Launch.

![Google-tag-extensie](/help/rtcdp/destinations/assets/gtag-advertising-extension.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de [!DNL Destinations] catalogus voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot Adobe Experience Platform Launch nodig. Platform starten wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend onderdeel. Contacteer uw organisatiebeheerder om toegang tot de Lancering van het Platform te krijgen en hen te vragen om u de **[!UICONTROL manage_properties]** toestemming te verlenen zodat kunt u uitbreidingen installeren.

## Extensie installeren {#install-extension}

De Google-tagextensie installeren:

1. In de [Adobe in real time CDP interface](http://platform.adobe.com/), ga naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configureren]** in de rechterrail. Als de **[!UICONTROL Configure]** controle grayed is, mist u de toestemming **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).
4. In het **[!UICONTROL Uitgezochte beschikbare de bezitsvenster]** van de Lancering van het Platform, selecteer het bezit van de Lancering van het Platform waarin u de uitbreiding wilt installeren. U kunt ook een nieuwe eigenschap maken bij het starten van het Platform. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de documentatie bij Starten van Platform.
5. Met de workflow gaat u naar Starten van Platform om de installatie te voltooien.

Raadpleeg de Google-tagpagina op Adobe Exchange voor informatie over de configuratieopties voor extensies en installatieondersteuning [](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

U kunt de extensie ook rechtstreeks in de [Adobe Experience Platform Launch-interface](https://launch.adobe.com/)installeren. Zie [Een nieuwe extensie](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) toevoegen in de documentatie bij het starten van het Platform.


## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen in Platform starten.

In de Lancering van het Platform, kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt uitbreidingen in de interface van de Lancering van het Platform vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt CDP-interface in realtime van Adobe nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kies de installatieworkflow zoals beschreven in de extensie [](#install-extension) Installeren om Platform starten te starten en uw extensie te configureren of te verwijderen.

Raadpleeg de [extensie voor een upgrade](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) van de extensie in de documentatie bij Starten van Platform.
