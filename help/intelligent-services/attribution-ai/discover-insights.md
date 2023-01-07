---
keywords: Experience Platform;inzichten;attributie ai;populaire onderwerpen;attributie ai inzichten
feature: Attribution AI
title: Inzichten in Attribution AI ontdekken
description: Dit document fungeert als richtlijn voor het communiceren met de inzichten van serviceversies in de gebruikersinterface van Adobe Intelligent Services.
exl-id: 6b8e51e7-1b56-4f4e-94cf-96672b426c88
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '1584'
ht-degree: 0%

---

# Inzichten in Attribution AI ontdekken

De instanties van de dienst van de Attribution AI geven inzicht die kunnen worden gebruikt om bij het maken en het meten van marketing besluiten met betrekking tot marketing prestaties en rendement van investering te helpen. Het selecteren van een de dienstinstantie verstrekt visualisaties en filters om u bij het begrijpen van het effect van elke klanteninteractie in elke fase van de klantenreis te helpen.

Dit document fungeert als richtlijn voor het communiceren met de inzichten van serviceversies in de gebruikersinterface van Adobe Intelligent Services.

## Aan de slag

Om inzichten voor Attribution AI te gebruiken, moet u een de dienstinstantie hebben met een succesvolle beschikbare looppasstatus. Als u een nieuwe service-instantie wilt maken, gaat u naar de [Handleiding voor de gebruikersinterface van Attribution AI](./user-guide.md). Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

## Overzicht van inzichten in servicevergaderingen

In de [!DNL Adobe Experience Platform] UI, selecteer **[!UICONTROL Services]** in de linkernavigatie. De **[!UICONTROL Services]** wordt weergegeven en geeft de beschikbare Adobe Intelligente services weer. Selecteer in de container voor Attribution AI de optie **[!UICONTROL Open]**.

![Toegang tot uw exemplaar](./images/insights/open_Attribution_ai.png)

De de dienstpagina van de Attribution AI verschijnt. Deze pagina bevat een overzicht van de service-instanties van Attribution AI en informatie over deze instanties, zoals de naam van de instantie, conversiegebeurtenissen, hoe vaak de instantie wordt uitgevoerd en de status van de laatste update. Selecteer de naam van een service-instantie om te beginnen.

>[!NOTE]
>
>Alleen serviceversies die een scoring hebben voltooid, kunnen worden geselecteerd.

![Instantie maken](./images/insights/select-service-instance.png)

Vervolgens wordt de pagina met inzichten voor die service-instantie weergegeven, waarin u een aantal visualisaties en filters hebt om met uw gegevens te werken. De visualisaties en filters worden in deze handleiding gedetailleerder uitgelegd.

![instellingspagina](./images/insights/landing-page.png)

### Details van serviceinstantie

Selecteer **[!UICONTROL Show more]** in de rechterbovenhoek.

![meer weergeven](./images/insights/show-more.png)

Er wordt een gedetailleerde lijst weergegeven. Ga voor meer informatie over de eigenschappen die worden vermeld naar [Gebruikershandleiding voor Attribution AI](./user-guide.md).

![details tonen](./images/insights/advanced-details.png)

### Een instantie bewerken

Selecteer **[!UICONTROL Edit]** in de navigatie rechtsboven.
![Klik op de knop Bewerken](./images/insights/edit-button.png)

Het dialoogvenster Bewerken wordt weergegeven. In dit venster kunt u de naam, beschrijving en frequentie van de instantie bewerken. Als de status van de instantie is uitgeschakeld, kan de scorefrequentie niet worden bewerkt. Als u uw wijzigingen wilt bevestigen en het dialoogvenster wilt sluiten, selecteert u **[!UICONTROL Save]** in de rechterbenedenhoek.

![popup bewerken](./images/insights/edit-popover.png)

### Meer handelingen {#more-actions}

De **[!UICONTROL More actions]** bevindt zich in de navigatie rechtsboven naast **[!UICONTROL Edit]**. Selecteren **[!UICONTROL More actions]** Hiermee opent u een vervolgkeuzelijst waarin u een van de volgende bewerkingen kunt selecteren:

- **[!UICONTROL Clone]**: Hiermee wordt de instantie gekloond.
- **[!UICONTROL Delete]**: Hiermee wordt de instantie verwijderd.
- **[!UICONTROL Download summary data]**: Hiermee downloadt u een CSV-bestand met de overzichtsgegevens.
- **[!UICONTROL Access scores]**: Selecteren **[!UICONTROL Access scores]** leidt u om aan [toegangscores voor zelfstudie Attribution AI](./download-scores.md).
- **[!UICONTROL View run history]**: Er wordt een pop-upmenu weergegeven met een lijst van alle scoring-reeksen die aan de service-instantie zijn gekoppeld.

![meer acties](./images/insights/more-actions.png)

## Gegevens filteren

Met Attribution AI-inzichten kunt u uw gegevens filteren en de gebruikersinterface-visuele elementen automatisch bijwerken op basis van de geselecteerde filters.

### Conversion-gebeurtenis

Wanneer u een nieuwe instantie maakt in Attribution AI, is een van de vereiste velden Conversiegebeurtenissen. Conversiegebeurtenissen zijn bedrijfsdoelstellingen die het effect van marketingactiviteiten, zoals e-commerceorders, aankopen in winkel en websitebezoeken, identificeren.

Van binnen de instantie, **[!UICONTROL Conversion events]** kunt u een van de gebeurtenissen selecteren die voor de instantie zijn gedefinieerd om uw gegevens te filteren. Als u specifieke gebeurtenissen selecteert, worden de gebruikersinterfacevisualisaties gewijzigd en worden conversies die bij die gebeurtenissen horen alleen gevuld.

![conversiegebeurtenis](./images/insights/conversion-event.png)

### Attributiemodel

Selecteren **[!UICONTROL Attribution Model]** Hiermee wordt een vervolgkeuzelijst geopend met alle verschillende beschikbare toewijzingsmodellen. U kunt meerdere modellen selecteren om de resultaten te vergelijken. Ga voor meer informatie over de verschillende toewijzingsmodellen en hoe ze werken naar de [Attribution AI](./overview.md) overzicht dat een lijst met informatie over elk model bevat.

![toewijzingsmodel](./images/insights/attribution-model.png)

### Regio

>[!NOTE]
>
>Dit filter is alleen aanwezig als u de optionele stap hebt uitgevoerd [regionale modellering](./user-guide.md#region-based-modeling-optional) in de gebruikersinterfacegids van de Attribution AI wanneer het creëren van uw de dienstinstantie.

Met dit filter kunt u alle gebieden selecteren die u hebt ingesteld in het proces voor het maken van instanties.

### Filters toevoegen

U kunt aanvullende filters toevoegen door de optie **filter** pictogram om het **[!UICONTROL Add filters]** popover. De **[!UICONTROL Add filters]** Met popover kunt u filteren op Kanaal, Geografie, Mediatype en Product. Alleen de toepasselijke filters voor een service-instantie worden gevuld door de pop-over. Als u bijvoorbeeld geen geografische gegevens of een mediatype hebt opgegeven, zijn deze filterkenmerken niet beschikbaar voor uw instantie.

![extra filters](./images/insights/additional-filters.png)

![filterpopup](./images/insights/filter-popover.png)

- **[!UICONTROL Channel]:** Als u het kanaalkenmerk selecteert, kunt u elk van de beschikbare marketingkanalen filteren. U kunt meerdere kanalen selecteren om ze te vergelijken.
- **[!UICONTROL Geography]:** Als u het kenmerk geography selecteert, kunt u landcodes filteren op basis van regionale modellen. Afhankelijk van uw gegevens kan dit filter al dan niet aanwezig zijn. Landcodes zijn twee tekens lang. Zie de volledige landencodelijst [hier](https://datahub.io/core/country-list).
- **[!UICONTROL Media type]:** Als u het kenmerk van het mediatype selecteert, kunt u elk van de gedefinieerde mediatypen filteren.
- **[!UICONTROL Product]:** Als u het kenmerk product selecteert, kunt u filteren op producten die oorspronkelijk zijn opgenomen in het ontwerp van de instantie.

### Datumbereik

Selecteer het kalenderpictogram om de popover van het datumbereik te openen. De begin- en einddatum van de conversiegebeurtenis bepalen hoeveel gegevens worden ingevuld in de gebruikersinterface. U kunt ervoor kiezen het datumbereik te beperken of uit te breiden om de hoeveelheid gegevens die is ingevuld, scherper te maken of uit te breiden.

![datumbereik](./images/insights/display-date-range.png)

## Overzicht van uw gegevens

De **[!UICONTROL Overview]** de kaart toont uw totale omzettingen door attributiemodel. Het totale aantal verandert op basis van hoe specifiek u de zoekopdracht maakt met de filters die eerder in dit document zijn beschreven. Als u meer modellen selecteert, worden extra cirkels aan het overzicht toegevoegd, elk met een eigen kleur die overeenkomt met de legenda.

![-overzicht](./images/insights/Overview.png)

## Wekelijkse trends

De **[!UICONTROL Weekly trends]** De kaart onderbreekt uw totale omzetting door de datumwaaier u tijdens het filtreren proces plaatst.

De ovalen rechtsboven in het dialoogvenster selecteren **Wekelijkse trends** op de kaart wordt een keuzelijst weergegeven waarmee u dagelijkse, wekelijkse of maandelijkse trends kunt selecteren.

Als u de muis boven de gegevensregel van een specifiek toewijzingsmodel houdt, wordt een pop-up gemaakt met het totale aantal conversies voor die datum.

![trends](./images/insights/weekly-trends.png)

## Uitsplitsing naar kanaal

De **[!UICONTROL Breakdown by channel]** kaart wordt gebruikt om het totale aantal omzettingen met betrekking tot elk kanaal te bepalen. Deze kaart kan worden gebruikt om besluiten te nemen over de doeltreffendheid van elk kanaal en het rendement van investeringen.

De ovalen rechtsboven in het dialoogvenster selecteren **[!UICONTROL Breakdown by channel]** -kaart opent een vervolgkeuzelijst waarmee u gegevens kunt vullen op basis van aanraakpunten.

![uitsplitsingskanaal](./images/insights/channel-breakdown.png)

## Beste campagnes

De **[!UICONTROL Top campaigns]** kaart geeft een overzicht van uw campagnes en hoe de campagne in elk kanaal presteert. Deze kaart kan u helpen uw team te informeren over de doeltreffendheid van een specifieke campagne voor een bepaald kanaal en kan inzichten verstrekken zoals welke campagnes u verder in zou moeten investeren.

![topcampagnes](./images/insights/top-campaigns.png)

## Uitsplitsing naar positie aanraakpunt

Het selecteren van **[!UICONTROL Path Analysis]** wordt geladen **[!UICONTROL Breakdown by touchpoint position]** en **[!UICONTROL Top conversion paths]** grafieken.

De **[!UICONTROL Breakdown by touchpoint position]** grafiek is een uitsplitsing van toegerekende omzettingen naar positie van het aanraakpunt in vergelijking met alle omzettingspaden. Deze grafiek helpt u begrijpen welke aanraakpunten effectiever zijn in verschillende stadia van het conversiepad. De stadia zijn starter, speler, en dichter.

- **Starter:** Geeft aan dat het aanraakpunt de eerste aanraking in een conversiepad was.
- **Speler:** Geeft aan dat het aanraakpunt niet het eerste of laatste aanraakpunt was dat tot een conversie heeft geleid.
- **Dichter:** Geeft aan dat het aanraakpunt de laatste aanraking vóór een conversie was.

>!![NOTE]
De som van de procentuele bijdrage voor een toewijzingsmodel voor alle aanraakpunten en posities moet gelijk zijn aan 100.

![gebruikerspad, onderbrekingspunt](./images/insights/user-paths.png)

## Bovenste omzetpaden

De **[!UICONTROL Top conversion paths]** in de grafiek worden de beïnvloede en algoritmische scores weergegeven op de bovenste omzettingspaden in de geselecteerde gebieden. In deze grafiek kunt u visualiseren wat aanraakpunten bijdragen aan conversies en wat de attributiescore is voor elk aanraakpunt. U kunt deze informatie gebruiken om de meest frequente paden in een bepaald gebied weer te geven en te zien of er patronen ontstaan tussen de verschillende sets aanraakpunten.

![Meest gangbare gebruikerspaden](./images/insights/Touchpoint-paths.png)

## Efficiëntie van aanraakpunten

Het selecteren van **[!UICONTROL Touchpoint Effectiveness]** wordt geladen **[!UICONTROL Touchpoint effectiveness]** kaart. Deze kaart gebruikt de verspreiding van gegevens door Attribution AI om informatie voor elk touchpoint te tonen. De gegevens voor deze tabel worden alleen gegenereerd voor specifieke tijdsperiodes zoals aangegeven door de **[!UICONTROL As of]** rechtsboven op de kaart.

![doeltreffendheid aanraakpunt selecteren](./images/insights/Touchpoint-effectiveness.png)

U kunt de **[!UICONTROL Touchpoint effectiveness]** kaartinformatie om te begrijpen hoe een aanraakpunt bijdraagt aan een conversie. U kunt ook zien hoe effectief elk aanraakpunt is met de volgende prestatiemetriek:

**Paden aangeraakt**: Deze metrische vertoningen een percentage wegen die of geen omzetting voor touchpoint bereiken. U zult hogere toegeschreven omzettingen zien als de verhouding van wegen (percentage) die omzetting tot wegen bereiken die geen omzetting bereiken hoog is.

![Paden raakten metrisch](./images/insights/Touchpoint-metrics.png)

**Efficiëntiemaatregel**: Deze metrische vertoningen sterren op een schaal van één tot vijf. De schaal geeft het relatieve belang aan van een aanraakpunt voor het maken van een conversie.

>[!NOTE]
Een hoger aanraakpuntvolume garandeert geen hogere efficiëntiemaatregel.

**Totaal volume**: Het totale aantal keren dat een aanraakpunt is aangeraakt door een gebruiker. Dit zijn inclusief aanraakpunten die worden weergegeven op een pad dat conversie mogelijk maakt, en paden die geen conversie tot gevolg hebben.

## Volgende stappen

Wanneer u de gegevens hebt gefilterd en de juiste gegevens hebt kunnen weergeven, hebt u de mogelijkheid om toegang te krijgen tot de scores. Ga voor een uitgebreide gids over het openen van uw scores naar de [toegangscores in Attribution AI](./download-scores.md) zelfstudie. Bovendien kunt u ook de samenvattingsgegevens downloaden, zoals aangegeven in [meer acties](#more-actions). Als u Samenvattingsgegevens downloaden selecteert, worden de samengevoegde gegevens gedownload op datums.

## Aanvullende bronnen

De volgende video is ontworpen om u te helpen bij het leren hoe u de pagina met Attribution AI-inzichten kunt gebruiken om inzicht te krijgen in het rendement van marketingkanalen en campagnes.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)
