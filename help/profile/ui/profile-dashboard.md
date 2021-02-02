---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: UI-gids voor profieldashboard
description: 'Deze handleiding geeft een overzicht van het gegevensdashboard voor het realtime klantprofiel dat beschikbaar is in de gebruikersinterface van Adobe Experience Platform. '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 0%

---


# (Alpha) [!DNL Real-time Customer Profile] dashboard {#profile-dashboard}

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven, bevindt zich momenteel in alfa en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw [!DNL Real-time Customer Profile] gegevens kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot [!DNL Profile] dashboard in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van alle profielfuncties binnen de gebruikersinterface van het Experience Platform, gelieve [de gids UI van het Profiel van de Klant in real time](user-guide.md) te bezoeken.

## Profieldashboardgegevens

Op het dashboard Profiel wordt een momentopname weergegeven van de kenmerkgegevens (record) die uw organisatie heeft in de profielopslag in Experience Platform. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard van het Profiel wordt niet in real time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

De metriek die in het dashboard van het Profiel wordt getoond zijn gebaseerd op het standaardsamenvoegbeleid voor uw organisatie. Voor meer informatie over samenvoegbeleid, en hoe te om uw standaard samenvoegbeleid te selecteren of te veranderen, gelieve [te bezoeken de gids UI van het Samenvoegingsbeleid](merge-policies.md).

## Het dashboard Profiel verkennen

Om aan het dashboard van het Profiel binnen Platform UI te navigeren, selecteer **[!UICONTROL Profielen]** in de linkerspoorstaaf, dan selecteer **[!UICONTROL Overzicht]** tabel om het dashboard te tonen.

![](../images/profile-dashboard/dashboard-overview.png)

### Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft. De datum en tijd &#39;laatst bijgewerkt&#39; op de widget geven aan wanneer de laatste momentopname van de gegevens is gemaakt.

![](../images/profile-dashboard/dashboard-timestamp.png)

## Beschikbare widgets

Experience Platform biedt meerdere widgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw profielgegevens. Selecteer de naam van een widget hieronder voor meer informatie:

* [[!UICONTROL Grootte publiek]](#audience-size)
* [[!UICONTROL Profielen op naamruimte]](#profiles-by-namespace)

### [!UICONTROL Grootte publiek] {#audience-size}

De **[!UICONTROL Audience size]** widget toont het totale aantal samengevoegde profielen binnen de de gegevensopslag van het Profiel op het tijdstip dat de momentopname werd genomen. Dit aantal is het resultaat van het standaardsamenvoegbeleid van uw organisatie dat op uw gegevens van het Profiel wordt toegepast om profielfragmenten samen te voegen om één enkel profiel voor elk individu te vormen.

Voor meer informatie over fragmenten en samengevoegde profielen, gelieve te beginnen door *de fragmenten van het Profiel vs samengevoegde profielen* sectie van [Profieloverzicht](../home.md) te lezen.

>[!NOTE]
>
>Het samenvoegbeleid dat wordt gebruikt om deze metrische waarde te berekenen is niet het zelfde als het systeem-geproduceerde fusiebeleid dat wordt gebruikt om [!UICONTROL Adresseerbare publiek] in [!UICONTROL het gebruik van de Vergunning ] dashboard te berekenen, daarom is het publiek aantal in [!DNL Profile] en [!UICONTROL Vergunningsgebruik] dashboards waarschijnlijk niet precies het zelfde.

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL Profielen op naamruimte] {#profiles-by-namespace}

Met de widget **[!UICONTROL Profielen op naamruimte]** wordt de uitsplitsing van naamruimten in alle samengevoegde profielen in het archief Profiel weergegeven. Het totale aantal profielen bij [!UICONTROL ID-naamruimte] (met andere woorden, het optellen van de waarden die voor elke naamruimte worden weergegeven) zal altijd hoger zijn dan het totale aantal samenvoegprofielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Voor meer informatie over naamruimten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profile-dashboard/profiles-by-namespace.png)

## Aanvullende dashboards

De interface van het Platform biedt extra dashboards voor het bekijken van momentopnamen van uw gegevens binnen Experience Platform. Deze dashboards omvatten segmentatie en vergunningsgebruik. Voor meer informatie over deze extra dashboards, selecteer van de volgende verbindingen:

* [Segmentdashboard](../../segmentation/ui/segment-dashboard.md)
* [Het gebruiksdashboard voor licenties](../../landing/license-usage-dashboard.md)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profiel vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Raadpleeg de [[!DNL Profile] UI-handleiding](user-guide.md) voor meer informatie over het werken met [!DNL Profile]-gegevens in de interface van het Experience Platform.