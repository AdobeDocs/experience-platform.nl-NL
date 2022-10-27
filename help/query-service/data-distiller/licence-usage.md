---
title: Gebruik van batch-query's controleren
description: De gebruikersinterface van Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het gebruik van de Data Distiller-licentie van uw organisatie.
source-git-commit: 0a44d15f9dfaf5100fa44e2e6442b1be23ee0ab0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Gebruik van batch-query&#39;s controleren {#monitor-license-usage}

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het de vergunningsgebruik van de Dienst van de Vraag van uw organisatie kunt bekijken.

Ga voor gedetailleerde instructies over het openen van het dashboard voor het licentiegebruik in de gebruikersinterface en voor meer informatie over de beschikbare metriek in het dashboard naar de [Handleiding voor het gebruiksdashboard voor licenties](../../dashboards/guides/license-usage.md).

Lees de [overzicht van dashboards](../../dashboards/home.md) voor een overzicht van alle dashboardfuncties in Experience Platform.

## Widgets {#widgets}

Het licentiegebruikdashboard bestaat uit widgets, die alleen-lezen cijfers weergeven die belangrijke informatie geven over het gebruik van de licentie van uw organisatie. De zichtbare metriek hangt van de specifieke vergunning van uw organisatie af.

Selecteer een keuzerondje om een sandbox voor analyse te kiezen en gebruik het vervolgkeuzemenu om een tijdsperiode voor de analyse te selecteren. De beschikbare opties zijn een periode van 30 dagen, 90 dagen, 12 maanden, het laatste jaar, de volledige contractperiode of een aangepaste datum.

## Rekenuren {#compute-hours}

De [!UICONTROL Compute hours] widget gebruikt een lijngrafiek om de tijd van de de partijvraag van uw organisatie elke dag visualiseren. De widget geeft drie metriek weer die door een getal linksboven in de widget wordt aangegeven. Deze zijn

- [!UICONTROL Actual]: Het totale aantal computeruren voor de tijdsperiode die is gekozen in de overzichtsvervolgkeuzelijst. Deze metrische waarde wordt ook op de grafiek aangegeven door een dichte lijn.
- [!UICONTROL Licensed]: Het totale aantal computeruren dat is toegestaan door de licentieovereenkomst van uw organisatie. Deze metrische waarde wordt ook op de grafiek aangegeven door een stippellijn.
- [!UICONTROL Usage]: Dit is het percentage van uw gebruik in verhouding tot de maximale computeruren die door uw licentie zijn overeengekomen.

>[!IMPORTANT]
>
>De [!UICONTROL Compute hours] widget is alleen van toepassing op klanten met de Data Distiller-licentie voor batchquery&#39;s.

![Het licentieverbruiksdashboard met de widget computeruren gemarkeerd.](../images/data-distiller/compute-hours.png)
