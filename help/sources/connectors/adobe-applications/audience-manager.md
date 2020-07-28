---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Audience Manager-aansluiting
topic: overview
translation-type: tm+mt
source-git-commit: fb4ffa2c95365905f5417586fa7ecf88523009a0
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---


# Audience Manager-aansluiting

De de gegevensschakelaar van de Adobe Audience Manager stroomt eerste partijgegevens die in Adobe Audience Manager aan Adobe Experience Platform worden verzameld. De schakelaar van de Audience Manager neemt drie categorieën gegevens aan Platform in:

- **Realtime gegevens:** Gegevens die in real time worden vastgelegd op de gegevensverzamelingsserver van de Audience Manager. Deze gegevens worden gebruikt in Audience Manager om op regel gebaseerde eigenschappen te bevolken en zullen in Platform in de kortste latentietijd oppervlakten.
- **Gegevens aan boord (binnenkomend):** Dit zijn de bestanden die door een gebruiker zijn geüpload naar een Amazon S3-locatie die door Audience Manager wordt gehost. De Audience Manager gebruikt deze gegevens om aan boord genomen eigenschappen te bevolken gebruikend de binnenkomende dossiermethode en zal één of andere latentie hebben.
- **Profielgegevens:** Audience Manager gebruikt realtime en opgenomen gegevens om klantprofielen af te leiden. Deze profielen worden gebruikt om identiteitsgrafieken en eigenschappen op segmentrealisaties te bevolken.

De schakelaar van de Audience Manager brengt deze gegevenscategorieën aan het schema van het Gegevensmodel van de Ervaring (XDM) in kaart en verzendt hen naar Platform. Realtime-gegevens en gegevens aan boord worden verzonden als XDM ExperienceEvent-gegevens, terwijl profielgegevens worden verzonden als XDM Individuele profielen.

Voor instructies bij het creëren van een verbinding met Adobe Audience Manager die de UI van het Platform gebruikt, zie het [schakelaarleerprogramma](../../tutorials/ui/create/adobe-applications/audience-manager.md)van de Audience Manager.

## Wat is het Model van de Gegevens van de Ervaring (XDM)?

XDM is een openbaar gedocumenteerde specificatie die een gestandaardiseerd kader verstrekt waardoor het Platform gegevens van de klantenervaring organiseert.

Door zich aan XDM-standaarden te houden, kunnen gegevens voor klantervaring op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over hoe XDM in Experience Platform wordt gebruikt, zie het overzicht [van het Systeem](../../../xdm/home.md)XDM. Meer over leren hoe de Schema&#39;s XDM zoals Profiel en ExperienceEvent gestructureerd zijn, zie de [grondbeginselen van schemacompositie](../../../xdm/schema/composition.md).

## Voorbeelden van XDM-schema&#39;s

Hieronder volgen voorbeelden van de structuur van de Audience Manager die aan XDM ExperienceEvent en het Individuele Profiel XDM in Platform in kaart wordt gebracht.

### ExperienceEvent - voor Realtime-gegevens en onboard-gegevens

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Afzonderlijk XDM-profiel - voor profielgegevens

![](images/aam-profile-xdm-for-profile-data.png)

## Hoe worden velden toegewezen van Adobe Audience Manager aan XDM?

Zie de documentatie voor [Audience Manager toewijzingsvelden](./mapping/audience-manager.md) voor meer informatie.

## Gegevensbeheer op Platform

### Gegevenssets

Datasets zijn een opslag- en beheerconstructie voor een verzameling gegevens, doorgaans een tabel, die schema (kolommen) en velden (rijen) bevat en beschikbaar wordt gesteld door een gegevensverbinding. De gegevens van de Audience Manager bestaan uit gegevens In real time, Binnenkomende gegevens, en de gegevens van het Profiel. Om van uw gegevensreeksen van de Audience Manager de plaats te bepalen, gebruik de onderzoeksfunctie in UI met de verstrekte noemende overeenkomsten voor elk type van gegevens.

De datasets van de Audience Manager worden onbruikbaar gemaakt voor Profiel door gebrek en de gebruikers hebben de capaciteit om datasets toe te laten of onbruikbaar te maken die op hun gebruiksgevallen worden gebaseerd. Het wordt niet geadviseerd om datasets onbruikbaar te maken die voor segmentlidmaatschap in Profiel zullen worden gebruikt.

| Naam gegevensset | Beschrijving |
| ------------ | ----------- |
| Realtime Audience Manager | Deze dataset bevat gegevens die door directe treffers op eindpunten DCS van de Audience Manager en identiteitskaarten voor Profielen van de Audience Manager worden verzameld. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. |
| Updates van Realtime-profiel voor Audience Manager | Deze dataset laat Realtime het richten van de eigenschappen en de segmenten van de Audience Manager toe. Het omvat informatie voor het regionale verpletteren van de Rand, eigenschap, en segmentlidmaatschap. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. |
| Apparaatgegevens Audience Managers | Apparaatgegevens met ECID&#39;s en bijbehorende segmentrealisaties geaggregeerd in Audience Manager. |
| Apparaatprofielgegevens Audience Managers | Wordt gebruikt voor de diagnose van Audience Manager-aansluiting. |
| Audience Manager geverifieerde profielen | Deze dataset bevat Audience Manager voor authentiek verklaarde profielen. |
| Metagegevens van Audience Manager geverifieerde profielen | Gebruikt voor de diagnostiek van de Verbinding van de Audience Manager. |
| Audience Manager binnenkomend {DataSource ID} **(afgekeurd)** | Deze dataset vertegenwoordigt geregistreerde verslagen in Audience Manager via de binnenkomende dossiermethode. Deze gegevensstroom is afgekeurd en wordt in een volgende versie verwijderd. |
| Audience Manager binnenkomende metagegevens **(afgekeurd)** | Wordt gebruikt voor de diagnose van Audience Manager-aansluiting. Deze gegevensstroom is afgekeurd en wordt in een volgende versie verwijderd. |

### Verbindingen

Adobe Audience Manager maakt één verbinding in catalogus: **Verbinding met** Audience Manager. Catalog is het systeem van de verslagen voor gegevensplaats en lijn binnen Adobe Experience Platform. Een verbinding is een voorwerp van de Catalogus dat een klant-specifiek geval van Connectors is. Zie het overzicht [van de](../../../catalog/home.md) Catalogusservice voor meer informatie over Catalogus, verbindingen en connectors.

## Wat is de verwachte latentie voor de Gegevens van de Audience Manager over Platform?

| Gegevens Audience Manager | Latentie | Notities |
| --- | --- | --- |
| Realtime gegevens | &lt; 35 minuten. | Tijd vanaf het vastleggen op het knooppunt Realtime tot het verschijnen op het Platform Data Lake. |
| Binnenkomende data | &lt; 13 uur | Tijd vanaf het vastleggen op S3-emmers tot het verschijnen op het Platform Data Lake. |
| Profielgegevens | &lt; 2 dagen | Tijd vanaf het vastleggen vanaf Realtime/Inbound-gegevens tot het toevoegen aan een gebruikersprofiel en ten slotte verschijnen op het Platform Data Lake. |