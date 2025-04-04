---
keywords: Google-advertenties;google-advertenties, extensie;Google Ads-extensie
title: Google Ads-extensie
description: De extensie Google Ads is een advertentiebestemming in Adobe Experience Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
exl-id: b563ce68-7b04-4cfb-b0c3-151f34ec7c1a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# [!DNL Google Ads] extension

## Overzicht {#overview}

Deze extensie volgt conversies van gebruikers die op de [!DNL Google Ads] klikken. U moet ook de extensie gtag.js installeren en deze toevoegen aan uw bibliotheek, omdat [!DNL Google Ads] hiervan afhankelijk is.

[!DNL Google Ads] is een advertentie-extensie in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op [ Adobe Exchange ](https://www.adobeexchange.com/experiencecloud.details.101383.google-ads.html).

Dit doel is een tagextensie. Voor meer informatie over hoe de markeringsuitbreidingen in Experience Platform werken, zie het [ overzicht van markeringsuitbreidingen ](../launch-extensions/overview.md).

![ uitbreiding van Advertenties Google ](../../assets/catalog/advertising/google-ads-extension/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus Doelen voor alle klanten die Experience Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang tot tags te krijgen en vraag hen om u de **[!UICONTROL manage_properties]** -machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De extensie [!DNL Google Ads] installeren:

In de [ interface van Experience Platform ](https://platform.adobe.com/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in de rechtertrack. Als het besturingselement **[!UICONTROL Configure]** grijs wordt weergegeven, ontbreekt de machtiging **[!UICONTROL manage_properties]** . Zie [ Eerste vereisten ](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Leer over eigenschappen in de [ sectie van de pagina van Eigenschappen ](../../../tags/ui/administration/companies-and-properties.md#properties-page) van in de markeringsdocumentatie.

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie en installatiesteun, zie de [ pagina van de Advertentie van Google op Adobe Exchange ](https://www.adobeexchange.com/experiencecloud.details.101383.google-ads.html).

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
