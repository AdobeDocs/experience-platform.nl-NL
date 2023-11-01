---
keywords: Marketo Web Personalization;marketo web personalization;Marketo Web Personalization extension;marketo web personalization extension;marketo;marketo;Marketo
title: Marketo Web Personalization extension
description: De extensie Marketo Web Personalization is een personalisatiebestemming in Adobe Experience Platform. Voor meer informatie over de uitbreidingsfunctionaliteit, zie de uitbreidingspagina op de Uitwisseling van de Adobe.
exl-id: 2f194a5e-13b7-460a-a968-29131771efca
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 0%

---

# [!DNL Marketo Web Personalization] extension {#marketo-web-personalization-extension}

## Overzicht {#overview}

Deze extensie implementeert het script voor [!DNL Marketo's] Web Personalization en ContentAI toepassingen. [!DNL Marketo] Webpersonalisatie identificeert en personaliseert inhoud op unieke wijze aan de kenmerken van webbezoekers, zoals zelfafbeeldingen voor anonieme bezoekers en een breed scala aan gedragskenmerken binnen de [!DNL Marketo] Aanpassingsplatform voor bekende bezoekers. [!DNL Marketo] ContentAI bevat mogelijkheden voor door AI aangedreven aanbevelingen en personalisatie voor web- en e-mailcampagnes die uniek zijn voor B2B-klanten.

[!DNL Marketo Web Personalization] is een personalisatie-uitbreiding in Adobe Experience Platform. Lees voor meer informatie over webpersonalisatie en ContentAI in Marketo [Overzicht van webpersonalisatie](https://experienceleague.adobe.com/docs/marketo/using/product-docs/web-personalization/understanding-web-personalization/web-personalization-overview.html).

Dit doel is een tagextensie. Raadpleeg voor meer informatie over de werking van tagextensies in Platform de klasse [overzicht van tagextensies](../launch-extensions/overview.md).

![Marketo Web Personalization Extension](../../assets/catalog/personalization/marketo-web-personalization/catalog.png)

## Vereisten {#prerequisites}

Deze extensie is beschikbaar in het dialoogvenster [!DNL Destinations] catalogus voor alle klanten die Platform hebben aangeschaft.

Als u deze extensie wilt gebruiken, hebt u toegang tot tags in Adobe Experience Platform nodig. Tags worden aan Adobe Experience Cloud-klanten aangeboden als een inbegrepen, waardetoevoegend element. Neem contact op met de systeembeheerder van uw organisatie om toegang te krijgen tot tags en vraag deze om u de **[!UICONTROL manage_properties]** toestemming zodat u extensies kunt installeren.

## Extensie installeren {#install-extension}

Als u het dialoogvenster [!DNL Marketo Web Personalization] extensie:

In de [Platforminterface](https://platform.adobe.com/), ga naar **[!UICONTROL Destinations]** > **[!UICONTROL Catalog]**.

Selecteer de extensie in de catalogus of gebruik de zoekbalk.

Klik op de bestemming om deze te markeren en selecteer vervolgens **[!UICONTROL Configure]** in het rechterspoor. Als de **[!UICONTROL Configure]** de controle is grijs uit, u mist **[!UICONTROL manage_properties]** toestemming. Zie [Vereisten](#prerequisites).

Selecteer de eigenschap waarin u de extensie wilt installeren. U kunt ook een nieuwe eigenschap maken. Een bezit is een inzameling van regels, gegevenselementen, gevormde uitbreidingen, milieu&#39;s, en bibliotheken. Meer informatie over eigenschappen in het dialoogvenster [Sectie Eigenschappen van pagina](../../../tags/ui/administration/companies-and-properties.md#properties-page) van in de tagdocumentatie.

Het werkschema begeleidt u door de stappen om de installatie te voltooien.

U kunt de extensie ook rechtstreeks installeren in het dialoogvenster [UI voor gegevensverzameling](https://experience.adobe.com/#/data-collection/). Zie de sectie over [toevoegen, nieuwe extensie](../../../tags/ui/managing-resources/extensions/overview.md#add-a-new-extension) in de tagdocumentatie.

## De extensie gebruiken {#how-to-use}

Nadat u de extensie hebt geïnstalleerd, kunt u regels instellen.

U kunt regels instellen voor geïnstalleerde extensies, zodat gebeurtenisgegevens alleen in bepaalde situaties naar de extensiebestemming worden verzonden. Voor meer informatie over het instellen van regels voor uw extensies raadpleegt u de [codedocumentatie](../../../tags/ui/managing-resources/rules.md).

## Uitbreiding configureren, bijwerken en verwijderen {#configure-upgrade-delete}

U kunt extensies configureren, upgraden en verwijderen in de gebruikersinterface voor gegevensverzameling.

>[!TIP]
>
>Als de extensie al op een van uw eigenschappen is geïnstalleerd, wordt de interface van het platform nog weergegeven **[!UICONTROL Install]** voor de extensie. Kies de installatieworkflow zoals beschreven in [Extensie installeren](#install-extension) om uw extensie te configureren of te verwijderen.

Als u uw extensie wilt upgraden, raadpleegt u de handleiding op het tabblad [upgradeproces voor extensie](../../../tags/ui/managing-resources/extensions/extension-upgrade.md) in de tagdocumentatie.
