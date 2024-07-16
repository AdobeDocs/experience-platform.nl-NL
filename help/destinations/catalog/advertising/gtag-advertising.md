---
keywords: gtag;google gtag;google extension;google gtag extension;GTAG
title: Google-tag-extensie
description: De Google-tag-extensie is een advertentiebestemming in Adobe Experience Platform. Zie de extensiepagina over Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 0%

---

# Google-tag-extensie {#gtag-advertising-extension}

>[!IMPORTANT]
>
>De hier beschreven Google-tagextensie is vervangen door de extensie [[!DNL Google Global Site Tag (gtag)] ](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) die is ontwikkeld door [!DNL Acronym] . U kunt de extensie [!DNL Google Global Site Tag (gtag)] vinden in de [[!UICONTROL Tags]](../../../tags/home.md) -werkruimte in de gebruikersinterface van de gegevensverzameling of de gebruikersinterface van het Experience Platform.

## Overzicht {#overview}

Laad Google `gtag.js` in uw site om gebeurtenisgegevens naar [!DNL Google Analytics] , Google Ads en [!DNL Google Marketing Platform] te verzenden. Met deze extensie voegt u alleen de tagcode toe aan uw site. U moet andere Google-extensies gebruiken om gebeurtenissen en handelingen toe te voegen die gtag gebruiken.

Google gtag is een advertentie-uitbreiding in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op [ Adobe Exchange ](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Dit doel is een tagextensie. Voor meer informatie over hoe de markeringsuitbreidingen in Platform werken, zie het [ overzicht van markeringsuitbreidingen ](../launch-extensions/overview.md).

![ Google gtag uitbreiding ](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus [!DNL Destinations] voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang tot tags te krijgen en vraag hen om u de **[!UICONTROL manage_properties]** -machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De Google-tagextensie installeren:

In de [ interface van het Platform ](https://platform.adobe.com/), ga **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in de rechtertrack. Als het besturingselement **[!UICONTROL Configure]** grijs wordt weergegeven, ontbreekt de machtiging **[!UICONTROL manage_properties]** . Zie [ Eerste vereisten ](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Leer over eigenschappen in de [ sectie van de pagina van Eigenschappen ](../../../tags/ui/administration/companies-and-properties.md#properties-page) van in de markeringsdocumentatie.

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie en installatiesteun, zie de [ Google gtag pagina op Adobe Exchange ](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

U kunt de uitbreiding direct in [ de Inzameling UI van Gegevens ](https://experience.adobe.com/#/data-collection/) ook installeren. Voor meer informatie, zie de sectie op [ toevoegend een nieuwe uitbreiding ](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in de markeringsdocumentatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen.

U kunt regels instellen voor geïnstalleerde extensies, zodat gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming worden verzonden. Voor meer informatie over vestiging regels voor uw uitbreidingen, zie de [ tagdocumentatie ](../../../tags/ui/managing-resources/rules.md).

## Uitbreiding configureren, bijwerken en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de interface van het platform nog steeds **[!UICONTROL Install]** weergegeven voor de extensie. Kik van het installatiewerkschema zoals die in [ wordt beschreven installeer uitbreiding ](#install-extension) om uw uitbreiding te vormen of te schrappen.

Om uw uitbreiding te bevorderen, zie de gids op het [ proces van de uitbreidingsverbetering ](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
