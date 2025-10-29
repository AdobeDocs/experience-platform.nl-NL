---
keywords: Experience Platform;inzichten;attributie ai;populaire onderwerpen;attributie ai inzichten
feature: Attribution AI
title: Inzichten in Attributie-AI ontdekken
description: Dit document fungeert als richtlijn voor het communiceren met de inzichten van serviceinstanties in de gebruikersinterface van Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1583'
ht-degree: 0%

---

# Inzichten in kenmerken van AI ontdekken

Attribution AI service instances verschaffen inzichten die kunnen worden gebruikt om marketingbeslissingen met betrekking tot marketingprestaties en rendement op investeringen te nemen en te meten. Het selecteren van een de dienstinstantie verstrekt visualisaties en filters om u bij het begrijpen van het effect van elke klanteninteractie in elke fase van de klantenreis te helpen.

Dit document fungeert als richtlijn voor het communiceren met de inzichten van serviceinstanties in de gebruikersinterface van Adobe Intelligent Services.

## Aan de slag

Om inzichten voor Attribution AI te gebruiken, moet u een de dienstinstantie hebben met een succesvolle looppasstatus beschikbaar. Om een nieuwe de dienstinstantie tot stand te brengen bezoek de [&#x200B; gebruikersinterfacegids van de Attributie AI &#x200B;](./user-guide.md). Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

## Overzicht van inzichten in servicevergaderingen

Selecteer in de gebruikersinterface van [!DNL Adobe Experience Platform] de optie **[!UICONTROL Services]** in de linkernavigatie. De browser **[!UICONTROL Services]** wordt weergegeven en geeft de beschikbare Adobe Intelligent Services weer. Selecteer **[!UICONTROL Open]** in de container for Attribution AI.

![&#x200B; Toegang hebbend tot uw instantie &#x200B;](./images/insights/open_Attribution_ai.png)

De pagina van de dienst van AI van de Attributie verschijnt. Deze pagina bevat een overzicht van de service-instanties van Attribution AI en geeft informatie over deze instanties, zoals de naam van de instantie, conversiegebeurtenissen, hoe vaak de instantie wordt uitgevoerd en de status van de laatste update. Selecteer de naam van een service-instantie om te beginnen.

>[!NOTE]
>
>Alleen serviceversies die een scoring hebben voltooid, kunnen worden geselecteerd.

![&#x200B; creeer instantie &#x200B;](./images/insights/select-service-instance.png)

Vervolgens wordt de pagina met inzichten voor die service-instantie weergegeven, waarin u een aantal visualisaties en filters hebt om met uw gegevens te werken. De visualisaties en filters worden in deze handleiding gedetailleerder uitgelegd.

![&#x200B; opstellingspagina &#x200B;](./images/insights/landing-page.png)

### Details van serviceinstantie

Als u meer details voor een service-instantie wilt weergeven, selecteert u **[!UICONTROL Show more]** rechtsboven.

![&#x200B; toon meer &#x200B;](./images/insights/show-more.png)

Er wordt een gedetailleerde lijst weergegeven. Voor meer informatie over om het even welke vermelde eigenschappen, gelieve de [&#x200B; AI gebruikersgids van de Attributie &#x200B;](./user-guide.md) te bezoeken.

![&#x200B; toon details &#x200B;](./images/insights/advanced-details.png)

### Een instantie bewerken

Als u een instantie wilt bewerken, selecteert u **[!UICONTROL Edit]** in de navigatie rechtsboven.
![&#x200B; klik uitgeven knoop &#x200B;](./images/insights/edit-button.png)

Het dialoogvenster Bewerken wordt weergegeven. In dit venster kunt u de naam, beschrijving en frequentie van de instantie bewerken. Als de status van de instantie is uitgeschakeld, kan de scorefrequentie niet worden bewerkt. Als u de wijzigingen wilt bevestigen en het dialoogvenster wilt sluiten, selecteert u **[!UICONTROL Save]** in de rechterbenedenhoek.

![&#x200B; geef popover uit &#x200B;](./images/insights/edit-popover.png)

### Meer acties {#more-actions}

De knop **[!UICONTROL More actions]** bevindt zich in de navigatie rechtsboven naast **[!UICONTROL Edit]** . Als u **[!UICONTROL More actions]** selecteert, wordt een vervolgkeuzelijst geopend waarin u een van de volgende bewerkingen kunt selecteren:

- **[!UICONTROL Clone]**: hiermee wordt de instantie gekloond.
- **[!UICONTROL Delete]** : hiermee verwijdert u de instantie.
- **[!UICONTROL Download summary data]**: hiermee downloadt u een CSV-bestand met de samenvattingsgegevens.
- **[!UICONTROL Access scores]**: Het selecteren **[!UICONTROL Access scores]** richt u aan de [&#x200B; toegangsscores voor de zelfstudie van AI van de Attributie &#x200B;](./download-scores.md) opnieuw.
- **[!UICONTROL View run history]**: Er wordt een pop-upmenu weergegeven met een lijst van alle scores die zijn gekoppeld aan de service-instantie.

![&#x200B; meer acties &#x200B;](./images/insights/more-actions.png)

## Gegevens filteren

Met Attribution AI-inzichten kunt u uw gegevens filteren en de UI-visuele elementen automatisch bijwerken op basis van de geselecteerde filters.

### Conversion-gebeurtenis

Wanneer u een nieuwe instantie maakt in Attribution AI, is een van de vereiste velden &#39;Conversiegebeurtenissen&#39;. Conversiegebeurtenissen zijn bedrijfsdoelstellingen die het effect van marketing activiteiten, zoals, e-commerceorders, in-store aankopen, en websitebezoeken identificeren.

Vanuit de instantie kunt u met het vervolgkeuzemenu **[!UICONTROL Conversion events]** de gebeurtenissen selecteren die voor de instantie zijn gedefinieerd om uw gegevens te filteren. Als u specifieke gebeurtenissen selecteert, worden de gebruikersinterfacevisualisaties gewijzigd en worden conversies die bij die gebeurtenissen horen alleen gevuld.

![&#x200B; omzettingsgebeurtenis &#x200B;](./images/insights/conversion-event.png)

### Attributiemodel

Als u **[!UICONTROL Attribution Model]** selecteert, wordt een vervolgkeuzelijst geopend met alle verschillende beschikbare toewijzingsmodellen. U kunt meerdere modellen selecteren om de resultaten te vergelijken. Voor meer informatie over de verschillende attributiemodellen en hoe zij werken, bezoek het [&#x200B; overzicht van de Attributie AI &#x200B;](./overview.md) dat een lijst met informatie over elk model bevat.

![&#x200B; attributiemodel &#x200B;](./images/insights/attribution-model.png)

### Regio

>[!NOTE]
>
>Dit filter is aanwezig slechts als u de facultatieve stap [&#x200B; op gebied-gebaseerde modellering &#x200B;](./user-guide.md#region-based-modeling-optional) in de gebruikersinterfacegids van Attributie AI uitvoerde toen het creëren van uw de dienstinstantie.

Met dit filter kunt u alle gebieden selecteren die u hebt ingesteld in het proces voor het maken van instanties.

### Filters toevoegen

U kunt extra filters toevoegen door het **filter** pictogram te selecteren om **[!UICONTROL Add filters]** popover te openen. Met de **[!UICONTROL Add filters]** popover kunt u filteren op Kanaal, Geografie, Mediatype en Product. Alleen de toepasselijke filters voor een service-instantie worden gevuld door de pop-over. Als u bijvoorbeeld geen geografische gegevens of een mediatype hebt opgegeven, zijn deze filterkenmerken niet beschikbaar voor uw instantie.

![&#x200B; extra filters &#x200B;](./images/insights/additional-filters.png)

![&#x200B; filter popover &#x200B;](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** het selecteren van het kanaalattribuut staat u toe om het even welk van uw beschikbare marketing kanalen te filtreren. U kunt meerdere kanalen selecteren om ze te vergelijken.
- **[!UICONTROL Geography]:** het selecteren van de geografie attributen staat u toe om landcodes te filtreren die op gebied-gebaseerde modellen worden gebaseerd. Afhankelijk van uw gegevens kan dit filter al dan niet aanwezig zijn. Landcodes zijn twee tekens lang. Zie de volledige lijst van landcodes [&#x200B; hier &#x200B;](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** Als u het mediatype-kenmerk selecteert, kunt u elk van de gedefinieerde mediatypen filteren.
- **[!UICONTROL Product]:** Als u het kenmerk product selecteert, kunt u filteren op producten die u aanvankelijk hebt ingeslikt tijdens het maken van de instantie.

### Datumbereik

Selecteer het kalenderpictogram om de popover van het datumbereik te openen. De begin- en einddatum van de conversiegebeurtenis bepalen hoeveel gegevens worden ingevuld in de gebruikersinterface. U kunt ervoor kiezen het datumbereik te beperken of uit te breiden om de hoeveelheid gegevens die is ingevuld, scherper te maken of uit te breiden.

![&#x200B; datumwaaier &#x200B;](./images/insights/display-date-range.png)

## Overzicht van uw gegevens

Op de **[!UICONTROL Overview]** -kaart worden de totale conversies weergegeven op basis van het toewijzingsmodel. Het totale aantal verandert op basis van hoe specifiek u de zoekopdracht maakt met de filters die eerder in dit document zijn beschreven. Als u meer modellen selecteert, worden extra cirkels aan het overzicht toegevoegd, elk met een eigen kleur die overeenkomt met de legenda.

![&#x200B; overzicht &#x200B;](./images/insights/Overview.png)

## Wekelijkse trends

De **[!UICONTROL Weekly trends]** -kaart splitst de totale conversie in het datumbereik dat u instelt tijdens het filterproces.

Het selecteren van de ellipsen in het hoogste recht van de **Wekelijkse tendensen** kaart toont een daling neer toestaand u om dagelijkse, wekelijkse, of maandelijkse tendensen te selecteren.

Als u de muis boven de gegevensregel van een specifiek toewijzingsmodel houdt, wordt een pop-up gemaakt met het totale aantal conversies voor die datum.

![&#x200B; trends &#x200B;](./images/insights/weekly-trends.png)

## Uitsplitsing naar kanaal

De **[!UICONTROL Breakdown by channel]** -kaart wordt gebruikt om het totale aantal conversies met betrekking tot elk kanaal te bepalen. Deze kaart kan worden gebruikt om beslissingen te nemen over de doeltreffendheid van elk kanaal en het rendement van investeringen.

Als u de ovalen rechtsboven op de **[!UICONTROL Breakdown by channel]** -kaart selecteert, wordt een vervolgkeuzelijst geopend waarmee u gegevens kunt vullen op basis van aanraakpunten.

![&#x200B; verdelingskanaal &#x200B;](./images/insights/channel-breakdown.png)

## Bovenste campagnes

De kaart van **[!UICONTROL Top campaigns]** toont een overzicht van uw campagnes en hoe de campagne in elk kanaal uitvoert. Deze kaart kan u helpen uw team te informeren over de doeltreffendheid van een specifieke campagne voor een bepaald kanaal en kan inzichten verstrekken zoals welke campagnes u verder in zou moeten investeren.

![&#x200B; hoogste campagnes &#x200B;](./images/insights/top-campaigns.png)

## Uitsplitsing naar positie aanraakpunt

Als u de tab **[!UICONTROL Path Analysis]** selecteert, worden de **[!UICONTROL Breakdown by touchpoint position]** - en **[!UICONTROL Top conversion paths]** -grafieken geladen.

De grafiek van **[!UICONTROL Breakdown by touchpoint position]** is een uitsplitsing van toegewezen omzettingen door positie van het aanraakpunt vergeleken over alle omzettingspaden. Deze grafiek helpt u begrijpen welke aanraakpunten effectiever zijn in verschillende stadia van het conversiepad. De stadia zijn starter, speler, en dichter.

- **Aanzet:** wijst op het aanraakpunt de eerste aanraking in een omzettingsweg was.
- **Speler:** wijst op het aanraakpunt niet de eerste of laatste aanraking was die tot een omzetting leidt.
- **dichtbij:** wijst op het aanraakpunt de laatste aanraking vóór een omzetting was.

>[!NOTE]
>
>De som van de procentuele bijdrage voor een toewijzingsmodel voor alle aanraakpunten en posities moet gelijk zijn aan 100.

![&#x200B; gebruiker-weg onderbreking touchpoint &#x200B;](./images/insights/user-paths.png)

## Bovenste omzetpaden

In de grafiek van **[!UICONTROL Top conversion paths]** worden de beïnvloede en algoritmische scores op de bovenste omzettingspaden in de geselecteerde gebieden weergegeven. In deze grafiek kunt u visualiseren wat aanraakpunten bijdragen aan conversies en wat de attributiescore is voor elk aanraakpunt. U kunt deze informatie gebruiken om de meest frequente paden in een bepaald gebied weer te geven en te zien of er patronen ontstaan tussen de verschillende sets aanraakpunten.

![&#x200B; gemeenschappelijkste gebruikerspaden &#x200B;](./images/insights/Touchpoint-paths.png)

## Efficiëntie van aanraakpunten

Als u het tabblad **[!UICONTROL Touchpoint Effectiveness]** selecteert, wordt de **[!UICONTROL Touchpoint effectiveness]** -kaart geladen. Deze kaart gebruikt de verspreiding van gegevens van Attribution AI aan vertoningsinformatie voor elk aanraakpunt. De gegevens voor deze tabel worden alleen gegenereerd voor specifieke tijdsperioden die worden aangegeven door de datum **[!UICONTROL As of]** rechtsboven op de kaart.

![&#x200B; selecteert de doeltreffendheid van touchpoint &#x200B;](./images/insights/Touchpoint-effectiveness.png)

U kunt de kaartgegevens van **[!UICONTROL Touchpoint effectiveness]** gebruiken om te begrijpen hoe een aanraakpunt bijdraagt aan een conversie. U kunt ook zien hoe effectief elk aanraakpunt is met de volgende prestatiewaarden:

**Aanraakten Wegen**: Deze metrische vertoningen een percentage wegen die/geen omzetting voor touchpoint bereiken. U zult hogere toegeschreven omzettingen zien als de verhouding van wegen (percentage) die omzetting tot wegen bereiken die geen omzetting bereiken hoog is.

![&#x200B; Gevonden Wegen metrisch &#x200B;](./images/insights/Touchpoint-metrics.png)

**de maatregel van de Efficiëntie**: Deze metrische vertoningensterren op een schaal van één tot vijf. De schaal geeft het relatieve belang aan van een aanraakpunt voor conversie.

>[!NOTE]
>
>Een hoger aanraakpuntvolume garandeert geen hogere efficiëntiemaatregel.

**Totaal volume**: Het totale aantal tijden een touchpoint werd aangeraakt door een gebruiker. Dit zijn inclusief aanraakpunten die worden weergegeven op een pad dat conversie mogelijk maakt, en paden die geen conversie tot gevolg hebben.

## Volgende stappen

Wanneer u de gegevens hebt gefilterd en de juiste gegevens hebt kunnen weergeven, hebt u de mogelijkheid om toegang te krijgen tot de scores. Voor een diepgaande gids op hoe te om tot uw scores toegang te hebben, bezoek de [&#x200B; toegangsscores in het attribuut AI &#x200B;](./download-scores.md) leerprogramma. Bovendien, kunt u uw summiere gegevens zoals die in [&#x200B; worden vermeld meer acties &#x200B;](#more-actions) ook downloaden. Als u Samenvattingsgegevens downloaden selecteert, worden de samengevoegde gegevens gedownload op datums.

## Aanvullende bronnen

De volgende video is ontworpen om u te helpen bij het leren hoe u de pagina Kenmerken AI-inzichten kunt gebruiken om inzicht te krijgen in de ROI van marketingkanalen en campagnes.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
