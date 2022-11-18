---
title: Gegevenssetvoorbeelden
description: De de steekproefdatasets van de Dienst van de vraag laten u toe om verkennende vragen over grote gegevens met zeer gereduceerde verwerkingstijd ten koste van vraagnauwkeurigheid te leiden. Deze gids verstrekt informatie over hoe te om uw steekproeven voor benaderende vraagverwerking te beheren
exl-id: 9e676d7c-c24f-4234-878f-3e57bf57af44
source-git-commit: 9d543b5c7c7f39e809b6a13b8adc46b9a99f51c7
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# (Beperkte release) Gegevenssetvoorbeelden

>[!IMPORTANT]
>
>De eigenschap van de gegevenssetsteekproeven is momenteel in een beperkte versie en niet beschikbaar aan alle klanten.

De Dienst van de Vraag van Adobe Experience Platform verstrekt steekproefdatasets als deel van zijn benaderende mogelijkheden van de vraagverwerking. Voorbeeldgegevenssets worden gemaakt met uniforme willekeurige steekproeven op basis van bestaande [!DNL Azure Data Lake Storage] (ADLS) datasets die slechts een percentage van verslagen van origineel gebruiken. Dit percentage staat bekend als de bemonsteringsfrequentie. Als u de samplingfrequentie aanpast om de balans tussen nauwkeurigheid en verwerkingstijd te bepalen, kunt u verkennende query&#39;s uitvoeren op grote gegevens met een aanzienlijk kortere verwerkingstijd, wat ten koste gaat van de nauwkeurigheid van de query.

Aangezien vele gebruikers geen nauwkeurig antwoord voor een gezamenlijke verrichting over een dataset nodig hebben, is het uitgeven van een benaderende vraag om een benaderend antwoord terug te keren efficiënter voor verkennende vragen over grote datasets. Aangezien de steekproefdatasets slechts een percentage van de gegevens van de originele dataset bevatten, laat het u toe om vraagnauwkeurigheid voor een betere reactietijd te ruilen. Bij read-time, moet de Dienst van de Vraag minder rijen aftasten die sneller resultaten dan veroorzaakt als u de volledige dataset moest vragen.

Om u te helpen uw steekproeven voor benaderende vraagverwerking beheren, steunt de Dienst van de Vraag de volgende verrichtingen voor datasetsteekproeven:

- [Maak een uniforme steekproef voor willekeurige gegevenssets.](#create-a-sample)
- [Bekijk de lijst van steekproeven voor een lijst ADLS.](#view-list-of-samples)
- [Vraag de steekproefdatasets direct.](#query-sample-datasets)
- [Verwijder een voorbeeld.](#delete-a-sample)
- Verwijder gekoppelde samples wanneer de oorspronkelijke ADLS-tabel wordt verwijderd.

## Aan de slag

Om de ongeveer hierboven gedetailleerde mogelijkheden van de vraagverwerking te gebruiken, moet u de zittingsvlag plaatsen aan `true`. Van de bevellijn van of de Redacteur van de Vraag of uw cliënt PSQL gaat de `SET aqp=true;` gebruiken.

>[!NOTE]
>
>U moet de zittingsvlag toelaten telkens als u login aan Platform.

![De redacteur van de Vraag met &quot;VASTGESTELDE qp=true;&quot;benadrukt bevel.](../images/sql/set-session-flag.png)

## Een uniforme steekproef voor een willekeurige gegevensset maken {#create-a-sample}

Gebruik de `ANALYZE TABLE` bevel met een datasetnaam om een eenvormige willekeurige steekproef van die dataset tot stand te brengen.

Het steekproeftarief is het percentage verslagen die van de originele dataset worden genomen. U kunt de samplefrequentie bepalen met de `TABLESAMPLE SAMPLERATE` trefwoorden. In dit voorbeeld komt de waarde 5,0 overeen met een bemonsteringsfrequentie van 50%. Een waarde van 2,5 komt overeen met 25% enzovoort.

>[!IMPORTANT]
>
>Het systeem staat maximaal vijf steekproeven voor elke dataset toe. Als u probeert om een zesde steekproefdataset tot stand te brengen, verschijnt een foutenmelding op het scherm die dat de steekproefgrens is bereikt.

```sql
ANALYZE TABLE example_dataset_name TABLESAMPLE SAMPLERATE 5.0;
```

## De lijst met voorbeelden weergeven {#view-list-of-samples}

Gebruik de `sample_meta()` gebruiken om de lijst met voorbeelden weer te geven die aan een ADLS-tabel zijn gekoppeld.

```sql
SELECT sample_meta('example_dataset_name')
```

De lijst van datasetsteekproeven wordt getoond in het formaat van het hieronder voorbeeld.

```shell
                  sample_table_name                  |    sample_dataset_id     |    parent_dataset_id     | sample_type | sampling_rate | sample_num_rows |       created      
-----------------------------------------------------+--------------------------+--------------------------+-------------+---------------+-----------------+---------------------
 x5e5cd8ea0a83c418a8ef0928_uniform_4_0_percent_ughk7 | 62ff19853d338f1c07b18965 | 5e5cd8ea0a83c418a8ef0928 | uniform     |           4.0 |             391 | 19/08/2022 05:03:01
(1 row)
```

## Vraag de steekproefdataset {#query-sample-datasets}

Gebruik de `{EXAMPLE_DATASET_NAME}` om steekproeflijsten direct te vragen. U kunt ook de opdracht `WITHAPPROXIMATE` sleutelwoord aan het eind van een vraag en de Dienst van de Vraag gebruikt automatisch de onlangs gecreeerd steekproef.

```sql
SELECT * FROM example_dataset_name WITHAPPROXIMATE;
```

## Gegevenssetvoorbeelden verwijderen {#delete-a-sample}

De schrappingsverrichting staat u toe om nieuwe steekproeven tot stand te brengen zodra de maximumgrens van vijf datasetsteekproeven is bereikt.

```sql
DROP TABLE SAMPLE x5e5cd8ea0a83c418a8ef0928_uniform_2_0_percent_bnhmc;
```

>[!NOTE]
>
>Als u veelvoudige steekproefdatasets hebt die uit een originele dataset van ADLS worden afgeleid, wanneer origineel wordt gelaten vallen alle bijbehorende steekproeven ook worden geschrapt.
