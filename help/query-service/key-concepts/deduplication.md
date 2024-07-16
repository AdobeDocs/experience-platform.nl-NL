---
keywords: Experience Platform;thuis;populaire onderwerpen;vraagdienst;de dienst van de vraag;gegevensdeduplicatie;deduplicatie;
solution: Experience Platform
title: Data Deduplication in Query Service
type: Tutorial
description: Dit document schetst sub-select en volledige voorbeelden van steekproefvraag voor het dedupliceren van drie veelvoorkomende gebruiksgevallen Ervaring Gebeurtenissen, aankopen, en metriek.
exl-id: 46ba6bb6-67d4-418b-8420-f2294e633070
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---

# Gegevensdeduplicatie in [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] ondersteunt gegevensdeduplicatie. Gegevensdeduplicatie kan worden uitgevoerd wanneer een volledige rij uit een berekening moet worden verwijderd of wanneer een specifieke set velden moet worden genegeerd, omdat slechts een deel van de gegevens in de rij dubbele informatie is.

Bij deduplicatie wordt doorgaans de functie `ROW_NUMBER()` in een venster gebruikt voor een id (of een paar id&#39;s) in de geordende tijd, waardoor een nieuw veld wordt geretourneerd dat het aantal keren aangeeft dat een duplicaat is gedetecteerd. De tijd wordt vaak vertegenwoordigd door het veld [!DNL Experience Data Model] (XDM) `timestamp` te gebruiken.

Wanneer de waarde van `ROW_NUMBER()` `1` is, verwijst deze naar de oorspronkelijke instantie. Over het algemeen is dat de instantie die u wilt gebruiken. Dit wordt meestal gedaan in een subselectie waar de deduplicatie wordt uitgevoerd op een hoger niveau `SELECT`, zoals bij het uitvoeren van een geaggregeerde telling.

Deduplicatie-gebruiksgevallen kunnen globaal zijn of beperkt zijn tot één gebruiker of eindgebruiker-id in de `identityMap` .

In dit document wordt beschreven hoe u deduplicatie kunt uitvoeren voor drie veelvoorkomende gebruiksgevallen: Geniet van gebeurtenissen, aankopen en metriek.

Elk voorbeeld bevat het bereik, de venstersleutel, een overzicht van de deduplicatiemethode en de volledige SQL-query.

## Experience Events {#experience-events}

In het geval van dubbele Gebeurtenissen van de Ervaring, zult u waarschijnlijk de volledige rij willen negeren.

>[!CAUTION]
>
>Voor veel datasets in [!DNL Experience Platform], waaronder die welke door de Adobe Analytics Data Connector worden geproduceerd, is al deduplicatie op ervaringsniveau op gebeurtenisniveau toegepast. Daarom is het opnieuw toepassen van dit niveau van deduplicatie onnodig en zal uw vraag vertragen.
>
>Het is belangrijk om de bron van uw datasets te begrijpen en te weten of is deduplicatie op ervaring-gebeurtenis-niveau reeds toegepast. Voor om het even welke datasets die (bijvoorbeeld, die van Adobe Target) worden gestroomd, zult u **** ervaring-gebeurtenis-vlakke deduplicatie moeten toepassen, aangezien die gegevensbronnen &quot;minstens eens&quot;semantiek hebben.

**Reikwijdte:** Globaal

**sleutel van het Venster:** `id`

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

Als u dubbele aankopen hebt, zult u waarschijnlijk het grootste deel van [!DNL Experience Event] rij willen houden, maar negeert de gebieden verbonden aan de aankoop (zoals `commerce.orders` metrisch). Aankopen bevatten een speciaal veld voor de aankoop-id, namelijk `commerce.order.purchaseID` .

Het wordt aanbevolen `purchaseID` binnen het bereik van de bezoeker te gebruiken, aangezien dit het standaard semantische veld is voor aankoop-id&#39;s binnen XDM. Het bereik van de bezoeker wordt aanbevolen voor het verwijderen van dubbele aankoopgegevens omdat de query sneller is dan het gebruik van een algemeen bereik en het onwaarschijnlijk is dat een aankoop-id wordt gedupliceerd op meerdere bezoekers-id&#39;s.

**Reikwijdte:** Bezoeker

**sleutel van het Venster:** identityMap [$NAMESPACE ].id &amp; commerce.order.purchaseID

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

>[!NOTE]
>
>In sommige gevallen waar de originele gegevens van de Analyse dubbele aankoop IDs over bezoeker IDs hebben, kunt u **** de dubbele telling van aankoopidentiteitskaart over alle bezoekers in werking moeten stellen. Wanneer de aankoop-id niet aanwezig is, moet u met deze methode een voorwaarde opnemen die in plaats daarvan de gebeurtenis-id gebruikt om de query zo snel mogelijk te houden.

### Volledig voorbeeld

In het onderstaande voorbeeld wordt een voorwaardsclausule gebruikt om de gebeurtenis-id te gebruiken wanneer de aankoop-id niet aanwezig is.

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

In XDM gebruiken bijna alle metriek het `Measure` gegevenstype dat een optioneel `id` veld bevat dat u kunt gebruiken voor deduplicatie.

**Reikwijdte:** Bezoeker

**sleutel van het Venster:** identityMap [$NAMESPACE ] .id &amp; id van voorwerp van de Maatregel

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

In dit document worden voorbeelden gegeven van gegevensdeduplicatie en wordt uitgelegd hoe u gegevensdeduplicatie kunt uitvoeren binnen Query Service. Voor meer beste praktijken wanneer het schrijven van vragen die de Dienst van de Vraag gebruiken, lees gelieve [ het schrijven van de gids van vragen ](../best-practices/writing-queries.md).
