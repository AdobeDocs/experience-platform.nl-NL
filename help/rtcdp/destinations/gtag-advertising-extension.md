---
title: Google-tag-extensie
seo-title: Google-tag-extensie
description: De Google-tagextensie is een advertentiebestemming in het Adobe Real-time Customer Data Platform. Zie de extensiepagina op Adobe Exchange voor meer informatie over de extensiefunctionaliteit.
seo-description: null
translation-type: tm+mt
source-git-commit: ff91395844c239415123a33d65fa0deb2221ae25

---


# Google-tag-extensie {#gtag-advertising-extension}

## Overzicht {#overview}

Laad Google&#39;s `gtag.js` in uw site om gebeurtenisgegevens naar Google Analytics, Google Ads en Google Marketing Platform te verzenden. Met deze extensie voegt u alleen de tagcode toe aan uw site. U moet andere Google-extensies gebruiken om gebeurtenissen en handelingen toe te voegen die gtag gebruiken.

Google-tag is een advertentie-extensie in Adobe Real-time Customer Data Platform. Zie de extensiepagina op [Adobe Exchange](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html)voor meer informatie over de extensiefunctionaliteit.

Deze bestemming is een uitbreiding van de Lancering van het Platform van de Ervaring. Voor meer informatie over hoe de uitbreidingen van de Lancering in Adobe in real time CDP werken, zie het Overzicht [van de uitbreidingen van de Lancering van het Platform van de](/help/rtcdp/destinations/experience-platform-launch-extensions.md)Ervaring Platform.

![Google-tag-extensie](/help/rtcdp/destinations/assets/gtag-advertising-extension.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus Doelen voor alle klanten die Adobe Real-time CDP hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot de Launch-functie van Experience Platform. Experience Platform Launch wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, voordelige functie. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot Starten en vraag hen om u de **[!UICONTROL manage_properties]** machtiging te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De Google-tagextensie installeren:

1. Ga in de [Adobe Real-time CDP-interface](http://platform.adobe.com/)naar **[!UICONTROL Destinations > Catalog]**.
2. Selecteer de extensie in de catalogus of gebruik de zoekbalk.
3. Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Install Extension]** in de rechtertrack. Als het **[!UICONTROL Install Extension]** besturingselement grijs wordt weergegeven, ontbreekt de **[!UICONTROL manage_properties]** bevoegdheid. Zie [Voorwaarden](#prerequisites).
4. Selecteer in het **[!UICONTROL Select available Launch property]** venster de eigenschap Launch waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in Launch. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](https://docs.adobe.com/content/help/en/launch/using/reference/admin/companies-and-properties.html#properties-page) Eigenschappen van de documentatie bij Starten.
5. Met de workflow gaat u naar Start om de installatie te voltooien.

Raadpleeg de Google-tagpagina op Adobe Exchange [](https://exchange.adobe.com/experiencecloud.details.102805.google-gtag.html)voor informatie over de configuratieopties voor extensies en de installatieondersteuning.

U kunt de extensie ook rechtstreeks installeren in de interface [Start van](https://launch.adobe.com/)Experience Platform. Zie [Een nieuwe extensie](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html#add-a-new-extension) toevoegen in de documentatie bij Starten.


## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen in Launch.

In Launch kunt u regels instellen voor geïnstalleerde extensies om gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming te verzenden. Raadpleeg de documentatie bij [Regels voor meer informatie over het instellen van regels voor uw extensies](https://docs.adobe.com/help/en/launch/using/reference/manage-resources/rules.html).

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de interface Launch.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de CDP-gebruikersinterface van Adobe Real-time nog steeds weergegeven **[!UICONTROL Install]** voor de extensie. Kies de installatieworkflow zoals beschreven in de extensie [](#install-extension) Installeren om de extensie te starten en te configureren of te verwijderen.

Zie [Extensies upgraden](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/extension-upgrade.html) in de documentatie bij Starten voor een upgrade van de extensie.
