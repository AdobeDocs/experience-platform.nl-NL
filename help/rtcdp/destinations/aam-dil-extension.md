---
title: Audience Manager DIL-extensie
seo-title: Audience Manager DIL-extensie
description: De Audience Manager DIL-extensie is een DMP-doel (Data Management Platform) in Adobe Real-time Customer Data Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
seo-description: De Audience Manager DIL-extensie is een DMP-doel (Data Management Platform) in Adobe Real-time Customer Data Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
translation-type: tm+mt
source-git-commit: b96286f6a06f0583b45343a513ee64f0025d79a7
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 5%

---


# Audience Manager DIL-extensie {#aam-dil-extension}

## Overzicht {#overview}

Dit is de uitbreiding van de Bibliotheek van de Integratie van Gegevens van de Adobe Audience Manager (cliënt-zijimplementatie). Opmerking: Deze extensie is niet bedoeld voor het doorsturen van gegevens via de server (SSF) van Adobe Analytics. Gebruik voor SSF de extensie Adobe Analytics. Belangrijk: Vanaf versie 8.0 is DIL sterk afhankelijk van de [!DNL Experience Cloud] ID-service, versie 3.3 of hoger. Implementeer zowel [!DNL Experience Cloud] ID Service als DIL voor volledige mogelijkheden voor [!DNL Audience Manager] gegevensintegratie.

[!DNL Audience Manager] DIL is een DMP-extensie (Data Management Platform) in Adobe Real-time Customer Data Platform. Zie de pagina [met extensies voor](https://docs.adobe.com/content/help/nl-NL/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) Audience Managers in de documentatie bij Experience Platforms Launch voor meer informatie over de extensiefunctionaliteit.

Dit doel is een [!DNL Experience Platform Launch] extensie. Zie Overzicht van extensies voor [](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platforms Launch voor meer informatie over hoe Launch-extensies werken in Adobe Real-time CDP.

![Audience Manager DIL-extensie](/help/rtcdp/destinations/assets/aam-dil-extension.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de [!DNL Destinations] catalogus voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wordt aangeboden aan klanten van Adobe Experience Cloud als inbegrepen, waardetoevoegend element. Neem contact op met uw organisatiebeheerder om toegang te krijgen [!DNL Launch] en vraag hem of haar om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

U installeert als volgt de [!DNL Audience Manager] DIL-extensie:

1. Ga in de [Adobe Real-time CDP-interface](http://platform.adobe.com/)naar **[!UICONTROL Doelen > Catalogus]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer Extensie **** installeren in de rechterrail. Als het besturingselement Extensie **** installeren grijs wordt weergegeven, ontbreekt u de machtiging **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).
4. Selecteer in het venster **[!UICONTROL Selecteer beschikbare]** starteigenschap de [!DNL Launch] eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in Launch. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de [!DNL Launch] documentatie.
5. U moet de installatie voltooien [!DNL Launch] om de workflow te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie de de uitbreidingspagina [van de](https://docs.adobe.com/content/help/nl-NL/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) Audience Manager in [!DNL Experience Launch] documentatie.

U kunt de extensie ook rechtstreeks in de interface [](https://launch.adobe.com/)Experience Platform Launch installeren. Zie [Een nieuwe extensie](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) toevoegen in de [!DNL Launch] documentatie.


## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen [!DNL Launch].

In [!DNL Launch], kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt uitbreidingen in de [!DNL Launch] interface vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt in de CDP-interface van Adobe Real-time nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kies de installatieworkflow die wordt beschreven in de extensie [](#install-extension) Installeren om de extensie te configureren [!DNL Launch] en te verwijderen.

Zie [Extensies upgraden](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de [!DNL Launch] documentatie voor een upgrade van de extensie.



