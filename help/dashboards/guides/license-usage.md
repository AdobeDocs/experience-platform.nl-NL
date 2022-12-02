---
keywords: Experience Platform;gebruikersinterface;UI;aanpassing;licentiegebruiksdashboard;dashboard;licentiegebruik;machtiging;consumptie
title: Handleiding voor het gebruiksdashboard voor licenties
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het gebruik van licenties voor uw organisatie.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: 255de9b9e83c11aeed747a3c0cdb7bd7a7949bd2
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%

---

# Het gebruiksdashboard voor licenties {#license-usage-dashboard}

De gebruikersinterface van Adobe Experience Platform (UI) verstrekt een dashboard waardoor u belangrijke informatie over het vergunningsgebruik van uw organisatie kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Deze gids schetst hoe te om tot en met het dashboard van het vergunningsgebruik in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een algemeen overzicht van de gebruikersinterface van het Platform gaat u naar de [UI-hulplijn Experience Platform](../../landing/ui-guide.md).

## Gegevens op het gebruiksdashboard voor licenties

Op het dashboard voor licentiegebruik wordt een momentopname weergegeven van de licentiegegevens van uw organisatie voor Experience Platform. De gegevens in het dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de opname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor licentiegebruik verkennen

Als u naar het dashboard voor licentiegebruik in de gebruikersinterface van het Platform wilt navigeren, selecteert u **[!UICONTROL License usage]** in het linkerspoor. Hierdoor wordt het **[!UICONTROL Overview]** tabblad met het dashboard.

>[!NOTE]
>
>Het dashboard voor licentiegebruik is niet standaard ingeschakeld. Gebruikers kunnen het dashboard alleen weergeven als ze de machtiging &#39;Licentiegebruiksdashboard weergeven&#39; hebben gekregen. Voor stappen voor het verlenen van toegangstoestemmingen voor het bekijken van het dashboard van het vergunningsgebruik, gelieve te verwijzen naar [Handleiding voor dashboardmachtigingen](../permissions.md).

![Het tabblad Overzicht van het dashboard voor licentiegebruik.](../images/license-usage/dashboard-overview.png)

### Een sandbox selecteren

Als u een sandbox wilt kiezen die u in het dashboard wilt weergeven, selecteert u [!UICONTROL Production] of [!UICONTROL Development]. De geselecteerde sandbox wordt aangegeven met het keuzerondje naast de naam van de sandbox.

Consumptierapporten voor sandboxen zijn cumulatief voor alle sandboxen van hetzelfde type. Met andere woorden: selecteren [!UICONTROL Production] of [!UICONTROL Development] verstrekt verbruiksrapporten voor alle productie of ontwikkelingszandbakken, respectievelijk.

![Het tabblad Overzicht van het dashboard voor licentiegebruik met de sandboxkiezer gemarkeerd.](../images/license-usage/select-sandbox.png)

>[!WARNING]
>
>Toestemming om het dashboard voor het gebruiksbewijs van licenties weer te geven, moet worden opgegeven op sandboxniveau. Dit betekent dat de machtiging voor het weergeven van het dashboard moet worden toegevoegd aan elke afzonderlijke sandbox. Deze beperking wordt in een toekomstige release opgelost. Ondertussen is de volgende oplossing beschikbaar:
>
>1. Maak een productprofiel in de Adobe Admin Console.
>2. Voeg onder Machtiging in de categorie Sandbox alle sandboxen toe die u wilt weergeven in het dashboard voor licentiegebruik.
>3. Voeg onder de categorie Machtiging voor dashboard van gebruiker de machtiging &#39;Licentiegebruiksdashboard weergeven&#39; toe.


### Een datumbereik selecteren

Nadat u een sandbox hebt geselecteerd, kunt u de vervolgkeuzelijst voor het datumbereik gebruiken om de periode te selecteren die moet worden weergegeven in het dashboard. Er zijn meerdere opties beschikbaar, waaronder de standaardwaarde van de laatste 30 dagen.

![Het tabblad Overzicht van het dashboard voor licentiegebruik met de vervolgkeuzelijst voor datumbereik gemarkeerd.](../images/license-usage/select-date-range.png)

U kunt ook **[!UICONTROL Custom date]** om de periode te kiezen die wordt getoond.

![Het tabblad Overzicht van het dashboard voor licentiegebruik met de opties voor het aangepaste datumbereik gemarkeerd.](../images/license-usage/select-custom-date.png)

## Widgets

Het licentiegebruikdashboard bestaat uit widgets, die alleen-lezen cijfers weergeven die belangrijke informatie geven over het gebruik van de licentie van uw organisatie. De zichtbare metriek hangen van de specifieke vergunning van uw organisatie af (zie [beschikbare cijfers](#available-metrics) voor meer informatie).

Elke widget geeft een lijngrafiek weer waarin de werkelijke nummers voor uw organisatie worden vergeleken met het totale beschikbare aantal voor licenties van uw organisatie en een percentage van het totale gebruik.

![Het tabblad Overzicht van het dashboard voor licentiegebruik met de lijngrafiek van de metrische widget voor samplelicentiegebruik gemarkeerd.](../images/license-usage/widgets.png)

## Beschikbare cijfers

Het dashboard van het vergunningsgebruik rapporteert over vier zeer belangrijke metriek, met meer metriek die in verdere versies moet worden toegevoegd. De beschikbare meetwaarden zijn:

* [!UICONTROL Addressable Audience]
* [!UICONTROL Average profile richness]
* [!UICONTROL Data scanned per segmentation ratio]
* [!UICONTROL Total consumed storage]

De beschikbaarheid van deze cijfers en de specifieke definitie van elk van deze cijfers variëren afhankelijk van de licenties die uw organisatie heeft aangeschaft. Raadpleeg de desbetreffende documentatie over de productbeschrijving voor gedetailleerde definities van elke meeteenheid:

| Licentie | Productbeschrijving |
|---|---|
| <ul><li>Adobe Experience Platform:OD LITE</li><li>Adobe Experience Platform:OD STANDARD</li><li>Adobe Experience Platform:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>Adobe Experience Platform:OD</li></ul> | [Experience Platform, toepassingsservices en intelligente services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT KLANTGEGEVENS, PLATFORM:OD</li><li>RT KLANTGEGEVENS PLATFORM:OD PRFL NAAR 10M</li><li>RT KLANTGEGEVENS PLATFORM:OD PRFL NAAR 50 M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL NAAR 10M</li><li>AEP:OD ACTIVATION PRFL TOT 50M</li></ul> | [Adobe Experience Platform-activering](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>Journey Optimizer SELECT:OD</li><li>Journey Optimizer PRIME:OD</li><li>Journey Optimizer ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Het dashboard voor het gebruiksgemak rapporteert alleen over de nieuwste licentie die voor uw organisatie is ingericht. Als de meest recente licentie die voor uw organisatie is ingesteld, niet in de bovenstaande tabel wordt weergegeven, wordt het licentiegebruiksdashboard mogelijk niet correct weergegeven. Ondersteuning voor extra licenties en meerdere licenties in één organisatie is gepland voor een toekomstige release.

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u het dashboard voor licentiegebruik vinden en een sandbox selecteren die u wilt weergeven. U kunt ook meer informatie vinden over beschikbare metriek voor uw organisatie, gebaseerd op de vergunning uw organisatie heeft gekocht.

Voor meer informatie over andere functies die beschikbaar zijn in de gebruikersinterface van het Experience Platform, raadpleegt u de [UI-hulplijn Platform](../../landing/ui-guide.md).
