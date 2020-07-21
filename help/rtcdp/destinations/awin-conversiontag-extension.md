---
title: Awin Advertiser Conversion Tag-extensie
seo-title: Awin Advertiser Conversion Tag-extensie
description: De extensie Awin Advertiser Conversion Tag is een advertentie-bestemming in het Adobe Real-time Platform van klantgegevens. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
seo-description: null
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 2%

---


# Awin Advertiser Conversion Tag-extensie {#awin-conversiontag-extension}

## Overzicht {#overview}

De conversietag is de verklaring van het voorwerp van JavaScript AWIN.Tracking.Sale, dat op de bevestigingspagina wordt gedaan om de Mastertag te instrueren dat een omzetting heeft plaatsgevonden. Vervolgens worden de benodigde traceerverzoeken uitgevoerd.

De conversietag van Awin Advertiser is een advertentie-uitbreiding in het Platform van de Gegevens van de Klant van Adobe In real time. Zie de extensiepagina op [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)voor meer informatie over de extensiefunctionaliteit.

Dit doel is een [!DNL Experience Platform Launch] extensie. Zie Overzicht [!DNL Launch] van extensies voor [](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Experience Platforms Launch voor meer informatie over hoe extensies werken in Adobe Real-time CDP.

![Awin Advertiser Conversiontag extension in UI](/help/rtcdp/destinations/assets/awin-conversiontag-extension.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus Doelen voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wordt aangeboden aan klanten van Adobe Experience Cloud als inbegrepen, waardetoevoegend element. Neem contact op met uw organisatiebeheerder om toegang te krijgen [!DNL Launch] en vraag hem of haar om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De [!DNL Awin Advertiser Conversion Tag] extensie installeren:

1. Ga in de [Adobe Real-time CDP-interface](http://platform.adobe.com/)naar **[!UICONTROL Doelen > Catalogus]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer Extensie **** installeren in de rechterrail. Als het besturingselement Extensie **** installeren grijs wordt weergegeven, ontbreekt u de machtiging **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).
4. Selecteer in het venster **[!UICONTROL Selecteer beschikbare]** starteigenschap de [!DNL Launch] eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in [!DNL Launch]. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de [!DNL Launch] documentatie.
5. U moet de installatie voltooien [!DNL Launch] om de workflow te voltooien.

Raadpleeg de pagina Conversietag voor [Adobe Advertiser op Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.103240.awin-conversion-tag.html)voor informatie over de configuratieopties voor extensies en de installatieondersteuning.

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
