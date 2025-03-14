---
solution: Experience Platform
title: Datasets van het dashboard verkennen, verifiëren en verwerken met de Query-service
type: Documentation
description: Leer hoe te om de Dienst van de Vraag te gebruiken om ruwe datasets te onderzoeken en te verwerken die profiel, publiek, en bestemmingsdashboards in Experience Platform aandrijven.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '934'
ht-degree: 0%

---

# Gegevenssets van dashboard verkennen, verifiëren en verwerken met [!DNL Query Service]

Adobe Experience Platform verstrekt belangrijke informatie over het profiel van uw organisatie, publiek, en bestemmingsgegevens door dashboards beschikbaar binnen de UI van het Experience Platform. Vervolgens kunt u Adobe Experience Platform [!DNL Query Service] gebruiken om de onbewerkte gegevenssets te verkennen, te verifiëren en te verwerken, waarmee deze dashboards in het datumpeer worden geactiveerd.

## Aan de slag met [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] ondersteunt marketers bij het verkrijgen van inzicht uit hun gegevens door het gebruik van standaard SQL voor het zoeken naar gegevens in het datumpeer mogelijk te maken. [!DNL Query Service] biedt een gebruikersinterface en een API aan die kunnen worden gebruikt om zich bij om het even welke dataset in het gegevensmeer aan te sluiten en de vraagresultaten als nieuwe datasets voor gebruik in rapportering, machine het leren, of voor opname in het Profiel van de Klant in real time vast te leggen.

Meer over [!DNL Query Service] en zijn rol binnen Experience Platform leren, gelieve te beginnen door het [[!DNL Query Service]  overzicht ](../query-service/home.md) te lezen.

## Toegang tot beschikbare gegevenssets

U kunt [!DNL Query Service] gebruiken om onbewerkte datasets voor profiel, publiek, en bestemmingsdashboards te vragen. Om uw beschikbare datasets, in het Experience Platform UI te bekijken, selecteer **Datasets** in de linkernavigatie om het dashboard van Datasets te openen. Het dashboard maakt een lijst van alle beschikbare datasets voor uw organisatie. De details worden getoond voor elke vermelde dataset, met inbegrip van zijn naam, het schema de dataset zich aan, en het statuut van de meest recente opnamelooppas aansluit.

![ Dataset doorbladert dashboard met het lusje van Datasets dat in de linkernavigatie wordt benadrukt.](./images/query/browse-datasets.png)

### Door het systeem gegenereerde gegevenssets {#system-generated-datasets}

>[!IMPORTANT]
>
>Door het systeem gegenereerde gegevenssets worden standaard verborgen. Standaard bevat het tabblad [!UICONTROL Browse] alleen gegevenssets waarin u gegevens hebt ingevoerd.

Om systeem-geproduceerde datasets te bekijken, selecteer het filterpictogram (![ A filterpictogram.](/help/images/icons/filter.png) ) links van de zoekbalk.

![ de Datasets doorbladeren lusje met het benadrukte filterpictogram.](./images/query/filter-datasets.png)

Er wordt een zijbalk weergegeven met twee schakelingen, [!UICONTROL Included in Profile] en [!UICONTROL Show system datasets] . Selecteer de knevel voor [!UICONTROL Show system datasets] om systeem-geproduceerde datasets binnen de doorbladerbare lijst van datasets te omvatten.

![ de Datasets doorbladeren lusje met de van de systeemdatasets van de Show benadrukte knevel.](./images/query/show-system-datasets.png)

### Gegevensbestanden van profielkenmerken {#profile-attribute-datasets}

De dashboardinzichten van het profiel zijn gebonden aan fusiebeleid dat door uw organisatie is bepaald. Voor elk actief fusiebeleid, is er een dataset van profielattributen beschikbaar in het gegevenspeer.

De noemende overeenkomst van deze datasets is **profiel-Snapshot-Uitvoer** die door een systeem-geproduceerde, willekeurige alpha numerieke waarde wordt gevolgd. Bijvoorbeeld: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f` .

Om het volledige schema van elke de uitvoerdataset van de profielmomentopname te begrijpen, kunt u voorproef en de datasets [ onderzoeken gebruikend de datasetkijker ](../catalog/datasets/user-guide.md) in Experience Platform UI.

![ een voorproef van de profiel-Momentopname-Uitvoer dataset.](images/query/profile-attribute.png)

#### Gegevenssets van profielkenmerken toewijzen om beleid-id&#39;s samen te voegen

De alfanumerieke waarde die wordt toegewezen aan elke door het systeem gegenereerde profielkenmerkgegevensset is een willekeurige tekenreeks die wordt toegewezen aan een samenvoegbeleid-id van een van de samenvoegbeleidsregels die door uw organisatie worden gemaakt. De toewijzing van elke identiteitskaart van het fusiebeleid aan zijn verwante reeks van de profielkenmerkdataset wordt gehandhaafd in de `adwh_dim_merge_policies` dataset.

De gegevensset `adwh_dim_merge_policies` bevat de volgende velden:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Deze dataset kan worden onderzocht gebruikend de Redacteur UI van de Vraag in Experience Platform. Meer leren over het gebruiken van de Redacteur van de Vraag, verwijs naar de [ gids UI van de Redacteur van de Vraag ](../query-service/ui/user-guide.md).

### Gegevensset met metagegevens van publiek

Er is een dataset van publieksmeta-gegevens beschikbaar in het gegevensmeer die meta-gegevens voor elk van uw publiek van organisatie bevatten.

De noemende overeenkomst van deze dataset is **Segmentdefinition-momentopname-Uitvoer** die door een alpha numerieke waarde wordt gevolgd. Bijvoorbeeld: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Om het volledige schema van elke de uitvoerdataset van de segmentdefinitiemomentopname te begrijpen, kunt u voorproef en de datasets [ onderzoeken gebruikend de datasetkijker ](../catalog/datasets/user-guide.md) in Experience Platform UI.

### Gegevensset met doelmetagegevens

De meta-gegevens voor elk van de geactiveerde bestemmingen van uw organisatie is beschikbaar als ruwe dataset in het gegevensmeer.

De noemende overeenkomst van deze dataset is **DIM_Destination**.

Om het volledige schema van de DIM bestemmingsdataset te begrijpen, kunt u voorproef en de dataset [ onderzoeken gebruikend de datasetkijker ](../catalog/datasets/user-guide.md) in Experience Platform UI.

![ een voorproef van de dataset DIM_Destination.](images/query/destinations-metadata.png)

## CDP-inzichtsrapporten (Customer Data Platform)

De eigenschap van de Modellen van Gegevens van Gegevens CDP van Inzichten stelt SQL bloot die de inzichten voor diverse profiel, bestemming en segmentatiewidgets drijft. U kunt deze SQl vraagmalplaatjes aanpassen om CDP- rapporten voor uw marketing en KPI gebruiksgevallen tot stand te brengen.

CDP het melden verstrekt inzichten in uw profielgegevens en zijn verhouding met publiek en bestemmingen. Zie de CDP documentatie van het Model van Gegevens van Inzichten voor gedetailleerde informatie over hoe te [ de Modellen van Gegevens CDP van Inzichten op uw bijzondere KPI gebruiksgevallen ](./data-models/cdp-insights-data-model-b2c.md) toepassen.

## Voorbeeldquery

De volgende voorbeeldquery&#39;s bevatten voorbeeld-SQL die in [!DNL Query Service] kan worden gebruikt om de onbewerkte datasets die uw dashboards bedienen, te verkennen, te verifiëren en te verwerken.

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

### Aantal profielen per publiek

Dit publieksinzicht verstrekt het totale aantal samengevoegde profielen binnen elk publiek in de dataset. Dit aantal is het resultaat van het toepassen van het beleid van de publiekssamenvoeging op uw gegevens van het Profiel om profielfragmenten samen te voegen om één enkel profiel voor elk individu in het publiek te vormen.

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## Volgende stappen

Door deze gids te lezen, kunt u [!DNL Query Service] nu gebruiken om verscheidene vragen uit te voeren om de ruwe datasets te onderzoeken en te verwerken die uw profiel, publiek, en bestemmingsdashboards aandrijven.

Als u meer wilt weten over elk dashboard en de bijbehorende metriek, selecteert u een dashboard in de lijst met beschikbare dashboards in de documentatienavigatie.
