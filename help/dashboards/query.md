---
solution: Experience Platform
title: Onbewerkte gegevenssets verkennen en verwerken waardoor Experience Platform-dashboards kunnen worden aangestuurd
type: Documentation
description: Leer hoe te om de Dienst van de Vraag te gebruiken om ruwe datasets te onderzoeken en te verwerken die profiel, segment, en bestemmingsdashboards in Experience Platform aandrijven.
source-git-commit: 1facf7079213918c2ef966b704319827eaa4a53d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 1%

---


# Onderzoek, verifieer en proces dashboarddatasets gebruikend de Dienst van de Vraag

Adobe Experience Platform verstrekt belangrijke informatie over het profiel van uw organisatie, segment, en bestemmingsgegevens door dashboards beschikbaar binnen de UI van het Experience Platform. U kunt de Dienst van de Vraag van Adobe Experience Platform dan gebruiken om, de ruwe datasets te onderzoeken te verifiëren en te verwerken die deze dashboards in het gegevensmeer aandrijven.

## Aan de slag met Query Service

De Dienst van de Vraag van Adobe Experience Platform steunt marketers in het verkrijgen van inzicht van hun gegevens door het gebruik van standaardSQL toe te laten om gegevens in het gegevensmeer te vragen. De Dienst van de vraag biedt een gebruikersinterface en een API aan die kunnen worden gebruikt om zich bij om het even welke dataset in het gegevensmeer aan te sluiten en de vraagresultaten als nieuwe datasets voor gebruik in rapportering, machine het leren, of voor opname in het Profiel van de Klant in real time te vangen.

Om meer over de Dienst van de Vraag en zijn rol binnen Experience Platform te leren, te beginnen door [overzicht van de Dienst van de Vraag te lezen](../query-service/home.md).

## Beschikbare gegevenssets

U kunt de Dienst van de Vraag gebruiken om ruwe datasets voor profiel, segment, en bestemmingsdashboards te vragen. De volgende secties beschrijven de ruwe datasets die u in het gegevensmeer kunt vinden.

### Gegevensbestanden van profielkenmerken

Voor elk actief fusiebeleid in het Profiel van de Klant in real time, is er een dataset van de profielattributen beschikbaar in het gegevensmeer.

De naamgevingsconventie van deze gegevenssets is **Profielkenmerk** gevolgd door een alfanumerieke waarde. Bijvoorbeeld: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Om het volledige schema van elke dataset te begrijpen, kunt u voorproef en de datasets onderzoeken gebruikend de datasetkijker in Experience Platform UI.

### Gegevensset voor segmentmetagegevens

Er is een dataset van segmentmeta-gegevens beschikbaar in het gegevensmeer die meta-gegevens voor elk van de segmenten van uw organisatie bevatten.

De naamgevingsconventie van deze gegevensset is **Profielsegmentdefinitie** gevolgd door een alfanumerieke waarde. Bijvoorbeeld: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

Om het volledige schema van de dataset te begrijpen, kunt u voorproef en het schema onderzoeken gebruikend de datasetkijker in Experience Platform UI.

![](images/query/segment-metadata.png)

### Gegevensset met doelmetagegevens

De meta-gegevens voor elk van de geactiveerde bestemmingen van uw organisatie is beschikbaar als ruwe dataset in het gegevensmeer.

De noemende overeenkomst van deze dataset is **DIM_Destination**.

Om het volledige schema van de dataset te begrijpen, kunt u voorproef en het schema onderzoeken gebruikend de datasetkijker in Experience Platform UI.

![](images/query/destinations-metadata.png)

## Voorbeeldquery

De volgende voorbeeldvragen omvatten steekproef SQL die in de Dienst van de Vraag kan worden gebruikt om, de ruwe datasets te onderzoeken te verifiëren en te verwerken die uw dashboards aandrijven.

### Aantal profielen op identiteit

Dit profielinzicht verstrekt een verdeling van identiteiten over alle samengevoegde profielen in de dataset. Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

**Query**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Aantal profielen per segment

Dit publieksinzicht verstrekt het totale aantal samengevoegde profielen binnen elk segment in de dataset. Dit getal is het resultaat van het toepassen van het samenvoegbeleid voor segmenten op de profielgegevens om profielfragmenten samen te voegen tot één profiel voor elke persoon in het segment.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

## Volgende stappen

Door deze gids te lezen, kunt u de Dienst van de Vraag nu gebruiken om verscheidene vragen uit te voeren om de ruwe datasets te onderzoeken en te verwerken die uw profiel, segment, en bestemmingsdashboards aandrijven.

Als u meer wilt weten over elk dashboard en de bijbehorende metriek, selecteert u een dashboard in de lijst met beschikbare dashboards in de documentatienavigatie.
