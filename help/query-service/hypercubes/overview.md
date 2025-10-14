---
title: Efficiënte grootse gegevensanalyse met hyperkubussen in Experience Query Service
description: Leer hoe u hyperkubussen in Adobe Experience Platform Query Service kunt gebruiken om de analyse van grote gegevens te optimaliseren met een unieke telling, waardoor de behoefte aan volledige gegevensverwerking afneemt.
source-git-commit: 67d4bcbf2a055d4427218ba7d98355f09d860a8c
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 1%

---

# Efficiënte grote gegevensanalyse met hyperkubussen

>[!AVAILABILITY]
>
>Deze functionaliteit is slechts beschikbaar aan gebruikers die [&#x200B; Gegevens Distiller SKU &#x200B;](../data-distiller/overview.md) hebben gekocht. Neem contact op met uw Adobe voor meer informatie.

Leer hoe u hyperkubussen kunt gebruiken in de Adobe Experience Platform Experience Query Service om geavanceerde gegevensanalyse met verbeterde efficiëntie uit te voeren. Dit document behandelt hoe te om geavanceerde functies van de [[!DNL Apache Datasketches]  bibliotheek &#x200B;](https://datasketches.apache.org/) te gebruiken om afzonderlijke tellingen en complexe berekeningen incrementeel te behandelen, zonder het moeten historische gegevens telkens opnieuw verwerken.

In de analyse van grote gegevens, impliceert het produceren van metriek zoals verschillende tellingen, aantallen, meest frequente punten, verbindingen, en grafiekanalyse vaak niet-additieve tellingen (waar de resultaten niet eenvoudig kunnen worden samengevat uit subgroepen). Traditionele methoden vereisen de opwerking van alle historische gegevens, die een intensieve en tijdrovende bron kunnen zijn. De schetsen van het gebruik, die compacte overzichten zijn die waarschijnlijkheden gebruiken om grote datasets te vertegenwoordigen, en de geavanceerde functies van de Dienst van de Vraag om dit proces te stroomlijnen door de behoefte aan herberekening te verminderen.

## Belangrijke functies van hyperkubussen {#key-functions}

Hyperkubussen bieden verschillende krachtige functies om de efficiëntie en flexibiliteit van gegevensanalyse te verbeteren.

1. **Aantal unieke gebruikers of verschillende vragen**: SQL van het gebruik mogelijkheden om unieke tellingen van gebruikers te produceren die met diverse afmetingen van gegevens, zoals productmeningen, plaatsbezoeken, of handelsactiviteit interactie aangaan, zonder herhaaldelijk het opnieuw analyseren van ruwe gegevens.
2. **Incrementele verwerking**: Voer stijgende updates uit om gegevenspunten over dimensies en tijd te voeden en samen te voegen zonder alles van kras opnieuw te berekenen.
3. **Multidimensionale analyse**: De hyperkubussen laten multi-dimensionaal filtreren en het herschikken van gegevens toe om summiere rijen tot stand te brengen die combinaties van dimensies vertegenwoordigen. Deze samenvattingen kunnen dan worden gebruikt om inzichten met minimale berekeningsoverheadkosten te produceren.

## Gebruik hoofdletters/kleine letters voor hyperkubussen {#use-cases}

Met hyperkubussen kunt u op efficiënte wijze duidelijke tellingen genereren voor verschillende gebruikersinteracties zonder dat de gegevens telkens opnieuw worden berekend. Hieronder volgen enkele praktische scenario&#39;s voor het gebruik ervan:

- Analyseer unieke bezoekers die specifieke producten tijdens een bepaalde tijdsperiode bekijken.
- Identificeer gebruikers die in een bepaalde periode met meerdere producten in wisselwerking staan om cross-sell analyse te verbeteren.
- Duidelijk gebruikers die met één product maar niet een andere in tijd werken om voorkeurspatronen te ontdekken.
- Combineer online en off-line interactiegegevens om een uitvoerige mening van gebruikersgedrag over een bepaalde periode te krijgen.
- Houd gebruikersbewegingen bij verschillende activiteiten binnen een gebeurtenis om de lay-out en services te optimaliseren.

## Voordelen van het gebruik van hyperkubussen

In deze situaties kunt u basisgegevens vooraf berekenen voor specifieke categorieën. Nochtans, wanneer het analyseren van gegevens over veelvoudige dimensies en tijdsperioden, moet u of alles van ruwe gegevens opnieuw berekenen of een hyperkubus van de Dienst van de Vraag gebruiken. Hyperkubussen stroomlijnen het proces door gegevens efficiënt te ordenen, wat flexibele filtering en multidimensionale analyse zonder opwerking mogelijk maakt. Zij gebruiken geavanceerde functies om resultaten snel en nauwkeurig te schatten om zeer belangrijke voordelen zoals betere verwerkingsefficiency, scalability, en aanpassingsvermogen voor complexe analytische taken aan te bieden.

### Efficiëntie voor gegevensgrootte voor queryverwerking

De Dienst van de vraag kan miljoenen of miljarden gegevenspunten (bijvoorbeeld, gebruiker IDs) in een compacte vorm samenpersen genoemd een schets. Deze schets heeft een beduidend gereduceerde gegevensgrootte voor vraagverwerking, die scalability handhaaft en het veel gemakkelijker en sneller maakt om met te werken. Hoe groot de oorspronkelijke gegevens ook zijn, de grootte van de schets blijft klein, waardoor het analyseren van grote gegevens veel beheerbaarder en efficiënter wordt.

In het onderstaande diagram ziet u hoe Commerce, Product Info en Web Dimension ExperienceEvents worden verwerkt in schetsen, die vervolgens worden gebruikt om unieke aantallen te benaderen.

![&#x200B; Infographic die de verwezenlijking van schetsen gebruikend de Dienst van de Vraag tonen. Het diagram illustreert hoe ExperienceEvents met Commerce, Info van het Product, en de afmetingen van het Web in schetsen worden verwerkt, die dan worden gebruikt om unieke tellingen te benaderen.](../images/hypercubes/hypercube-overview.png)

### Schetsen samenvoegen om gegevensanalyse sneller en eenvoudiger te maken

U voorkomt herberekening en verbeterde verwerkingssnelheid door schetsen van verschillende categorieën of groepen samen te voegen. De Dienst van de vraag vereenvoudigt ook het ontwerp door uw gegevens in een hyperkubus te organiseren, waar elke rij een samenvatting van zijn verdeling (een inzameling van afmetingen) naast de schetskolom wordt. Elke rij van de hyperkubus bevat de dimensiecombinatie maar heeft geen onbewerkte gegevens. Wanneer het uitvoeren van een vraag, specificeer de dimensionele kolommen u voor de bouw van additieve metriek wilt gebruiken en de schetsen voor die rijen samenvoegen.

![&#x200B; het diagram toont hoe de schetsen van verschillende ExperienceEvents worden samengevoegd om tot benaderende unieke tellingen over diverse afmetingen te leiden.](../images/hypercubes/merge-sketches.png)

### Kosteneffectiviteit {#cost-effectiveness}

De gegevens van de klant zijn vaak grootschalig, maar u kunt de behoefte elimineren om historische gegevens door stijgende verwerking te gebruiken opnieuw te verwerken. Schetsen zijn veel kleiner en bieden snellere, real-time resultaten en besparen tegelijk op computerbronnen en kosten. Deze gegevenstransformatie maakt interactieve vragen uitvoerbaarder en efficiënter.

## Overzicht functies

In deze sectie wordt beschreven hoe elke functie gegevensverwerking optimaliseert en analytische mogelijkheden verbetert door efficiënt gebruik van schetsen en hyperkubussen. Het detailleert hun doel, voorbeeldsyntaxis, parameters, en verwachte output.

### Unieke telschattingen maken met HLL-schetsen

`hll_build_agg` is een geaggregeerde functie die een HLL-schets (HyperLogLog) maakt. Deze functie is een compacte, probabilistische methode om het aantal unieke waarden binnen een kolom of een uitdrukking in een gegroepeerde dataset te schatten.

#### Functiedefinitie

```sql
hll_build_agg(column [, lgConfigK])
```

**Gebruik:**

In het volgende voorbeeld wordt getoond hoe de functie binnen een query kan worden gestructureerd.

```sql
SELECT
   [dim1, dim2 ... ,] hll_build_agg(coalesce(col1, col2, col3)) AS sketch_col
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parameters

| Parameter | Beschrijving |
|---------------------------|---------------------------------------|
| `column` | De kolom- of kolomnaam waarop een schets moet worden gemaakt. |
| `lgConfigK` | *Int* (Facultatief) logboek-basis-2 van K, waar K het aantal emmers of groeven voor de Schets van de HULLING is. Min. waarde: 4. Max. waarde: 12. Standaardwaarde: 12. |

#### Uitvoer

| Uitvoerkolom | Beschrijving |
|---------------------------|---------------------------------------|
| `sketch_res` | Een kolom van het type die de stringified HLL-schets bevat. |

#### SQL-voorbeeld

In het volgende voorbeeld wordt een geaggregeerde schets gemaakt op de kolom `customer_id` :

```sql
SELECT
  country,
  hll_build_agg(customer_id, 10) AS sketch
FROM
  EXPLODE(
    ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
      ('UA', 'customer_id_1', 'invoice_id_11'),
      ('CZ', 'customer_id_2', 'invoice_id_22'),
      ('CZ', 'customer_id_2', 'invoice_id_23'),
      ('BR', 'customer_id_3', 'invoice_id_31'),
      ('UA', 'customer_id_2', 'invoice_id_24')
    ])
GROUP BY country;
```

**SQL voorbeeldoutput:**

| Land | Schets |
|---------|------------------------------------------------------------|
| UA | AgEHBAMAAgCR9mUEulKKCQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA= |
| CZ | AgEHBAMAAQC6UooJAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA= |
| BR | AgEHBAMAAQCcmH0HAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA= |

### De verschillende tellingen met HLL-schetsen schatten

`hll_estimate` is een scalaire functie die een schatting van de verschillende telling binnen elke rij van een dataset verstrekt. In tegenstelling tot statistische functies werkt `hll_estimate` rijsgewijs en wordt het gebruikt voor het schatten van het aantal elementen dat wordt onderscheiden van een schets binnen afzonderlijke rijen.

>[!NOTE]
>
>Deze functie kan niet worden gebruikt als een geaggregeerde functie. Gebruik `sketch_count` voor geaggregeerde tellingen.

#### Functiedefinitie

```sql
hll_estimate(sketch_col)
```

**Gebruik:**

In het volgende voorbeeld wordt getoond hoe de functie binnen een query kan worden gestructureerd.

```sql
SELECT
   [col1, col2 ... ,] hll_estimate(sketch_column) AS estimate
FROM fact_sketch_table
```

#### Parameters

| Parameter | Beschrijving |
|---------------------------|---------------------------------------|
| `sketch_column` | Kolom met een verstrengde HLL-schets. Het schat de verschillende telling voor de schets in elke rij. |

#### Uitvoer

| Uitvoerkolom | Beschrijving |
|---------------------------|---------------------------------------|
| `estimate` | Een kolom van type dubbel die de schatting van de schets, rond aan twee decimale plaatsen verstrekt. |

#### SQL-voorbeeld

In het volgende voorbeeld wordt het aantal klanten per land bepaald met behulp van de functie `hll_estimate` op een HLL-schets:

```sql
SELECT
  country,
  hll_estimate(hll_build_agg(customer_id, 10)) AS distinct_customers_by_country
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id, 10) AS sketch
    FROM 
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
  );
```

**SQL Uitvoer van het Voorbeeld:**

| Land | different_customer_by_country |
|---------|-------------------------------|
| UA | 2,00 |
| CZ | 1,00 |
| BR | 1,00 |

### Meerdere HLL-schetsen samenvoegen met `hll_merge_agg`

`hll_merge_agg` is een geaggregeerde functie waarmee meerdere HLL-schetsen in een groep worden samengevoegd. Hierdoor wordt een nieuwe schets als uitvoer gegenereerd. Het maakt de combinatie van schetsen tussen verdelingen of dimensies mogelijk, waardoor de flexibiliteit van gegevensanalyse wordt vergroot.

#### Functiedefinitie

```sql
hll_merge_agg(sketch_col [, allowDifferentLgConfigK])
```

**Gebruik:**

In het volgende voorbeeld wordt getoond hoe de functie binnen een query kan worden gestructureerd.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_agg(sketch_column.sketch) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parameters

| Parameter | Beschrijving |
|---------------------------|---------------------------------------|
| `sketch_column` | Kolom met de stringified HLL-schets. |
| `allowDifferentLgConfigK` | *Van Boole* (Facultatief) als reeks aan waar, staat het samenvoegen van schetsen met verschillende `lgConfigK` waarden toe. De standaardwaarde is false. Er wordt een uitzondering gegenereerd wanneer de waarde false is en schetsen andere `lgConfigK` -waarden hebben. |

>[!NOTE]
>
>Als `allowDifferentLgConfigK` is ingesteld op false, resulteert het samenvoegen van schetsen met verschillende `lgConfigK` -waarden in een `UnsupportedOperationException` .

#### Uitvoer

| Uitvoerkolom | Beschrijving |
|----------------|-------------------------------------------------|
| `sketch_res` | Een kolom van het type HLL-schets die de verstrengde samengevoegde HLL-schets bevat. |

#### SQL-voorbeeld

In het volgende voorbeeld worden meerdere HLL-schetsen samengevoegd in de kolom `customer_id` :

```sql
SELECT
   hll_merge_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**SQL Uitvoer van het Voorbeeld:**

| Land | hll_merge_agg(sketch, true) |
|---------|--------------------------------------------|
| UA | AgEHDAMAAwiR9mUEulKKCQAAAAAAAAAAAAAA= |
| CZ | AgEHDAMAAQi6UooJAAAAAAAAAAAAAAAAAAAAAAAAAA== |
| BR | AgEHDAMAAQicmH0HAAAAAAAAAAAAAAAAAAAAAAAA== |
| MX | AgEHFQMAAgiGL/kNdAAAAAAAAAAAAAAAAAAAAAAAAA= |

### Kardinaliteit schatten met `hll_merge_count_agg`

`hll_merge_count_agg` is een statistische functie die de kardinaliteit (aantal unieke elementen) schat van een of meer schetsen in een kolom. Er wordt één schatting geretourneerd voor alle schetsen die binnen de groep worden aangetroffen. Deze functie wordt gebruikt voor het samenvoegen van schetsen en kan niet worden gebruikt als een rijgewijze transformatie. Gebruik `sketch_estimate` voor rijsgewijze schattingen.

#### Functiedefinitie

```sql
hll_merge_count_agg(sketch_col [, allowDifferentLgConfigK])
```

**Gebruik:**

In het volgende voorbeeld wordt getoond hoe de functie binnen een query kan worden gestructureerd.

```sql
SELECT
   [dim1, dim2 ... ,] hll_merge_count_agg(sketch_column) AS estimate
FROM fact_sketch_table
  [GROUP BY dimension1, dimension2 ...]
```

#### Parameters

| Parameter | Beschrijving |
|-------------------------|----------------------------------------------|
| `sketch_column` | Een kolom die de stringified HLL-schets bevat. |
| `allowDifferentLgConfigK` | *Van Boole* (Facultatief) de standaardwaarde is vals. Indien true, is het mogelijk om schetsen met verschillende `lgConfigK` -waarden samen te voegen. Anders wordt een `UnsupportedOperationException` gegenereerd. |

#### Uitvoer

| Uitvoerkolom | Beschrijving |
|---------------|----------------------------------------------------------|
| `estimate` | Een kolom van type Double met een schatting van de schets. |

#### SQL-voorbeeld

In het volgende voorbeeld wordt het aantal unieke klanten met facturen geschat dat de functie `hll_merge_count_agg` gebruikt:

```sql
SELECT
   hll_merge_count_agg(hll_sketch) AS uniq_customers_with_invoice
FROM
  (
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_11'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('CZ', 'customer_id_2', 'invoice_id_22'),
          ('CZ', 'customer_id_2', 'invoice_id_23'),
          ('BR', 'customer_id_3', 'invoice_id_31'),
          ('UA', 'customer_id_2', 'invoice_id_24')
        ])
    GROUP BY country
    UNION
    SELECT
      country,
      hll_build_agg(customer_id) AS hll_sketch
    FROM
      EXPLODE(
        ARRAY<STRUCT<country STRING, customer_id STRING, invoice_id STRING>>[
          ('UA', 'customer_id_1', 'invoice_id_21'),
          ('MX', 'customer_id_3', 'invoice_id_31'),
          ('MX', 'customer_id_2', 'invoice_id_21')
        ])
    GROUP BY country
  )
GROUP BY customer_id;
```

**SQL Uitvoer van het Voorbeeld:**

| Land | hll_merge_count_agg(schetch, true) |
|---------|----------------------------------|
| UA | 2,0 |
| CZ | 1,0 |
| BR | 1,0 |
| MX | 2,0 |

## Beperkingen

Schetsen kunnen op dit moment niet worden bijgewerkt als ze eenmaal zijn gemaakt. In toekomstige updates wordt de mogelijkheid geïntroduceerd om schetsen bij te werken. Met deze functionaliteit kunt u gemiste looppas en laat-aankomende gegevens effectiever behandelen.

## Volgende stappen

Door dit document te lezen, weet u nu hoe u hyperkubussen en bijbehorende schetsfuncties kunt gebruiken om efficiënte gegevensverwerking uit te voeren voor complexe, multidimensionale analyses zonder dat u historische gegevens opnieuw hoeft te verwerken. Deze aanpak bespaart tijd, verlaagt de kosten en biedt de flexibiliteit die nodig is voor interactieve realtime query&#39;s, waardoor deze een waardevol instrument zijn voor analyse van grote gegevens in Adobe Experience Platform.

Daarna, onderzoek andere zeer belangrijke concepten zoals [&#x200B; stijgende lading &#x200B;](../key-concepts/incremental-load.md) en [&#x200B; gegevensdeduplicatie &#x200B;](../key-concepts/deduplication.md) om uw begrip van te verdiepen hoe te om deze functies effectief voor uw specifieke gegevensbehoeften te gebruiken.


