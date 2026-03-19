---
keywords: Audience Manager DIL-extensie;doelpublieksbeheer;dil-extensie
title: Audience Manager DIL Extension
description: De Audience Manager DIL-extensie is een bestemming voor een Data Management Platform (DMP) in Adobe Experience Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 2dd4ae4146f7c1c5228e22d24ff2ba31010adedb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---

# Audience Manager DIL Extension {#aam-dil-extension}

## Overzicht {#overview}

Dit is de Adobe Audience Manager Data Integration Library-extensie (client-side implementatie). Opmerking: deze extensie is niet bedoeld voor het doorsturen van Adobe Analytics-gegevens via de server (SSF). Gebruik voor SSF de extensie Adobe Analytics. Belangrijk: vanaf versie 8.0 is DIL sterk afhankelijk van de [!DNL Experience Cloud] ID Service, versie 3.3 of hoger. Implementeer zowel [!DNL Experience Cloud] ID Service als DIL voor volledige [!DNL Audience Manager] mogelijkheden voor gegevensintegratie.

[!DNL Audience Manager] DIL is een extensie voor Data Management Platform (DMP) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de [ de uitbreidingspagina van Audience Manager ](../../../tags/extensions/client/audience-manager/overview.md) in de markeringsdocumentatie.

Dit doel is een tagextensie. Voor meer informatie over hoe de uitbreidingen in Experience Platform werken, zie het [ overzicht van markeringsuitbreidingen ](../launch-extensions/overview.md).

![ de uitbreiding van Audience Manager DIL ](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus [!DNL Destinations] voor alle klanten die Experience Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang tot tags te krijgen en vraag hen om u de **[!UICONTROL manage_properties]** -machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

U installeert als volgt de extensie [!DNL Audience Manager] DIL:

In de [ interface van Experience Platform ](https://platform.adobe.com/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Selecteer het doel en selecteer vervolgens **[!UICONTROL Configure]** in de rechterrails. Als het besturingselement **[!UICONTROL Configure]** grijs wordt weergegeven, ontbreekt de machtiging **[!UICONTROL manage_properties]** . Zie [ Eerste vereisten ](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Leer over eigenschappen in de [ tagdocumentatie ](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie de [ de uitbreidingspagina van Audience Manager ](../../../tags/extensions/client/audience-manager/overview.md) in de markeringsdocumentatie.

U kunt de uitbreiding direct in [ de Inzameling UI van Gegevens ](https://experience.adobe.com/#/data-collection/) ook installeren. Zie de gids op [ toevoegend een nieuwe uitbreiding ](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) voor meer informatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen. In de UI van de Inzameling van Gegevens, kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Voor meer informatie over vestiging regels voor uw uitbreidingen, zie het overzicht op [ regels ](../../../tags/ui/managing-resources/rules.md) in de markeringsdocumentatie.

## Uitbreiding configureren, bijwerken en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de interface nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kik van het installatiewerkschema zoals die in [ wordt beschreven installeer uitbreiding ](#install-extension) om uw uitbreiding te vormen of te schrappen.

Om uw uitbreiding te bevorderen, zie de gids op het [ proces van de uitbreidingsverbetering ](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
