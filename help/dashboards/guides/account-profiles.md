---
title: Dashboardgids voor accountprofielen
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie over de B2B-accountprofielen van uw organisatie kunt bekijken.
exl-id: c9a3d786-6240-4ba4-96c8-05f658e1150c
source-git-commit: 19d6d3c03e6b3b0f9f82ceeee30816fa054261a3
workflow-type: tm+mt
source-wordcount: '1009'
ht-degree: 0%

---

# [!UICONTROL Account Profiles] dashboard

De gebruikersinterface van Adobe Experience Platform (UI) biedt een dashboard waarmee u belangrijke informatie over uw accountprofielen kunt bekijken, zoals vastgelegd tijdens een dagelijkse momentopname. In deze handleiding wordt beschreven hoe u de [!UICONTROL Account Profiles] dashboard in UI en verstrekt meer informatie over de visualisaties die in het dashboard worden getoond.

Voor een overzicht van alle functies in de gebruikersinterface van het accountprofiel gaat u naar de [gebruikersgids voor accountprofiel](../../rtcdp/accounts/account-profile-ui-guide.md).

## Aan de slag

U moet recht hebben op [Real-time Customer Data Platform B2B Edition](../../rtcdp/b2b-overview.md) om toegang te krijgen tot B2B [!UICONTROL Account Profiles] dashboard.

## Gegevens van accountprofielen

De [!UICONTROL Account Profiles] het dashboard toont een momentopname van verenigde rekeningsinformatie van de veelvoudige bronnen over uw marketing kanalen en de diverse systemen die uw organisatie momenteel gebruikt om de informatie van de klantenrekening op te slaan.

De profielgegevens in de momentopname geven de gegevens precies zo weer als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en de [!UICONTROL Account Profiles] het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Ontdek de [!UICONTROL Account Profiles] dashboard

Ga naar de [!UICONTROL Account Profiles] dashboard in de interface van het Platform, selecteert u **[!UICONTROL Profiles]** krachtens [!UICONTROL Accounts] in het linkernavigatievenster.

![De gebruikersinterface van het Platform met accountprofielen in de linkernavigatie gemarkeerd en het overzichtstabblad weergegeven.](../images/account-profiles/account-profiles-dashboard.png)

Van de [!UICONTROL Account Profiles] dashboard: [door de accountprofielen bladeren die in uw organisatie worden opgenomen](#browse-account-profiles), of [de volledige gegevens van uw accountprofiel in één oogopslag weergeven met widgets](#standard-widgets) die aspecten van de gegevens visualiseren.

## Accountprofielen zoeken {#browse-account-profiles}

De [!UICONTROL Browse] kunt u de alleen-lezen accountprofielen die in uw organisatie worden ingevoerd, doorzoeken en bekijken met een account-id van een verbonden onderneming of door de brongegevens rechtstreeks in te voeren. Hier ziet u belangrijke informatie die bij het accountprofiel hoort, zoals de naam, industrie, inkomsten en segmenten.

Selecteer [!UICONTROL Profile ID] uit de resultaten die op de [!UICONTROL Browse] om de [!UICONTROL Details] voor het accountprofiel.

![Op het tabblad Accountprofielen worden de resultaten weergegeven en de profiel-id gemarkeerd.](../images/account-profiles/account-profiles-browse-tab.png)

De accountprofielgegevens die worden weergegeven op het tabblad [!UICONTROL Details] tabblad is samengevoegd vanuit meerdere profielfragmenten om een enkele weergave van de afzonderlijke account te vormen. Zie de documentatie op [bladeren door accountprofielen in Real-time Customer Data Platform](../../rtcdp/accounts/account-profile-ui-guide.md#browse-account-profiles) voor meer informatie over de weergavemogelijkheden van het accountprofiel in de gebruikersinterface van het Platform.

## De [!UICONTROL Account Profiles] [!UICONTROL Overview] {#overview}

De [!UICONTROL Overview] tab bestaat uit widgets die alleen-lezen gegevens bieden om belangrijke informatie over uw accountprofielen over te brengen. Selecteren **[!UICONTROL Modify dashboard]** om de vormgeving van de [!UICONTROL Overview] door widgets te verplaatsen en te vergroten of te verkleinen.

![Het tabblad Overzicht van accountprofielen waarop het dashboard Wijzigen is gemarkeerd.](../images/account-profiles/modify-dashboard.png)

Raadpleeg het document op [wijzigen, dashboards](../customize/modify.md) en de [Overzicht van widgetbibliotheek](../customize/widget-library.md) voor meer informatie.

## Standaardwidgets {#standard-widgets}

Adobe biedt standaardwidgets die u kunt gebruiken voor het visualiseren van verschillende meetgegevens die betrekking hebben op uw accountprofielen.

Als u meer wilt weten over elk van de beschikbare standaardwidgets, selecteert u de naam van een widget in de volgende lijst:

* [Totaal rekeningen per bedrijfstak](#total-accounts-by-industry)
* [Accountprofielen toegevoegd](#account-profiles-added)
* [Predictieve spreiding van scores](#predictive-scoring-distribution)
* [Predictieve scoring van invloedrijke factoren](#predictive-scoring-top-influential-factors)

### Totaal rekeningen per bedrijfstak {#total-accounts-by-industry}

Deze widget geeft het totale aantal accounts in één meting weer en gebruikt een donutgrafiek om de proportionele aantallen te illustreren voor de bedrijfstakken die het totale aantal vormen. De sleutel verstrekt de informatie van de kleurencodering voor de verschillende industrieën die omhoog de donutgrafiek maken.

Individuele tellingen voor de verschillende industrieën worden getoond in een dialoog wanneer de curseur over de respectieve sectie van de donutgrafiek hangt.

![De totale accounts per bedrijfswidget.](../images/account-profiles/total-accounts-by-industry-widget.png)

### Accountprofielen toegevoegd {#account-profiles-added}

Deze widget gebruikt een kleurengecodeerd staafdiagram om het aantal profielen te illustreren dat gedurende een bepaalde periode aan een account is toegevoegd, en het aandeel van verschillende bedrijfstakken die deze toegevoegde profielen vormen. De industrieën zijn kleurengecodeerd, en een sleutel verstrekt de informatie van de kleurencodering voor de verschillende industrieën die omhoog het bar grafiek maken. De analyseperiode wordt geselecteerd van het widgetdropdown menu. Het staafdiagram kan worden weergegeven over een periode van 30 dagen, 90 dagen en 12 maanden.

>[!NOTE]
>
>Aangezien profielen alleen aan een account worden toegevoegd en nooit worden verwijderd, is het laagste aantal profielen dat over een bepaalde periode wordt toegevoegd, nul.

![De widget Accountprofielen toegevoegd.](../images/account-profiles/accounts-profiles-added-widget.png)

### Predictieve spreiding van scores {#predictive-scoring-distribution}

De [!UICONTROL Predictive scoring distribution] widget geeft de verdeling van de score van alle accountprofielen weer om u te helpen de gezondheid van uw verkooppijplijn in één oogopslag te begrijpen . De het scoren gegevens worden overgebracht door een donutgrafiek en een kolomgrafiek.

Het donutdiagram toont het aandeel van uw totale accountprofielen in elk van de sterke, gemiddelde en lage neiging om emmers te kopen. De sleutel bevat meer details over de secties met kleurcodes, waaronder de bereiken van het scoremmer en het aantal accountprofielen in dat bereik.

De kolomgrafiek verstrekt een meer korrelige het scoren mislukking. Elke kolom toont het aantal rekeningsprofielen in elk van de 20 5-punt verhogende emmers.

Met het vervolgkeuzemenu in de widget kunt u het accountscoremodel selecteren.

![De widget voor voorspellende codeverdeling.](../images/account-profiles/predictive-scoring-distribution.png)

### Predictieve scoring van invloedrijke factoren {#predictive-scoring-top-influential-factors}

De [!UICONTROL Predictive scoring top influential factors] widget helpt u de belangrijkste factoren te begrijpen die de scores voor elke aandrijvingsemmer drijven.

Deze widget toont de belangrijkste invloedrijke factoren voor elk van de hoge, gemiddelde, en lage aandrijvingsemmers. Een staaf voor elke invloedrijke factor geeft het percentage aan van de accountprofielen in dat eigenschapssemmer dat de specifieke invloedrijke factor bevat.

Met het vervolgkeuzemenu in de widget kunt u het accountscoremodel selecteren.

![De widget Voorspelende score met invloedrijke factoren.](../images/account-profiles/predictive-scoring-top-influential-factors.png)

## Volgende stappen

Door dit document te volgen, moet u nu weten hoe u de [!UICONTROL Account Profiles] dashboard. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Als u meer wilt weten over het werken met accountprofielen als onderdeel van uw B2B-gegevens in de interface van het Experience Platform, raadpleegt u de [overzicht van accountprofielen](../../rtcdp/accounts/account-profile-overview.md) voor Adobe Real-Time CDP, B2B Edition.
