---
solution: Experience Platform
title: Onbewerkte gegevenssets verkennen en verwerken waardoor Platform-dashboards kunnen worden aangestuurd
type: Documentation
description: Leer hoe te om de Dienst van de Vraag te gebruiken om ruwe datasets te onderzoeken en te verwerken die profiel, segment, en bestemmingsdashboards in Experience Platform aandrijven.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
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

De dashboardinzichten van het profiel zijn gebonden aan fusiebeleid dat door uw organisatie is bepaald. Voor elk actief fusiebeleid, is er een dataset van profielattributen beschikbaar in het gegevenspeer.

De naamgevingsconventie van deze gegevenssets is **Profile-Snapshot-Export** gevolgd door een door het systeem gegenereerde, willekeurige alfanumerieke waarde. Bijvoorbeeld: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Om het volledige schema van elke de uitvoerdataset van de profielmomentopname te begrijpen, kunt u voorproef en de datasets [onderzoeken gebruikend de datasetkijker](../catalog/datasets/user-guide.md) in Experience Platform UI.

![](images/query/profile-attribute.png)

#### Gegevenssets van profielkenmerken toewijzen om beleid-id&#39;s samen te voegen

Elke profielkenmerkgegevensset heeft de naam **Profielmomentopname exporteren** gevolgd door een door het systeem gegenereerde, willekeurige alfanumerieke waarde. Bijvoorbeeld: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Deze alpha numerieke waarde is een door het systeem gegenereerde, willekeurige tekenreeks die is toegewezen aan een samenvoegbeleid-id van een van de samenvoegbeleidsregels die door uw organisatie zijn gemaakt. De afbeelding van elke identiteitskaart van het fusiebeleid aan zijn verwante reeks van de profielkenmerkdataset wordt gehandhaafd in de `adwh_dim_merge_policies` dataset.

De `adwh_dim_merge_policies` dataset bevat de volgende gebieden:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Deze dataset kan worden onderzocht gebruikend de Redacteur UI van de Vraag in Experience Platform. Meer over het gebruiken van de Redacteur van de Vraag, verwijs naar [de gids UI van de Redacteur van de Vraag](../query-service/ui/user-guide.md).

### Gegevensset voor segmentmetagegevens

Er is een dataset van segmentmeta-gegevens beschikbaar in het gegevensmeer die meta-gegevens voor elk van de segmenten van uw organisatie bevatten.

De naamgevingsconventie van deze gegevensset is **Segmentdefinition-Snapshot-Export** gevolgd door een alfanumerieke waarde. Bijvoorbeeld: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Om het volledige schema van elke de uitvoerdataset van de segmentdefinitiemomentopname te begrijpen, kunt u voorproef en de datasets [onderzoeken gebruikend de datasetkijker](../catalog/datasets/user-guide.md) in Experience Platform UI.

![](images/query/segment-metadata.png)

### Gegevensset met doelmetagegevens

De meta-gegevens voor elk van de geactiveerde bestemmingen van uw organisatie is beschikbaar als ruwe dataset in het gegevensmeer.

De noemende overeenkomst van deze dataset is **DIM_Destination**.

Om het volledige schema van de DIM bestemmingsdataset te begrijpen, kunt u voorproef en de dataset [onderzoeken gebruikend de datasetkijker](../catalog/datasets/user-guide.md) in Experience Platform UI.

![](images/query/destinations-metadata.png)

## Voorbeeldquery

De volgende voorbeeldvragen omvatten steekproef SQL die in de Dienst van de Vraag kan worden gebruikt om, de ruwe datasets te onderzoeken te verifiëren en te verwerken die uw dashboards aandrijven.

### Aantal profielen op identiteit

Dit profielinzicht verstrekt een verdeling van identiteiten over alle samengevoegde profielen in de dataset.

>[!NOTE]
>
>Het totale aantal profielen op basis van identiteit (met andere woorden, door de waarden voor elke naamruimte bij elkaar op te tellen) kan hoger zijn dan het totale aantal samengevoegde profielen, omdat aan één profiel meerdere naamruimten kunnen zijn gekoppeld. Bijvoorbeeld, als een klant met uw merk op meer dan één kanaal in wisselwerking staat, zullen de veelvoudige namespaces met die individuele klant worden geassocieerd.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Volgende stappen

Door deze gids te lezen, kunt u de Dienst van de Vraag nu gebruiken om verscheidene vragen uit te voeren om de ruwe datasets te onderzoeken en te verwerken die uw profiel, segment, en bestemmingsdashboards aandrijven.

Als u meer wilt weten over elk dashboard en de bijbehorende metriek, selecteert u een dashboard in de lijst met beschikbare dashboards in de documentatienavigatie.
