---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1066'
ht-degree: 0%

---

# (Bèta) [!UICONTROL Profiles] dashboard

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over uw [!DNL Real-time Customer Profile] gegevens kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het [!UICONTROL Profiles] dashboard in UI toegang te hebben en te werken en verstrekt informatie betreffende de metriek die in het dashboard wordt getoond.

Voor een overzicht van alle profielfuncties binnen de gebruikersinterface van het Experience Platform, gelieve [de gids UI van het Profiel van de Klant in real time](../../profile/ui/user-guide.md) te bezoeken.

## Profieldashboardgegevens

Het [!UICONTROL Profiles] dashboard toont een momentopname van de attributen (verslag) gegevens die uw organisatie binnen de opslag van het Profiel in Experience Platform heeft. De momentopname bevat geen gebeurtenis (tijdreeks)-gegevens.

De kenmerkgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard van het Profiel wordt niet in real time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard [!UICONTROL Profiles] verkennen

Als u naar het [!UICONTROL Profiles]-dashboard in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Profiles]** in de linkertrack en selecteert u vervolgens het tabblad **[!UICONTROL Overview]** om het dashboard weer te geven.

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

* [[!UICONTROL Audience size]](#audience-size)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace overlap]](#namespace-overlap)

### [!UICONTROL Audience size] {#audience-size}

De widget **[!UICONTROL Audience size]** geeft het totale aantal samengevoegde profielen weer in de profielgegevensopslag op het moment dat de momentopname werd gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Lees voor meer informatie over fragmenten en samengevoegde profielen eerst de sectie *Profielfragmenten vs samengevoegde profielen* van het [Real-time Customer Profile overview](../../profile/home.md).

>[!NOTE]
>
>Het samenvoegbeleid dat wordt gebruikt om deze metrische waarde te berekenen is niet het zelfde als het systeem-geproduceerde fusiebeleid dat wordt gebruikt om [!UICONTROL Addressable audiences] in het [!UICONTROL License usage] dashboard te berekenen, daarom zal de publiekstelling in [!UICONTROL Profiles] en [!UICONTROL License usage] dashboards waarschijnlijk niet precies het zelfde zijn.

![](../images/profiles/audience-size.png)

### [!UICONTROL Profiles added] {#profiles-added}

De widget **[!UICONTROL Profiles added]** geeft het totale aantal samengevoegde profielen weer dat sinds de laatste momentopname is gemaakt, aan de profielgegevensopslag is toegevoegd. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

De widget **[!UICONTROL Profiles added over time]** geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen dagelijks is toegevoegd aan de opslag van profielgegevens. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen.

Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

Met de widget **[!UICONTROL Profiles by namespace]** wordt de indeling van naamruimten in alle samengevoegde profielen in het archief Profiel weergegeven. Het totale aantal profielen per [!UICONTROL ID namespace] (met andere woorden, het optellen van de waarden die voor elke naamruimte worden weergegeven) kan hoger zijn dan het totale aantal samenvoegprofielen omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Voor meer informatie over naamruimten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace overlap] {#namespace-overlap}

De widget **[!UICONTROL Namespace overlap]** geeft een Venn-diagram weer of stelt een diagram in waarin de overlapping van profielen in uw profielenarchief met meerdere naamruimten wordt getoond.

Nadat u de vervolgkeuzemenu&#39;s op de widget hebt gebruikt om de naamruimten te selecteren die u wilt vergelijken, worden cirkels weergegeven met de relatieve grootte van elke naamruimte, waarbij het aantal profielen met beide naamruimten wordt weergegeven door de grootte van de overlapping tussen de cirkels.

Als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteitsnaamruimte bevatten.

Voor meer informatie over naamruimten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met [!DNL Profile]-gegevens in de interface van het Experience Platform, raadpleegt u de [UI-gids voor het realtime profiel van klanten](../../profile/ui/user-guide.md).
