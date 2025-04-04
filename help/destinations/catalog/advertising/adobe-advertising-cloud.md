---
keywords: Advertentie Cloud;adverteren cloudextentie; adverteren cloudbestemming
title: Adobe Advertising Cloud Extension
description: De extensie Adobe Advertising Cloud is een advertentiedoel in Adobe Experience Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
exl-id: 3415a85f-5678-4f5b-b7cf-e185a66d084f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Adobe Advertising Cloud Extension {#adobe-advertising-cloud-extension}

## Overzicht {#overview}

Dit is de [!DNL Advertising Cloud] -extensie voor het implementeren van [!DNL Advertising Cloud] -conversie en publiekstags voor zowel de DSP als de Search (DCO wordt momenteel niet ondersteund).

Adobe Advertising Cloud is een advertentie-extensie in Adobe Experience Platform.

Dit doel is een tagextensie. Voor meer informatie over hoe de uitbreidingen van markeringen in Experience Platform werken, zie het [ overzicht van markeringsuitbreidingen ](../launch-extensions/overview.md).

![ uitbreiding van de Wolk van de Reclame van Adobe ](../../assets/catalog/advertising/adobe-advertising-cloud/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus Doelen voor alle klanten die Experience Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot de functies voor gegevensverzameling in de gebruikersinterface en vraag hen om u de machtiging **[!UICONTROL manage_properties]** te verlenen, zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De extensie Adobe Advertising Cloud installeren:

In de [ interface van Experience Platform ](https://platform.adobe.com/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in de rechtertrack. Als het besturingselement **[!UICONTROL Configure]** grijs wordt weergegeven, ontbreekt de machtiging **[!UICONTROL manage_properties]** . Zie [ Eerste vereisten ](#prerequisites).

Selecteer de eigenschap tag waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Leer over eigenschappen in de [ tagdocumentatie ](../../../tags/ui/administration/companies-and-properties.md).

De werkstroom neemt u aan de UI van de Inzameling van Gegevens om de installatie te voltooien.

U kunt de uitbreiding direct in [ de Inzameling UI van Gegevens ](https://experience.adobe.com/#/data-collection/) ook installeren. Zie de gids op [ toevoegend een nieuwe uitbreiding ](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) voor meer informatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen. In de UI van de Inzameling van Gegevens, kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Voor meer informatie over vestiging regels voor uw uitbreidingen, zie het overzicht op [ regels ](../../../tags/ui/managing-resources/rules.md) in de markeringsdocumentatie.

## Uitbreiding configureren, bijwerken en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de interface nog steeds **[!UICONTROL Install]** voor de extensie weergegeven. Kik van het installatiewerkschema zoals die in [ wordt beschreven installeer uitbreiding ](#install-extension) om uw uitbreiding te vormen of te schrappen.

Om uw uitbreiding te bevorderen, zie de gids op het [ proces van de uitbreidingsverbetering ](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
