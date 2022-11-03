---
keywords: gtag;google gtag;google extension;google gtag extension;GTAG
title: Google-tag-extensie
description: De Google-tag-extensie is een advertentiebestemming in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
exl-id: 14a466f2-78a0-4493-93cd-3dcdae048042
source-git-commit: c3f6650df5fabe9736e4b11a43c41ae39f014425
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Google-tag-extensie {#gtag-advertising-extension}

>[!IMPORTANT]
>
>De hier beschreven Google-tagextensie is vervangen door de extensie [[!DNL Google Global Site Tag (gtag)]](https://exchange.adobe.com/apps/ec/101437/google-global-site-tag-gtag) uitbreiding ontwikkeld door [!DNL Acronym]. U kunt de [!DNL Google Global Site Tag (gtag)] binnen de [[!UICONTROL Tags]](../../../tags/home.md) werkruimte in de UI voor gegevensverzameling of Experience Platform.

## Overzicht {#overview}

Google laden `gtag.js` op uw site om gebeurtenisgegevens naar [!DNL Google Analytics], Google Ads, en [!DNL Google Marketing Platform]. Met deze extensie voegt u alleen de tagcode toe aan uw site. U moet andere Google-extensies gebruiken om gebeurtenissen en handelingen toe te voegen die gtag gebruiken.

Google gtag is een advertentie-uitbreiding in Adobe Experience Platform. Zie de extensiepagina op voor meer informatie over de extensiefunctionaliteit [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

Dit doel is een tagextensie. Zie voor meer informatie over de manier waarop tagextensies werken in Platform de [overzicht van tagextensies](../launch-extensions/overview.md).

![Google-tag-extensie](../../assets/catalog/advertising/gtag-advertising/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in het dialoogvenster [!DNL Destinations] catalogus voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot tags en vraag deze om u de **[!UICONTROL manage_properties]** toestemming zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De Google-tagextensie installeren:

In de [Interface Platform](https://platform.adobe.com/), ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in het rechterspoor. Als de **[!UICONTROL Configure]** de controle is grijs uit, u mist **[!UICONTROL manage_properties]** toestemming. Zie [Vereisten](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen in het dialoogvenster [Sectie Eigenschappen van pagina](../../../tags/ui/administration/companies-and-properties.md#properties-page) van in de tagdocumentatie.

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

Voor informatie over de opties van de uitbreidingsconfiguratie en installatiesteun, zie [Google-tagpagina op Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html).

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
