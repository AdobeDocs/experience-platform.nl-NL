---
keywords: Parseren. ly;parverse;Parse;parse.ly;Parse.ly
title: Parse.ly Analytics-extensie
description: De extensie Parse.ly Analytics is een analysedoel in Adobe Experience Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
exl-id: 84d98e74-3e34-406c-9b80-81100c766dc8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# [!DNL Parse.ly Analytics] extension {#parsely-analytics-extension}

## Overzicht {#overview}

Met [!DNL Parse.ly Analytics] kunnen meer dan 2500 bedrijven gegevens gebruiken om hun onlinepubliek te begrijpen. Deze extensie installeert een JavaScript-fragment dat bijhoudt hoe bezoekers met inhoud op uw site werken.

Parse.ly is een analytische extensie in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie [ Analytics Parse.ly ](https://www.parse.ly/).

Dit doel is een tagextensie. Voor meer informatie over hoe de markeringsuitbreidingen in Experience Platform werken, zie het [ overzicht van markeringsuitbreidingen ](../launch-extensions/overview.md).

![ Parse.ly de Uitbreiding van Analytics ](../../assets/catalog/analytics/parsely/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus [!DNL Destinations] voor alle klanten die Experience Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang tot tags te krijgen en vraag hen om u de **[!UICONTROL manage_properties]** -machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De extensie [!DNL Parse.ly] installeren:

In de [ interface van Experience Platform ](https://platform.adobe.com/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in de rechtertrack. Als het besturingselement **[!UICONTROL Configure]** grijs wordt weergegeven, ontbreekt de machtiging **[!UICONTROL manage_properties]** . Zie [ Eerste vereisten ](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Leer over eigenschappen in de [ sectie van de pagina van Eigenschappen ](../../../tags/ui/administration/companies-and-properties.md#properties-page) van in de markeringsdocumentatie.

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

U kunt de uitbreiding direct in [ de Inzameling UI van Gegevens ](https://experience.adobe.com/#/data-collection/) ook installeren. Voor meer informatie, zie de sectie op [ toevoegend een nieuwe uitbreiding ](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in de markeringsdocumentatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen.

U kunt regels instellen voor geïnstalleerde extensies, zodat gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming worden verzonden. Voor meer informatie over vestiging regels voor uw uitbreidingen, zie de [ tagdocumentatie ](../../../tags/ui/managing-resources/rules.md).

## Uitbreiding configureren, bijwerken en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de gebruikersinterface van Experience Platform nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kik van het installatiewerkschema zoals die in [ wordt beschreven installeer uitbreiding ](#install-extension) om uw uitbreiding te vormen of te schrappen.

Om uw uitbreiding te bevorderen, zie de gids op het [ proces van de uitbreidingsverbetering ](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
