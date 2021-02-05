---
keywords: Experience Platform;profiel;segment;segmenten;segmentatie;gebruikersinterface;UI;aanpassing;segmentdashboard;dashboard
title: UI-gids voor segmentdashboard
description: 'In deze handleiding wordt het segmentdashboard beschreven dat beschikbaar is in de gebruikersinterface van Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---


# (Alpha) Segmentdashboard {#segment-dashboard}

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven, bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw segmenten kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het segmentdashboard in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een overzicht van alle functies van de Adobe Experience Platform Segmentation Service binnen de gebruikersinterface van het Platform, gelieve [de gids van de Dienst van de Segmentatie ](overview.md) te bezoeken.

## Segmentdashboardgegevens

Het segmentdashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of monster van de gegevens, en het segmentdashboard werkt niet in echt bij - tijd.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het segmentdashboard verkennen

Als u naar het segmentdashboard in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Segmenten]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overzicht]** om het dashboard weer te geven.

![](../images/ui/segment-dashboard/dashboard-overview.png)

### Een segment selecteren

Als u een segment wilt selecteren dat in het dashboard moet worden weergegeven, kiest u de dialoogkiezer voor het tekstvak **[!UICONTROL Segment selecteren]**.

![](../images/ui/segment-dashboard/select-segment.png)

>[!NOTE]
>
>Als er al een segment is geselecteerd, gebruikt u `X` om eerst het segment te verwijderen en verschijnt dan de dialoogkiezer.
>
>![](../images/ui/segment-dashboard/remove-segment.png)

Het **[!UICONTROL Uitgezochte segment]** dialoog opent, toestaand u om het segment te kiezen u wenst om te bekijken. Nadat u het gewenste segment hebt gekozen, gebruikt u **[!UICONTROL Select]** om terug te keren naar het dashboard.

![](../images/ui/segment-dashboard/select-segment-dialog.png)

### Samenvoegbeleid

Nadat het selecteren van een segment, zal het de tekstvakje van het fusiebeleid automatisch met het fusiebeleid met betrekking tot dat segment bevolken.

Meer over het bouwen van segmenten in Experience Platform leren, bezoek [de gids UI van de Bouwer van het Segment](segment-builder.md). Voor meer informatie over samenvoegbeleid, gelieve te beginnen door [overzicht van het Profiel van de Klant in real time](../../profile/home.md) te lezen.

![](../images/ui/segment-dashboard/merge-policy.png)

### Widgets en metriek

Het segmentdashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over het geselecteerde segment verschaffen. De datum en tijd &#39;laatst bijgewerkt&#39; op de widget geven aan wanneer de laatste momentopname van de gegevens is gemaakt.

![](../images/ui/segment-dashboard/widget-timestamp.png)

## Beschikbare widgets

Experience Platform biedt meerdere widgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw segment. Selecteer de naam van een widget hieronder voor meer informatie:

* [[!UICONTROL Segmentgrootte]](#segment-size)
* [[!UICONTROL Profielen op naamruimte]](#profiles-by-namespace)

### [!UICONTROL Segmentgrootte] {#segment-size}

Met de widget **[!UICONTROL Segmentgrootte]** wordt het totale aantal samengevoegde profielen weergegeven binnen het geselecteerde segment op het moment dat de momentopname werd gemaakt. Dit getal is het resultaat van het toepassen van het samenvoegbeleid voor segmenten op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon in het segment.

Voor meer informatie over fragmenten en samengevoegde profielen, gelieve te beginnen door [overzicht van het Profiel van de Klant in real time](../home.md) te lezen.

![](../images/ui/segment-dashboard/segment-size.png)

### [!UICONTROL Profielen op naamruimte] {#profiles-by-namespace}

Met de widget **[!UICONTROL Profielen op naamruimte]** wordt de uitsplitsing van naamruimten in alle samengevoegde profielen in het geselecteerde segment weergegeven. Het totale aantal profielen bij [!UICONTROL ID namespace] (met andere woorden, het samenvoegen van de waarden die voor elke namespace worden getoond) zal gewoonlijk hoger zijn dan het totale aantal profielen in het segment omdat één profiel veelvoudige namespaces verbonden aan het kon hebben. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, kunnen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Voor meer informatie over naamruimten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/ui/segment-dashboard/profiles-by-namespace.png)

## Aanvullende dashboards

De interface van het Platform biedt extra dashboards voor het bekijken van momentopnamen van uw gegevens binnen Experience Platform. Deze dashboards omvatten het Profiel van de Klant in real time en [!UICONTROL Gebruik van de vergunning]. Voor meer informatie over deze extra dashboards, selecteer van de volgende verbindingen:

* [[!DNL Profile] dashboard](../../profile/ui/profile-dashboard.md)
* [[!UICONTROL Licentie ] voor gebruik van het dashboard](../../landing/license-usage-dashboard.md)

## Volgende stappen

Als u dit document volgt, kunt u nu het segmentdashboard vinden en een segment selecteren dat u wilt bekijken. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Meer over het werken met segmenten in de UI van het Experience Platform leren, gelieve te verwijzen naar [de gids UI van de Dienst van de Segmentatie](overview.md).