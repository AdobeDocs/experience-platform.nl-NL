---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 2f2459c1c88c97a3ab322b08ee178463fbb4a592
workflow-type: tm+mt
source-wordcount: '1122'
ht-degree: 0%

---


# (Bèta) [!UICONTROL Profielen] dashboard

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw [!DNL Real-time Customer Profile] gegevens kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het [!UICONTROL dashboard van Profielen] in UI toegang te hebben en te werken en verstrekt informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van alle profielfuncties binnen de gebruikersinterface van het Experience Platform, gelieve [de gids UI van het Profiel van de Klant in real time](../../profile/ui/user-guide.md) te bezoeken.

## Profieldashboardgegevens

Op het dashboard [!UICONTROL Profielen] wordt een momentopname weergegeven van de kenmerkgegevens (record) die uw organisatie heeft in de profielopslag in Experience Platform. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard van het Profiel wordt niet in real time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het [!UICONTROL dashboard Profielen] verkennen

Als u naar het [!UICONTROL Profiel]-dashboard in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Profielen]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overzicht]** om het dashboard weer te geven.

![](../images/profiles/dashboard-overview.png)

### Samenvoegbeleid selecteren

De metriek die in [!UICONTROL Profiles] dashboard wordt getoond zijn gebaseerd op samenvoegbeleid dat op uw gegevens van het Profiel van de Klant in real time wordt toegepast. Wanneer gegevens uit veelvoudige bronnen worden samengebracht, is het mogelijk voor de gegevens om conflicterende waarden (bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden) en het is de baan van het fusiebeleid om te bepalen welke gegevens aan prioriteit en vertoning als deel van het profiel moeten.

Het dashboard selecteert automatisch een samenvoegbeleid dat moet worden weergegeven, maar u kunt het samenvoegbeleid dat is geselecteerd wijzigen in het keuzemenu. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de vervolgkeuzelijst naast de naam van het samenvoegbeleid en selecteert u vervolgens het samenvoegbeleid dat u wilt weergeven.

>[!NOTE]
>
>In het vervolgkeuzemenu ziet u alleen samenvoegbeleid met betrekking tot de XDM Individual Profile Class. Als uw organisatie echter meerdere samenvoegingsbeleidsregels heeft gemaakt, moet u mogelijk schuiven om de volledige lijst met beschikbare samenvoegingsbeleidsregels weer te geven.

Voor meer informatie over samenvoegbeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven en te verklaren, te bezoeken gelieve [beleidsgids UI van de fusie](../../profile/ui/merge-policies.md).

![](../images/profiles/select-merge-policy.png)

### Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft. De datum en tijd &#39;laatst bijgewerkt&#39; op een widget geeft aan wanneer de laatste momentopname van de gegevens is gemaakt.

![](../images/profiles/dashboard-timestamp.png)

## Beschikbare widgets

Experience Platform biedt meerdere widgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw profielgegevens. Selecteer de naam van een widget hieronder voor meer informatie:

* [[!UICONTROL Grootte publiek]](#audience-size)
* [[!UICONTROL Profielen toegevoegd]](#profiles-added)
* [[!UICONTROL Profielen die in de loop der tijd zijn toegevoegd]](#profiles-added-over-time)
* [[!UICONTROL Profielen op naamruimte]](#profiles-by-namespace)
* [[!UICONTROL Naamruimte-overlapping]](#namespace-overlap)

### [!UICONTROL Grootte publiek] {#audience-size}

De **[!UICONTROL Audience size]** widget toont het totale aantal samengevoegde profielen binnen de de gegevensopslag van het Profiel op het tijdstip dat de momentopname werd genomen. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Lees voor meer informatie over fragmenten en samengevoegde profielen eerst de sectie *Profielfragmenten vs samengevoegde profielen* van het [Real-time Customer Profile overview](../../profile/home.md).

>[!NOTE]
>
>Het samenvoegbeleid dat wordt gebruikt om deze metrische waarde te berekenen is niet het zelfde als het systeem-geproduceerde fusiebeleid dat wordt gebruikt om [!UICONTROL Adresseerbare publiek] in [!UICONTROL het gebruik van de Vergunning ] dashboard te berekenen, daarom is het kijkaantal in [!UICONTROL Profielen] en [!UICONTROL Vergunningsgebruik] dashboards waarschijnlijk niet precies het zelfde.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profielen toegevoegd] {#profiles-added}

De **[!UICONTROL toegevoegde profielen]** widget geeft het totale aantal samengevoegde profielen weer dat aan de profielgegevensopslag is toegevoegd sinds de laatste momentopname is gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profielen die in de loop der tijd zijn toegevoegd] {#profiles-added-over-time}

In de widget **[!UICONTROL Profielen die in de loop der tijd zijn toegevoegd]** wordt het totale aantal samengevoegde profielen weergegeven dat de afgelopen 30 dagen dagelijks is toegevoegd aan de opslag van profielgegevens. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen.

Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profielen op naamruimte] {#profiles-by-namespace}

Met de widget **[!UICONTROL Profielen op naamruimte]** wordt de uitsplitsing van naamruimten in alle samengevoegde profielen in het archief Profiel weergegeven. Het totale aantal profielen dat wordt weergegeven door [!UICONTROL ID-naamruimte] (met andere woorden, door de waarden die worden weergegeven voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samenvoegprofielen omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Voor meer informatie over naamruimten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Naamruimte-overlapping] {#namespace-overlap}

Met de widget **[!UICONTROL Namespace overlap]** wordt een koppelingsdiagram weergegeven of wordt een insteldiagram weergegeven waarin de overlapping van profielen in uw profielarchief met meerdere naamruimten wordt getoond.

Nadat u de vervolgkeuzemenu&#39;s op de widget hebt gebruikt om de naamruimten te selecteren die u wilt vergelijken, worden cirkels weergegeven met de relatieve grootte van elke naamruimte, waarbij het aantal profielen met beide naamruimten wordt weergegeven door de grootte van de overlapping tussen de cirkels.

Als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteitsnaamruimte bevatten.

Voor meer informatie over naamruimten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met [!DNL Profile]-gegevens in de interface van het Experience Platform, raadpleegt u de [UI-gids voor het realtime profiel van klanten](../../profile/ui/user-guide.md).