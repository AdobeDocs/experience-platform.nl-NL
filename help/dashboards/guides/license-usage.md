---
keywords: Experience Platform;gebruikersinterface;UI;aanpassing;licentiegebruiksdashboard;dashboard;licentiegebruik;machtiging;consumptie
title: Handleiding voor het gebruiksdashboard voor licenties
description: Adobe Experience Platform biedt een dashboard waarmee u belangrijke informatie kunt bekijken over het gebruik van licenties voor uw organisatie.
type: Documentation
exl-id: 143d16bb-7dc3-47ab-9b93-9c16683b9f3f
source-git-commit: fc0cb582d74f5ab52410991f65aa14ba05df3f97
workflow-type: tm+mt
source-wordcount: '1933'
ht-degree: 0%

---

# Het gebruiksdashboard voor licenties {#license-usage-dashboard}

>[!CONTEXTUALHELP]
>id="platform_dashboards_licenseUsage"
>title="Het gebruiksdashboard voor licenties"
>abstract="Het dashboard Licentiegebruik biedt inzicht in de Adobe Experience Platform-producten die u hebt aangeschaft. In het dashboardoverzicht worden de belangrijkste maatstaven voor uw producten weergegeven, inclusief uw gebruik voor elk van de primaire meetgegevens en het bedrag van de gecontracteerde licentie. In de werkruimte Details wordt een uitsplitsing weergegeven van de meetgegevens voor elk product binnen specifieke sandboxen."

U kunt belangrijke informatie over het gebruik van uw licentie via de Adobe Experience Platform bekijken [!UICONTROL License usage] dashboard. De hier weergegeven informatie wordt vastgelegd tijdens een dagelijkse momentopname van uw platforminstantie.

De gebruiksrapporten van de vergunning verstrekken een hoge graad van granulariteit over uw metriek van het vergunningsgebruik. Het dashboard biedt gebruiksmaatstaven voor elk aangeschaft product, het geconsolideerde gebruik van metriek in alle productie- of ontwikkelingssandboxen en de gebruikstemetriek van een specifieke sandbox. De volgende Experience Platforms kunnen met gebruiksmetriek worden gevolgd: Real-time Customer Data Platform, Adobe Journey Optimizer, en Customer Journey Analytics.

Deze gids schetst hoe te om tot en met het dashboard van het vergunningsgebruik in UI toegang te hebben en te werken en verstrekt meer informatie betreffende de visualisaties die in het dashboard worden getoond.

Voor een algemeen overzicht van de interface van het platform raadpleegt u de [UI-hulplijn Experience Platform](../../landing/ui-guide.md).

## [!UICONTROL License usage] dashboardgegevens

De [!UICONTROL License usage] op het dashboard wordt een lijst weergegeven met alle Experience Platforms die u hebt aangeschaft. In deze lijst vindt u een momentopname van de licentiegegevens van uw organisatie voor Experience Platform in elke bijbehorende sandbox.

De gegevens in dit dashboard worden precies zo weergegeven als op het specifieke tijdstip waarop de momentopname is gemaakt. Met andere woorden, de momentopname is geen benadering of voorbeeld van de gegevens en het dashboard wordt niet in real-time bijgewerkt.

>[!NOTE]
>
>Wijzigingen of updates die zijn aangebracht in de gegevens nadat de momentopname is gemaakt, worden pas in het dashboard weergegeven als de volgende momentopname is gemaakt.

## Het dashboard voor licentiegebruik verkennen {#explore}

Als u naar het dashboard voor licentiegebruik in de interface van het platform wilt navigeren, selecteert u **[!UICONTROL License usage]** in het linkerspoor. De [!UICONTROL Overview] wordt geopend, met daarin een lijst met beschikbare producten.

>[!NOTE]
>
>Het dashboard voor licentiegebruik is niet standaard ingeschakeld. Gebruikers moeten de machtiging &#39;Dashboard voor licentiegebruik weergeven&#39; hebben om het dashboard te kunnen weergeven. Raadpleeg voor meer informatie over het verlenen van toegangsmachtigingen voor het weergeven van het dashboard voor het gebruik van licenties de [Handleiding voor dashboardmachtigingen](../permissions.md).

![Het tabblad Overzicht van het dashboard voor licentiegebruik, met Licentiegebruik gemarkeerd in de linkernavigatiebalk.](../images/license-usage/dashboard-overview.png)

## [!UICONTROL Overview] tab {#overview-tab}

Op dit dashboard worden al uw Adobe Experience Platform-producten met licentie, inclusief invoegtoepassingen, weergegeven in een tabelindeling. De tabel bevat belangrijke informatie over het gebruik van uw licentie voor al uw beschikbare profielen.

| Kolomnaam | Beschrijving |
|---|---|
| **[!UICONTROL Product]** | De oplossing van de Adobe die door uw organisatie wordt vergunning gegeven. |
| **[!UICONTROL Primary Metric]** | De primaire metrisch die voor het volgen binnen voor dat product wordt gebruikt. |
| **[!UICONTROL License Amount]** | De gecontracteerde waarde voor het maximale bedrag van de primaire metrische waarde zoals overeengekomen in uw productlicentieovereenkomst. |
| **[!UICONTROL Usage]** | De hoeveelheid primaire metrisch die wordt gebruikt. Deze waarde geeft het totale gebruik van die metrische waarde voor alle sandboxen aan, productie of ontwikkeling. |
| **[!UICONTROL Usage %]** | Het percentage van de primaire metrische waarde dat wordt gebruikt op basis van uw licentiehoeveelheid. |

>[!NOTE]
>
>Toevoegingen aan de [!UICONTROL License Amount] als gevolg van invoegtoepassingen worden toegevoegd boven op het tabblad [!UICONTROL License Amount] voor basisproducten zoals Real-time Customer Data Platform, Adobe Journey Optimizer en Customer Journey Analytics. Het gebruik van dat gelicentieerde bedrag (na de toe:voegen-ons) wordt door de basisproducten gevolgd. Als u bijvoorbeeld één verpakking met vijf sandboxen koopt, wordt de hoeveelheid van vijf toegevoegd aan die van het basisproduct. In dit geval wordt met de invoegtoepassing een [!UICONTROL License Amount] van één, en het gebruik voor die toe:voegen-op is &quot;leeg&quot;aangezien het gebruik door het basisproduct wordt gevolgd.

De lijst wijst op primaire metrisch voor elk product, aangezien elk product talrijke metriek kan volgen.

## [!UICONTROL Summary] tab {#summary-tab}

Als u meer cijfers en gedetailleerd inzicht in het gebruik van uw productlicentie wilt bekijken, selecteert u een productnaam in de lijst. De [!UICONTROL Summary] wordt weergegeven voor dat product. Alle beschikbare metriek worden weergegeven op het tabblad [!UICONTROL Summary] tab. De beschikbare maatstaven zijn afhankelijk van het product met licentie. Deze weergave biedt **een geconsolideerde weergave van alle metriek in alle productie- of ontwikkelingssandboxen**. Hetzelfde analyseniveau geldt voor zowel productie- als ontwikkelingssandboxen.

![De summiere mening van een Product van het Platform dat alle beschikbare metriek voor dat product toont.](../images/license-usage/summary-tab.png)

Op het tabblad Overzicht bevat de tabel de [!UICONTROL Metric] kolom. Deze beschrijvingen die leesbaar zijn voor mensen, geven alle metriek aan die voor dat type sandbox wordt gebruikt.

### Een sandbox selecteren {#select-sandbox}

Als u de weergave wilt wijzigen tussen de typen productie- en ontwikkelingssandbox, selecteert u [!UICONTROL Production sandboxes] of [!UICONTROL Development sandboxes]. Het geselecteerde type sandbox wordt aangegeven door het keuzerondje naast de naam van de sandbox.

Consumptierapporten voor sandboxen zijn cumulatief voor alle sandboxen van hetzelfde type. Met andere woorden: selecteren [!UICONTROL Production] of [!UICONTROL Development] verstrekt verbruiksrapporten voor alle productie of ontwikkelingszandbakken, respectievelijk.

![De summiere mening van een Product van het Platform met de zanddozen van de Productie en van de Ontwikkeling benadrukte.](../images/license-usage/summary-tab-sandboxes.png)

>[!WARNING]
>
>Toestemming om het dashboard voor het gebruiksbewijs van licenties weer te geven, moet worden opgegeven op sandboxniveau. Voeg machtigingen toe aan elke afzonderlijke sandbox om deze in het dashboard weer te geven. Deze beperking wordt in een toekomstige release opgelost. Ondertussen is de volgende oplossing beschikbaar:
>
>1. Maak een productprofiel in de Adobe Admin Console.
>2. Voeg onder Machtiging in de categorie Sandbox alle sandboxen toe die u wilt weergeven in het dashboard voor licentiegebruik.
>3. Voeg onder de categorie Machtiging voor dashboard van gebruiker de machtiging &#39;Licentiegebruiksdashboard weergeven&#39; toe.

## De [!UICONTROL Details] tab {#details-tab}

Zie **een bepaald gebruik metrisch van een specifieke zandbak**, navigeert u naar de [!UICONTROL Details] tab. De [!UICONTROL Details] worden alle beschikbare sandboxen weergegeven in de sandboxen Productie of Ontwikkeling.

![Het tabblad Details van het gebruiksdashboard voor licenties.](../images/license-usage/details-tab.png)

In deze weergave kunt u ![Het pictogram Inspecteren.](../images/license-usage/inspect-icon.png) naast de naam van een sandbox om de visualisatie voor die metrische waarde weer te geven. Er wordt een dialoogvenster geopend met een visualisatie voor die metrische waarde.

### Visualisaties {#visualizations}

Elke visualisatiewidget bevat de volgende aspecten:

- Een lijngrafiek die de metrische wijziging in de tijd volgt
- Een sleutel voor de lijngrafiek
- De naam van de sandbox
- Een vervolgkeuzemenu voor het aanpassen van de tijdsperiode voor de lijngrafiek

De lijngrafieken vergelijken de gebruiksaantallen voor uw organisatie met het totaal beschikbaar met de vergunning van uw organisatie en verstrekken een percentage van totaal gebruik.

![De visualisatie van een metrische waarde.](../images/license-usage/visualization.png)

De terugkijkperiode van analyse kan van het dropdown menu worden aangepast. De standaardwaarde van de laatste 30 dagen

Als u een datumbereik wilt selecteren, selecteert u met de vervolgkeuzelijst voor het datumbereik de periode die u in het dashboard wilt weergeven. Er zijn meerdere opties beschikbaar, waaronder de standaardwaarde van de laatste 30 dagen.

![Het dialoogvenster voor visualisatie met de vervolgkeuzelijst voor datumbereik gemarkeerd.](../images/license-usage/date-range.png)

U kunt ook **[!UICONTROL Custom date]** om de periode te kiezen die wordt getoond.

![Het tabblad Overzicht van het dashboard voor licentiegebruik met de aangepaste datumbereikopties gemarkeerd.](../images/license-usage/custom-date-range.png)

## Beschikbare cijfers {#available-metrics}

Het dashboard van het vergunningsgebruik rapporteert over verscheidene unieke metriek die op veelvoudige producten in de organisatie van toepassing zijn. De beschikbare meetwaarden zijn:

| Metrisch | Beschrijving |
|---|---|
| [!UICONTROL Audience Activation Size] | De totale grootte van profielen die in een jaar op een op een bestand gebaseerd doel zijn geactiveerd. Opmerking: hieronder vallen geen profielen die via streamingdoelen worden verzonden. |
| [!UICONTROL Addressable Audience] | De som van de rechten van uw zakelijke publiek en de rechten van het consumentenpubliek. Een publiek voor de consument wordt gedefinieerd als het aantal personenprofielen dat op de verkooporder als &quot;Consumentenpubliek&quot; wordt aangeduid. Een zakelijk publiek wordt gedefinieerd als het aantal bedrijfspersoonprofielen dat als &quot;BedrijfsPubliek&quot;op de verkooporde wordt geïdentificeerd. |
| [!UICONTROL Adhoc Query Service Users Packs] | Een add-on om uw geautoriseerde machtiging voor gelijktijdige gebruikers van Query Service te verhogen met vijf extra gelijktijdige gebruikers van Query Service en één extra query tegelijk voor ad-hocquery per pakket. Er kan een licentie worden verleend voor meerdere extra Ad hoc Query User-pakketten. |
| [!UICONTROL Average profile richness] | De som van alle productiegegevens die binnen de dienst van het Profiel van de Hub op om het even welk ogenblik worden opgeslagen, gedeeld door vijf keer het aantal gemachtigde bedrijfspersoonprofielen. [!UICONTROL Average profile richness] is een gedeelde functie. |
| [!UICONTROL CJA Rows Available] | De dagelijkse gemiddelde rijen van gegevens beschikbaar voor analyse binnen Customer Journey Analytics. |
| [!UICONTROL Computed Attributes] | Het totale aantal geaggregeerde gedragsgegevens van het profiel. Geaggregeerde gedragsgegevens voor profielen zijn gebaseerd op ervaringsgebeurtenissen die worden omgezet in een profielkenmerk en kunnen worden opgenomen in een persoonprofiel of bedrijfspersoonprofiel. |
| [!UICONTROL Consumer Audience] | Het aantal personenprofielen dat op de verkooporder als &quot;Consumer Audience&quot; is geïdentificeerd. |
| [!UICONTROL Data Export Size] | De hoeveelheid gegevens die via gegevenssetactivering in een jaar wordt verzonden. |
| [!UICONTROL Data Exports] | De totale omvang van gegevenssets die (direct of indirect) naar een niet-Adobe oplossing in een jaar kunnen worden uitgevoerd. |
| [!UICONTROL Data Lake Storage] | De hoeveelheid die in Adobe Experience Platform wordt gebruikt voor de opslag van analysegegevens. |
| [!UICONTROL Engageable Audience] | Deze maatstaf verwijst naar het publiek van controleerbare profielen. Een aanspreekbaar profiel is een record met informatie die een individu vertegenwoordigt en wordt weergegeven in de profielservice. Deze records zijn profielen die u in de afgelopen 12 maanden hebt proberen te gebruiken voor het schrijven, beslissen, leveren, experimenteren of orchestreren van Journey Optimizer. |
| [!UICONTROL Look-alike Audiences] | Het aantal doelgroepen dat wordt gegenereerd door een bestaand publiek voor consumenten te modelleren om te bepalen welke personenprofielen vergelijkbaar zijn met het bestaande publiek voor consumenten. |
| [!UICONTROL Number of AMM Models] | Een telling van het machine het leren model (ingebouwde Adobe Mix Modeler) dat wordt gebruikt om een gespecificeerd resultaat te meten en/of te voorspellen die op uw investeringen wordt gebaseerd. |
| [!UICONTROL Number of Sandboxes] | Het aantal logische scheidingen binnen uw instantie van om het even welke Adobe On-demand Dienst die tot Adobe Experience Platform toegang heeft isolerend gegevens en verrichtingen. |
| [!UICONTROL Profile Richness No of Packs] | Een verhoging van uw geautoriseerde Gemiddelde rijsheid van het Profiel met 25 KB per profiel voor elk Extra rijvaardigheidspak van het Profiel. |
| [!UICONTROL Query Service Compute Hours] | Een maatregel van de hoeveelheid tijd die door de motoren van de Dienst van de Vraag wordt genomen om, gegevens terug in het gegevensmeer te lezen te verwerken en te schrijven wanneer een partijvraag wordt uitgevoerd. |
| [!UICONTROL Streaming Segmentation No of Packs] | De pakketten werken segmentlidmaatschap voor een persoonprofiel bij aangezien de nieuwe gegevens de Dienst van de Segmentatie door een het stromen stroom ingaan. Het lidmaatschap van een segment wordt beoordeeld op basis van de kenmerken van het huidige personenprofiel en de waarde van de huidige gebeurtenis, zonder rekening te houden met het historische gedrag. Streaming segmentatie is een gedeelde functie. |

<!-- |  [!UICONTROL Sandbox No of Packs] |  A logical separation within your instance of any Adobe On-demand Service that accesses Adobe Experience Platform isolating data and operations | -->

De beschikbaarheid van deze cijfers en de specifieke definitie van elk van deze cijfers variëren afhankelijk van de licenties die uw organisatie heeft aangeschaft. Raadpleeg de desbetreffende documentatie bij de productbeschrijving voor gedetailleerde definities van elke metrische waarde:

| Licentie | Productbeschrijving |
|---|---|
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD LITE</li><li>ADOBE EXPERIENCE PLATFORM:OD STANDARD</li><li>ADOBE EXPERIENCE PLATFORM:OD HEAVY</li></ul> | [Adobe Experience Platform](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform.html) |
| <ul><li>ADOBE EXPERIENCE PLATFORM:OD</li></ul> | [Experience Platform, toepassingsservices en intelligente services](https://helpx.adobe.com/legal/product-descriptions/exp-platform-app-svcs.html) |
| <ul><li>RT-KLANTENGEGEVENSPLATFORM:OD</li><li>RT KLANTENGEGEVENSPLATFORM:OD PRFL NAAR 10M</li><li>RT KLANTENGEGEVENSPLATFORM:OD PRFL NAAR 50M</li></ul> | [Adobe Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) |
| <ul><li>AEP:OD ACTIVATION</li><li>AEP:OD ACTIVATION PRFL NAAR 10M</li><li>AEP:OD ACTIVATION PRFL TOT 50M</li></ul> | [Adobe Experience Platform-activering](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform0.html) |
| <ul><li>AEP:OD INTELLIGENCE</li></ul> | [Adobe Experience Platform Intelligence](https://helpx.adobe.com/legal/product-descriptions/adobe-experience-platform-intelligence---product-description.html) |
| <ul><li>JOURNEY OPTIMIZER SELECT:OD</li><li>JOURNEY OPTIMIZER PRIME:OD</li><li>JOURNEY OPTIMIZER ULTIMATE:OD</li><li>UNP AJO PRIME STARTER:OD</li><li>UNP AJO ULTIMATE STARTER:OD</li><li>UNP Real-Time CDP:OD PROFILE ORCHESTRATION</li></ul> | [Adobe Journey Optimizer](https://helpx.adobe.com/legal/product-descriptions/adobe-journey-optimizer.html) |

>[!WARNING]
>
>Het dashboard voor het gebruiksgemak rapporteert alleen over de nieuwste licentie die voor uw organisatie is ingericht. Als de meest recente licentie die voor uw organisatie is ingesteld, niet in de bovenstaande tabel wordt weergegeven, wordt het licentiegebruiksdashboard mogelijk niet correct weergegeven. Ondersteuning voor extra licenties en meerdere licenties in één organisatie is gepland voor een toekomstige release.

## Volgende stappen

Nadat u dit document hebt gelezen, kunt u het dashboard voor het licentiegebruik vinden en de gebruiksgegevens voor elk aangeschaft product, voor alle productie- of ontwikkelingssandboxen en voor een specifieke sandbox bekijken. Meer informatie over de beschikbare metriek voor uw organisatie vindt u op basis van de licentie die uw organisatie heeft aangeschaft.

Als u meer wilt weten over andere functies die beschikbaar zijn in de gebruikersinterface van het Experience Platform, raadpleegt u de [Handleiding voor platforminterface](../../landing/ui-guide.md).
