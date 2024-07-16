---
title: Aanpasbare inzichten
description: Leer meer over de gebruiksgevallen, essentiële mogelijkheden en vereiste stappen voor het ontwikkelen van een aanpasbaar dashboard voor inzichten met Data Distiller. Ontdek hoe de aanpasbare mogelijkheden voor inzichten binnen Data Distiller de transparantie kunnen verbeteren en operationele inzichten kunnen verkrijgen in verschillende dimensies, zoals profielen, publiek, campagnes, reizen, rechten en toestemming.
exl-id: f807d0fd-c8ec-42d4-96a0-5ffc5681943b
source-git-commit: bb95e0aa8ee92aee5a2f126d85e78308e652a061
workflow-type: tm+mt
source-wordcount: '941'
ht-degree: 0%

---

# Aanpasbare inzichten

Creeer op maat gebaseerde rapporteringsgegevensmodellen om diepgaande inzichten te halen, strategieën te optimaliseren, en analyses aan te passen aan specifieke bedrijfsbehoeften met Gegevens Distiller Aanpasbare Inzichten. Gebruik de Customizable Insights-mogelijkheid om de transparantie te verbeteren en operationele inzichten van uw Adobe Experience Platform-gegevens te verkrijgen in verschillende dimensies, zoals profielen, publiek, campagnes, reizen, rechten en toestemming. Deze mogelijkheid biedt een veelzijdige, adaptieve oplossing om de rapporteringsgegevensmodellen van uw organisatie aan te passen aan uw specifieke bedrijfsbehoeften.

Om [ visualiseren uw Aanpasbare Inzichten ](../../../dashboards/data-distiller/overview.md) kunt u [ vraag pro wijze ](../../../dashboards/data-distiller/customizable-insights/query-pro-mode.md) gebruiken om complexe analyse met douaneSQL vragen te leiden en uw gegevens in gemakkelijk te interpreteren grafieken om te zetten. Gebruik query pro-modus om op maat gemaakte inzichten en inzichten op uw dashboards te maken en rekening te houden met zowel technisch als niet-technisch publiek door uw inzichten als CSV-bestanden te downloaden.

In dit document worden gebruiksgevallen, essentiële functies en vereiste stappen beschreven voor het ontwikkelen van een aanpasbaar inzichtsdashboard met Data Distiller.

## Vereisten

Deze zelfstudie gebruikt door de gebruiker gedefinieerde dashboards om gegevens van uw aangepaste gegevensmodel in de gebruikersinterface van het platform te visualiseren. Zie [ user-defined dashboards documentatie ](../../../dashboards/user-defined-dashboards.md) om meer over deze eigenschap te leren.

## Aan de slag

Distiller SKU van Gegevens wordt vereist om een model van douanegegevens voor uw rapporteringsinzichten te bouwen en de de gegevensmodellen van Real-Time CDP uit te breiden die de verrijkte gegevens van het Platform houden. Zie het [ verpakken ](../../packaging.md), [ guardrails ](../../guardrails.md#query-accelerated-store), en [ verlenen van vergunningen ](../../data-distiller/license-usage.md) documentatie die op het SKU van Gegevens Distiller betrekking heeft. Als u geen gegevens Distiller SKU hebt, contacteer uw vertegenwoordiger van de klantendienst van de Adobe voor meer informatie.

## Aanpasbare gevallen voor gebruik van inzichten {#use-cases}

Hieronder ziet u veelvoorkomende gebruiksgevallen die effectief kunnen worden aangepakt met Aanpasbare inzichten in Data Distiller.

### Transparantie voor profiel- en publieksgebruik {#usage-transparency}

**Uitdaging:** hoe te om Zeer belangrijke Indicatoren van Prestaties (KPIs) door specifieke criteria zoals bedrijfseenheden, loyaliteitsstatus, of de Waarde van het Leven van de Klant (CLTV) te onderbreken.

**Aanpasbare Oplossing van Inzichten:** Gegevens Distiller laat de uitbreiding van het melden van gegevensmodellen in Adobe Experience Platform toe, die [ de toevoeging van de attributen van het douaneprofiel zoals CLTV ](../../use-cases/customer-lifetime-value.md) of loyaliteitsstatus vergemakkelijkt.

### Constante anomalieën bijhouden {#consent-anomaly-tracking}

**Uitdaging:** hoe te om publieksoverlapping en de rapporten van de groottetrendline op aangepaste toestemmingsattributen voor kanalen zoals e-mail, SMS, en telefoon toe te passen.

**Aanpasbare Oplossing van Inzichten:** het rapporteringsgegevensmodel kan worden uitgebreid om veranderingen in toestemmingsvoorkeur in tijd te volgen. Dit impliceert de bouw van extra feiten en afmetingslijsten aan de voorkeur van de trendtoestemming en het plannen van [ stijgende gegevens verfrissen zich ](../../key-concepts/incremental-load.md).

### Segmentatiestrategie voor het publiek optimaliseren {#optimize-audience-segmentation-strategy}

**Uitdaging:** hoe te om het Leren van de Machine (ML) model-geproduceerde aandrijvingsscores in hun publiekKPI rapporten te integreren.

**Aanpasbare Oplossing van Inzichten:** Distiller van Gegevens staat de opneming van [ bezitsscores van modellen van douaneML ](../../use-cases/propensity-score.md) toe, die de berekening van gezamenlijke scores op het publieksniveau vergemakkelijken. Deze gegevens kunnen vervolgens worden gerapporteerd naast standaard-KPI&#39;s.

### Uitbreiding publiek {#audience-expansion}

**Uitdaging:** hoe te om meer dan enkel profieltellingen in publiek te verwerven overlapt rapporten en extra demografische gegevens of voorkeur te bereiken om de strategieën van de publieksuitbreiding te begeleiden.

**Aanpasbare Oplossing van Inzichten:** door het rapporteringsgegevensmodel uit te breiden, kunnen de gebruikers extra profielattributen opnemen, die het publiek verrijken overlappen rapport met relevante demografische gegevens en voorkeur.

## Belangrijke mogelijkheden voor het genereren van aanpasbare inzichten {#key-capabilities}

In de onderstaande afbeelding worden verschillende essentiële mogelijkheden voor het genereren van aanpasbare inzichten beschreven. Deze mogelijkheden omvatten:

1. **visualisaties van Gegevens:** Incorporating visuele elementen zoals tendensen en staafgrafieken voor een uitvoerige mening van gegevenstrends.
1. **het schrijven van het dashboard:** toelatend de verwezenlijking van douanedashboards die aan specifieke gebruiksgevallen worden aangepast, die een meer gepersonaliseerde en gerichte analytische ervaring verstrekken.
1. **Flexibele SQL gegevensmodellering:** gebruik een veelzijdige SQL benadering van gegevensmodellering die gebruikers toestaat om verschillende datasets naadloos te combineren en te manipuleren, die aanpassingsvermogen, en analytische diepte verbeteren.
1. **Versnelde opslag:** Uitvoerend een versneld opslagmechanisme om samengevoegde inzichten door SQL efficiënt te dienen, die gestroomlijnde en snelle toegang tot waardevolle informatie verzekeren.
1. **connectiviteit van BI:** Faciliterend naadloze integratie met populaire hulpmiddelen van de Business Intelligence (BI), met inbegrip van Power BI, Tableau, Looker, en Apache Superset. Deze connectiviteit zorgt voor compatibiliteit met verschillende BI-omgevingen en biedt gebruikers de flexibiliteit om hun keuze te gebruiken voor diepgaande analyse en rapportage.

![ Visuele vertegenwoordiging van de belangrijkste mogelijkheden van Gegevens Distiller Aanpasbare Inzichten.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Stappen voor het maken van aanpasbare inzichten {#steps-to-create}

Volg de onderstaande stapsgewijze instructies om een aanpasbaar dashboard met inzichten in Data Distiller te ontwikkelen.

1. **Ad hoc vraagexploratie:** begin door ad hoc `SELECT` vragen uit te voeren om ruwe gegevens over het gegevenshoeveelheid te onderzoeken. Hierdoor kan ter plekke een verkennende gegevensanalyse worden uitgevoerd om gegevens te experimenteren, en worden gegevens gevalideerd wanneer de resultaten van de query&#39;s niet in het datumpeer zijn opgeslagen.
1. **het vraaggebruik van de Partij van de Partij:** de partijvragen van het Gebruik [ creëren geplande banen ](../../api/scheduled-queries.md#create-a-new-scheduled-query) voor het produceren van inzichten samengevoegde lijsten, die een systematische en geautomatiseerde benadering van gegevensverwerking verzekeren. Batchquery&#39;s worden uitgevoerd `INSERT TABLE AS SELECT` en `CREATE TABLE AS SELECT` -query&#39;s om gegevens op te schonen, vorm te geven, te manipuleren en te verrijken. De resultaten van deze vragen worden opgeslagen op het gegevens meer.
1. **Geaggregeerde inzichten die laden:** Laad de geproduceerde bijeengevoegde inzichten in de versnelde opslag en gebruik SQL om vragen te testen, en de nauwkeurigheid en de efficiency van gegevensherwinning te verzekeren. Leren hoe te om stateless vragen aan de versnelde opslag ](../../api/accelerated-queries.md) te maken, zie de documentatie.[
1. **Toegang en integratie:** heb toegang tot de inzichten die in de versnelde opslag foutloos door met Adobe Experience Platform [ te integreren gebruiker-bepaalde Dashboards ](../../../dashboards/user-defined-dashboards.md) of andere aangewezen Business Intelligence (BI) hulpmiddelen worden opgeslagen. Deze integratie met externe clients maakt een consistente en intuïtieve ervaring voor gebruikers mogelijk.

![ een infografisch illustrerend de vier stappen aan Aanpasbare Inzichten in Gegevens Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in de gebruiksgevallen, essentiële mogelijkheden en noodzakelijke stappen voor het ontwikkelen van een aanpasbaar dashboard voor inzichten met Data Distiller. Om verder te leren over het creëren van maats het melden gegevensmodellen, zie de [ rapporterende gids van het gegevensmodel van inzichten ](./reporting-insights-data-model.md).
