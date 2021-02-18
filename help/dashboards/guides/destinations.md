---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Doeldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie over de actieve doelen van uw organisatie kunt bekijken.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---


# (Bèta) [!UICONTROL Doelen] dashboard

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over de actieve bestemmingen van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot het dashboard van bestemmingen in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van bestemmingen, evenals een catalogus van alle beschikbare bestemmingen binnen Experience Platform, gelieve [bestemmingen overzicht](../../destinations/home.md) te bezoeken.

## [!UICONTROL Gegevens ] bestemmingsSdashboard  {#destinations-dashboard-data}

Het dashboard [!UICONTROL Doelen] toont een momentopname van de bestemmingen die uw organisatie binnen het Profiel van de Ervaring heeft toegelaten. De gegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of steekproef van de gegevens, en het dashboard van bestemmingen werkt niet in echt bij - tijd.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor doelen verkennen

Als u naar het dashboard voor doelen in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Doelen]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overzicht]** om het dashboard weer te geven.

![](../images/destinations/dashboard-overview.png)

## Beschikbare widgets

Experience Platform biedt meerdere widgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw doelen. Selecteer de naam van een widget hieronder voor meer informatie:

* [[!UICONTROL Meest gebruikte bestemmingen]](#most-used-destinations)
* [[!UICONTROL Onlangs gemaakte doelen]](#recently-created-destinations)
* [[!UICONTROL Onlangs geactiveerde segmenten]](#recently-activated-segments)

### [!UICONTROL Meest gebruikte bestemmingen] {#most-used-destinations}

De **[!UICONTROL Meest gebruikte bestemmingen]** widget toont de hoogste bestemmingen van uw organisatie door aantal in kaart gebrachte segmenten, vanaf de laatste momentopname. Deze rangschikking biedt inzicht in welke bestemmingen worden gebruikt en toont mogelijk ook de bestemmingen die mogelijk onderbenut zijn.

Bijvoorbeeld, als u een bestemming gisteren vormde maar geen segmenten aan het in kaart gebracht, zou u kunnen zien dat de bestemming momenteel onderbenut is.

Het aantal in kaart gebrachte segmenten die in de kolom van de segmenttelling worden getoond is nauwkeurig vanaf de laatste dagelijkse momentopname. Als u een nieuw segment toewijst aan de bestemming, wordt de telling pas bijgewerkt wanneer de volgende momentopname wordt gemaakt.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails zoals deze zijn gekoppeld op het tabblad **[!UICONTROL Bladeren]**. U kunt ook **[!UICONTROL Alles weergeven]** selecteren om naar het tabblad **[!UICONTROL Bladeren]** te navigeren en vervolgens de naam van een bestemming selecteren om de details ervan weer te geven.

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL Onlangs gemaakte doelen] {#recently-created-destinations}

Met de widget **[!UICONTROL Onlangs gemaakte doelen]** kunt u een lijst weergeven met de laatst geconfigureerde doelen van uw organisatie.

De gecreeerde getoonde datum is nauwkeurig aan de laatste dagelijkse momentopname. Met andere woorden, als u een nieuwe bestemming creeert, zal het niet in de lijst verschijnen tot nadat de volgende momentopname wordt genomen.

Als u de naam van een doel selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de doeldetails zoals deze zijn gekoppeld op het tabblad **[!UICONTROL Bladeren]**. U kunt ook **[!UICONTROL Alles weergeven]** selecteren om naar het tabblad **[!UICONTROL Bladeren]** te navigeren en vervolgens de naam van een bestemming selecteren om de details ervan weer te geven.

Meer over hoe te om specifieke soorten bestemmingen te vormen, bezoek [doeldocumentatie](../../destinations/home.md).

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL Onlangs geactiveerde segmenten] {#recently-activated-segments}

De **[!UICONTROL Onlangs geactiveerde segmenten]** widget verstrekt een lijst van de segmenten onlangs in kaart gebracht aan een bestemming. Deze lijst verstrekt een momentopname van welke segmenten en bestemmingen actief in gebruik in het systeem zijn en kan in het oplossen van problemen helpen om het even welke onjuiste afbeeldingen.

De bijgewerkte getoonde datum toont de laatste tijd het segment aan de bestemming werd geactiveerd en aan de laatste dagelijkse momentopname nauwkeurig is. Met andere woorden, als u een segment aan de bestemming activeert, zal de bijgewerkte datum niet veranderen tot na de volgende momentopname wordt genomen.

Als u de naam van een segment selecteert in de lijst die wordt weergegeven op de widget, gaat u naar de segmentdetails. U kunt **[!UICONTROL allen van de Mening ook selecteren]** om aan het segment te navigeren doorbladert lusje en dan de naam van een segment selecteren om zijn details te bekijken.

Voor meer informatie over het werken met segmenten in Experience Platform, gelieve te beginnen door [Overzicht van de Dienst van de Segmentatie](../../segmentation/home.md) te lezen.

![](../images/destinations/recently-activated-segments.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor doelen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Meer over het werken met bestemmingen in Experience Platform, gelieve te verwijzen naar [doeldocumentatie](../../destinations/home.md).