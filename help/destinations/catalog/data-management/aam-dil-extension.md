---
keywords: Audience Manager DIL extension;destination audience manager;dil extension
title: Audience Manager DIL-extensie
seo-title: Audience Manager DIL-extensie
description: De uitbreiding van de DIL van de Audience Manager is een bestemming van het Platform van het Beheer van Gegevens (DMP) in het Platform van de Gegevens van de Klant in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
seo-description: De uitbreiding van de DIL van de Audience Manager is een bestemming van het Platform van het Beheer van Gegevens (DMP) in het Platform van de Gegevens van de Klant in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
translation-type: tm+mt
source-git-commit: 0bb1622895b1e0f97fc47b5c61d456bc369746c8
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 0%

---


# Audience Manager DIL-extensie {#aam-dil-extension}

## Overzicht {#overview}

Dit is de extensie Adobe Audience Manager Data Integration Library (client-side implementatie). Opmerking: Deze extensie is niet bedoeld voor het doorsturen van Adobe Analytics-gegevens via de server (SSF). Gebruik voor SSF de extensie Adobe Analytics. Belangrijk: Vanaf versie 8.0 is DIL sterk afhankelijk van de [!DNL Experience Cloud] id-service, versie 3.3 of hoger. Implementeer zowel [!DNL Experience Cloud] ID Service als DIL voor volledige mogelijkheden voor [!DNL Audience Manager] gegevensintegratie.

[!DNL Audience Manager] DIL is een DMP-extensie (Data Management Platform) in Real-time Customer Data Platform. Zie de pagina [met extensies voor](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) Audience Managers in de documentatie bij Experience Platforms Launch voor meer informatie over de extensiefunctionaliteit.

Dit doel is een [!DNL Experience Platform Launch] extensie. Voor meer informatie over hoe de uitbreidingen van de Lancering in CDP in real time werken, zie het overzicht [van de uitbreidingen van het](../launch-extensions/overview.md)Experience Platform Launch.

![Audience Manager DIL-extensie](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de [!DNL Destinations] catalogus voor alle klanten die CDP in realtime hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend element. Neem contact op met uw organisatiebeheerder om toegang te krijgen [!DNL Platform Launch] en vraag hem of haar om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De extensie [!DNL Audience Manager] DIL installeren:

Ga in de [Real-time CDP interface](http://platform.adobe.com/)naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configureren]** in de rechterrail. Als de **[!UICONTROL Configure]** controle grayed is, mist u de toestemming **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).

Selecteer in het venster **[!UICONTROL Selecteer beschikbare]** starteigenschap de [!DNL Launch] eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in Launch. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de [!DNL Launch] documentatie.

U moet de installatie voltooien [!DNL Launch] om de workflow te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie de de uitbreidingspagina [van de](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) Audience Manager in [!DNL Experience Launch] documentatie.

U kunt de extensie ook rechtstreeks in de [Adobe Experience Platform Launch-interface](https://launch.adobe.com/)installeren. Zie [Een nieuwe extensie](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) toevoegen in de [!DNL Platform Launch] documentatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen [!DNL Platform Launch].

In [!DNL Platform Launch], kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt uitbreidingen in de [!DNL Platform Launch] interface vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt in real-time CDP-interface nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kies de installatieworkflow die wordt beschreven in de extensie [](#install-extension) Installeren om de extensie te configureren [!DNL Platform Launch] en te verwijderen.

Zie [Extensies upgraden](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de [!DNL Platform Launch] documentatie voor een upgrade van de extensie.



