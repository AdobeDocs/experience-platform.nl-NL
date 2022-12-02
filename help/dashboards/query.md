---
solution: Experience Platform
title: Datasets van het dashboard verkennen, verifiëren en verwerken met de Query-service
type: Documentation
description: Leer hoe te om de Dienst van de Vraag te gebruiken om ruwe datasets te onderzoeken en te verwerken die profiel, segment, en bestemmingsdashboards in Experience Platform aandrijven.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: 4826731682bcaf5a43c7ce047220c1805d97243a
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 0%

---

# Ontdek, verifieer en proces dashboarddatasets gebruikend [!DNL Query Service]

Adobe Experience Platform verstrekt belangrijke informatie over het profiel van uw organisatie, segment, en bestemmingsgegevens door dashboards beschikbaar binnen de UI van het Experience Platform. U kunt dan Adobe Experience Platform gebruiken [!DNL Query Service] om, de ruwe datasets te onderzoeken te verifiëren en te verwerken die deze dashboards in het gegevensmeer aandrijven.

## Aan de slag met [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] steunt marketers in het verkrijgen van inzichten van hun gegevens door het gebruik van standaardSQL toe te laten om gegevens in het gegevensmeer te vragen. [!DNL Query Service] biedt een gebruikersinterface en API aan die kunnen worden gebruikt om zich bij om het even welke dataset in het gegevensmeer aan te sluiten en de vraagresultaten als nieuwe datasets voor gebruik in rapportering, machine het leren, of voor opname in het Profiel van de Klant in real time te vangen.

Meer informatie over [!DNL Query Service] en zijn rol binnen het Experience Platform , gelieve eerst te lezen [[!DNL Query Service] overzicht](../query-service/home.md).

## Toegang tot beschikbare gegevenssets

U kunt [!DNL Query Service] om ruwe datasets voor profiel, segment, en bestemmingsdashboards te vragen. Om uw beschikbare datasets, in het Experience Platform UI te bekijken, selecteer **Gegevenssets** in de linkernavigatie om het dashboard van Datasets te openen. Het dashboard maakt een lijst van alle beschikbare datasets voor uw organisatie. De details worden getoond voor elke vermelde dataset, met inbegrip van zijn naam, het schema de dataset zich aan, en het statuut van de meest recente opnamelooppas aansluit.

![De Dataset doorbladert dashboard met het lusje van Datasets die in de linkernavigatie wordt benadrukt.](./images/query/browse-datasets.png)

### Door het systeem gegenereerde gegevenssets

>[!IMPORTANT]
>
>Door het systeem gegenereerde gegevenssets worden standaard verborgen. Standaard worden de [!UICONTROL Browse] het lusje toont slechts datasets die u gegevens in hebt opgenomen.

Om systeem-geproduceerde datasets te bekijken, selecteer het filterpictogram (![Een filterpictogram.](./images/query/filter.png)) links van de zoekbalk.

![Het tabblad Datasets Bladeren met het filterpictogram gemarkeerd.](./images/query/filter-datasets.png)

Er verschijnt een zijbalk met twee schakelingen. [!UICONTROL Included in Profile] en [!UICONTROL Show system datasets]. De schakeloptie selecteren voor [!UICONTROL Show system datasets] om systeem-geproduceerde datasets binnen de doorbladerbare lijst van datasets te omvatten.

![De Datasets doorbladeren tabel met de gemarkeerde schakeloptie voor systeemdatasets weergeven.](./images/query/show-system-datasets.png)

### Gegevensbestanden van profielkenmerken

De dashboardinzichten van het profiel zijn gebonden aan fusiebeleid dat door uw organisatie is bepaald. Voor elk actief fusiebeleid, is er een dataset van profielattributen beschikbaar in het gegevenspeer.

De naamgevingsconventie van deze gegevenssets is **Profile-Snapshot-export** gevolgd door een door het systeem gegenereerde, willekeurige alfanumerieke waarde. Bijvoorbeeld: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Om het volledige schema van elke de uitvoerdataset van de profielmomentopname te begrijpen, kunt u voorproef en de datasets onderzoeken [het gebruiken van de datasetkijker](../catalog/datasets/user-guide.md) in de gebruikersinterface van het Experience Platform.

![Een voorvertoning van de gegevensset Profielmomentopname-Exporteren.](images/query/profile-attribute.png)

#### Gegevenssets van profielkenmerken toewijzen om beleid-id&#39;s samen te voegen

De alfanumerieke waarde die wordt toegewezen aan elke door het systeem gegenereerde profielkenmerkgegevensset is een willekeurige tekenreeks die wordt toegewezen aan een samenvoegbeleid-id van een van de samenvoegbeleidsregels die door uw organisatie worden gemaakt. De afbeelding van elke identiteitskaart van het fusiebeleid aan zijn verwante koord van de de gegevensreeks van profielattributen wordt gehandhaafd in `adwh_dim_merge_policies` dataset.

De `adwh_dim_merge_policies` dataset bevat de volgende velden:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Deze dataset kan worden onderzocht gebruikend de Redacteur UI van de Vraag in Experience Platform. Als u meer wilt weten over het gebruik van de Query Editor, raadpleegt u de [Handleiding voor de Query Editor](../query-service/ui/user-guide.md).

### Gegevensset voor segmentmetagegevens

Er is een dataset van segmentmeta-gegevens beschikbaar in het gegevensmeer die meta-gegevens voor elk van de segmenten van uw organisatie bevatten.

De naamgevingsconventie van deze gegevensset is **Segmentdefinition-Snapshot-export** gevolgd door een alfanumerieke waarde. Bijvoorbeeld: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Om het volledige schema van elke de uitvoerdataset van de segmentdefinitiemomentopname te begrijpen, kunt u voorproef en de datasets onderzoeken [het gebruiken van de datasetkijker](../catalog/datasets/user-guide.md) in de gebruikersinterface van het Experience Platform.

![Een voorvertoning van de dataset Segmentdefinition-Snapshot-Export.](images/query/segment-metadata.png)

### Gegevensset met doelmetagegevens

De meta-gegevens voor elk van de geactiveerde bestemmingen van uw organisatie is beschikbaar als ruwe dataset in het gegevensmeer.

De naamgevingsconventie van deze gegevensset is **DIM_Doel**.

Om het volledige schema van de DIM bestemmingsdataset te begrijpen, kunt u voorproef en de dataset onderzoeken [het gebruiken van de datasetkijker](../catalog/datasets/user-guide.md) in de gebruikersinterface van het Experience Platform.

![Een voorvertoning van de gegevensset DIM_Destination.](images/query/destinations-metadata.png)

## (Beta) CDP-rapporten (Customer Data Platform)

>[!IMPORTANT]
>
>De eigenschap van de Modellen van Gegevens van Gegevens CDP van Inzichten is in bèta. De kenmerken en documentatie van het programma kunnen worden gewijzigd.

De eigenschap van de Modellen van Gegevens van Gegevens CDP van Inzichten stelt SQL bloot die de inzichten voor diverse profiel, bestemming en segmentatiewidgets drijft. U kunt deze SQl vraagmalplaatjes aanpassen om CDP- rapporten voor uw marketing en KPI gebruiksgevallen tot stand te brengen.

CDP het melden verstrekt inzichten in uw profielgegevens en zijn verhouding met segmenten en bestemmingen. Zie de CDP documentatie van het Gegevensmodel van Inzichten voor gedetailleerde informatie over hoe te [Pas de CDP Modellen van Gegevens van Inzichten op uw specifieke KPI gebruiksgevallen toe](./cdp-insights-data-model.md).

## Voorbeeldquery

De volgende voorbeeldvragen omvatten voorbeeld SQL dat in kan worden gebruikt [!DNL Query Service] om, de ruwe datasets te onderzoeken te verifiëren en te verwerken die uw dashboards aandrijven.

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

Door deze handleiding te lezen, kunt u nu [!DNL Query Service] om verscheidene vragen uit te voeren om de ruwe datasets te onderzoeken en te verwerken die uw profiel, segment, en bestemmingsdashboards aandrijven.

Als u meer wilt weten over elk dashboard en de bijbehorende metriek, selecteert u een dashboard in de lijst met beschikbare dashboards in de documentatienavigatie.
