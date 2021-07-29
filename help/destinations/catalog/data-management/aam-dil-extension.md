---
keywords: Audience Manager DIL extensie;doelpublieksbeheer;dil-extensie
title: Audience Manager DIL-extensie
description: De extensie Audience Manager van de DIL is een DMP-bestemming (Data Management Platform) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Audience Manager DIL-extensie {#aam-dil-extension}

## Overzicht {#overview}

Dit is de extensie Adobe Audience Manager Data Integration Library (client-side implementatie). Opmerking: Deze extensie is niet bedoeld voor het doorsturen van Adobe Analytics-gegevens via de server (SSF). Gebruik voor SSF de extensie Adobe Analytics. Belangrijk: Vanaf versie 8.0 is DIL sterk afhankelijk van [!DNL Experience Cloud] ID Service, versie 3.3 of hoger. Implementeer zowel [!DNL Experience Cloud] ID-service als DIL voor volledige [!DNL Audience Manager] mogelijkheden voor gegevensintegratie.

[!DNL Audience Manager] DIL is een extensie DMP (Data Management Platform) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie [de uitbreidingspagina van de Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) in de markeringsdocumentatie.

Dit doel is een tagextensie. Voor meer informatie over hoe de uitbreidingen in Platform werken, zie [markeringsuitbreidingen overzicht](../launch-extensions/overview.md).

![Audience Manager DIL-extensie](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus [!DNL Destinations] voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang tot tags te krijgen en vraag hen om u de **[!UICONTROL manage_properties]** toestemming te geven zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De extensie [!DNL Audience Manager] DIL installeren:

Ga in [Platform interface](http://platform.adobe.com/) naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer **[!UICONTROL Configure]** in de rechtertrack. Als het **[!UICONTROL Configure]** besturingselement grijs is, ontbreekt u de **[!UICONTROL manage_properties]** toestemming. Zie [Eerste vereisten](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de [tagdocumentatie](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie [de uitbreidingspagina van de Audience Manager](../../../tags/extensions/web/audience-manager/overview.md) in de markeringsdocumentatie.

U kunt de extensie ook rechtstreeks installeren in de gebruikersinterface [Gegevensverzameling](https://experience.adobe.com/#/data-collection/). Zie de gids op [toevoegend een nieuwe uitbreiding](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) voor meer informatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen. In de UI van de Inzameling van Gegevens, kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Voor meer informatie over opstellingsregels voor uw uitbreidingen, zie het overzicht over [regels](../../../tags/ui/managing-resources/rules.md) in de markeringsdocumentatie.

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt **[!UICONTROL Install]** voor de extensie nog steeds weergegeven. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om de extensie te configureren of te verwijderen.

Als u de extensie wilt bijwerken, raadpleegt u de handleiding bij het [upgradeproces van de extensie](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de documentatie bij de codes.
