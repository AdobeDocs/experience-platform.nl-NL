---
title: Klantencontrole voorspellen met op SQL gebaseerde logistieke regressie
description: Leer hoe te om klantenkroon te voorspellen gebruikend op SQL-Gebaseerde logistieke regressie. Deze gids behandelt het volledige proces van modelverwezenlijking tot evaluatie en voorspelling. Verkrijg actionable inzicht van het gedrag van de klantenaankoop om pro-actieve bewaarstrategieën uit te voeren en bedrijfsbesluiten te optimaliseren.
source-git-commit: 95c7ad3f8eb86cacd42077008824eea9e25b4db0
workflow-type: tm+mt
source-wordcount: '1126'
ht-degree: 0%

---

# Klantencontrole voorspellen met op SQL gebaseerde logistieke regressie

Het voorspellen klantenkroon helpt ondernemingen klanten behouden, middelen optimaliseren, en rentabiliteit verhogen door tevredenheid en loyaliteit door actionable inzichten te verbeteren.

Ontdek hoe u op SQL gebaseerde logistieke regressie kunt gebruiken om het churn van de klant te voorspellen. Gebruik deze uitgebreide SQL-handleiding om onbewerkte e-commercegegevens om te zetten in betekenisvolle klantinzichten op basis van toetsgedragsmaatstaven (zoals aankoopfrequentie, gemiddelde orderwaarde en recenentie van laatste aankoop). Het document behandelt het volledige proces van gegevensvoorbereiding en eigenschapengineering tot modelverwezenlijking, evaluatie, en voorspellingen.

Gebruik deze handleiding om een krachtig model voor de voorspelling van schurnen te bouwen dat klanten met een verhoogd risico identificeert, retentiestrategieën verfijnt en betere bedrijfsbeslissingen aanstuurt. Het omvat geleidelijke instructies, SQL vragen, en gedetailleerde verklaringen om u te helpen machine het leren technieken binnen uw gegevensmilieu op een betrouwbare manier toepassen.

## Aan de slag

Voordat u het churn-model maakt, is het belangrijk dat u de belangrijkste functies en gegevensvereisten van de klant verkent. In de volgende secties worden essentiële klantkenmerken en vereiste gegevensvelden voor een nauwkeurige modeltraining beschreven.

### Klantfuncties definiëren {#define-customer-features}

Het model analyseert aankoopgewoonten en trends om de keten nauwkeurig te classificeren. In de onderstaande tabel worden de belangrijkste gedragskenmerken van de klant beschreven die in het model worden gebruikt:

| Functie | Beschrijving |
|---------------------------|-------------------------------------------------------|
| `total_purchases` | Het totale aantal aankopen dat de klant heeft gedaan. |
| `total_revenue` | De totale opbrengst die van klantenaankopen wordt geproduceerd. |
| `avg_order_value` | De gemiddelde waarde van de aankopen van een klant. |
| `customer_lifetime` | Het aantal dagen tussen de eerste en laatste aankoop van de klant. |
| `days_since_last_purchase` | Het aantal dagen sinds de laatste aankoop van de klant. |
| `purchase_frequency` | Het aantal afzonderlijke maanden waarin de klant aankopen heeft gedaan. |

### Aannames en vereiste velden {#assumptions-required-fields}

Voor het genereren van prognoses voor het aantal kolommen bij de klant, hangt het model af van de belangrijkste velden in de `webevents` -tabel waarin de transactiegegevens van de klant zijn opgenomen. Uw dataset moet de volgende gebieden omvatten:

| Veld | Beschrijving |
|--------------------------------|----------------------------------------------------|
| `identityMap['ECID'][0].id` | Een unieke id die wordt gebruikt om klanten tijdens sessies bij te houden. |
| `productListItems.priceTotal[0]` | De totale kosten van gekochte objecten per transactie. |
| `productListItems.quantity[0]` | Het totale aantal objecten in een aankoop. |
| `timestamp` | De exacte datum en tijd van elke koopgebeurtenis. |
| `commerce.order.purchaseID` | Een vereiste waarde die een voltooide aankoop bevestigt. |

De dataset moet gestructureerde historische verslagen van de klantentransactie bevatten, met elke rij die een aankoopgebeurtenis vertegenwoordigt. Elke gebeurtenis moet timestamps in een aangewezen datum-tijd formaat verenigbaar met de SQL `DATEDIFF` functie (bijvoorbeeld, YYYY-MM-DD HH :MI: SS) omvatten. Bovendien moet elke record een geldige Experience Cloud-id (`ECID`) in het veld `identityMap` bevatten om klanten op unieke wijze te identificeren.

>[!TIP]
>
>De verwerking van grote datasets met miljoenen verslagen kan prestaties beduidend beïnvloeden. Om vraaguitvoering te optimaliseren, verdeel de ervaringsdataset door timestamp, voer stijgende verwerking uit gebruikend momentopnamen, en pas efficiënte samenvoegingsfuncties toe zoals nodig. Bovendien, filter gegevens vóór samenvoeging om verwerkingsoverheadkosten te verminderen.

## Een model maken {#create-a-model}

Om klantenkring te voorspellen, moet u een op SQL-Gebaseerd logistiek regressiemodel tot stand brengen dat de geschiedenis van de klantenaankoop en gedragsmetriek analyseert. In het model worden klanten geclassificeerd als `churned` of `not churned` door te bepalen of ze een aankoop hebben gedaan in de afgelopen 90 dagen.

### SQL gebruiken om het model van de kinnevoorspelling te creëren {#sql-create-model}

Het op SQL-Gebaseerde model verwerkt `webevents` gegevens door zeer belangrijke metriek te groeperen en karnetiketten toe te wijzen die op een 90 dag onactiviteitregel worden gebaseerd. Deze benadering maakt onderscheid tussen actieve klanten en klanten die risico lopen. De SQL-query voert ook functietechniek uit om de nauwkeurigheid van het model te verbeteren en de indeling van de kolommen te verbeteren. Deze inzichten stellen uw bedrijf in staat om gerichte retentiestrategieën te implementeren, het vertrouwen te verminderen en de waarde van de levensduur van de klant te maximaliseren.

>[!NOTE]
>
>In het model van de voorspelling van de kleur wordt een standaarddrempel van 90 dagen gebruikt om klanten in te delen als gehuurde klanten. Om deze drempel aan te passen om zich aan uw bedrijfsdoelstellingen en behoudstrategieën te richten, wijzig de `DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90` voorwaarde in de SQL vragen.

Gebruik de volgende SQL-instructie om het `retention_model_logistic_reg` -model te maken met de opgegeven functies en labels:

```sql
CREATE MODEL retention_model_logistic_reg
TRANSFORM (
  vector_assembler(array(total_purchases, total_revenue, avg_order_value, customer_lifetime, days_since_last_purchase, purchase_frequency)) features
  -- Combines selected customer metrics into a feature vector for model training
)
OPTIONS (
  MODEL_TYPE = 'logistic_reg',  -- Specifies logistic regression as the model type
  LABEL = 'churned'             -- Defines the target label for churn classification
)
AS
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID from identityMap
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  -- Calculates the average order value, and handles null values with COALESCE
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, -- The sum of all purchase values per customer
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  -- The total number of items purchased by the customer
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  -- The days between first and last recorded purchase
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  -- The days since the last purchase event
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  -- The count of unique months with purchases
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Filters transactions with valid total price
      AND commerce.`order`.purchaseID <> ''  -- Ensures the order has a valid purchase ID
    GROUP BY customer_id 
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  -- Extract the unique customer ID for labeling
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Marks the customer as churned if no purchase occurred in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id  
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id  -- Join features with churn labels
ORDER BY RANDOM()  -- Shuffles rows randomly for training
LIMIT 500000;  -- Limit the dataset to 500,000 rows for model training
```

### Modeluitvoer {#model-output}

De outputdataset bevat klant-gerelateerde metriek en hun kernostatus. Elke rij vertegenwoordigt een klant, hun eigenschapwaarden, en hun kernostatus. U kunt deze output gebruiken om klantengedrag te analyseren, voorspellende modellen op te leiden, en gerichte bewaarstrategieën te ontwikkelen om klanten op risico te behouden. Hieronder ziet u een voorbeeld van een uitvoertabel:

```console
 customer_id  | total_purchases | total_revenue | avg_order_value  | customer_lifetime | days_since_last_purchase | purchase_frequency | churned |
--------------+-----------------+---------------+------------------+-------------------+--------------------------+--------------------+----------
  100001      | 25              | 1250.00       | 50.00            | 540               | 20                       | 10                 | 0       
  100002      | 3               | 90.00         | 30.00            | 120               | 95                       | 1                  | 1       
  100003      | 60              | 7200.00       | 120.00           | 800               | 5                        | 24                 | 0       
  100004      | 15              | 750.00        | 50.00            | 365               | 60                       | 8                  | 0       
  100005      | 1               | 25.00         | 25.00            | 60                | 180                      | 1                  | 1       
```

| Kolom | Beschrijving |
|-----------|------------------------------------------------------------------------------------|
| `churned` | De waarde geeft aan of de klant een aankoop heeft gedaan binnen de laatste 90 dagen (0 = niet ingehuurd, 1 = ingehuurd). |

## SQL gebruiken om het model te evalueren {#model-evaluation}

Daarna, evalueer het model van de kinnevoorspelling om zijn doeltreffendheid te bepalen in het identificeren van op risico-klanten. Evalueer modelprestaties met zeer belangrijke metriek die nauwkeurigheid en betrouwbaarheid meten.

Gebruik de functie `model_evaluate` om de nauwkeurigheid van het `retention_model_logistic_reg` -model te meten in het voorspellen van de klantketen. In het volgende SQL-voorbeeld wordt het model geëvalueerd aan de hand van een gegevensset die is gestructureerd zoals de trainingsgegevens:

```sql
SELECT * 
FROM model_evaluate(retention_model_logistic_reg, 1,
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue,
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases, 
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency 
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)
      AND commerce.`order`.purchaseID <> ''
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1 
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0) 
      AND commerce.`order`.purchaseID <> '' 
    GROUP BY customer_id
)
SELECT
    f.customer_id,
    f.total_purchases,
    f.total_revenue,
    f.avg_order_value,
    f.customer_lifetime,
    f.days_since_last_purchase,
    f.purchase_frequency,
    l.churned
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id); -- Joins customer features with churn labels
```

### Uitvoering modelevaluatie

De evaluatieoutput omvat zeer belangrijke prestatiesmetriek, zoals AUC-ROC, nauwkeurigheid, precisie, en herinnering. Deze metriek verstrekt inzicht in modeldoeltreffendheid die u kunt gebruiken om bewaarstrategieën te verfijnen en gegeven-gedreven besluiten te nemen.

>[!NOTE]
>
>Prestatiewaarden variëren van 0 tot 1, waarbij 1,0 de perfecte prestaties vertegenwoordigt.

```console
 auc_roc | accuracy | precision | recall 
---------+----------+-----------+--------
1        | 0.99998  |  1        |  1      
```

| Metrisch | Beschrijving |
|------------|-------------------------------------------------------------------------|
| `auc_roc` | Deze metrische waarde geeft aan hoe geschikt het model is om onderscheid te maken tussen klanten met en zonder koeien. Een waarde dichter bij 1 geeft betere prestaties aan. |
| `accuracy` | De nauwkeurigheidsnorm geeft het aandeel van correcte voorspellingen aan, die een algemene maat van modelprestaties verstrekken. |
| `precision` | Precisie toont het aandeel correct geïdentificeerde gekoesterde klanten, en wijst op betrouwbaarheid in koordvoorspelling. Een hoge waarde betekent minder valse positieven. |
| `recall` | Recall meet het vermogen van het model om alle werkelijk gekochte klanten te identificeren. Een hoge terugroepwaarde geeft aan dat er minder klanten met gemiste kans zijn. |

>[!NOTE]
>
>De bijna perfecte scores in dit voorbeeld zijn voor demonstratiedoeleinden. In de praktijk kunnen gegevens in de praktijk lagere waarden opleveren als gevolg van ruis en variabiliteit.

## Modelvoorspelling {#model-prediction}

Nadat het model is geëvalueerd, gebruikt u `model_predict` om het toe te passen op een nieuwe gegevensset en de klant een nieuwe keuze te laten maken. U kunt deze voorspellingen gebruiken om klanten op risico te identificeren en gerichte bewaarstrategieën uit te voeren.

### SQL gebruiken om veelhoekvoorspelling te genereren {#sql-model-predict}

In de SQL-query hieronder wordt het model `retention_model_logistic_reg` gebruikt om te voorspellen wat de klant doet met een gegevensset die is gestructureerd zoals de trainingsgegevens:

```sql
SELECT * 
FROM model_predict(retention_model_logistic_reg, 1,  -- Applies the trained model for churn prediction
WITH customer_features AS (
    SELECT
       identityMap['ECID'][0].id AS customer_id,
       AVG(COALESCE(productListItems.priceTotal[0], 0)) AS avg_order_value,  
       SUM(COALESCE(productListItems.priceTotal[0], 0)) AS total_revenue, 
       COUNT(COALESCE(productListItems.quantity[0], 0)) AS total_purchases,  
       DATEDIFF(MAX(timestamp), MIN(timestamp)) AS customer_lifetime,  
       DATEDIFF(CURRENT_DATE, MAX(timestamp)) AS days_since_last_purchase,  
       COUNT(DISTINCT CONCAT(YEAR(timestamp), MONTH(timestamp))) AS purchase_frequency  
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  -- Ensures only valid purchase data is considered
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
),
customer_labels AS (
    SELECT
      identityMap['ECID'][0].id AS customer_id,  
      CASE
          WHEN DATEDIFF(CURRENT_DATE, MAX(timestamp)) > 90 THEN 1  -- Identify customers who have not purchased in the last 90 days
          ELSE 0
      END AS churned
    FROM
        webevents
    WHERE EXISTS(productListItems, value -> value.priceTotal > 0)  
      AND commerce.`order`.purchaseID <> ''  
    GROUP BY customer_id
)
SELECT
    f.customer_id,  
    f.total_purchases,  
    f.total_revenue,  
    f.avg_order_value,  
    f.customer_lifetime,  
    f.days_since_last_purchase,  
    f.purchase_frequency,  
    l.churned  
FROM
    customer_features f
JOIN
    customer_labels l
ON f.customer_id = l.customer_id);  -- Matches features with their churn labels for prediction
```

### Modelvoorspellingsuitvoer {#prediction-output}

De outputdataset omvat zeer belangrijke klanteneigenschappen en hun voorspelde koordstatus, die erop wijst of een klant waarschijnlijk zal leiden. Gebruik deze inzichten om pro-actieve bewaarstrategieën uit te voeren en klantenkring te verminderen.

```console
 total_purchases | total_revenue | avg_order_value | customer_lifetime | days_since_last_purchase | purchase_frequency | churned | prediction
-----------------+---------------+-----------------+-------------------+--------------------------+--------------------+---------+------------
 2               | 299           | 149.5           | 0                 | 13                        | 1                  | 0       | 0
 1               | 710           | 710.00          | 0                 | 149                       | 1                  | 1       | 1
 1               | 19.99         | 19.99           | 0                 | 30                        | 1                  | 0       | 0
 1               | 4528          | 4528.00         | 0                 | 26                        | 1                  | 0       | 0
 1               | 21.84         | 21.84           | 0                 | 90                        | 1                  | 0       | 0
 1               | 16.64         | 16.64           | 0                 | 268                       | 1                  | 1       | 1
```

| Kolom | Beschrijving |
|---------------|-------------------------------------------------------------------------------|
| `prediction` | De door de klant voorspelde chatstatus op basis van het model (0 = niet ingetekend, 1 = ingetekend). |

## Volgende stappen

U hebt nu geleerd om een op SQL gebaseerd model te maken, te evalueren en te gebruiken om de klant te voorspellen. Met deze stichting, kunt u klantengedrag analyseren, klanten op risico identificeren, en pro-actieve behoudstrategieën uitvoeren om klantenbehoud te verbeteren. Neem de volgende stappen om uw model voor de voorspelling van fouten verder te verbeteren en toe te passen:

- Automatiseer het proces: integreer het model in een gegevenspijplijn voor ononderbroken controle en inzicht in real time. [ onderzoek hoe te om datasets met SQL ](../../../dashboards/query.md) te verifiëren en te verwerken.
- Prestaties van het model bewaken: het model voortdurend beoordelen met nieuwe gegevens om nauwkeurigheid en relevantie te behouden.  De Medewerker van AI van het gebruik [&#128279;](../../../ai-assistant/landing.md) in Adobe Experience Platform UI om zeer belangrijke prestatiesveranderingen te controleren en [ het voorspellen van publiekstrends ](../../../ai-assistant/new-features/audience-forecasting.md).
