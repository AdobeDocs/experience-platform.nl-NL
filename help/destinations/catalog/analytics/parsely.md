---
keywords: Parseren. ly;parverse;Parse;parse.ly;Parse.ly
title: Parse.ly Analytics-extensie
description: De extensie Parse.ly Analytics is een analysedoel in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
exl-id: 84d98e74-3e34-406c-9b80-81100c766dc8
source-git-commit: b4e869f9bc29122db4fc66ccda752a50c7db729f
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# [!DNL Parse.ly Analytics] extension {#parsely-analytics-extension}

## Overzicht {#overview}

[!DNL Parse.ly Analytics] helpt meer dan 2500 bedrijven gegevens te gebruiken om hun online publiek te begrijpen . Met deze extensie installeert u een JavaScript-fragment dat bijhoudt hoe bezoekers de inhoud van uw site beïnvloeden.

Parse.ly is een analytische extensie in Adobe Experience Platform. Zie voor meer informatie over de extensiefunctionaliteit [Parse.ly Analytics](https://www.parse.ly/).

Dit doel is een tagextensie. Zie voor meer informatie over de manier waarop tagextensies werken in Platform de [overzicht van tagextensies](../launch-extensions/overview.md).

![Parse.ly Analytics-extensie](../../assets/catalog/analytics/parsely/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in het dialoogvenster [!DNL Destinations] catalogus voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot tags en vraag deze om u de **[!UICONTROL manage_properties]** toestemming zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

Als u het dialoogvenster [!DNL Parse.ly] extensie:

In de [Interface Platform](https://platform.adobe.com/), ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in het rechterspoor. Als de **[!UICONTROL Configure]** de controle is grijs uit, u mist **[!UICONTROL manage_properties]** toestemming. Zie [Vereisten](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen in het dialoogvenster [Sectie Eigenschappen van pagina](../../../tags/ui/administration/companies-and-properties.md#properties-page) van in de tagdocumentatie.

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

U kunt de extensie ook rechtstreeks installeren in het dialoogvenster [UI voor gegevensverzameling](https://experience.adobe.com/#/data-collection/). Zie de sectie over [toevoegen, nieuwe extensie](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in de tagdocumentatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen.

U kunt regels instellen voor geïnstalleerde extensies, zodat gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming worden verzonden. Voor meer informatie over het instellen van regels voor uw extensies raadpleegt u de [codedocumentatie](../../../tags/ui/managing-resources/rules.md).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de interface van het Platform nog weergegeven **[!UICONTROL Install]** voor de extensie. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om uw extensie te configureren of te verwijderen.

Als u uw extensie wilt upgraden, raadpleegt u de handleiding op het tabblad [upgradeproces voor extensie](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
