---
keywords: Audience Manager DIL extensie;doelpublieksbeheer;dil-extensie
title: Audience Manager DIL-extensie
description: De extensie Audience Manager van de DIL is een DMP-bestemming (Data Management Platform) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
exl-id: 7e1099de-0650-4ee2-b746-721afe194097
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 0%

---

# Audience Manager DIL-extensie {#aam-dil-extension}

## Overzicht {#overview}

Dit is de extensie Adobe Audience Manager Data Integration Library (client-side implementatie). Opmerking: Deze extensie is niet bedoeld voor het doorsturen van Adobe Analytics-gegevens via de server (SSF). Gebruik voor SSF de extensie Adobe Analytics. Belangrijk: Vanaf versie 8.0 is DIL sterk afhankelijk van de [!DNL Experience Cloud] ID Service, versie 3.3 of hoger. Voer beide uit [!DNL Experience Cloud] ID-service en DIL voor volledige [!DNL Audience Manager] mogelijkheden voor gegevensintegratie.

[!DNL Audience Manager] DIL is een extensie DMP (Data Management Platform) in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit raadpleegt u de [Audience Manager extensiepagina](../../../tags/extensions/client/audience-manager/overview.md) in de tagdocumentatie.

Dit doel is een tagextensie. Raadpleeg voor meer informatie over de manier waarop extensies werken in Platform de [overzicht van tagextensies](../launch-extensions/overview.md).

![Audience Manager DIL-extensie](../../assets/catalog/data-management-platform/aam-dil-extension/configure.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in het dialoogvenster [!DNL Destinations] catalogus voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot tags en vraag deze om u de **[!UICONTROL manage_properties]** toestemming zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

Als u het dialoogvenster [!DNL Audience Manager] DIL-extensie:

In de [Interface Platform](https://platform.adobe.com/), ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in het rechterspoor. Als de **[!UICONTROL Configure]** de controle is grijs uit, u mist **[!UICONTROL manage_properties]** toestemming. Zie [Vereisten](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen in het dialoogvenster [codedocumentatie](../../../tags/ui/administration/companies-and-properties.md#properties-page).

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie, zie [Audience Manager extensiepagina](../../../tags/extensions/client/audience-manager/overview.md) in de tagdocumentatie.

U kunt de extensie ook rechtstreeks installeren in het dialoogvenster [UI voor gegevensverzameling](https://experience.adobe.com/#/data-collection/). Zie de handleiding op [toevoegen, nieuwe extensie](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) voor meer informatie .

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen. In de UI van de Inzameling van Gegevens, kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Voor meer informatie over het instellen van regels voor uw extensies raadpleegt u het overzicht over [regels](../../../tags/ui/managing-resources/rules.md) in de tagdocumentatie.

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de interface nog weergegeven **[!UICONTROL Install]** voor de extensie. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om uw extensie te configureren of te verwijderen.

Als u uw extensie wilt upgraden, raadpleegt u de handleiding op het tabblad [upgradeproces voor extensie](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
