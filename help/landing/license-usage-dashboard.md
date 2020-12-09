---
keywords: Experience Platform;user interface;UI;customization;license usage dashboard;dashboard;license usage;entitlement;consumption
title: Het gebruiksdashboard voor licenties
description: 'In deze handleiding wordt het dashboard voor het gebruiksrecht van licenties weergegeven dat beschikbaar is in de gebruikersinterface van Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 63758450276d47e7e0eddeb047779222cb80a3e2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---


# (Alfa) [!UICONTROL Licentiegebruikdashboard] {#license-usage-dashboard}

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven, bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het vergunningsgebruik van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het dashboard van het vergunningsgebruik in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een algemeen overzicht van de gebruikersinterface van het Platform raadpleegt u de gebruikersgids [van het](ui-guide.md)Experience Platform.

## Gegevens op het gebruiksdashboard voor licenties

Op het dashboard voor licentiegebruik wordt een momentopname weergegeven van de licentiegegevens van uw organisatie voor Experience Platform. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de opname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor licentiegebruik verkennen

Als u naar het gebruiksdashboard voor licenties in de gebruikersinterface van het Platform wilt navigeren, selecteert u **[!UICONTROL Licentiegebruik]** in de linkerrail. Dit wordt geopend met het tabblad **[!UICONTROL Overzicht]** waarin het dashboard wordt weergegeven.

![](images/license-usage-dashboard/dashboard-overview.png)

### Een sandbox selecteren

Selecteer [!UICONTROL Productie] of [!UICONTROL Ontwikkeling]om een sandbox te kiezen die u wilt weergeven in het dashboard. De geselecteerde sandbox wordt aangegeven met het keuzerondje naast de naam van de sandbox.

>[!NOTE]
>
>Consumptierapporten voor sandboxen zijn cumulatief voor alle sandboxen van hetzelfde type. Met andere woorden, als u [!UICONTROL Productie] of [!UICONTROL Ontwikkeling] selecteert, wordt een rapport opgesteld over alle productie- of ontwikkelingssandboxen.

![](images/license-usage-dashboard/select-sandbox.png)

### Een datumbereik selecteren

Nadat u een sandbox hebt geselecteerd, kunt u de vervolgkeuzelijst voor het datumbereik gebruiken om de periode te selecteren die moet worden weergegeven in het dashboard. Er zijn drie opties beschikbaar: [!UICONTROL Afgelopen 30 dagen], [!UICONTROL Afgelopen 90 dagen]en [!UICONTROL Laatste 12 maanden]. De laatste 30 dagen zijn standaard geselecteerd.

![](images/license-usage-dashboard/select-date-range.png)

### Widgets en metriek

Het licentiegebruikdashboard bestaat uit widgets, die alleen-lezen cijfers weergeven die belangrijke informatie geven over het gebruik van de licentie van uw organisatie. Zie de sectie over beschikbare widgets in deze handleiding voor meer informatie over deze widgets.

## Beschikbare widgets {#available-widgets}

Experience Platform bevat momenteel één widget waarmee u het licentiegebruik kunt visualiseren. Binnenkort worden er meer widgets uitgebracht.

### [!UICONTROL Adresseerbaar publiek] {#addressable-audiences}

De **[!UICONTROL Adressable publiek]** widget meet het totale aantal publiek dat in de opslag van het Profiel bestaat, na het toepassen van een systeem-geproduceerd fusiebeleid om alle huidige datasets te combineren gebruikend een deterministisch (privé) grafiekalgoritme. Het samenvoegbeleid dat wordt gebruikt om deze metrisch te berekenen wordt geproduceerd door Platform en kan niet worden uitgegeven, noch kan een verschillend fusiebeleid worden geselecteerd.

![](images/license-usage-dashboard/addressable-audiences.png)

## Aanvullende dashboards

De interface van het Platform biedt extra dashboards voor het bekijken van momentopnamen van uw gegevens binnen Experience Platform. Deze dashboards omvatten het Profiel en de segmenten van de Klant in real time. Voor meer informatie over deze dashboards, selecteer van de volgende verbindingen:

* [[!DNL Profile] dashboard](../profile/ui/profile-dashboard.md)
* [Segmentdashboard](../segmentation/ui/segment-dashboard.md)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor licentiegebruik vinden en een sandbox selecteren die u wilt weergeven. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Voor meer informatie over de gebruikersinterface van het Experience Platform raadpleegt u de gebruikersgids [voor het](ui-guide.md)Platform.