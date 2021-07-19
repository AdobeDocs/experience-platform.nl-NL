---
Keywords: ECID;ecid
title: Experience Cloud ID Service-extensie
description: De uitbreiding van de Dienst van identiteitskaart van de Experience Cloud is een verpersoonlijkingsbestemming in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van Adobe.
exl-id: 4cc49c14-66ec-43e0-a106-70d9c3646d87
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# [!DNL Experience Cloud] ID Service-extensie {#adobe-ecid-extension}

## Overzicht {#overview}

Deze extensie implementeert de [!DNL Experience Cloud] ID-service, die bezoekers identificeert voor alle [!DNL Experience Cloud]-oplossingen.

[!DNL Experience Cloud] ID Service is een personalisatie-uitbreiding in Adobe Experience Platform. Zie [Experience Cloud ID Service extension page](../../../tags/extensions/web/id-service/overview.md) in [!DNL Experience Platform Launch] documentatie voor meer informatie over de extensiefunctionaliteit.

Dit doel is een extensie [!DNL Adobe Experience Platform Launch]. Voor meer informatie over hoe [!DNL Platform Launch] uitbreidingen in Platform werken, zie [Overzicht van de uitbreidingen van het Experience Platform Launch](../launch-extensions/overview.md).

![Adobe ECID-extensie](../../assets/catalog/personalization/adobe-ecid/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in de catalogus Doelen voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang nodig tot [!DNL Experience Platform Launch]. [!DNL Experience Platform Launch] wordt aangeboden aan Adobe Experience Cloud-klanten als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot [!DNL Launch] en vraag hen om u de **[!UICONTROL manage_properties]** toestemming te verlenen zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

De extensie [!DNL Experience Cloud] ID-service installeren:

Ga in [Platform interface](http://platform.adobe.com/) naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer **[!UICONTROL Configure]** in de rechtertrack. Als het **[!UICONTROL Configure]** besturingselement grijs is, ontbreekt u de **[!UICONTROL manage_properties]** toestemming. Zie [Eerste vereisten](#prerequisites).

Selecteer in het venster **[!UICONTROL Select available Platform Launch property]** de eigenschap [!DNL Platform Launch] waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken in [!DNL Platform Launch]. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen vindt u in de sectie [Eigenschappen op de pagina](../../../tags/ui/administration/companies-and-properties.md#properties-page) van de [!DNL Launch]-documentatie.

Met de workflow gaat u naar [!DNL Platform Launch] om de installatie te voltooien.

Zie [Experience Cloud ID Service extension page](../../../tags/extensions/web/id-service/overview.md) in [!DNL Experience Launch] documentatie voor informatie over de configuratieopties voor extensies en installatieondersteuning.

U kunt de extensie ook rechtstreeks installeren in de [Adobe Experience Platform Launch-interface](https://launch.adobe.com/). Zie [Een nieuwe extensie toevoegen](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in de [!DNL Platform Launch]-documentatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u rechtstreeks regels voor de extensie instellen in [!DNL Platform Launch].

In [!DNL Platform Launch] kunt u regels instellen voor geïnstalleerde extensies om gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming te verzenden. Zie [Documentatie van regels](../../../tags/ui/managing-resources/rules.md) voor meer informatie over instellingsregels voor uw extensies.

## De extensie configureren, upgraden en verwijderen {#configure-upgrade-delete}

U kunt uitbreidingen in de [!DNL Platform Launch] interface vormen, bevorderen en schrappen.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt **[!UICONTROL Install]** voor de extensie nog steeds weergegeven in de interface van het Platform. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om naar [!DNL Platform Launch] te gaan en uw extensie te configureren of verwijderen.

Zie [Extensie upgrade](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de [!DNL Platform Launch]-documentatie om de extensie te upgraden.
