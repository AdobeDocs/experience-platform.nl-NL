---
title: De extensie Bing Ads Universal Event Tracking (UET)
seo-title: De extensie Bing Ads Universal Event Tracking (UET)
description: De extensie Bing Ads Universal Event Tracking (UET) is een advertentiebestemming in het Adobe Real-time Platform met klantgegevens. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
seo-description: null
translation-type: tm+mt
source-git-commit: be4cf64c89a189a09a4a7774c8fadc76c6ee8458
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# [!DNL Bing Ads Universal Event Tracking] (UET)-extensie {#bing-ads-extension}

## Overzicht {#overview}

[!DNL Bing Ads Universal Event Tracking] (UET) for [!DNL Experience Platform Launch] is een nuttige manier om te volgen wat gebeurt nadat iemand op uw zoekadvertentie heeft geklikt. Door één UET-tag te gebruiken om op te nemen wat klanten op uw website doen, kunt u deze gegevens benutten, zodat u conversies of doelgroepen kunt bijhouden met behulp van remarketing lijsten.

[!DNL Bing Ads Universal Event Tracking] (UET) is een advertentie-uitbreiding in het Adobe Real-time Platform van de Gegevens van de Klant. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van [Adobe](https://exchange.adobe.com/experiencecloud.details.100154.html).

Dit doel is een [!DNL Experience Platform Launch] extensie. Voor meer informatie over hoe de [!DNL Launch] uitbreidingen in Adobe in real time CDP werken, zie het overzicht [van de uitbreidingen van het](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platform Launch.

![Bing Ads-extensie](assets/bing-extension.png)


## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de [!DNL Destinations] catalogus voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend element. Neem contact op met uw organisatiebeheerder om toegang te krijgen [!DNL Launch] en vraag hem of haar om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

U installeert als volgt de extensie [!DNL Bing Ads Universal Event Tracking] (UET):

1. In de [Adobe in real time CDP interface](http://platform.adobe.com/), ga naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer Extensie **** installeren in de rechterrail. Als het besturingselement Extensie **** installeren grijs wordt weergegeven, ontbreekt u de machtiging **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).
4. Selecteer in het venster **[!UICONTROL Selecteer beschikbare]** starteigenschap de [!DNL Launch] eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in [!DNL Launch]. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de [!DNL Launch] documentatie.
5. U moet de installatie voltooien [!DNL Launch] om de workflow te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie en installatiesteun, zie de pagina van het [Bing Ads Universal Event Tracking (UET) op de Uitwisseling](https://exchange.adobe.com/experiencecloud.details.100154.html)van Adobe.

U kunt de extensie ook rechtstreeks in de interface [](https://launch.adobe.com/)Experience Platform Launch installeren. Zie [Een nieuwe extensie](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) toevoegen in de [!DNL Launch] documentatie.


## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen [!DNL Launch].

In [!DNL Launch], kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt uitbreidingen in de [!DNL Launch] interface vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt CDP-interface in realtime van Adobe nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kies de installatieworkflow die wordt beschreven in de extensie [](#install-extension) Installeren om de extensie te configureren [!DNL Launch] en te verwijderen.

Zie [Extensies upgraden](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de [!DNL Launch] documentatie voor een upgrade van de extensie.
