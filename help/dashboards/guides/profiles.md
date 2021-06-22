---
keywords: Experience Platform;profiel;real-time klantprofiel;gebruikersinterface;UI;aanpassing;profiel dashboard;dashboard
title: Profieldashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over de gegevens van het klantprofiel in realtime van uw organisatie.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '1140'
ht-degree: 0%

---

# [!UICONTROL Profiles] dashboard

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

>[!NOTE]
>
>Als uw organisatie nieuw aan Platform is en nog geen actieve datasets van het Profiel of gecreeerd samenvoegbeleid heeft, is [!UICONTROL Profiles] dashboard niet zichtbaar. In plaats daarvan bevat het tabblad [!UICONTROL Overview] koppelingen en documentatie waarmee u aan de slag kunt gaan met het realtime profiel van de klant.

![](../images/profiles/dashboard-overview.png)

### Het dashboard [!UICONTROL Profiles] wijzigen

U kunt de weergave van het [!UICONTROL Profiles] dashboard wijzigen door **[!UICONTROL Modify dashboard]** te selecteren. Hierdoor kunt u widgets verplaatsen, toevoegen en verwijderen van het dashboard en toegang krijgen tot [!UICONTROL Widget library] om beschikbare widgets te verkennen en aangepaste widgets voor uw organisatie te maken.

Raadpleeg de documentatie [modifying dashboards](../modify.md) and [widget library](../widget-library.md) voor meer informatie.

## Beleid samenvoegen

De metriek die in [!UICONTROL Profiles] dashboard wordt getoond zijn gebaseerd op samenvoegbeleid dat op uw gegevens van het Profiel van de Klant in real time wordt toegepast. Wanneer gegevens uit veelvoudige bronnen worden samengebracht om het klantenprofiel tot stand te brengen, is het mogelijk voor de gegevens om conflicterende waarden te bevatten (bijvoorbeeld, kan één dataset een klant als &quot;enig&quot;vermelden terwijl een andere dataset de klant als &quot;gehuwd&quot;kan vermelden). Het is de taak van het fusiebeleid om te bepalen welke gegevens aan prioriteren en vertoning als deel van het profiel moeten.

Voor meer informatie over samenvoegbeleid, met inbegrip van hoe te om, een standaard fusiebeleid voor uw organisatie tot stand te brengen uit te geven en te verklaren, gelieve te beginnen door [overzicht van fusiebeleid te lezen](../../profile/merge-policies/overview.md).

Het dashboard selecteert automatisch een samenvoegbeleid dat moet worden weergegeven, maar u kunt het samenvoegbeleid dat is geselecteerd wijzigen in het keuzemenu. Als u een ander samenvoegbeleid wilt kiezen, selecteert u de vervolgkeuzelijst naast de naam van het samenvoegbeleid en selecteert u vervolgens het samenvoegbeleid dat u wilt weergeven.

>[!NOTE]
>
>In het vervolgkeuzemenu ziet u alleen samenvoegbeleid met betrekking tot de XDM Individual Profile Class. Als uw organisatie echter meerdere samenvoegingsbeleidsregels heeft gemaakt, moet u mogelijk schuiven om de volledige lijst met beschikbare samenvoegingsbeleidsregels weer te geven.

![](../images/profiles/select-merge-policy.png)

## Widgets en metriek

Het dashboard bestaat uit widgets. Dit zijn alleen-lezen metriek die belangrijke informatie over uw profielgegevens verschaft.

De datum en tijd &#39;laatst bijgewerkt&#39; op een widget geeft aan wanneer de laatste momentopname van de gegevens is gemaakt. De datum en het tijdstip van de momentopname worden in UTC vermeld; het bevindt zich niet in de tijdzone van de individuele gebruiker of IMS-organisatie.

## Beschikbare widgets

Experience Platform biedt meerdere widgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw profielgegevens. Selecteer de naam van een widget hieronder voor meer informatie:

* [[!UICONTROL Profile count]](#profile-count)
* [[!UICONTROL Profiles added]](#profiles-added)
* [[!UICONTROL Profiles count trend]](#profiles-count-trend)
* [[!UICONTROL Profiles by identity]](#profiles-by-identity)
* [[!UICONTROL Identity overlap]](#identity-overlap)

### [!UICONTROL Profile count] {#profile-count}

De widget **[!UICONTROL Profile count]** geeft het totale aantal samengevoegde profielen weer in de profielgegevensopslag op het moment dat de momentopname werd gemaakt. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

Lees voor meer informatie over fragmenten en samengevoegde profielen eerst de sectie *Profielfragmenten vs samengevoegde profielen* van het [Real-time Customer Profile overview](../../profile/home.md).

![](../images/profiles/profile-count.png)

### [!UICONTROL Profiles added] {#profiles-added}

De widget **[!UICONTROL Profiles added]** geeft het totale aantal samengevoegde profielen weer dat met ingang van de laatste momentopname die is gemaakt, aan de gegevensopslagruimte Profiel is toegevoegd. Dit getal is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

U kunt de keuzekiezer gebruiken om de profielen weer te geven die in de afgelopen 30 dagen, 90 dagen of 12 maanden zijn toegevoegd.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Profiles count trend] {#profiles-count-trend}

De widget **[!UICONTROL Profiles count trend]** geeft het totale aantal samengevoegde profielen weer dat de afgelopen 30 dagen, 90 dagen of 12 maanden dagelijks is toegevoegd aan de profielgegevensopslag. Dit aantal wordt bijgewerkt elke dag wanneer de momentopname wordt genomen, daarom als u profielen in Platform zou moeten opnemen, zou het aantal profielen niet worden weerspiegeld tot de volgende momentopname wordt genomen.

Het aantal toegevoegde profielen is het resultaat van het geselecteerde samenvoegbeleid dat wordt toegepast op uw profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon.

![](../images/profiles/profile-count-trend.png)

### [!UICONTROL Profiles by identity] {#profiles-by-identity}

Met de widget **[!UICONTROL Profiles by identity]** wordt de indeling van de identiteiten in alle samengevoegde profielen in de winkel Profiel weergegeven. Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

Voor meer informatie over identiteiten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Identity overlap] {#identity-overlap}

De widget **[!UICONTROL Identity overlap]** geeft een Venn-diagram weer of stelt een diagram in waarin de overlapping van profielen in de winkel Profiel met meerdere identiteiten wordt weergegeven.

Nadat u de vervolgkeuzemenu&#39;s op de widget hebt gebruikt om de identiteiten te selecteren die u wilt vergelijken, worden cirkels weergegeven met de relatieve grootte van elke identiteit, waarbij het aantal profielen met beide naamruimten wordt weergegeven door de grootte van de overlapping tussen de cirkels.

Als een klant op meer dan één kanaal met uw merk in wisselwerking staat, zullen de veelvoudige identiteiten met die individuele klant worden geassocieerd, daarom is het waarschijnlijk dat uw organisatie veelvoudige profielen zal hebben die fragmenten van meer dan één identiteit bevatten.

Voor meer informatie over identiteiten gaat u naar de [documentatie van de Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/identity-overlap.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard Profielen vinden en begrijpen welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met [!DNL Profile]-gegevens in de interface van het Experience Platform, raadpleegt u de [UI-gids voor het realtime profiel van klanten](../../profile/ui/user-guide.md).
