---
keywords: Experience Platform;gebruikersinterface;UI;aanpassing;licentiegebruiksdashboard;dashboard;licentiegebruik;machtiging;consumptie
title: Licentiegebruiksdashboard
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het gebruik van licenties voor uw organisatie.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 47c4113d45b0101a761fa7d703013609e8729dbb
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Licentiedashboard {#license-usage-dashboard}

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het vergunningsgebruik van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het dashboard van het vergunningsgebruik in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een algemeen overzicht van het Platform UI, gelieve [Experience Platform UI gids](../../landing/ui-guide.md) te bezoeken.

## Gegevens op het gebruiksdashboard voor licenties

Op het dashboard voor licentiegebruik wordt een momentopname weergegeven van de licentiegegevens van uw organisatie voor Experience Platform. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de opname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor licentiegebruik verkennen

Als u naar het dashboard voor licentiegebruik in de interface van het Platform wilt navigeren, selecteert u **[!UICONTROL License usage]** in de linkertrack. Hiermee wordt het tabblad **[!UICONTROL Overview]** geopend waarin het dashboard wordt weergegeven.

>[!NOTE]
>
>Het dashboard voor licentiegebruik is niet standaard ingeschakeld. Gebruikers kunnen het dashboard alleen weergeven als ze de machtiging &#39;Licentiegebruiksdashboard weergeven&#39; hebben gekregen. Raadpleeg de [handleiding voor dashboardmachtigingen voor dashboardmachtigingen](../permissions.md) voor stappen voor het verlenen van toegangsmachtigingen voor het weergeven van het dashboard voor het gebruik van licenties.

![](../images/license-usage/dashboard-overview.png)

### Een sandbox selecteren

Selecteer [!UICONTROL Production] of [!UICONTROL Development] om een sandbox te kiezen die u wilt weergeven in het dashboard. De geselecteerde sandbox wordt aangegeven met het keuzerondje naast de naam van de sandbox.

Consumptierapporten voor sandboxen zijn cumulatief voor alle sandboxen van hetzelfde type. Met andere woorden, als u [!UICONTROL Production] of [!UICONTROL Development] selecteert, worden verbruiksrapporten voor respectievelijk alle productie- of ontwikkelingssandboxen geleverd.

![](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>Toestemming om het dashboard voor het gebruiksbewijs van licenties weer te geven, moet worden opgegeven op sandboxniveau. Dit betekent dat de machtiging voor het weergeven van het dashboard moet worden toegevoegd aan elke afzonderlijke sandbox. Deze beperking wordt in een toekomstige release opgelost. Ondertussen is de volgende oplossing beschikbaar:
>
>1. Maak een productprofiel in de Adobe Admin Console.
>2. Voeg onder Machtiging in de categorie Sandbox alle sandboxen toe die u wilt weergeven in het dashboard voor licentiegebruik.
>3. Voeg onder de categorie Machtiging voor dashboard van gebruiker de machtiging &#39;Licentiegebruiksdashboard weergeven&#39; toe.


### Een datumbereik selecteren

Nadat u een sandbox hebt geselecteerd, kunt u de vervolgkeuzelijst voor het datumbereik gebruiken om de periode te selecteren die moet worden weergegeven in het dashboard. Er zijn meerdere opties beschikbaar, waaronder de standaardwaarde van de laatste 30 dagen.

![](../images/license-usage/select-date-range.png)

U kunt **[!UICONTROL Custom date]** ook selecteren om de tijdspanne te kiezen die wordt getoond.

![](../images/license-usage/select-custom-date.png)

## Widgets

Het licentiegebruikdashboard bestaat uit widgets, die alleen-lezen cijfers weergeven die belangrijke informatie geven over het gebruik van de licentie van uw organisatie. De zichtbare metriek hangen van de specifieke vergunning van uw organisatie af (zie [beschikbare metriek](#available-metrics) sectie voor details).

Elke widget geeft een lijngrafiek weer waarin de werkelijke nummers voor uw organisatie worden vergeleken met het totale beschikbare aantal voor licenties van uw organisatie en een percentage van het totale gebruik.

![](../images/license-usage/widgets.png)

## Beschikbare cijfers

Het dashboard van het vergunningsgebruik rapporteert over vier zeer belangrijke metriek, met meer metriek die in verdere versies moet worden toegevoegd. De beschikbare metriek worden hieronder vermeld.

>[!NOTE]
>
>Drie van de beschikbare metriek bevinden zich momenteel in bèta.

* [!UICONTROL Addressable Audience]
* [!UICONTROL Average profile richness] (bèta)
* [!UICONTROL Data scanned per segmentation ratio] (bèta)
* [!UICONTROL Total consumed storage] (bèta)

>[!WARNING]
>
>Bekende beperking van de metrische waarde [!UICONTROL Total consumed storage]: Wanneer u batchgegevens verwijdert, wordt die batch gedurende 7 dagen in een &#39;soft delete&#39;-status geplaatst om het gebruik van gegevens voor gegevensherstel te ondersteunen. Na 7 dagen wordt de batch verplaatst naar een status voor verwijderen op papier. De rapportering over de totale verbruikte opslag zal geen verandering in de trendgrafiek weerspiegelen tot de partij in de harde schrappingsstaat is. Dit probleem wordt in een toekomstige release opgelost.

De beschikbaarheid van deze cijfers en de specifieke definitie van elk van deze cijfers variëren afhankelijk van de licenties die uw organisatie heeft aangeschaft. Raadpleeg de desbetreffende documentatie over de productbeschrijving voor gedetailleerde definities van elke meeteenheid:

| Licentie | Productbeschrijving |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, toepassingsservices en intelligente services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT KLANTGEGEVENS, PLATFORM:OD</li><li>RT KLANTGEGEVENS PLATFORM:OD PRFL NAAR 10M</li><li>RT KLANTGEGEVENS PLATFORM:OD PRFL NAAR 50 M</li></ul> | [Real-time Platform voor klantgegevens](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL NAAR 10M</li><li>AEP:OD ACTIVATION PRFL TOT 50M</li></ul> | [Adobe Experience Platform-activering](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |

>[!WARNING]
>
>Het dashboard voor het gebruiksgemak rapporteert alleen over de nieuwste licentie die voor uw organisatie is ingericht. Als de meest recente licentie die voor uw organisatie is ingesteld, niet in de bovenstaande tabel wordt weergegeven, wordt het licentiegebruiksdashboard mogelijk niet correct weergegeven. Ondersteuning voor extra licenties en meerdere licenties in één organisatie is gepland voor een toekomstige release.

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u het dashboard voor licentiegebruik vinden en een sandbox selecteren die u wilt weergeven. U kunt ook meer informatie vinden over beschikbare metriek voor uw organisatie, gebaseerd op de vergunning uw organisatie heeft gekocht.

Voor meer informatie over andere eigenschappen beschikbaar in de UI van het Experience Platform, gelieve te verwijzen naar [Platform UI guide](../../landing/ui-guide.md).
