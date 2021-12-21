---
keywords: Experience Platform;thuis;populaire onderwerpen;Audience Manager-aansluiting;Audience Manager;publieksmanager
solution: Experience Platform
title: Overzicht van Audience Manager Source Connector
topic-legacy: overview
description: De de bronschakelaarstromen van Adobe Audience Manager eerste-partijgegevens die in Audience Manager aan Adobe Experience Platform worden verzameld.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: d0b6885b6e8606692cfe1173b75c7d3537800a5f
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%

---

# Audience Manager-aansluiting

De Adobe Audience Manager-gegevensconnector streamt gegevens van de eerste partij die in Adobe Audience Manager naar Adobe Experience Platform zijn verzameld. De schakelaar van de Audience Manager neemt twee categorieën gegevens aan Platform op:

- **Gegevens in realtime:** Gegevens die in real time worden vastgelegd op de gegevensverzamelingsserver van de Audience Manager. Deze gegevens worden gebruikt in Audience Manager om op regel gebaseerde eigenschappen te bevolken en zullen in Platform in de kortste latentietijd oppervlakten.
- **Profielgegevens:** De Audience Manager gebruikt gegevens in real time en aan boord om klantenprofielen af te leiden. Deze profielen worden gebruikt om identiteitsgrafieken en eigenschappen op segmentrealisaties te bevolken.

De schakelaar van de Audience Manager brengt deze gegevenscategorieën aan het schema van het Gegevensmodel van de Ervaring (XDM) in kaart en verzendt hen naar Platform. Real-time gegevens worden verzonden als XDM ExperienceEvent-gegevens, terwijl profielgegevens worden verzonden als XDM Individuele profielen.

Voor instructies over het maken van een verbinding met Adobe Audience Manager met behulp van de interface van het Platform raadpleegt u de [Zelfstudie over Audience Manager-aansluiting](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Wat is het Model van de Gegevens van de Ervaring (XDM)?

XDM is een openbaar gedocumenteerde specificatie die een gestandaardiseerd kader verstrekt waardoor het Platform gegevens van de klantenervaring organiseert.

Door zich aan XDM-standaarden te houden, kunnen gegevens voor klantervaring op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over hoe XDM in Experience Platform wordt gebruikt, zie [XDM System, overzicht](../../../xdm/home.md). Als u meer wilt weten over de structuur van XDM-schema&#39;s, zoals Profiel en ExperienceEvent, raadpleegt u de [grondbeginselen van de schemacompositie](../../../xdm/schema/composition.md).

## Voorbeelden van XDM-schema&#39;s

Hieronder volgen voorbeelden van de structuur van de Audience Manager die aan XDM ExperienceEvent en het Individuele Profiel XDM in Platform in kaart wordt gebracht.

### ExperienceEvent - voor gegevens in real time en onboard gegevens

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Afzonderlijk XDM-profiel - voor profielgegevens

![](images/aam-profile-xdm-for-profile-data.png)

## Hoe worden velden toegewezen van Adobe Audience Manager aan XDM?

Zie de documentatie voor [Toewijzingsvelden voor Audience Managers](./mapping/audience-manager.md) voor meer informatie .

## Gegevensbeheer op Platform

### Gegevenssets

Datasets zijn een opslag- en beheerconstructie voor een verzameling gegevens, doorgaans een tabel, die schema (kolommen) en velden (rijen) bevat en beschikbaar wordt gesteld door een gegevensverbinding. De gegevens van de Audience Manager bestaan uit gegevens in real time, Binnenkomende gegevens, en de gegevens van het Profiel. Om van uw gegevensreeksen van de Audience Manager de plaats te bepalen, gebruik de onderzoeksfunctie in UI met de verstrekte noemende overeenkomsten voor elk type van gegevens.

De datasets van de Audience Manager worden onbruikbaar gemaakt voor Profiel door gebrek en de gebruikers hebben de capaciteit om datasets toe te laten of onbruikbaar te maken die op hun gebruiksgevallen worden gebaseerd. Het wordt niet geadviseerd om datasets onbruikbaar te maken die voor segmentlidmaatschap in Profiel zullen worden gebruikt.

>[!NOTE]
>
>AAM In real time is de enige dataset die naar [!DNL Data Lake]. Alle andere gegevensreeksen van de Audience Manager gaan naar [!DNL Profile], als deze zijn ingeschakeld voor [!DNL Profile]. Als deze opties niet zijn ingeschakeld voor [!DNL Profile]Dan ontvangen ze geen gegevens en worden ze als leeg weergegeven.

| Naam gegevensset | Beschrijving | Klasse |
| --- | --- | --- |
| AAM in realtime | Deze dataset bevat gegevens die door directe treffers op eindpunten DCS van de Audience Manager en identiteitskaarten voor Profielen van de Audience Manager worden verzameld. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. | Gebeurtenis Experience |
| Updates van real-time profiel AAM | Deze dataset laat in real time het richten van de eigenschappen en de segmenten van de Audience Manager toe. Het omvat informatie voor het regionale verpletteren van de Rand, eigenschap, en segmentlidmaatschap. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Apparaatgegevens AAM | Apparaatgegevens met ECID&#39;s en bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Apparaatprofielgegevens AAM | Wordt gebruikt voor de diagnose van Audience Manager-aansluiting. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| AAM geverifieerde profielen | Deze dataset bevat Audience Manager voor authentiek verklaarde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Metagegevens geverifieerde profielen AAM | Gebruikt voor de diagnostiek van de Verbinding van de Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Gegevensback-up AAM apparaten | Dataset van het brengen in vroegere apparatengegevens. Dit bevat ECID&#39;s en de bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** schakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Back-up van geverifieerde profielen AAM | Dataset van het brengen in verleden voor authentiek verklaarde gegevens. Dit bevat voor Audience Managers geverifieerde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** schakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |

### Verbindingen

Adobe Audience Manager maakt één verbinding in Catalog: Verbinding met Audience Manager. Catalog is het systeem van de verslagen voor gegevensplaats en lijn binnen Adobe Experience Platform. Een verbinding is een voorwerp van de Catalogus dat een klant-specifiek geval van Connectors is. Zie de [Overzicht van Catalog Service](../../../catalog/home.md) voor meer informatie over Catalog, verbindingen, en schakelaars.

## Wat is de verwachte latentie voor de Gegevens van de Audience Manager over Platform?

| Gegevens Audience Manager | Latentie | Notities |
| --- | --- | --- |
| Gegevens in realtime | &lt; 35 minuten. | Tijd vanaf het vastleggen bij het knooppunt Edge van de Audience Manager tot het verschijnen op het Data Lake van het Platform. |
| Profielgegevens | &lt; 2 dagen | Tijd van vastleggen via DCS/PCS Edge-gegevens en gegevens aan boord, die worden verwerkt naar een gebruikersprofiel, tot weergave in profiel. Deze gegevens landen niet rechtstreeks op het Platform Data Lake. De knevel van het profiel kan voor de datasets van het Profiel van de Audience Manager worden toegelaten om deze gegevens in Profiel direct in te gaan. |
