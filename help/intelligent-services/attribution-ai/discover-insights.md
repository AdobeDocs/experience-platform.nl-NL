---
keywords: Experience Platform;insights;attribution ai;popular topics
solution: Experience Platform
title: Inzichten in Attributie AI opzoeken
topic: Attribution AI insights
translation-type: tm+mt
source-git-commit: 0ea96de956adb5a6c5286433a547772118c43aee
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---


# Inzichten in Attributie AI opzoeken

Attribution AI service instances verschaffen inzichten die kunnen worden gebruikt om marketingbeslissingen met betrekking tot marketingprestaties en rendement op investeringen te nemen en te meten. Het selecteren van een de dienstinstantie verstrekt visualisaties en filters om u bij het begrijpen van het effect van elke klanteninteractie in elke fase van de klantenreis te helpen.

Dit document dient als richtlijn voor het communiceren met de inzichten van serviceversies in de gebruikersinterface van Adobe Intelligent Services.

## Aan de slag

Om inzichten voor Attribution AI te gebruiken, moet u een de dienstinstantie hebben met een succesvolle looppasstatus beschikbaar. Ga naar de handleiding voor de [gebruikersinterface](./user-guide.md)van Attribution AI om een nieuwe service-instantie te maken. Als u onlangs een de dienstinstantie creeerde en het nog opleidt en het scoring, gelieve 24 uren voor het te beëindigen loopt.

## Overzicht van inzichten in servicevergaderingen

Klik in de [!DNL Adobe Experience Platform] gebruikersinterface op **Services** in de linkernavigatie. De browser *Services* wordt weergegeven en beschikbaar gesteld Adobe Intelligent Services. Klik in de container voor Kenmerken AI op **Openen**.

![Toegang tot uw exemplaar](./images/insights/open_Attribution_ai.png)

De servicepagina Kenmerk AI wordt weergegeven. Deze pagina bevat een overzicht van de service-instanties van Attribution AI en geeft informatie over deze instanties, zoals de naam van de instantie, conversiegebeurtenissen, hoe vaak de instantie wordt uitgevoerd en de status van de laatste update. Klik op de naam van een service-instantie om te beginnen.

>[!NOTE] Alleen serviceversies die een scoring hebben voltooid, kunnen worden geselecteerd.

![Instantie maken](./images/insights/select-service-instance.png)

Vervolgens wordt de pagina met inzichten voor die service-instantie weergegeven, waarin u een aantal visualisaties en filters hebt om met uw gegevens te werken. De visualisaties en filters worden in deze handleiding gedetailleerder uitgelegd.

![instellingspagina](./images/insights/landing-page.png)

### Details van serviceinstantie

Als u meer details voor een service-instantie wilt weergeven, klikt u rechtsboven op Meer **** tonen.

![meer weergeven](./images/insights/show-more.png)

Er wordt een gedetailleerde lijst weergegeven. Meer informatie over de vermelde eigenschappen vindt u in de gebruikershandleiding [van](./user-guide.md)Attribution AI.

![details tonen](./images/insights/advanced-details.png)

### Een instantie bewerken

Als u een instantie wilt bewerken, klikt u op *Bewerken* in de navigatie rechtsboven.
![Klik op de knop Bewerken](./images/insights/edit-button.png)

Het dialoogvenster Bewerken wordt geopend, waarin u de beschrijving en de scores van de instantie kunt bewerken. Klik in de rechterbenedenhoek op *Bewerken* om de wijzigingen te bevestigen en het dialoogvenster te sluiten.

![popup bewerken](./images/insights/edit-popover.png)

### Meer handelingen {#more-actions}

De knop *Meer handelingen* bevindt zich in de navigatie rechtsboven naast *Bewerken*. Klik op **Meer handelingen** om een vervolgkeuzelijst te openen waarin u een van de volgende bewerkingen kunt selecteren:

- **Verwijderen**: Hiermee wordt de instantie verwijderd.
- **Samenvattingsgegevens** downloaden: Hiermee downloadt u een CSV-bestand met de overzichtsgegevens.
- **Toegangscores**: Als u op *Toegangscores* klikt, wordt u omgeleid naar de [toegangscores voor de Attribution AI-zelfstudie](./download-scores.md).
- **Runtimegeschiedenis** weergeven: Er wordt een pop-upmenu weergegeven met een lijst van alle scoring-reeksen die aan de service-instantie zijn gekoppeld.

![meer acties](./images/insights/more-actions.png)

## Gegevens filteren

Met Attribution AI-inzichten kunt u uw gegevens filteren en de UI-visuele elementen automatisch bijwerken op basis van de geselecteerde filters.

>[!NOTE] Standaard is elk filter ingesteld op Alles, behalve het filter *Attributiemodel* , dat is ingesteld op &quot;Incrementele en Influenced toewijzingsconversies&quot;.

### Conversion-gebeurtenis

Wanneer u een nieuwe instantie maakt in Attribution AI, is een van de vereiste velden &#39;Conversiegebeurtenissen&#39;. Conversiegebeurtenissen zijn bedrijfsdoelstellingen die het effect van marketing activiteiten, zoals, e-commerceorders, in-store aankopen, en websitebezoeken identificeren.

Vanuit de instantie kunt u met het vervolgkeuzemenu *Conversiegebeurtenissen* een van de gebeurtenissen selecteren die voor de instantie zijn gedefinieerd om uw gegevens te filteren. Als u specifieke gebeurtenissen selecteert, worden de gebruikersinterfacevisualisaties gewijzigd en worden conversies die bij die gebeurtenissen horen alleen gevuld.

![conversiegebeurtenis](./images/insights/conversion-event.png)

### Attributiemodel

Als u op het *kenmerkingsmodel* klikt, wordt een vervolgkeuzelijst geopend met alle verschillende beschikbare attributiemodellen. U kunt meerdere modellen selecteren om de resultaten te vergelijken. Ga voor meer informatie over de verschillende attributiemodellen en hoe ze werken naar het [Attribution AI](./overview.md) -overzicht dat een tabel bevat met informatie over elk model.

![toewijzingsmodel](./images/insights/attribution-model.png)

### Product

Met het filter *Product* kunt u een keuze maken uit alle producten die u aanvankelijk hebt opgenomen in het ontwerp van uw instantie. Klik op het vervolgkeuzemenu en gebruik de zoekfunctie om snel alle producten te selecteren die u wilt vergelijken.

![productfilter](./images/insights/product-filter.png)

### Geografie

Met het filter *Geografie* worden landcodes gevuld op basis van regionale modellen. Afhankelijk van uw gegevens kan dit filter al dan niet aanwezig zijn.

>[!NOTE] Landcodes zijn twee tekens lang. Een volledige lijst vindt u hier in [ISO 3166-1 alpha-2](https://datahub.io/core/country-list).

### Regio

>[!NOTE] Dit filter is alleen aanwezig als u tijdens het maken van uw serviceversie de optionele stap [op regio gebaseerde modellering](./user-guide.md#region-based-modeling-optional) in de handleiding voor de gebruikersinterface van Attribution AI hebt uitgevoerd.

Met dit filter kunt u alle gebieden selecteren die u hebt ingesteld in het proces voor het maken van instanties.

### Kanaal

Klik op het filter *Kanaal* om een vervolgkeuzelijst weer te geven met al uw beschikbare marketingkanalen. U kunt meerdere kanalen selecteren om ze te vergelijken.

![Kanaal](./images/insights/channel.png)

### Datumbereik

Klik op het kalenderpictogram om de popover van het datumbereik te openen. De begin- en einddatum van de conversiegebeurtenis bepalen hoeveel gegevens worden ingevuld in de gebruikersinterface. U kunt ervoor kiezen het datumbereik te beperken of uit te breiden om de hoeveelheid gegevens die is ingevuld, scherper te maken of uit te breiden.

![datumbereik](./images/insights/display-date-range.png)

## Overzicht van uw gegevens

De *kaart van het Overzicht* toont uw totale omzettingen door attributiemodel. Het totale aantal verandert op basis van hoe specifiek u de zoekopdracht maakt met de filters die eerder in dit document zijn beschreven. Als u meer modellen selecteert, worden extra cirkels aan het overzicht toegevoegd, elk met een eigen kleur die overeenkomt met de legenda.

![overzicht](./images/insights/Overview.png)

## Wekelijkse trends

De *kaart voor wekelijkse trends* splitst uw totale conversie in op het datumbereik dat u instelt tijdens het filterproces.

![trends](./images/insights/weekly-trends.png)

Als u klikt op de ellipsen in de rechterbovenhoek van de *Wekelijkse trends* kaart, wordt een vervolgkeuzelijst weergegeven waarmee u dagelijkse, wekelijkse of maandelijkse trends kunt selecteren.

Als u de muis boven de gegevensregel van een specifiek toewijzingsmodel houdt, wordt een pop-up gemaakt met het totale aantal conversies voor die datum.

![tendensen aanwijzen](./images/insights/weekly-trend-hover.png)

## Uitsplitsing naar kanaal

De *uitsplitsing per kanaal* wordt gebruikt om het totale aantal omzettingen met betrekking tot elk kanaal te bepalen. Deze kaart kan worden gebruikt om beslissingen te nemen over de doeltreffendheid van elk kanaal en het rendement van investeringen.

![uitsplitsingskanaal](./images/insights/channel-breakdown.png)

Als u klikt op de ellipsen rechtsboven in de kaart *Onderbreken via kanaal* , wordt een vervolgkeuzelijst geopend waarin u gegevens kunt vullen op basis van aanraakpunten.

![aanraakpunten](./images/insights/breakdown-by-touchpoints.png)

## Beste campagnes

De *bovenste campagnerekaart* geeft een overzicht van uw campagnes en hoe de campagne in elk kanaal presteert. Deze kaart kan uw team helpen de doeltreffendheid van een specifieke campagne voor een bepaald kanaal te informeren en inzicht te geven in waar te om verder te investeren.

![topcampagnes](./images/insights/top-campaigns.png)

## Volgende stappen

Wanneer u de gegevens hebt gefilterd en de juiste gegevens hebt kunnen weergeven, hebt u de mogelijkheid om toegang te krijgen tot de scores. Ga naar de [toegangsscores in de zelfstudie Attribution AI](./download-scores.md) voor een uitgebreide handleiding over het openen van uw scores. Bovendien kunt u de samenvattingsgegevens ook downloaden, zoals aangegeven in [meer acties](#more-actions). Als u Samenvattingsgegevens downloaden selecteert, worden de samengevoegde gegevens gedownload op datums.

## Aanvullende bronnen

De volgende video is ontworpen om u te helpen bij het leren hoe u de pagina Kenmerken AI-inzichten kunt gebruiken om inzicht te krijgen in de ROI van marketingkanalen en campagnes.

>[!VIDEO](https://video.tv.adobe.com/v/32669?learn=on&quality=12)