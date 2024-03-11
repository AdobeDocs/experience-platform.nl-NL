---
keywords: Experience Platform;thuis;populaire onderwerpen;Audience Manager-aansluiting;Audience Manager;publieksmanager
solution: Experience Platform
title: Overzicht van Bron Audience Manager
description: De Adobe Audience Manager-bronstroom streamt gegevens van de eerste partij die in Audience Manager naar Adobe Experience Platform zijn verzameld.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 8ef9fedcc77f39707ef5191988a5b7360e1118cc
workflow-type: tm+mt
source-wordcount: '1120'
ht-degree: 0%

---

# Bron Audience Manager

>[!IMPORTANT]
>
>Bij de eerste configuratie retourneert de Adobe Audience Manager-bron een foutbericht waarin wordt uitgelegd dat een naamruimte van een identiteit met een opgegeven `namespaceCode={VALUE}` bestaat niet. **Opmerking**: Aan de achterkant, `namespaceCode` wordt gebruikt om naar het identiteitssymbool te verwijzen. Om uw integratie te voltooien, moet u:
>
>- [Een aangepaste naamruimte maken in Identity Service](../../../identity-service/features/namespaces.md#create-custom-namespaces) met het opgegeven identiteitssymbool (`VALUE`).
>- Voer uw gegevens opnieuw in.

De Adobe Audience Manager-bronstroom streamt gegevens van de eerste partij die in Adobe Audience Manager zijn verzameld voor activering in Adobe Experience Platform. De bron van de Audience Manager neemt twee soorten gegevens aan Platform op:

- **Gegevens in realtime:** Gegevens in real time vastgelegd op de gegevensverzamelingsserver van de Audience Manager. Deze gegevens worden gebruikt in Audience Manager om op regel-gebaseerde eigenschappen te bevolken en zullen in Platform in de kortste latentietijd oppervlakten.
- **Profielgegevens:** Audience Manager gebruikt real-time en onbeheerde gegevens om klantprofielen af te leiden. Deze profielen worden gebruikt om identiteitsgrafieken en eigenschappen op segmentrealisaties te bevolken.

De bron van de Audience Manager brengt deze gegevenstypes aan een Model van de Gegevens van de Ervaring (XDM) schema in kaart en verzendt hen dan naar Platform. In real time gegevens worden verzonden als gegevens XDM ExperienceEvent, terwijl de gegevens van het Profiel als gegevens van het Individuele Profiel XDM worden verzonden.

Lees voor meer informatie de handleiding op [het creëren van een Audience Manager bronverbinding in UI](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## Wat is het Model van de Gegevens van de Ervaring (XDM)?

XDM is een openbaar gedocumenteerde specificatie die een gestandaardiseerd kader verstrekt waardoor het Platform gegevens van de klantenervaring organiseert.

Door zich aan XDM-standaarden te houden, kunnen gegevens voor klantervaring op uniforme wijze worden opgenomen, waardoor het eenvoudiger wordt om gegevens te leveren en informatie te verzamelen.

Voor meer informatie over hoe XDM in Experience Platform wordt gebruikt, lees [XDM System, overzicht](../../../xdm/home.md). Als u meer wilt weten over de structuur van XDM-schema&#39;s tussen profielen en gebeurtenissen, leest u de [grondbeginselen van de schemacompositie](../../../xdm/schema/composition.md).

## Voorbeelden van XDM-schema&#39;s

Hieronder volgen voorbeelden van de structuur van de Audience Manager die is toegewezen aan XDM ExperienceEvent en XDM Individual Profile in Platform.

### ExperienceEvent - voor realtime gegevens en onbeheerde gegevens

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Afzonderlijk XDM-profiel - voor profielgegevens

![](images/aam-profile-xdm-for-profile-data.png)

Voor informatie over hoe de gebieden van Audience Manager aan XDM in kaart worden gebracht, lees de documentatie op [Toewijzingsvelden voor Audience Managers](./mapping/audience-manager.md).

## Gegevensbeheer op platform

### Gegevenssets

Een dataset is een opslag en beheersconstructie voor een inzameling van gegevens, typisch een lijst, die een schema (kolommen) en gebieden (rijen) bevat en door een gegevensverbinding ter beschikking wordt gesteld. De gegevens van de Audience Manager bestaan uit gegevens in real time, binnenkomende gegevens, en de gegevens van het Profiel. Om van uw gegevensreeksen van de Audience Manager de plaats te bepalen, gebruik de onderzoeksfunctie in UI met de verstrekte noemende overeenkomsten voor elk type van gegevens.

De datasets van de Audience Manager worden onbruikbaar gemaakt voor Profiel door gebrek en de gebruikers hebben de capaciteit om datasets toe te laten of onbruikbaar te maken die op hun gebruiksgevallen worden gebaseerd. Het wordt niet geadviseerd om datasets onbruikbaar te maken die voor segmentlidmaatschap in Profiel zullen worden gebruikt.

>[!NOTE]
>
>AAM Real-time is de enige dataset die naar het datumpeer gaat. Alle andere gegevensreeksen van de Audience Manager gaan naar [!DNL Profile], als deze zijn ingeschakeld voor [!DNL Profile]. Als deze opties niet zijn ingeschakeld voor [!DNL Profile]Dan ontvangen ze geen gegevens en worden ze als leeg weergegeven.

| Naam gegevensset | Beschrijving | Klasse |
| --- | --- | --- |
| AAM in realtime | Deze dataset bevat gegevens die door directe treffers op eindpunten DCS van de Audience Manager en identiteitskaarten voor Profielen van de Audience Manager worden verzameld. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. | Gebeurtenis Experience |
| Updates van real-time profiel AAM | Deze dataset laat in real time het richten van de eigenschappen en de segmenten van de Audience Manager toe. Het omvat informatie voor het regionale verpletteren van de Rand, eigenschap, en segmentlidmaatschap. Laat deze gegevensset ingeschakeld voor het opnemen van profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Apparaatgegevens AAM | Apparaatgegevens met ECID&#39;s en bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Apparaatprofielgegevens AAM | Wordt gebruikt voor diagnostiek van de Audience Manager-connector. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| AAM geverifieerde profielen | Deze dataset bevat Audience Manager voor authentiek verklaarde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Metagegevens geverifieerde profielen AAM | Wordt gebruikt voor diagnostiek van Audience Manager Connector. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Gegevensback-up AAM apparaten | Dataset van het brengen in vroegere apparatengegevens. Dit bevat ECID&#39;s en de bijbehorende segmentrealisaties geaggregeerd in Audience Manager. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** schakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |
| Back-up van geverifieerde profielen AAM | Dataset van het brengen in verleden voor authentiek verklaarde gegevens. Dit bevat voor Audience Managers geverifieerde profielen. Gegevens zijn niet zichtbaar als batches in de gegevensset. U kunt de **[!UICONTROL Profile]** schakelen om de gegevens rechtstreeks in te voeren in Profiel. | Opnemen |

### Verbindingen

Adobe Audience Manager maakt één verbinding in Catalog: Audience Manager Connection. Catalog is het systeem van de verslagen voor gegevensplaats en lijn binnen Adobe Experience Platform. Een verbinding is een voorwerp van de Catalogus dat een klant-specifiek geval van schakelaars is. Lees de [Overzicht van Catalog Service](../../../catalog/home.md) voor meer informatie over Catalog, verbindingen, en schakelaars.

### Segmentpopulatie voor profieleffect

De de bevolkingsgrootte van het segment heeft een directe invloed op de aantallen van het Profiel wanneer u eerst een segment van de Audience Manager naar Platform verzendt. Dit betekent dat het selecteren van alle segmenten mogelijk Profieloverschrijdingen kan veroorzaken die uw gebruiksrechten voor licenties overschrijden. Platform maakt ook onderscheid tussen nieuwe gegevens en historische gegevens voor het opnemen van profielen. Een segment met 100 op de eerste plaats gebaseerde identiteiten zal tot 100 profielen leiden. Als de populatie van hetzelfde segment echter tot 150 werd verhoogd en aan Platform werd geconsumeerd, zal het aantal profielen slechts met 50 stijgen, aangezien er slechts 50 nieuwe profielen zijn.

U kunt ook het profielgebruik controleren dat uw account beschikbaar heeft via de [Licentiegebruiksdashboard](../../../dashboards/guides/license-usage.md).

## Wat is de verwachte latentie voor de Gegevens van de Audience Manager op Platform?

| Gegevens Audience Manager | Type | Latentie | Notities |
| --- | --- | --- | --- |
| Gegevens in realtime | Gebeurtenissen | &lt;25 minuten | Tijd vanaf het vastleggen bij het knooppunt Audience Manager Edge tot het verschijnen in het datumpeer. |
| Gegevens in realtime | Profielupdates | &lt;10 minuten | Tijd om in het Profiel van de Klant in real time te landen. |
| Gegevens in realtime en ongeboekt | Profielupdates | 24 tot 36 uur | Tijd vanaf het vastleggen via DCS/PCS Edge-gegevens en opgenomen gegevens, dat wordt verwerkt naar een gebruikersprofiel en vervolgens wordt weergegeven in Real-Time klantprofiel. Momenteel landen deze gegevens niet rechtstreeks in het datumpeer. De knevel van het profiel kan voor de datasets van het Profiel van de Audience Manager worden toegelaten om deze gegevens direct in het Profiel van de Klant in real time in te voeren. |
