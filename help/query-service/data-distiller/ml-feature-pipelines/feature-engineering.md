---
title: Functies van engineer voor machinaal leren
description: Leer hoe u gegevens in Adobe Experience Platform omzet in functies of variabelen die door een model voor machinaal leren kunnen worden gebruikt. Met Data Distiller kunt u op schaal XML-functies berekenen en deze functies delen met uw computerleeromgeving.
source-git-commit: 12926f36514d289449cf0d141b5828df3fac37c2
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 13%

---

# Engineer-functies voor machinaal leren

In dit document wordt getoond hoe u gegevens in Adobe Experience Platform kunt omzetten in **functies**, of variabelen, die door een machine het leren model kunnen worden verbruikt. Dit proces wordt **functieengineering**. Met Data Distiller kunt u op schaal XML-functies berekenen en deze functies delen met uw computerleeromgeving. Dit betreft het volgende:

1. Maak een querysjabloon om de doellabels en -functies te definiëren die u voor uw model wilt berekenen
2. Voer de vraag uit en sla de resultaten in een trainingsdataset op

## Uw trainingsgegevens definiëren {#define-training-data}

Het volgende voorbeeld illustreert een vraag om opleidingsgegevens uit een dataset van de Gebeurtenissen van de Ervaring voor een model af te leiden om de neiging van een gebruiker te voorspellen om aan een nieuwsbrief in te tekenen. Abonnementsgebeurtenissen worden vertegenwoordigd door het gebeurtenistype `web.formFilledOut`en andere gedragsgebeurtenissen in de dataset worden gebruikt om eigenschappen op profielniveau af te leiden om abonnementen te voorspellen.

### Positieve en negatieve labels voor query {#query-positive-and-negative-labels}

Een volledige dataset voor de opleiding van een (onder toezicht staande) machinaal leermodel omvat doelvariabele of -label die het te voorspellen resultaat vertegenwoordigt, en een reeks eigenschappen of verklarende variabelen die worden gebruikt om de voorbeeldprofielen te beschrijven die worden gebruikt om het model op te leiden.

In dit geval is het label een variabele met de naam `subscriptionOccurred` dat gelijk is aan 1 als het gebruikersprofiel een gebeurtenis met type heeft `web.formFilledOut` , en 0 in andere gevallen. De volgende vraag keert een reeks van 50.000 gebruikers van de gebeurtenisdataset, met inbegrip van alle gebruikers met positieve etiketten terug (`subscriptionOccurred = 1`) plus een willekeurig geselecteerde gebruiker met negatieve labels om de grootte van het gebruikersmonster van 50.000 te voltooien. Dit zorgt ervoor dat de trainingsgegevens zowel positieve als negatieve voorbeelden bevatten waarvan het model kan leren.

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)

query_labels = f"""
SELECT *
FROM (
    SELECT
        eventType,
        _{tenant_id}.user_id as userId,
        SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
            OVER (PARTITION BY _{tenant_id}.user_id) 
            AS "subscriptionOccurred",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
"""

df_labels = dd_cursor.query(query_labels, output="dataframe")
print(f"Number of classes: {len(df_labels)}")
df_labels.head()
```

**Voorbeelduitvoer**

Aantal klassen: 50000

|   | eventType | userId | subscriptionOccurred | random_row_number_for_user |
| ---  |   ---  |   ---  |   ---  |   --- | 
| 0 | directMarketing.emailClicked | 01027994177972439148069092698714414382 | 0 | 1 |
| 1 | directMarketing.emailOpened | 01054714817856066632264746967668888198 | 0 | 1 |
| 2 | web.formFilledOut | 01117296890525140996735553609305695042 | 1 | 15 |
| 3 | directMarketing.emailClicked | 01149554820363915324573708359099551093 | 0 | 1 |
| 4 | directMarketing.emailClicked | 01172121447143590196349410086995740317 | 0 | 1 |

{style="table-layout:auto"}

### Samengevoegde gebeurtenissen om functies voor ML te definiëren {#define-features}

De volgende vraag voegt de gebeurtenissen in de dataset in zinvolle, numerieke eigenschappen samen die kunnen worden gebruikt om een aandrijvingsmodel te trainen:

- **Aantal e-mails** die voor marketingdoeleinden zijn verzonden en door de gebruiker zijn ontvangen.
- Gedeelte van deze e-mails die **geopend**.
- Gedeelte van deze e-mailberichten waar de gebruiker **geselecteerd** de koppeling.
- **Aantal producten** die zijn bekeken.
- Aantal **voorstellen die verband houden met**.
- Aantal **afgewezen voorstellen**.
- Aantal **geselecteerde koppelingen**.
- Aantal minuten tussen twee opeenvolgende ontvangen e-mails.
- Aantal minuten tussen twee opeenvolgende e-mails geopend.
- Het aantal minuten tussen twee opeenvolgende e-mailberichten waarin de gebruiker de koppeling heeft geselecteerd.
- Aantal minuten tussen twee opeenvolgende productweergaven.
- Het aantal minuten tussen twee voorstellingen waarmee interactie is opgetreden.
- Aantal minuten tussen twee voorstellen die zijn afgewezen.
- Aantal minuten tussen twee geselecteerde koppelingen.

+++Selecteren om voorbeeldquery weer te geven

```python
query_features = f"""
SELECT
    _{tenant_id}.user_id as userId,
    SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsReceived",
    SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsOpened",       
    SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "emailsClicked",       
    SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "productsViewed",       
    SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "propositionInteracts",       
    SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "propositionDismissed",
    SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "webLinkClicks" ,
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailSent",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailOpened",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_emailClick",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_productView",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_propositionInteract",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_propositionDismiss",
    TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
       OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
       AS "minutes_since_linkClick"
FROM {table_name}
"""

df_features = dd_cursor.query(query_features, output="dataframe")
df_features.head()
```

+++

**Voorbeelduitvoer**

|   | userId | emailsReceived | e-mailsGeopend | emailsClicked | productsViewed | propositionInteracts | voorstelAfgewezen | webLinkClicks | minutes_since_emailSent | minutes_since_emailOpened | minutes_since_emailClick | minutes_since_productView | minutes_since_propositionInteract | minutes_since_propositionDismiss | minutes_since_linkClick |
| --- |    --- |    ---   |  ---  |   ---  |   ---  |  ---  |  ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---  |   --- | 
| 0 | 01102546977582484968046916668339306826 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | Geen | NaN |
| 1 | 01102546977582484968046916668339306826 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | Geen | NaN |
| 2 | 01102546977582484968046916668339306826 | 3 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | Geen | NaN |
| 3 | 01102546977582484968046916668339306826 | 3 | 1 | 0 | 0 | 0 | 0 | 0 | 540.0 | 0.0 | NaN | NaN | NaN | Geen | NaN |
| 4 | 01102546977582484968046916668339306826 | 3 | 2 | 0 | 0 | 0 | 0 | 0 | 588.0 | 0.0 | NaN | NaN | NaN | Geen | NaN |

{style="table-layout:auto"}

#### Tags en functies combineren {#combine-queries}

Tot slot kunnen de etiketvraag en de eigenschapvraag in één enkele vraag worden gecombineerd die een opleidingsdataset van etiketten en eigenschappen terugkeert:

+++Selecteren om voorbeeldquery weer te geven

```python
query_training_set = f"""
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name} LIMIT 1000
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
ORDER BY timestamp
"""

df_training_set = dd_cursor.query(query_training_set, output="dataframe")
df_training_set.head()
```

+++

**Voorbeelduitvoer**

|  | userId | eventType | timestamp | subscriptionOccurred | emailsReceived | e-mailsGeopend | emailsClicked | productsViewed | propositionInteracts | voorstelAfgewezen | webLinkClicks | minutes_since_emailSent | minutes_since_emailOpened | minutes_since_emailClick | minutes_since_productView | minutes_since_propositionInteract | minutes_since_propositionDismiss | minutes_since_linkClick | random_row_number_for_user |
| ---  |  --- |   ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---  |  ---   | ---  |  ---  |  ---  |  --- |    
| 0 | 02554909162592418347780983091131567290 | directMarketing.emailSent | 2023-06-17 13:44:59.086 | 0 | 2 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | Geen | NaN | 1 |
| 1 | 01130334080340815140184601481559659945 | directMarketing.emailOpened | 2023-06-19 06:01:55.366 | 0 | 1 | 3 | 0 | 1 | 0 | 0 | 0 | 1921.0 | 0.0 | NaN | 1703.0 | NaN | Geen | NaN | 1 |
| 2 | 01708961660028351393477273586554010192 | web.formFilledOut | 2023-06-19 18:36:49.083 | 1 | 1 | 2 | 2 | 0 | 0 | 0 | 0 | 2365.0 | 26.0 | 1.0 | NaN | NaN | Geen | NaN | 7 |
| 3 | 01809182902320674899156240602124740853 | directMarketing.emailSent | 2023-06-21 19:17:12.535 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | Geen | NaN | 1 |
| 4 | 03441761949943678951106193028739001197 | directMarketing.emailSent | 2023-06-21 21:58:29.482 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0.0 | NaN | NaN | NaN | NaN | Geen | NaN | 1 |

{style="table-layout:auto"}

## Creeer een vraagmalplaatje om trainingsgegevens incrementeel te verwerken

Het is typisch om een model met bijgewerkte opleidingsgegevens periodiek om te herscholen om nauwkeurigheid van het model in tijd te handhaven. Als beste praktijken voor efficiënt het bijwerken van uw trainingsdataset, kunt u een malplaatje van uw vraag van de opleidingsreeks tot stand brengen om nieuwe opleidingsgegevens in oplopende mate te verwerken. Dit staat u toe gegevens verwerkt etiketten en eigenschappen slechts van gegevens die aan de originele dataset van de Gebeurtenissen van de Ervaring werden toegevoegd aangezien de opleidingsgegevens het laatst werden bijgewerkt, en neemt de nieuwe etiketten en de eigenschappen in de bestaande opleidingsdataset op.

Dit vereist een paar wijzigingen aan de vraag van de trainingsreeks:

- Voeg logica toe om een nieuwe opleidingsdataset tot stand te brengen als het niet bestaat, en neem de nieuwe etiketten en de eigenschappen in de bestaande opleidingsdataset anders op. Hiervoor is een reeks van twee versies van de query voor de trainingsset vereist:
   - Als eerste gebruikt u de `CREATE TABLE IF NOT EXISTS {table_name} AS` statement
   - Vervolgens gebruikt u de `INSERT INTO {table_name}` verklaring voor het geval dat het opleidingsgegevensbestand reeds bestaat
- Voeg een `SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id` instructie om de query te beperken tot gebeurtenisgegevens die binnen een opgegeven interval zijn toegevoegd. De `$` op momentopname IDs wijst erop dat zij variabelen zijn die binnen zullen worden overgegaan wanneer het vraagmalplaatje wordt uitgevoerd.

Als u deze wijzigingen toepast, wordt de volgende query uitgevoerd:

+++Selecteren om voorbeeldquery weer te geven

```python
ctas_table_name = "propensity_training_set"

query_training_set_template = f"""
$$ BEGIN

SET @my_table_exists = SELECT table_exists('{ctas_table_name}');

CREATE TABLE IF NOT EXISTS {ctas_table_name} AS
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
    SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id
)
WHERE (subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1)
ORDER BY timestamp;

INSERT INTO {ctas_table_name}
SELECT *
FROM (
    SELECT _{tenant_id}.user_id as userId, 
       eventType,
       timestamp,
       SUM(CASE WHEN eventType='web.formFilledOut' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id) 
           AS "subscriptionOccurred",
       SUM(CASE WHEN eventType='directMarketing.emailSent' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsReceived",
       SUM(CASE WHEN eventType='directMarketing.emailOpened' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsOpened",       
       SUM(CASE WHEN eventType='directMarketing.emailClicked' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "emailsClicked",       
       SUM(CASE WHEN eventType='commerce.productViews' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "productsViewed",       
       SUM(CASE WHEN eventType='decisioning.propositionInteract' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionInteracts",       
       SUM(CASE WHEN eventType='decisioning.propositionDismiss' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "propositionDismissed",
       SUM(CASE WHEN eventType='web.webinteraction.linkClicks' THEN 1 ELSE 0 END) 
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "webLinkClicks" ,
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailSent', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailSent",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailOpened', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailOpened",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'directMarketing.emailClicked', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_emailClick",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'commerce.productViews', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_productView",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'decisioning.propositionInteract', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionInteract",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'propositionDismiss', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_propositionDismiss",
       TIME_BETWEEN_PREVIOUS_MATCH(timestamp, eventType = 'web.webinteraction.linkClicks', 'minutes')
           OVER (PARTITION BY _{tenant_id}.user_id ORDER BY timestamp ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) 
           AS "minutes_since_linkClick",
        row_number() OVER (PARTITION BY _{tenant_id}.user_id ORDER BY randn()) AS random_row_number_for_user
    FROM {table_name}
    SNAPSHOT BETWEEN $from_snapshot_id AND $to_snapshot_id
)
WHERE 
    @my_table_exists = 't' AND
    ((subscriptionOccurred = 1 AND eventType = 'web.formFilledOut') OR (subscriptionOccurred = 0 AND random_row_number_for_user = 1))
ORDER BY timestamp;

EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';

END $$;
"""
```

+++

Tot slot bewaart de volgende code het vraagmalplaatje in Gegevens Distiller:

```python
template_res = dd.createQueryTemplate({
  "sql": query_training_set_template,
  "queryParameters": {},
  "name": "Template for propensity training data"
})
template_id = template_res["id"]

print(f"Template for propensity training data created as ID {template_id}")
```

**Voorbeelduitvoer**

`Template for propensity training data created as ID f3d1ec6b-40c2-4d13-93b6-734c1b3c7235`

Met het bewaarde malplaatje, kunt u de vraag op elk ogenblik uitvoeren door malplaatjeidentiteitskaart van verwijzingen te voorzien en de waaier van momentopname IDs te specificeren die in de vraag zou moeten worden omvat. De volgende vraag wint de momentopnamen van de originele dataset van de Gebeurtenissen van de Ervaring terug:

```python
query_snapshots = f"""
SELECT snapshot_id 
FROM (
    SELECT history_meta('{table_name}')
) 
WHERE is_current = true OR snapshot_generation = 0 
ORDER BY snapshot_generation ASC
"""

df_snapshots = dd_cursor.query(query_snapshots, output="dataframe")
```

De volgende code toont uitvoering van het vraagmalplaatje aan, gebruikend eerste en laatste momentopnamen om de volledige dataset te vragen:

```python
snapshot_start_id = str(df_snapshots["snapshot_id"].iloc[0])
snapshot_end_id = str(df_snapshots["snapshot_id"].iloc[1])

query_final_res = qs.postQueries(
    name=f"[CMLE][Week2] Query to generate training data created by {username}",
    templateId=template_id,
    queryParameters={
        "from_snapshot_id": snapshot_start_id,
        "to_snapshot_id": snapshot_end_id,
    },
    dbname=f"{cat_conn.sandbox}:all"
)
query_final_id = query_final_res["id"]
print(f"Query started successfully and got assigned ID {query_final_id} - it will take some time to execute")
```

**Voorbeelduitvoer**

`Query started successfully and got assigned ID c6ea5009-1315-4839-b072-089ae01e74fd - it will take some time to execute`

U kunt de volgende functie bepalen om de status van de vraag periodiek te controleren:

```python
def wait_for_query_completion(query_id):
    while True:
        query_info = qs.getQuery(query_id)
        query_state = query_info["state"]
        if query_state in ["SUCCESS", "FAILED"]:
            break
        print("Query is still in progress, sleeping…")
        time.sleep(60)

    duration_secs = query_info["elapsedTime"] / 1000
    if query_state == "SUCCESS":
        print(f"Query completed successfully in {duration_secs} seconds")
    else:
        print(f"Query failed with the following errors:", file=sys.stderr)
        for error in query_info["errors"]:
            print(f"Error code {error['code']}: {error['message']}", file=sys.stderr)

wait_for_query_completion(query_final_id)
```

**Voorbeelduitvoer**

```console
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query is still in progress, sleeping…
Query completed successfully in 473.8 seconds
```

## Volgende stappen:

Door dit document te lezen hebt u geleerd hoe u gegevens in Adobe Experience Platform kunt transformeren in functies, of variabelen, die door een model voor machinaal leren kunnen worden verbruikt. De volgende stap bij het maken van functiepijpleidingen van Experience Platform naar aangepaste modellen in uw computerleeromgeving is: [gegevensbestanden met exportfuncties](./export-data.md).
