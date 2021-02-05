---
keywords: Audience Manager DIL extensie;doelpublieksbeheer;dil-extensie
title: Audience Manager DIL-extensiebestemming
description: De extensie Audience Manager van de DIL is een DMP-bestemming (Data Management Platform) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
translation-type: tm+mt
source-git-commit: 6655714d4b57d9c414cd40529bcee48c7bcd862d
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 0%

---


# Audience Manager DIL-extensie {#aam-dil-extension}

Dit is de extensie Adobe Audience Manager Data Integration Library (client-side implementatie). Opmerking: Deze extensie is niet bedoeld voor het doorsturen van Adobe Analytics-gegevens via de server (SSF). Gebruik voor SSF de extensie Adobe Analytics. Belangrijk: Vanaf versie 8.0 is DIL sterk afhankelijk van [!DNL Experience Cloud] ID Service, versie 3.3 of hoger. Implementeer zowel [!DNL Experience Cloud] ID-service als DIL voor volledige [!DNL Audience Manager] mogelijkheden voor gegevensintegratie.

[!DNL Audience Manager] DIL is een extensie DMP (Data Management Platform) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie [de uitbreidingspagina van de Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) in de documentatie van het Experience Platform Launch.

Dit doel is een extensie [!DNL Experience Platform Launch]. Voor meer informatie over hoe de uitbreidingen van de Lancering in Platform werken, zie [overzicht van de uitbreidingen van het Experience Platform Launch](../launch-extensions/overview.md).

![Audience Manager DIL-extensie](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus [!DNL Destinations] voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Adobe Experience Platform Launch]. [!DNL Platform Launch] wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot [!DNL Platform Launch] en vraag hen om u de **[!UICONTROL manage_properties]** toestemming te geven zodat u extensies kunt installeren.

## Extensie {#install-extension} installeren

De extensie [!DNL Audience Manager] DIL installeren:

Ga in [Platform interface](http://platform.adobe.com/), naar **[!UICONTROL Doelen]** > **[!UICONTROL Catalogus]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om het te benadrukken, dan uitgezocht **[!UICONTROL vorm]** in het juiste spoor. Als de **[!UICONTROL Configure]** controle uit grijs is, mist u **[!UICONTROL manage_properties]** toestemming. Zie [Eerste vereisten](#prerequisites).

Selecteer in het venster **[!UICONTROL Selecteer de beschikbare opstarteigenschap]** de eigenschap [!DNL Launch] waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in Launch. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://experienceleague.adobe.com/docs/launch/using/reference/admin/companies-and-properties.html#properties-page) van de [!DNL Launch]-documentatie.

Met de workflow gaat u naar [!DNL Launch] om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie [de uitbreidingspagina van de Audience Manager](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-audience-manager-extension.html) in [!DNL Experience Launch] documentatie.

U kunt de extensie ook rechtstreeks installeren in de [Adobe Experience Platform Launch-interface](https://launch.adobe.com/). Zie [Een nieuwe extensie toevoegen](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/overview.html?lang=en#add-a-new-extension) in de [!DNL Platform Launch]-documentatie.

## De extensie {#how-to-use} gebruiken

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen in [!DNL Platform Launch].

In [!DNL Platform Launch] kunt u regels instellen voor geïnstalleerde extensies om gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming te verzenden. Zie [Documentatie van regels](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/rules.html) voor meer informatie over instellingsregels voor uw extensies.

## De uitbreiding {#configure-upgrade-delete} vormen, bevorderen en schrappen

U kunt uitbreidingen in de [!DNL Platform Launch] interface vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt **[!UICONTROL Install]** voor de extensie nog steeds weergegeven in de interface van het Platform. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om naar [!DNL Platform Launch] te gaan en uw extensie te configureren of verwijderen.

Zie [Extensie upgrade](https://experienceleague.adobe.com/docs/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de [!DNL Platform Launch]-documentatie om de extensie te upgraden.



