---
keywords: gtag;google gtag;google extension;google gtag extension;GTAG
title: Google-tag-extensie
description: De Google-tag-extensie is een advertentiebestemming in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Google-tag-extensie {#gtag-advertising-extension}

## Overzicht {#overview}

Laad Google `gtag.js` in uw site om gebeurtenisgegevens naar [!DNL Google Analytics], Google Ads en [!DNL Google Marketing Platform] te verzenden. Met deze extensie voegt u alleen de tagcode toe aan uw site. U moet andere Google-extensies gebruiken om gebeurtenissen en handelingen toe te voegen die gtag gebruiken.

Google-tag is een advertentie-extensie in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op [Adobe Uitwisseling](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Dit doel is een Adobe Experience Platform Launch-extensie. Voor meer informatie over hoe de uitbreidingen van de Platform launch in Platform werken, zie [overzicht van de uitbreidingen van Adobe Experience Platform Launch](../launch-extensions/overview.md).

![Google-tag-extensie](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus [!DNL Destinations] voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot Adobe Experience Platform Launch nodig. platform launch wordt aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang tot de Platform launch te krijgen en vraag hen om u de **[!UICONTROL manage_properties]** toestemming te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De Google-tagextensie installeren:

Ga in [Platform interface](http://platform.adobe.com/) naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer **[!UICONTROL Configure]** in de rechtertrack. Als het **[!UICONTROL Configure]** besturingselement grijs is, ontbreekt u de **[!UICONTROL manage_properties]** toestemming. Zie [Eerste vereisten](#prerequisites).

Selecteer in het venster **[!UICONTROL Select available Platform Launch property]** de eigenschap Platform launch waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in de Platform launch. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](../../../tags/ui/administration/companies-and-properties.md#properties-page) van de documentatie bij Platform launches.

De werkstroom neemt u aan Platform launch om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie en installatiesteun, zie [Google gtag pagina op Adobe Uitwisseling](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

U kunt de extensie ook rechtstreeks installeren in de [Adobe Experience Platform Launch-interface](https://launch.adobe.com/). Zie [Een nieuwe extensie toevoegen](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in de documentatie van de Platform launch.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks in Platform launch regels voor de extensie instellen.

In Platform launch, kunt u opstellingsregels voor uw geïnstalleerde uitbreidingen om gebeurtenisgegevens naar de uitbreidingsbestemming slechts in bepaalde situaties te verzenden. Zie [Documentatie van regels](../../../tags/ui/managing-resources/rules.md) voor meer informatie over instellingsregels voor uw extensies.

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de interface van de Platform launch.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt **[!UICONTROL Install]** voor de extensie nog steeds weergegeven in de interface van het Platform. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om de Platform launch te starten en uw extensie te configureren of te verwijderen.

Om uw uitbreiding te bevorderen, zie [Uitbreiding verbetering](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de documentatie van de Platform launch.
