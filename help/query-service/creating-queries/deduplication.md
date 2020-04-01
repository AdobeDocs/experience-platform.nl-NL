---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevensdeduplicatie
topic: queries
translation-type: tm+mt
source-git-commit: 7d5d98d8e32607abf399fdc523d2b3bc99555507

---


# Gegevensdeduplicatie in Query-service

Adobe Experience Platform Query Service ondersteunt gegevensdeduplicatie wanneer het nodig kan zijn een hele rij uit een berekening te verwijderen of een specifieke set velden te negeren omdat slechts een deel van de gegevens in de rij een duplicaat is. Het gemeenschappelijke patroon voor deduplicatie impliceert het gebruiken van de `ROW_NUMBER()` functie over een venster voor een identiteitskaart, of paar IDs, over geordende tijd (gebruikend het Model van de Gegevens van de Ervaring (XDM) `timestamp` gebied) om een nieuw gebied terug te keren dat het aantal tijden vertegenwoordigt een duplicaat is ontdekt. Wanneer deze waarde is `1`, verwijst dat naar de oorspronkelijke instantie en in de meeste gevallen die instantie is die u wilt gebruiken, waarbij elke andere instantie wordt genegeerd. Dit zal het vaakst binnen een sub-uitgezochte worden gedaan waar deduplicatie in een hoger niveau wordt gedaan `SELECT` zoals het uitvoeren van een gezamenlijke telling.

## Gebruik hoofdletters

Sommige gevallen van gebruik voor deduplicatie zijn globaal in het datumbereik en sommige zijn beperkt tot één bezoeker of eindgebruiker-id binnen het `identityMap`datumbereik.

Dit document schetst sub-select en volledige voorbeelden van steekproefvraag voor het dedupliceren van drie gemeenschappelijke gebruiksgevallen:
- [ExperienceEvents](#experienceevents)
- [Aankopen](#purchases)
- [Metrisch](#metrics)

### ExperienceEvents {#experienceevents}

In het geval van dubbele ExperienceEvents, zult u waarschijnlijk de volledige rij willen negeren.

>[!CAUTION] Voor veel gegevenssets in het ervaringsplatform, waaronder de gegevensconnector van Adobe Analytics Data, is al deduplicatie op ervaringsniveau toegepast. Daarom is het opnieuw toepassen van dit niveau van deduplicatie onnodig en zal uw vraag vertragen. Het is belangrijk om de bron van uw Datasets te begrijpen en te weten of is deduplicatie op het ExperienceEvent-niveau reeds toegepast. Voor gegevenssets die worden gestreamd (bijvoorbeeld gegevenssets van Adobe Target), moet u deduplicatie op ervaringsniveau toepassen omdat deze gegevensbronnen &#39;minstens één keer&#39; semantiek hebben.

**Toepassingsgebied:** Algemeen

**Venstersleutel:** id

#### Subselectie maken

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

#### Volledig voorbeeld

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

### Aankopen {#purchases}

Als u dubbele aankopen hebt, zult u waarschijnlijk het grootste deel van de rij van ExperienceEvent willen houden, maar negeert de gebieden verbonden aan de aankoop (zoals `commerce.orders` metrisch). Voor aankopen is er een speciaal veld voor de aankoop-id. Dit veld is `commerce.order.purchaseID`.

**Toepassingsgebied:** Bezoeker

**Venstersleutel:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

#### Subselectie maken

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

#### Volledig voorbeeld

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

### Metrisch {#metrics}

Als u metrisch hebt die facultatieve unieke identiteitskaart gebruikt en een duplicaat van die identiteitskaart verschijnt, zult u waarschijnlijk die metrische waarde willen negeren en de rest van ExperienceEvent houden. In XDM, bijna gebruiken alle metriek het `Measure` gegevenstype dat een facultatief `id` gebied omvat dat u voor deduplicatie kon gebruiken.

**Toepassingsgebied:** Bezoeker

**Venstersleutel:** identityMap[$NAMESPACE].id &amp; id van object Meetlat

#### Subselectie maken

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

#### Volledig voorbeeld

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
