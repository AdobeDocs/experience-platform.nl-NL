---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Doeldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie over de actieve doelen van uw organisatie kunt bekijken.
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 8571d86e1ce9dc894e54fe72dea75b9f8fe84f0b
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# [!UICONTROL Destinations] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over de actieve bestemmingen van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot het dashboard van bestemmingen in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van de bestemmingen en een lijst van alle beschikbare bestemmingen in Experience Platform, gelieve te bezoeken [documentatie voor doelen](../../destinations/home.md).

## [!UICONTROL Destinations] dashboardgegevens {#destinations-dashboard-data}

De [!UICONTROL Destinations] het dashboard toont een momentopname van de bestemmingen die uw organisatie binnen Experience Platform heeft toegelaten. De gegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of steekproef van de gegevens, en het dashboard van bestemmingen werkt niet in echt bij - tijd.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor doelen verkennen

Als u naar het dashboard voor doelen wilt navigeren binnen de interface van het Platform, selecteert u **[!UICONTROL Destinations]** in het linkerspoor, dan selecteer **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Experience Platform is en nog geen actieve bestemmingen heeft, [!UICONTROL Destinations] dashboard en [!UICONTROL Overview] zijn niet zichtbaar. In plaats daarvan selecteert u [!UICONTROL Destinations] van de linkernavigatie toont de [!UICONTROL Catalog] tab. Meer informatie over de [!UICONTROL Catalog] tabblad, verwijst naar de [[!UICONTROL Destinations] werkruimtegids](../../destinations/ui/destinations-workspace.md).

![](../images/destinations/dashboard-overview.png)

### Het dashboard voor doelen wijzigen

U kunt de weergave van het dashboard voor doelen wijzigen door **[!UICONTROL Modify dashboard]**. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot de **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de [wijzigen, dashboards](../customize/modify.md) en [Overzicht van widgetbibliotheek](../customize/widget-library.md) documentatie voor meer informatie.

## Standaardwidgets

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens voor uw doelen. U kunt ook aangepaste widgets maken die u met uw organisatie kunt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst de [Overzicht van widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

De **[!UICONTROL Most used destinations]** widget geeft de belangrijkste doelen van uw organisatie weer op basis van het aantal segmenten dat is toegewezen, vanaf de laatste momentopname. Deze rangschikking biedt inzicht in welke bestemmingen worden gebruikt en toont mogelijk ook de bestemmingen die mogelijk onderbenut zijn.

Bijvoorbeeld, als u een bestemming gisteren vormde maar geen segmenten aan het in kaart gebracht, zou u kunnen zien dat de bestemming momenteel onderbenut is.

Het aantal in kaart gebrachte segmenten die in de kolom van de segmenttelling worden getoond is nauwkeurig vanaf de laatste dagelijkse momentopname. Als u een nieuw segment toewijst aan de bestemming, wordt de telling pas bijgewerkt wanneer de volgende momentopname wordt gemaakt.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails die zijn gekoppeld vanuit het menu **[!UICONTROL Browse]** tab. U kunt ook **[!UICONTROL View All]** om naar de **[!UICONTROL Browse]** en selecteert u vervolgens de naam van een bestemming om de details ervan weer te geven.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

De **[!UICONTROL Recently created destinations]** widget laat u toe om een lijst van onlangs gevormde bestemmingen van uw organisatie te zien.

De gecreeerde getoonde datum is nauwkeurig aan de laatste dagelijkse momentopname. Met andere woorden, als u een nieuwe bestemming creeert, zal het niet in de lijst verschijnen tot nadat de volgende momentopname wordt genomen.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails die zijn gekoppeld vanuit het menu **[!UICONTROL Browse]** tab. U kunt ook **[!UICONTROL View All]** om naar de **[!UICONTROL Browse]** en selecteert u vervolgens de naam van een bestemming om de details ervan weer te geven.

Om meer over te leren hoe te om specifieke soorten bestemmingen te vormen, bezoek [documentatie voor doelen](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

De **[!UICONTROL Recently activated segments]** widget bevat een lijst met de segmenten die het laatst zijn toegewezen aan een doel. Deze lijst verstrekt een momentopname van welke segmenten en bestemmingen actief in gebruik in het systeem zijn en kan in het oplossen van problemen helpen om het even welke onjuiste afbeeldingen.

De bijgewerkte getoonde datum toont de laatste tijd het segment aan de bestemming werd geactiveerd en aan de laatste dagelijkse momentopname nauwkeurig is. Met andere woorden, als u een segment aan de bestemming activeert, zal de bijgewerkte datum niet veranderen tot na de volgende momentopname wordt genomen.

Als u de naam van een segment selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de segmentdetails. U kunt ook **[!UICONTROL View All]** om aan het segment te navigeren doorbladert lusje en selecteert dan de naam van een segment om zijn details te bekijken.

Voor meer informatie over het werken met segmenten in Experience Platform, gelieve te beginnen door te lezen [Overzicht van segmentatieservice](../../segmentation/home.md).

![](../images/destinations/recently-activated-segments.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor doelen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met bestemmingen in Experience Platform, raadpleegt u de [documentatie voor doelen](../../destinations/home.md).
