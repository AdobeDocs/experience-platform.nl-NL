---
keywords: Advertising Cloud;advertising cloud extension; advertising cloud destination
title: Adobe Advertising Cloud-extensie
seo-title: Adobe Advertising Cloud-extensie
description: De extensie Adobe Advertising Cloud is een advertentiebestemming in Real-time Customer Data Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
seo-description: De extensie Adobe Advertising Cloud is een advertentiebestemming in Real-time Customer Data Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
translation-type: tm+mt
source-git-commit: c24676970629f5a39297001357f8af40895533d9
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 0%

---


# Adobe Advertising Cloud-extensie {#adobe-advertising-cloud-extension}

## Overzicht {#overview}

Dit is de [!DNL Advertising Cloud] uitbreiding voor het uitvoeren van [!DNL Advertising Cloud] omzetting en segmentmarkeringen voor zowel de DSP als het Onderzoek (DCO wordt momenteel niet gesteund).

Adobe Advertising Cloud is een advertentie-uitbreiding in Real-time Customer Data Platform.

Dit doel is een [!DNL Adobe Experience Platform Launch] extensie. Voor meer informatie over hoe de [!DNL Platform Launch] uitbreidingen in CDP in real time werken, zie het overzicht [van de uitbreidingen van het](../launch-extensions/overview.md)Experience Platform Launch.

![Adobe Advertising Cloud-extensie](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Vereisten {#prerequisites}

Deze uitbreiding is beschikbaar in de catalogus van Doelen voor alle klanten die CDP in real time hebben gekocht.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend element. Neem contact op met uw organisatiebeheerder om toegang te krijgen [!DNL Launch] en vraag hem of haar om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De Adobe Advertising Cloud-extensie installeren:

Ga in de [Real-time CDP interface](http://platform.adobe.com/)naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configureren]** in de rechterrail. Als de **[!UICONTROL Configure]** controle grayed is, mist u de toestemming **[!UICONTROL manage_properties]** . Zie [Voorwaarden](#prerequisites).

Selecteer in het **[!UICONTROL venster Beschikbare Platform starten-eigenschap]** selecteren de [!DNL Platform Launch] eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in [!DNL Platform Launch]. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de [!DNL Launch] documentatie.

U moet de installatie voltooien [!DNL Platform Launch] om de workflow te voltooien.

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
