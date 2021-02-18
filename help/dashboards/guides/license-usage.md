---
keywords: Experience Platform;gebruikersinterface;UI;aanpassing;licentiegebruiksdashboard;dashboard;licentiegebruik;machtiging;consumptie
title: Licentiegebruiksdashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het gebruik van licenties voor uw organisatie.
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 084aaa315f694d696abee7f078be3a121111f6cc
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 0%

---


# (Beta) [!UICONTROL Licentiegebruik] dashboard {#license-usage-dashboard}

>[!IMPORTANT]
>
>De dashboardfunctionaliteit die in dit document wordt beschreven is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het vergunningsgebruik van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het dashboard van het vergunningsgebruik in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een algemeen overzicht van het Platform UI, gelieve [Experience Platform UI gids](../../landing/ui-guide.md) te bezoeken.

## Gegevens op het gebruiksdashboard voor licenties

Op het dashboard voor licentiegebruik wordt een momentopname weergegeven van de licentiegegevens van uw organisatie voor Experience Platform. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de opname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor licentiegebruik verkennen

Als u naar het dashboard voor licentiegebruik in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL Licentiegebruik]** in de linkertrack. Dit wordt geopend met het tabblad **[!UICONTROL Overzicht]** waarin het dashboard wordt weergegeven.

![](../images/license-usage/dashboard-overview.png)

### Een sandbox selecteren

Selecteer [!UICONTROL Productie] of [!UICONTROL Ontwikkeling] om een sandbox te kiezen die u wilt weergeven in het dashboard. De geselecteerde sandbox wordt aangegeven met het keuzerondje naast de naam van de sandbox.

>[!NOTE]
>
>Consumptierapporten voor sandboxen zijn cumulatief voor alle sandboxen van hetzelfde type. Met andere woorden, als u [!UICONTROL Production] of [!UICONTROL Development] selecteert, wordt respectievelijk een rapport over alle productie- of ontwikkelingssandboxen weergegeven.

![](../images/license-usage/select-sandbox.png)

### Een datumbereik selecteren

Nadat u een sandbox hebt geselecteerd, kunt u de vervolgkeuzelijst voor het datumbereik gebruiken om de periode te selecteren die moet worden weergegeven in het dashboard. Er zijn drie opties beschikbaar: [!UICONTROL Laatste 30 dagen], [!UICONTROL Laatste 90 dagen], en [!UICONTROL Laatste 12 maanden]. De laatste 30 dagen zijn standaard geselecteerd.

![](../images/license-usage/select-date-range.png)

### Widgets en metriek

Het licentiegebruikdashboard bestaat uit widgets, die alleen-lezen cijfers weergeven die belangrijke informatie geven over het gebruik van de licentie van uw organisatie. Zie de sectie over beschikbare widgets in deze handleiding voor meer informatie over deze widgets.

## Beschikbare widgets {#available-widgets}

Experience Platform bevat momenteel één widget waarmee u het licentiegebruik kunt visualiseren. Binnenkort worden er meer widgets uitgebracht.

### [!UICONTROL Adresseerbaar publiek] {#addressable-audiences}

Met de widget **[!UICONTROL Adresseerbare doelgroepen]** wordt het totale aantal samengevoegde profielen weergegeven in de profielgegevensopslagruimte, nadat een door het systeem gegenereerd samenvoegbeleid is toegepast om profielfragmenten van alle huidige gegevenssets te combineren met een deterministisch (privé) grafiekalgoritme.

Voor meer informatie over fragmenten en samengevoegde profielen, gelieve te beginnen door *de fragmenten van het Profiel vs samengevoegde profielen* sectie van [Profieloverzicht](../../profile/home.md) te lezen.

>[!NOTE]
>
>Het samenvoegbeleid dat wordt gebruikt om deze metrisch te berekenen wordt geproduceerd door Experience Platform en kan niet worden uitgegeven, noch kan een verschillend fusiebeleid worden geselecteerd. Dit door het systeem gegenereerde samenvoegingsbeleid is niet hetzelfde als het standaardsamenvoegbeleid dat wordt gebruikt om [!UICONTROL Audience size] in het [!DNL Profile] dashboard te berekenen. Daarom is het onwaarschijnlijk dat het aantal gebruikers in het [!UICONTROL Licentiegebruik] en [!DNL Profile] dashboards precies hetzelfde zullen zijn.

![](../images/license-usage/addressable-audiences.png)

## Volgende stappen

Als u dit document volgt, kunt u nu het dashboard voor licentiegebruik vinden en een sandbox selecteren die u wilt weergeven. U moet ook weten welke maatstaven worden weergegeven in de beschikbare widgets. Voor meer informatie over het Experience Platform UI, gelieve te verwijzen naar [Platform UI guide](../../landing/ui-guide.md).