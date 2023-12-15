---
title: Aanpasbare inzichten
description: Leer meer over de gebruiksgevallen, essentiële mogelijkheden en vereiste stappen voor het ontwikkelen van een aanpasbaar dashboard voor inzichten met Data Distiller. Ontdek hoe de aanpasbare mogelijkheden voor inzichten binnen Data Distiller de transparantie kunnen verbeteren en operationele inzichten kunnen verkrijgen in verschillende dimensies, zoals profielen, publiek, campagnes, reizen, rechten en toestemming.
source-git-commit: 18c1d32bbc2732c38a9c37ee8fb9d36a23d4e515
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 0%

---

# Aanpasbare inzichten

Creeer op maat gebaseerde rapporteringsgegevensmodellen om diepgaande inzichten te halen, strategieën te optimaliseren, en analyses aan te passen aan specifieke bedrijfsbehoeften met Gegevens Distiller Aanpasbare Inzichten. Gebruik de Customizable Insights-mogelijkheid om de transparantie te verbeteren en operationele inzichten van uw Adobe Experience Platform-gegevens te verkrijgen in verschillende dimensies, zoals profielen, publiek, campagnes, reizen, rechten en toestemming. Deze mogelijkheid biedt een veelzijdige, adaptieve oplossing om de rapporteringsgegevensmodellen van uw organisatie aan te passen aan uw specifieke bedrijfsbehoeften.

In dit document worden gebruiksgevallen, essentiële functies en vereiste stappen beschreven voor het ontwikkelen van een aanpasbaar inzichtsdashboard met Data Distiller.

## Vereisten

Deze zelfstudie gebruikt door de gebruiker gedefinieerde dashboards om gegevens van uw aangepaste gegevensmodel in de gebruikersinterface van het platform te visualiseren. Zie de [door de gebruiker gedefinieerde dashboarddocumentatie](../../../dashboards/user-defined-dashboards.md) voor meer informatie over deze functie.

## Aan de slag

Distiller SKU van Gegevens wordt vereist om een model van douanegegevens voor uw rapporteringsinzichten te bouwen en de de gegevensmodellen van Real-Time CDP uit te breiden die de verrijkte gegevens van het Platform houden. Zie de [verpakking](../../packaging.md), [guardrails](../../guardrails.md#query-accelerated-store), en  [licenties](../../data-distiller/license-usage.md) documentatie die betrekking heeft op de gegevens Distiller SKU. Als u geen gegevens Distiller SKU hebt, contacteer uw vertegenwoordiger van de klantendienst van de Adobe voor meer informatie.

## Aanpasbare gevallen voor gebruik van inzichten {#use-cases}

Hieronder ziet u veelvoorkomende gebruiksgevallen die effectief kunnen worden aangepakt met Aanpasbare inzichten in Data Distiller.

### Transparantie voor profiel- en publieksgebruik {#usage-transparency}

**Uitdaging:** Hoe te om de Belangrijkste Indicatoren van Prestaties (KPIs) door specifieke criteria zoals bedrijfseenheden, loyaliteitsstatus, of de Waarde van het Leven van de Klant (CLTV) te verdelen.

**Aanpasbare oplossing voor inzichten:** Data Distiller maakt het mogelijk gegevensmodellen in Adobe Experience Platform uit te breiden, waardoor [de toevoeging van aangepaste profielkenmerken, zoals CLTV](../../use-cases/customer-lifetime-value.md) of loyaliteitsstatus.

### Constante anomalieën bijhouden {#consent-anomaly-tracking}

**Uitdaging:** Hoe te om publieksoverlap en de grootte trendlinerapporten op aangepaste toestemmingsattributen voor kanalen zoals e-mail, SMS, en telefoon toe te passen.

**Aanpasbare oplossing voor inzichten:** Het rapportagegegevensmodel kan worden uitgebreid om wijzigingen in de voorkeuren voor toestemming in de loop van de tijd te volgen. Dit omvat het bouwen van extra feiten en dimensietabellen aan tendenstoestemmingsvoorkeur en het plannen [incrementele gegevensvernieuwing](../../key-concepts/incremental-load.md).

### Segmentatiestrategie voor het publiek optimaliseren {#optimize-audience-segmentation-strategy}

**Uitdaging:** Hoe te om het Leren van de Machine (ML) model-geproduceerde aandrijvingsscores in hun publiekPKI- rapporten te integreren.

**Aanpasbare oplossing voor inzichten:** Data Distiller staat de opname van [propensecores van aangepaste ML-modellen](../../use-cases/propensity-score.md)de berekening van de geaggregeerde scores op het niveau van de doelgroep te vergemakkelijken. Deze gegevens kunnen vervolgens worden gerapporteerd naast standaard-KPI&#39;s.

### Uitbreiding publiek {#audience-expansion}

**Uitdaging:** Hoe te om meer dan enkel profieltellingen in publiek te verwerven overlapt rapporten en aanvullende demografische gegevens of voorkeur te bereiken om de strategieën van de publieksuitbreiding te begeleiden.

**Aanpasbare oplossing voor inzichten:** Door het rapportgegevensmodel uit te breiden, kunnen de gebruikers extra profielattributen opnemen, die het publiek verrijken overlappen rapport met relevante demografische gegevens en voorkeur.

## Belangrijke mogelijkheden voor het genereren van aanpasbare inzichten {#key-capabilities}

In de onderstaande afbeelding worden verschillende essentiële mogelijkheden voor het genereren van aanpasbare inzichten beschreven. Deze mogelijkheden omvatten:

1. **Gegevensvisualisaties:** Opnemen van visuele elementen, zoals trends en staafdiagrammen, voor een uitgebreide weergave van gegevenstrends.
1. **Dashboard-authoring:** Het maken van aangepaste dashboards op maat van specifieke gebruiksgevallen, zodat u over een meer persoonlijke en doelgerichte ervaring op het gebied van analyse beschikt.
1. **Flexibele SQL-gegevensmodellen:** Gebruik een veelzijdige SQL-benadering voor gegevensmodellering die gebruikers in staat stelt verschillende gegevenssets naadloos te combineren en te manipuleren, waardoor het aanpassingsvermogen en de analytische diepte worden verbeterd.
1. **Versnelde opslag:** Een versneld opslagmechanisme implementeren om op efficiënte wijze geaggregeerde inzichten via SQL te bedienen, zodat u verzekerd bent van gestroomlijnde en snelle toegang tot waardevolle informatie.
1. **BI-connectiviteit:** Het vergemakkelijken van naadloze integratie met populaire hulpmiddelen van de Business Intelligence (BI), met inbegrip van Power BI, Tableau, Looker, en Apache Superset. Deze connectiviteit zorgt voor compatibiliteit met verschillende BI-omgevingen en biedt gebruikers de flexibiliteit om hun keuze te gebruiken voor diepgaande analyse en rapportage.

![Visuele vertegenwoordiging van de belangrijkste mogelijkheden van Gegevens Distiller Aanpasbare Inzichten.](../../images/data-distiller/customizable-insights/key-capabilities-of-customizable-insights.png)

## Stappen voor het maken van aanpasbare inzichten {#steps-to-create}

Volg de onderstaande stapsgewijze instructies om een aanpasbaar dashboard met inzichten in Data Distiller te ontwikkelen.

1. **Ad-hoczoekopdracht:** Beginnen met uitvoeren van ad hoc `SELECT` zoekopdrachten om ruwe gegevens over het data Lake te verkennen. Hierdoor kan ter plekke een verkennende gegevensanalyse worden uitgevoerd om gegevens te experimenteren, en worden gegevens gevalideerd wanneer de resultaten van de query&#39;s niet in het datumpeer zijn opgeslagen.
1. **Batchquerygebruik:** Batchquery&#39;s gebruiken voor [geplande taken maken](../../api/scheduled-queries.md#create-a-new-scheduled-query) voor het genereren van inzichten aggregatietabellen, zorgen voor een systematische en geautomatiseerde aanpak van gegevensverwerking. Batchquery&#39;s uitvoeren `INSERT TABLE AS SELECT` en `CREATE TABLE AS SELECT` query&#39;s voor het opschonen, vormgeven, manipuleren en verrijken van gegevens. De resultaten van deze vragen worden opgeslagen op het gegevens meer.
1. **Samengevoegde inzichten laden:** Laad de gegenereerde geaggregeerde inzichten in de versnelde opslag en gebruik SQL om query&#39;s te testen en zorg voor de nauwkeurigheid en efficiëntie van gegevensophaling. Leren hoe te [stel stateless vragen aan de versnelde opslag](../../api/accelerated-queries.md), raadpleegt u de documentatie.
1. **Toegang en integratie:** Toegang tot de inzichten die zijn opgeslagen in de versnelde opslag, zonder problemen door integratie met Adobe Experience Platform [Door gebruiker gedefinieerde dashboards](../../../dashboards/user-defined-dashboards.md) of andere voorkeursgereedschappen voor Businessen Intelligence (BI). Deze integratie met externe clients maakt een consistente en intuïtieve ervaring voor gebruikers mogelijk.

![An infographic illustrating the four stappen to Customizable Insights in Data Distiller.](../../images/data-distiller/customizable-insights/steps-to-customizable-insights.png)

## Volgende stappen

Door dit document te lezen, hebt u nu een beter inzicht in de gebruiksgevallen, essentiële mogelijkheden en noodzakelijke stappen voor het ontwikkelen van een aanpasbaar dashboard voor inzichten met Data Distiller. Als u meer wilt leren over het maken van modellen met op maat gesneden rapportgegevens, raadpleegt u de [handleiding voor het rapporteren van inzichten](./reporting-insights-data-model.md).
