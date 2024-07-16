---
title: Aanpasbare inzichten voor uitgebreide toepassingsrapportage
description: Leer hoe u SQL-query's kunt gebruiken om inzichten voor uw aangepaste dashboards te genereren.
exl-id: c60a9218-4ac0-4638-833b-bdbded36ddf5
source-git-commit: 5bb954da7c1e05922a4e0f8d0bc7d3ab5c8e0e58
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Aanpasbare inzichten voor uitgebreide toepassingsrapportage

Gebruik aangepaste SQL-query&#39;s om inzichten effectief te extraheren uit verschillende gestructureerde datasets. De technische mensen kunnen vraag pro wijze gebruiken om complexe analyse met SQL uit te voeren en dan deze analyse met niet-technische gebruikers door grafieken op uw douanedashboard te delen of hen in Csv- dossiers uit te voeren. Deze methode voor het creëren van inzicht is zeer geschikt voor lijsten met duidelijke verhoudingen en staat voor een grotere graad van aanpassing binnen uw inzichten en filters toe die niche gebruiksgevallen kunnen aanpassen.

>[!IMPORTANT]
>
>De vraag pro wijze is slechts beschikbaar aan gebruikers die [ Gegevens Distiller SKU ](../../../query-service/data-distiller/overview.md) hebben gekocht.

Als u inzichten wilt genereren op basis van SQL, moet u eerst een dashboard maken.

## Een aangepast dashboard maken {#create-custom-dashboard}

Als u een aangepast dashboard wilt maken, selecteert u **[!UICONTROL Dashboards]** in het navigatievenster aan de linkerkant om de werkruimte Dashboards te openen. Selecteer vervolgens **[!UICONTROL Create dashboard]** .

![ de inventaris van het dashboard met Create benadrukte dashboard.](../../images/customizable-insights/create-dashboard.png)

Het dialoogvenster **[!UICONTROL Create dashboard]** wordt weergegeven. Er zijn twee opties waaruit u de methode voor het maken van het dashboard kunt kiezen. Om uw inzichten tot stand te brengen kunt u of een bestaand gegevensmodel met [[!UICONTROL Guided design mode]](../../user-defined-dashboards.md) of uw eigen SQL met [!UICONTROL Query pro mode] gebruiken.

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Het gebruik van een bestaand gegevensmodel biedt de voordelen van een gestructureerd, efficiënt en schaalbaar framework dat is afgestemd op uw specifieke bedrijfsbehoeften. Leren hoe te om [ inzichten van een bestaand gegevensmodel ](../../user-defined-dashboards.md#create-widget) tot stand te brengen, verwijs naar de gids van het douanedashboard.

De inzichten die van SQL vragen worden geproduceerd bieden veel grotere flexibiliteit en aanpassing aan. De technische mensen kunnen vraag pro wijze gebruiken om complexe analyse op SQL uit te voeren en dan deze analyse met niet-technische gebruikers door dit dashboardvermogen te delen. Selecteer **[!UICONTROL Query pro mode]** gevolgd door **[!UICONTROL Save]** .

>[!NOTE]
>
>Als u eenmaal een selectie hebt gemaakt, kunt u deze selectie in het dashboard niet meer wijzigen. In plaats daarvan moet u een nieuw dashboard maken met een andere methode voor het maken van het dashboard.

![ de [!UICONTROL Create dashboard] dialoog met Vraag pro wijze en sparen benadrukte.](../../images/customizable-insights/query-pro-mode.png)

## Een grafiek maken {#create-a-chart}

Zie de [ vraag pro wijze gids ](./query-pro-mode.md) voor geleidelijke instructies bij het creëren van een grafiek met SQL.
