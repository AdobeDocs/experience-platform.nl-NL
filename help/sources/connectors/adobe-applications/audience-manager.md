---
keywords: Experience Platform;thuis;populaire onderwerpen;Audience Manager-aansluiting;Audience Manager;publieksmanager
solution: Experience Platform
title: Overzicht van Audience Manager Source Connector
topic: overview
description: De de bronschakelaarstromen van Adobe Audience Manager eerste-partijgegevens die in Audience Manager aan Adobe Experience Platform worden verzameld.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# Audience Manager-aansluiting

De Adobe Audience Manager-gegevensconnector streamt gegevens van de eerste partij die in Adobe Audience Manager naar Adobe Experience Platform zijn verzameld. De schakelaar van de Audience Manager neemt twee categorieën gegevens aan Platform op:

- **Real-time gegevens:** gegevens die in real-time worden vastgelegd op de gegevensverzamelingsserver van de Audience Manager. Deze gegevens worden gebruikt in Audience Manager om op regel gebaseerde eigenschappen te bevolken en zullen in Platform in de kortste latentietijd oppervlakten.
- **Profielgegevens:** Audience Manager gebruikt real-time gegevens en gegevens aan boord om klantprofielen af te leiden. Deze profielen worden gebruikt om identiteitsgrafieken en eigenschappen op segmentrealisaties te bevolken.

De schakelaar van de Audience Manager brengt deze gegevenscategorieën aan het schema van het Gegevensmodel van de Ervaring (XDM) in kaart en verzendt hen naar Platform. Real-time gegevens worden verzonden als XDM ExperienceEvent-gegevens, terwijl profielgegevens worden verzonden als XDM Individuele profielen.

Voor instructies bij het creëren van een verbinding met Adobe Audience Manager die de interface van het Platform gebruiken, zie [de schakelaarleerprogramma ](../../tutorials/ui/create/adobe-applications/audience-manager.md) van de Audience Manager.

## Wat is het Model van de Gegevens van de Ervaring (XDM)?

XDM is een openbaar gedocumenteerde specificatie die een gestandaardiseerd kader verstrekt waardoor het Platform gegevens van de klantenervaring organiseert.

Door zich aan XDM-standaarden te houden, kunnen gegevens voor klantervaring op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over hoe XDM in Experience Platform wordt gebruikt, zie [XDM System overview](../../../xdm/home.md). Meer over leren hoe de Schema&#39;s XDM zoals Profiel en ExperienceEvent gestructureerd zijn, zie [grondbeginselen van schemacompositie](../../../xdm/schema/composition.md).

## Voorbeelden van XDM-schema&#39;s

Hieronder volgen voorbeelden van de structuur van de Audience Manager die aan XDM ExperienceEvent en het Individuele Profiel XDM in Platform in kaart wordt gebracht.

### ExperienceEvent - voor gegevens in real time en onboard gegevens

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Afzonderlijk XDM-profiel - voor profielgegevens

![](images/aam-profile-xdm-for-profile-data.png)

## Hoe worden velden toegewezen van Adobe Audience Manager aan XDM?

Zie de documentatie voor [Audience Manager mapping fields](./mapping/audience-manager.md) voor meer informatie.

## Gegevensbeheer op Platform

### Gegevenssets

Datasets zijn een opslag- en beheerconstructie voor een verzameling gegevens, doorgaans een tabel, die schema (kolommen) en velden (rijen) bevat en beschikbaar wordt gesteld door een gegevensverbinding. De gegevens van de Audience Manager bestaan uit gegevens in real time, Binnenkomende gegevens, en de gegevens van het Profiel. Om van uw gegevensreeksen van de Audience Manager de plaats te bepalen, gebruik de onderzoeksfunctie in UI met de verstrekte noemende overeenkomsten voor elk type van gegevens.

De datasets van de Audience Manager worden onbruikbaar gemaakt voor Profiel door gebrek en de gebruikers hebben de capaciteit om datasets toe te laten of onbruikbaar te maken die op hun gebruiksgevallen worden gebaseerd. Het wordt niet geadviseerd om datasets onbruikbaar te maken die voor segmentlidmaatschap in Profiel zullen worden gebruikt.

| Naam gegevensset | Beschrijving |
| ------------ | ----------- |
| AAM in realtime | Deze dataset bevat gegevens die door directe treffers op eindpunten DCS van de Audience Manager en identiteitskaarten voor Profielen van de Audience Manager worden verzameld. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. |
| Updates van real-time profiel AAM | Deze dataset laat in real time het richten van de eigenschappen en de segmenten van de Audience Manager toe. Het omvat informatie voor het regionale verpletteren van de Rand, eigenschap, en segmentlidmaatschap. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten, om de gegevens aan Profiel direct in te gaan. |
| Apparaatgegevens AAM | Apparaatgegevens met ECID&#39;s en bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten, om de gegevens aan Profiel direct in te gaan. |
| Apparaatprofielgegevens AAM | Wordt gebruikt voor de diagnose van Audience Manager-aansluiting. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten, om de gegevens aan Profiel direct in te gaan. |
| AAM geverifieerde profielen | Deze dataset bevat Audience Manager voor authentiek verklaarde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten, om de gegevens aan Profiel direct in te gaan. |
| Metagegevens geverifieerde profielen AAM | Gebruikt voor de diagnostiek van de Verbinding van de Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten, om de gegevens aan Profiel direct in te gaan. |
| Gegevensback-up AAM apparaten | Dataset van het brengen in vroegere apparatengegevens. Dit bevat ECID&#39;s en de bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten om de gegevens aan Profiel direct in te gaan. |
| Back-up van geverifieerde profielen AAM | Dataset van het brengen in verleden voor authentiek verklaarde gegevens. Dit bevat voor Audience Managers geverifieerde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profiel]** knevel toelaten om de gegevens aan Profiel direct in te gaan. |

### Verbindingen

Adobe Audience Manager maakt één verbinding in Catalog: Verbinding met Audience Manager. Catalog is het systeem van de verslagen voor gegevensplaats en lijn binnen Adobe Experience Platform. Een verbinding is een voorwerp van de Catalogus dat een klant-specifiek geval van Connectors is. Zie [Overzicht van catalogusservice](../../../catalog/home.md) voor meer informatie over Catalog, verbindingen en connectors.

## Wat is de verwachte latentie voor de Gegevens van de Audience Manager over Platform?

| Gegevens Audience Manager | Latentie | Notities |
| --- | --- | --- |
| Gegevens in realtime | &lt; 35=&quot;&quot; minutes=&quot;&quot;> | Tijd vanaf het vastleggen bij het knooppunt Edge van de Audience Manager tot het verschijnen op het Data Lake van het Platform. |
| Profielgegevens | &lt; 2=&quot;&quot; days=&quot;&quot;> | Tijd van vastleggen via DCS/PCS Edge-gegevens en gegevens aan boord, die worden verwerkt naar een gebruikersprofiel, tot weergave in profiel. Deze gegevens landen niet rechtstreeks op het Platform Data Lake. De knevel van het profiel kan voor de datasets van het Profiel van de Audience Manager worden toegelaten om deze gegevens in Profiel direct in te gaan. |