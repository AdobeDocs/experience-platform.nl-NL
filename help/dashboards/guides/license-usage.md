---
keywords: Experience Platform;gebruikersinterface;UI;aanpassing;licentiegebruiksdashboard;dashboard;licentiegebruik;machtiging;consumptie
title: Licentiegebruiksdashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het gebruik van licenties voor uw organisatie.
topic-legacy: guide
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---

# (bèta) Licentiegebruikdashboard {#license-usage-dashboard}

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

Als u naar het dashboard voor licentiegebruik in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL License usage]** in de linkertrack. Dit wordt geopend met het tabblad **[!UICONTROL Overview]** waarop het dashboard wordt weergegeven.

![](../images/license-usage/dashboard-overview.png)

### Een sandbox selecteren

Selecteer [!UICONTROL Production] of [!UICONTROL Development] om een sandbox te kiezen die u wilt weergeven in het dashboard. De geselecteerde sandbox wordt aangegeven met het keuzerondje naast de naam van de sandbox.

>[!NOTE]
>
>Consumptierapporten voor sandboxen zijn cumulatief voor alle sandboxen van hetzelfde type. Met andere woorden, als u [!UICONTROL Production] of [!UICONTROL Development] selecteert, worden verbruiksrapporten voor respectievelijk alle productie- of ontwikkelingssandboxen geleverd.

![](../images/license-usage/select-sandbox.png)

### Een datumbereik selecteren

Nadat u een sandbox hebt geselecteerd, kunt u de vervolgkeuzelijst voor het datumbereik gebruiken om de periode te selecteren die moet worden weergegeven in het dashboard. Er zijn drie opties beschikbaar: [!UICONTROL Last 30 days], [!UICONTROL Last 90 days] en [!UICONTROL Last 12 months]. De laatste 30 dagen zijn standaard geselecteerd.

![](../images/license-usage/select-date-range.png)

## Widgets

Het licentiegebruikdashboard bestaat uit widgets, die alleen-lezen cijfers weergeven die belangrijke informatie geven over het gebruik van de licentie van uw organisatie. De zichtbare metriek hangen van de specifieke vergunning van uw organisatie af (zie [beschikbare metriek](#available-metrics) sectie voor details).

Elke widget geeft een lijngrafiek weer waarin de werkelijke nummers voor uw organisatie worden vergeleken met het totale beschikbare aantal voor licenties van uw organisatie en een percentage van het totale gebruik.

![](../images/license-usage/widgets.png)

## Beschikbare cijfers

Er zijn momenteel vier metriek beschikbaar in het dashboard van het vergunningsgebruik:

* [!UICONTROL Addressable Audience] (gemeten op basis van het aantal profielen)
* [!UICONTROL Average profile richness]
* [!UICONTROL Total consumed storage]
* [!UICONTROL Data scanned per segmentation ratio]

De definitie van elk van deze cijfers is afhankelijk van de licenties die uw organisatie heeft aangeschaft. Raadpleeg de desbetreffende documentatie over de productbeschrijving voor gedetailleerde definities van elke meeteenheid:

| Licentie | Productbeschrijving |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, toepassingsservices en intelligente services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT KLANTGEGEVENS, PLATFORM:OD</li><li>RT KLANTGEGEVENS PLATFORM:OD PRFL NAAR 10M</li><li>RT KLANTGEGEVENS PLATFORM:OD PRFL NAAR 50 M</li></ul> | [Real-time Platform voor klantgegevens](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL NAAR 10M</li><li>AEP:OD ACTIVATION PRFL TOT 50M</li></ul> | [Adobe Experience Platform-activering](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u het dashboard voor licentiegebruik vinden en een sandbox selecteren die u wilt weergeven. U kunt ook meer informatie vinden over beschikbare metriek voor uw organisatie, gebaseerd op de vergunning uw organisatie heeft gekocht.

Voor meer informatie over andere eigenschappen beschikbaar in de UI van het Experience Platform, gelieve te verwijzen naar [Platform UI guide](../../landing/ui-guide.md).
