---
keywords: target extension;target
title: Adobe Target-extensie
seo-title: Adobe Target-extensie
description: De uitbreiding van Adobe Target is een verpersoonlijkingsbestemming in het Platform van de Gegevens van de Klant van Adobe in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
seo-description: De uitbreiding van Adobe Target is een verpersoonlijkingsbestemming in het Platform van de Gegevens van de Klant van Adobe in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
translation-type: tm+mt
source-git-commit: d9bf874dbfcc00c0a6e267f1a2e96f1223054825
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 2%

---


# Adobe Target-extensie {#adobe-target-extension}

## Overzicht {#overview}

Adobe Target is de Adobe Experience Cloud-oplossing die alles biedt wat u nodig hebt om de ervaring van uw klanten op maat te maken en aan te passen en zo uw omzet op uw website en mobiele sites, apps, sociale media en andere digitale kanalen te maximaliseren.

Adobe Target is een personalisatie-uitbreiding in het Platform van de Gegevens van de Klant van de Adobe in real time. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van [Adobe](https://exchange.adobe.com/experiencecloud.details.100162.html).

Dit doel is een [!DNL Adobe Experience Platform Launch] extensie. Voor meer informatie over hoe de [!DNL Platform Launch] uitbreidingen in Adobe in real time CDP werken, zie het overzicht [van de uitbreidingen van het](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Adobe Target-extensie](/help/rtcdp/destinations/assets/adobe-target-extension.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de [!DNL Destinations] catalogus voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend element. Neem contact op met uw organisatiebeheerder om toegang te krijgen [!DNL Platform Launch] en vraag hem of haar om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De Adobe Target-extensie installeren:

1. In de [Adobe in real time CDP interface](http://platform.adobe.com/), ga naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configureren]** in de rechterrail. Als de **[!UICONTROL Configure]** controle grayed is, mist u de toestemming **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).
4. Selecteer in het **[!UICONTROL venster Beschikbare Platform starten-eigenschap]** selecteren de [!DNL Platform Launch] eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in [!DNL Platform Launch]. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de [!DNL Launch] documentatie.
5. U moet de installatie voltooien [!DNL Platform Launch] om de workflow te voltooien.

Zie de [Adobe Target-extensiepagina](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/target-extension/overview.html) in de [!DNL Launch] documentatie bij Experience voor informatie over de configuratieopties voor extensies.

U kunt de extensie ook rechtstreeks in de [Adobe Experience Platform Launch-interface](https://launch.adobe.com/)installeren. Zie [Een nieuwe extensie](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) toevoegen in de [!DNL Platform Launch] documentatie.


## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen [!DNL Platform Launch].

In [!DNL Platform Launch], kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt uitbreidingen in de [!DNL Platform Launch] interface vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt CDP-interface in realtime van Adobe nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kies de installatieworkflow die wordt beschreven in de extensie [](#install-extension) Installeren om de extensie te configureren [!DNL Platform Launch] en te verwijderen.

Zie [Extensies upgraden](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de [!DNL Platform Launch] documentatie voor een upgrade van de extensie.
