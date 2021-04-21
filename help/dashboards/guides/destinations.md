---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Doeldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie over de actieve doelen van uw organisatie kunt bekijken.
topic-legacy: guide
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 0%

---

# (Bèta) [!UICONTROL Destinations] dashboard

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over de actieve bestemmingen van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot het dashboard van bestemmingen in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van bestemmingen, evenals een catalogus van alle beschikbare bestemmingen binnen Experience Platform, gelieve [bestemmingen overzicht](../../destinations/home.md) te bezoeken.

## [!UICONTROL Destinations] dashboardgegevens  {#destinations-dashboard-data}

Het [!UICONTROL Destinations] dashboard toont een momentopname van de bestemmingen die uw organisatie binnen het Profiel van de Ervaring heeft toegelaten. De gegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of steekproef van de gegevens, en het dashboard van bestemmingen werkt niet in echt bij - tijd.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor doelen verkennen

Als u naar het doeldashboard in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Destinations]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overview]** om het dashboard weer te geven.

![](../images/destinations/dashboard-overview.png)

## Beschikbare widgets

Experience Platform biedt meerdere widgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw doelen. Selecteer de naam van een widget hieronder voor meer informatie:

* [[!UICONTROL Most used destinations]](#most-used-destinations)
* [[!UICONTROL Recently created destinations]](#recently-created-destinations)
* [[!UICONTROL Recently activated segments]](#recently-activated-segments)

### [!UICONTROL Most used destinations] {#most-used-destinations}

Met de widget **[!UICONTROL Most used destinations]** worden de belangrijkste doelen van uw organisatie weergegeven op basis van het aantal segmenten dat is toegewezen, vanaf de laatste momentopname. Deze rangschikking biedt inzicht in welke bestemmingen worden gebruikt en toont mogelijk ook de bestemmingen die mogelijk onderbenut zijn.

Bijvoorbeeld, als u een bestemming gisteren vormde maar geen segmenten aan het in kaart gebracht, zou u kunnen zien dat de bestemming momenteel onderbenut is.

Het aantal in kaart gebrachte segmenten die in de kolom van de segmenttelling worden getoond is nauwkeurig vanaf de laatste dagelijkse momentopname. Als u een nieuw segment toewijst aan de bestemming, wordt de telling pas bijgewerkt wanneer de volgende momentopname wordt gemaakt.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails zoals deze zijn gekoppeld op het tabblad **[!UICONTROL Browse]**. U kunt ook **[!UICONTROL View All]** selecteren om naar het **[!UICONTROL Browse]** lusje te navigeren en dan de naam van een bestemming te selecteren om zijn details te bekijken.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Recently created destinations] {#recently-created-destinations}

Met de widget **[!UICONTROL Recently created destinations]** kunt u een lijst weergeven met de laatst geconfigureerde doelen van uw organisatie.

De gecreeerde getoonde datum is nauwkeurig aan de laatste dagelijkse momentopname. Met andere woorden, als u een nieuwe bestemming creeert, zal het niet in de lijst verschijnen tot nadat de volgende momentopname wordt genomen.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails zoals deze zijn gekoppeld op het tabblad **[!UICONTROL Browse]**. U kunt ook **[!UICONTROL View All]** selecteren om naar het **[!UICONTROL Browse]** lusje te navigeren en dan de naam van een bestemming te selecteren om zijn details te bekijken.

Meer over hoe te om specifieke soorten bestemmingen te vormen, bezoek [doeldocumentatie](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Recently activated segments] {#recently-activated-segments}

De widget **[!UICONTROL Recently activated segments]** biedt een lijst met de segmenten die het laatst zijn toegewezen aan een doel. Deze lijst verstrekt een momentopname van welke segmenten en bestemmingen actief in gebruik in het systeem zijn en kan in het oplossen van problemen helpen om het even welke onjuiste afbeeldingen.

De bijgewerkte getoonde datum toont de laatste tijd het segment aan de bestemming werd geactiveerd en aan de laatste dagelijkse momentopname nauwkeurig is. Met andere woorden, als u een segment aan de bestemming activeert, zal de bijgewerkte datum niet veranderen tot na de volgende momentopname wordt genomen.

Als u de naam van een segment selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de segmentdetails. U kunt **[!UICONTROL View All]** ook selecteren om aan het segment te navigeren doorbladert lusje en dan de naam van een segment selecteren om zijn details te bekijken.

Voor meer informatie over het werken met segmenten in Experience Platform, gelieve te beginnen door [Overzicht van de Dienst van de Segmentatie](../../segmentation/home.md) te lezen.

![](../images/destinations/recently-activated-segments.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor doelen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Meer over het werken met bestemmingen in Experience Platform, gelieve te verwijzen naar [doeldocumentatie](../../destinations/home.md).
