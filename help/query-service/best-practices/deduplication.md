---
keywords: Experience Platform;thuis;populaire onderwerpen;vraagdienst;de dienst van de vraag;gegevensdeduplicatie;deduplicatie;
solution: Experience Platform
title: Data Deduplication in Query Service
topic-legacy: queries
type: Tutorial
description: Dit document schetst sub-select en volledige voorbeelden van steekproefvraag voor het dedupliceren van drie veelvoorkomende gebruiksgevallen Ervaring Gebeurtenissen, aankopen, en metriek.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: b140037ed5f055a8e7c583540910cc6b18bbf0bd
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---

# Gegevensdeduplicatie in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] ondersteunt gegevensdeduplicatie. Data deduplication may be done when it is required to remove an entire row from a calculation or ignore a specific set of fields because only part of the data in the row is duplicate information.

Bij deduplicatie wordt doorgaans het `ROW_NUMBER()` functie over een venster voor een identiteitskaart (of een paar IDs) over bevolen tijd, die een nieuw gebied terugkeert dat het aantal tijden vertegenwoordigt een duplicaat is ontdekt. De tijd wordt vaak vertegenwoordigd door het [!DNL Experience Data Model] (XDM) `timestamp` veld.

Wanneer de waarde van de `ROW_NUMBER()` is `1`, verwijst het naar het oorspronkelijke exemplaar. Generally, that is the instance that you would wish to use. Dit gebeurt meestal binnen een subselectie waar deduplicatie op een hoger niveau wordt uitgevoerd `SELECT` zoals het uitvoeren van een geaggregeerde telling.

Gebruiksgevallen voor deduplicatie kunnen globaal zijn of zijn beperkt tot één gebruiker of eindgebruiker-id in het dialoogvenster `identityMap`.

In dit document wordt beschreven hoe u deduplicatie kunt uitvoeren voor drie veelvoorkomende gebruiksgevallen: Ervaar gebeurtenissen, aankopen en metriek.

Elk voorbeeld bevat het bereik, de venstersleutel, een overzicht van de deduplicatiemethode en de volledige SQL-query.

## Experience Events {#experience-events}

In the case of duplicate Experience Events, you will likely wish to ignore the entire row.

>[!CAUTION]
>
>Veel gegevenssets in [!DNL Experience Platform], met inbegrip van de door de Adobe Analytics Data Connector gegenereerde deduplicatie op ervaringsniveau op gebeurtenisniveau. Daarom is het opnieuw toepassen van dit niveau van deduplicatie onnodig en zal uw vraag vertragen.
>
>Het is belangrijk om de bron van uw datasets te begrijpen en te weten of is deduplicatie op ervaring-gebeurtenis-niveau reeds toegepast. Voor alle gegevenssets die worden gestreamd (bijvoorbeeld gegevenssets uit Adobe Target), kunt u **zal** de noodzaak om deduplicatie op ervaringsniveau toe te passen, aangezien deze gegevensbronnen &quot;minstens één keer&quot; semantiek hebben.

**Toepassingsgebied:** Algemeen

**Window key:** `id`

### Voorbeeld van deduplicatie

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Full example

```sql
SELECT COUNT(*) AS num_events FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num
  FROM experience_events
) WHERE id_dup_num = 1
```

## Aankopen {#purchases}

Als u dubbele aankopen hebt, zult u waarschijnlijk het grootste deel van willen houden [!DNL Experience Event] , maar negeer de velden die aan de aankoop zijn gekoppeld (zoals de `commerce.orders` metrisch). Purchases contain a special field for the purchase ID, which is `commerce.order.purchaseID`.

Het wordt aanbevolen `purchaseID` binnen het bereik van de bezoeker, aangezien dit het standaard semantische veld is voor aankoop-id&#39;s binnen XDM. Visitor scope is recommended for removing duplicate purchase data because the query is faster than using global scope and it is unlikely that a purchase ID is duplicated across multiple visitor IDs.

**Toepassingsgebied:** Bezoeker

**Venstersleutel:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Deduplication example

```sql
SELECT *,
  IF(LENGTH(commerce.`order`.purchaseID) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, commerce.`order`.purchaseID
            ORDER BY timestamp ASC
      ),
    1) AS purchaseID_dup_num
FROM experience_events
```

>[!NOTE]
>
>In some instances where the original Analytics data has duplicate purchase IDs across visitor IDs, you **may** need to run the purchase ID duplicate counting across all visitors. Wanneer de aankoop-id niet aanwezig is, moet u met deze methode een voorwaarde opnemen die in plaats daarvan de gebeurtenis-id gebruikt om de query zo snel mogelijk te houden.

### Volledig voorbeeld

In het onderstaande voorbeeld wordt een voorwaardsclausule gebruikt om de gebeurtenis-id te gebruiken als de aankoop-id niet aanwezig is.

```sql
SELECT SUM(commerce.purchases.value) AS num_purchases FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(commerce.`order`.purchaseID) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, commerce.order.purchaseID
              ORDER BY timestamp ASC
        ),
      1) AS purchaseID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND purchaseID_dup_num = 1
```

## Metrics {#metrics}

Als u metrisch hebt die facultatieve unieke identiteitskaart gebruikt en een duplicaat van die identiteitskaart verschijnt, zult u waarschijnlijk die metrische waarde willen negeren en de rest Gebeurtenis van de Ervaring houden.

In XDM, almost all metrics use the `Measure` data type that includes an optional `id` field that you could use for deduplication.

**Scope:** Visitor

**Venstersleutel:** identityMap[$NAMESPACE].id en id van object Meetlat

### Voorbeeld van deduplicatie

```sql
SELECT *,
  IF(LENGTH(application.launches.id) > 0,
    ROW_NUMBER()
      OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
            ORDER BY timestamp ASC
      ),
    1) AS launchesID_dup_num
FROM experience_events
```

### Full example

```sql
SELECT SUM(application.launches.value) AS num_launches FROM (
  SELECT *,
    ROW_NUMBER()
      OVER (PARTITION BY id
            ORDER BY timestamp ASC
      ) AS id_dup_num,
    IF(LENGTH(application.launches.id) > 0,
      ROW_NUMBER()
        OVER (PARTITION BY identityMap['ECID'].id, application.launches.id
              ORDER BY timestamp ASC
        ),
      1) AS launchesID_dup_num
  FROM experience_events
) WHERE id_dup_num = 1 AND launchesID_dup_num = 1
```

## Volgende stappen

This document outlined how to perform data deduplication within Query Service, as well as examples of data deduplication. Voor meer beste praktijken wanneer het schrijven van vragen die de Dienst van de Vraag gebruiken, gelieve te lezen [handleiding voor het schrijven van query&#39;s](./writing-queries.md).
