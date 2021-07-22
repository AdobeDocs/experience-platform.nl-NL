---
keywords: Experience Platform;profiel;segment;segmenten;segmentatie;gebruikersinterface;UI;aanpassing;segmentdashboard;dashboard
title: Segmentdashboard
description: 'Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over segmenten die uw organisatie heeft gemaakt. '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 41ef7a6e6d3b0ee9afe762b19c8c286ceb361dbb
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Segmentdashboard {#segment-dashboard}

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw segmenten kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het segmentdashboard in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een overzicht van alle functies van de Adobe Experience Platform Segmentation Service binnen de gebruikersinterface van het Platform, gelieve [de gids van de Dienst van de Segmentatie ](../../segmentation/ui/overview.md) te bezoeken.

## Segmentdashboardgegevens

Het segmentdashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of monster van de gegevens, en het segmentdashboard werkt niet in echt bij - tijd.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het segmentdashboard verkennen

Als u naar het [!UICONTROL Segments]-dashboard in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Segments]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overview]** om het dashboard weer te geven.

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, is [!UICONTROL Segments] dashboard niet zichtbaar. In plaats daarvan, toont het [!UICONTROL Overview] lusje verbindingen en documentatie om u te helpen met segmentatie beginnen.

![](../images/segments/dashboard-overview.png)

### Het dashboard [!UICONTROL Segments] wijzigen

U kunt de weergave van het [!UICONTROL Segments] dashboard wijzigen door **[!UICONTROL Modify dashboard]** te selecteren. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot **[!UICONTROL Widget library]** om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de documentatie [modifying dashboards](../customize/modify.md) and [widget library overview](../customize/widget-library.md) voor meer informatie.

## Een segment selecteren

Het dashboard selecteert automatisch een segment aan vertoning, nochtans kunt u het segment veranderen door het drop-down menu of de segmentselecteur te gebruiken.

Als u een ander segment wilt kiezen, selecteert u de vervolgkeuzelijst naast de segmentnaam of gebruikt u de segmentkiezer om het dialoogvenster voor segmentselectie te openen.

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widgets en metriek

Het segmentdashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over het geselecteerde segment verschaft.

De datum en tijd &#39;laatst bijgewerkt&#39; op een widget geeft aan wanneer de laatste momentopname van de gegevens is gemaakt. De datum en het tijdstip van de momentopname worden in UTC vermeld; het bevindt zich niet in de tijdzone van de individuele gebruiker of IMS-organisatie.

![](../images/segments/widget-timestamp.png)

## Standaardwidgets

Adobe biedt meerdere standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende maateenheden voor uw segmenten. U kunt ook aangepaste widgets maken die u met uw organisatie wilt delen met de [!UICONTROL Widget library]. Als u meer wilt weten over het maken van aangepaste widgets, leest u eerst het [overzicht van de widgetbibliotheek](../customize/widget-library.md).

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Audience size trend]](#audience-size-trend)
* [[!UICONTROL Identity overlap]](#identity-overlap)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)

### [!UICONTROL Audience size] {#audience-size}

De widget **[!UICONTROL Audience size]** geeft het totale aantal samengevoegde profielen weer binnen het geselecteerde segment op het moment dat de momentopname werd gemaakt. Dit getal is het resultaat van het toepassen van het samenvoegbeleid voor segmenten op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon in het segment.

Voor meer informatie over fragmenten en samengevoegde profielen, gelieve te beginnen door [overzicht van het Profiel van de Klant in real time](../../profile/home.md) te lezen.

![](../images/segments/audience-size.png)

### [!UICONTROL Audience size trend] {#audience-size-trend}

De widget **[!UICONTROL Audience size trend]** biedt informatie over het totale aantal profielen in het segment dat is vastgelegd tijdens de dagelijkse momentopname, gedurende de laatste 30 dagen, 90 dagen of 12 maanden. Deze widget geeft aan hoe de segmentgrootte in de loop der tijd kan zijn verschoven omdat nieuwe profielen in aanmerking komen voor of het segment verlaten.

Raadpleeg de [documentatie bij Segmentatieservice](../../segmentation/home.md) voor meer informatie over segmentbeoordeling en hoe profielen in aanmerking komen en uit segmenten worden afgesloten.

![](../images/segments/audience-size-trend.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

De widget **[!UICONTROL Identity overlap]** geeft een Venn-diagram weer of stelt een diagram in waarin de overlapping van profielen in uw segment met meerdere identiteiten wordt getoond.

Nadat u de vervolgkeuzemenu&#39;s op de widget hebt gebruikt om de identiteiten te selecteren die u wilt vergelijken, worden cirkels weergegeven met de relatieve grootte van elke identiteit, waarbij het aantal profielen met beide naamruimten wordt weergegeven door de grootte van de overlapping tussen de cirkels.

Als een klant op meer dan één kanaal met uw merk in wisselwerking staat, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteit bevatten.

Voor meer informatie over identiteiten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/identity-overlap.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

De widget **[!UICONTROL Profiles by identity]** geeft de indeling van de identiteiten in alle samengevoegde profielen in het geselecteerde segment weer. Het totale aantal profielen per identiteit kan hoger zijn dan het totale aantal profielen in het segment, omdat aan één profiel meerdere identiteiten kunnen zijn gekoppeld. Met andere woorden, het samenvoegen van de waarden die voor elke identiteit worden getoond kan meer dan de totale publieksgrootte in het segment totaal omdat als een klant met uw merk op meer dan één kanaal interactie aangaat, de veelvoudige identiteiten met die individuele klant kunnen worden geassocieerd.

Voor meer informatie over identiteiten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/segments/profiles-by-identity.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het segmentdashboard vinden en een segment selecteren dat u wilt bekijken. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Meer over het werken met segmenten in de UI van het Experience Platform leren, gelieve te verwijzen naar [de gids UI van de Dienst van de Segmentatie](../../segmentation/ui/overview.md).
