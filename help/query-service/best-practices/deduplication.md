---
keywords: Experience Platform;thuis;populaire onderwerpen;vraagdienst;de dienst van de vraag;gegevensdeduplicatie;deduplicatie;
solution: Experience Platform
title: Data Deduplication in Query Service
topic: queries
type: Tutorial
description: Dit document schetst sub-select en volledige voorbeelden van steekproefvraag voor het dedupliceren van drie veelvoorkomende gebruiksgevallen Ervaring Gebeurtenissen, aankopen, en metriek.
translation-type: tm+mt
source-git-commit: 97dc0b5fb44f5345fd89f3f56bd7861668da9a6e
workflow-type: tm+mt
source-wordcount: '494'
ht-degree: 0%

---


# Gegevensdeduplicatie in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] ondersteunt gegevensdeduplicatie. Gegevensdeduplicatie kan worden uitgevoerd wanneer een volledige rij uit een berekening moet worden verwijderd of wanneer een specifieke set velden moet worden genegeerd, omdat slechts een deel van de gegevens in de rij dubbele informatie is.

Bij deduplicatie wordt doorgaans de functie `ROW_NUMBER()` in een venster gebruikt voor een id (of een paar id&#39;s) in een geordende tijd, die een nieuw veld retourneert dat het aantal keren aangeeft dat een duplicaat is gedetecteerd. De tijd wordt vaak vertegenwoordigd door het [!DNL Experience Data Model] (XDM) `timestamp` gebied te gebruiken.

Wanneer de waarde van `ROW_NUMBER()` `1` is, verwijst het naar de originele instantie. Over het algemeen is dat de instantie die u wilt gebruiken. Dit zal het vaakst binnen een sub-uitgezochte worden gedaan waar deduplicatie in een hoger niveau `SELECT` als het uitvoeren van een gezamenlijke telling wordt gedaan.

Deduplicatie-gebruiksgevallen kunnen globaal zijn of beperkt zijn tot één gebruiker of eindgebruiker-id in het `identityMap`.

In dit document wordt beschreven hoe u deduplicatie kunt uitvoeren voor drie veelvoorkomende gebruiksgevallen: Ervaar gebeurtenissen, aankopen en metriek.

Elk voorbeeld bevat het bereik, de venstersleutel, een overzicht van de deduplicatiemethode en de volledige SQL-query.

## Experience Events {#experience-events}

In het geval van dubbele Gebeurtenissen van de Ervaring, zult u waarschijnlijk de volledige rij willen negeren.

>[!CAUTION]
>
>Bij veel datasets in [!DNL Experience Platform], waaronder die welke door de Adobe Analytics Data Connector worden geproduceerd, is al deduplicatie op ervaringsniveau op gebeurtenisniveau toegepast. Daarom is het opnieuw toepassen van dit niveau van deduplicatie onnodig en zal uw vraag vertragen.
>
>Het is belangrijk om de bron van uw datasets te begrijpen en te weten of is deduplicatie op ervaring-gebeurtenis-niveau reeds toegepast. Voor om het even welke datasets die (bijvoorbeeld, die van Adobe Target) worden gestroomd, moet u **will** ervaring-gebeurtenis-vlakke deduplicatie toepassen, aangezien die gegevensbronnen &quot;minstens eens&quot;semantiek hebben.

**bereik:** globaal

**Venstersleutel:** `id`

### Voorbeeld van deduplicatie

```sql
SELECT *,
  ROW_NUMBER()
    OVER (PARTITION BY id
          ORDER BY timestamp ASC
    ) AS id_dup_num
FROM experience_events
```

### Volledig voorbeeld

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

Als u dubbele aankopen hebt, zult u waarschijnlijk het grootste deel van de rij van de Gebeurtenis van de Ervaring willen houden, maar negeert de gebieden verbonden aan de aankoop (zoals `commerce.orders` metrisch). Aankopen bevatten een speciaal veld voor de aankoop-id, namelijk `commerce.order.purchaseID`.

**bereik:** bezoeker

**Venstersleutel:** identityMap[$NAMESPACE].id &amp; commerce.order.purchaseID

### Voorbeeld van deduplicatie

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

### Volledig voorbeeld

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

## Cijfers {#metrics}

Als u metrisch hebt die facultatieve unieke identiteitskaart gebruikt en een duplicaat van die identiteitskaart verschijnt, zult u waarschijnlijk die metrische waarde willen negeren en de rest Gebeurtenis van de Ervaring houden.

In XDM, bijna gebruiken alle metriek het `Measure` gegevenstype dat een facultatief `id` gebied omvat dat u voor deduplicatie kon gebruiken.

**bereik:** bezoeker

**Venstersleutel:** identityMap[$NAMESPACE].id &amp; id van meetobject

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

### Volledig voorbeeld

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

Dit document beschreef hoe te om gegevensdeduplicatie binnen de Dienst van de Vraag, evenals voorbeelden van gegevensdeduplicatie uit te voeren. Voor meer beste praktijken wanneer het schrijven van vragen die de Dienst van de Vraag gebruiken, gelieve [het schrijven van vragen te lezen gidsen](./writing-queries.md).