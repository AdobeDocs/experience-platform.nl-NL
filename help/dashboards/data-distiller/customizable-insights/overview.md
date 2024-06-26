---
title: Aanpasbare inzichten voor uitgebreide toepassingsrapportage
description: Leer hoe u SQL-query's kunt gebruiken om inzichten voor uw aangepaste dashboards te genereren.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '322'
ht-degree: 0%

---

# Aanpasbare inzichten voor uitgebreide toepassingsrapportage

Gebruik aangepaste SQL-query&#39;s om inzichten effectief te extraheren uit verschillende gestructureerde datasets. De technische mensen kunnen vraag pro wijze gebruiken om complexe analyse met SQL uit te voeren en dan deze analyse met niet-technische gebruikers door grafieken op uw douanedashboard te delen of hen in Csv- dossiers uit te voeren. Deze methode voor het creëren van inzicht is zeer geschikt voor lijsten met duidelijke verhoudingen en staat voor een grotere graad van aanpassing binnen uw inzichten en filters toe die niche gebruiksgevallen kunnen aanpassen.

>[!IMPORTANT]
>
>De modus Query Pro is alleen beschikbaar voor gebruikers die de [Data Distiller SKU](../../../query-service/data-distiller/overview.md).

Als u inzichten wilt genereren op basis van SQL, moet u eerst een dashboard maken.

## Een aangepast dashboard maken {#create-custom-dashboard}

Als u een aangepast dashboard wilt maken, selecteert u **[!UICONTROL Dashboards]** in het navigatievenster aan de linkerkant om de dashboardwerkruimte te openen. Selecteer vervolgens **[!UICONTROL Create dashboard]**.

![Het dashboardoverzicht met het dashboard maken gemarkeerd.](../../images/customizable-insights/create-dashboard.png)

De **[!UICONTROL Create dashboard]** wordt weergegeven. Er zijn twee opties waaruit u de methode voor het maken van het dashboard kunt kiezen. Om uw inzichten te creëren kunt u of een bestaand gegevensmodel met gebruiken [[!UICONTROL Guided design mode]](../../user-defined-dashboards.md) of uw eigen SQL met de [!UICONTROL Query pro mode].

<!-- Maybe reference Guided design mode in other places on UDD doc. -->

Het gebruik van een bestaand gegevensmodel biedt de voordelen van een gestructureerd, efficiënt en schaalbaar framework dat is afgestemd op uw specifieke bedrijfsbehoeften. Leren hoe te [inzichten maken op basis van een bestaand gegevensmodel](../../user-defined-dashboards.md#create-widget), raadpleegt u de aangepaste dashboardhandleiding.

De inzichten die van SQL vragen worden geproduceerd bieden veel grotere flexibiliteit en aanpassing aan. De technische mensen kunnen vraag pro wijze gebruiken om complexe analyse op SQL uit te voeren en dan deze analyse met niet-technische gebruikers door dit dashboardvermogen te delen. Selecteren **[!UICONTROL Query pro mode]** gevolgd door **[!UICONTROL Save]**.

>[!NOTE]
>
>Als u eenmaal een selectie hebt gemaakt, kunt u deze selectie in het dashboard niet meer wijzigen. In plaats daarvan moet u een nieuw dashboard maken met een andere methode voor het maken van het dashboard.

![De [!UICONTROL Create dashboard] met de modus Query Pro en Opslaan gemarkeerd.](../../images/customizable-insights/query-pro-mode.png)

## Een grafiek maken {#create-a-chart}

Zie de [handleiding voor query pro-modus](./query-pro-mode.md) voor stapsgewijze instructies voor het maken van een grafiek met SQL.
