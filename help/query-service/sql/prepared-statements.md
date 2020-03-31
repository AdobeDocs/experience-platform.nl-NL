---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vooraf voorbereide instructies
topic: prepared statements
translation-type: tm+mt
source-git-commit: 5699022d1f18773c81a0a36d4593393764cb771a

---


# Vooraf voorbereide instructies

In SQL, worden de voorbereide verklaringen gebruikt om gelijkaardige vragen of updates te templatiseren. Adobe Experience Platform Query Service ondersteunt voorbereide instructies door gebruik te maken van een geparametriseerde query. Dit kan worden gebruikt om prestaties te optimaliseren, aangezien u een vraag niet meer zult moeten opnieuw parseren opnieuw en opnieuw.

## Vooraf voorbereide instructies gebruiken

Wanneer u kant-en-klare instructies gebruikt, worden de volgende syntaxis ondersteund:

- [PREPARE](#prepare)
- [UITVOEREN](#execute)
- [VERWIJDEREN](#deallocate)

### Een voorbereide instructie voorbereiden {#prepare}

Deze SQL-query slaat de geschreven SELECT-query op met de opgegeven naam. `PLAN_NAME` U kunt variabelen gebruiken, zoals `$1` in plaats van werkelijke waarden. Deze voorbereide instructie wordt opgeslagen tijdens de huidige sessie. Houd er rekening mee dat de namen van de plannen **niet** hoofdlettergevoelig zijn.

#### SQL-indeling

```sql
PREPARE {PLAN_NAME} AS {SELECT_QUERY}
```

#### Voorbeeld-SQL

```sql
PREPARE test AS SELECT * FROM table WHERE country = $1 AND city = $2;
```

### Een voorbereide instructie uitvoeren {#execute}

Deze SQL-query gebruikt de voorbereide instructie die eerder is gemaakt.

#### SQL-indeling

```sql
EXECUTE {PLAN_NAME}('{PARAMETERS}')
```

#### Voorbeeld-SQL

```sql
EXECUTE test('canada', 'vancouver');
```

### Toewijzing van een voorbereid overzicht opheffen {#deallocate}

Deze SQL-query wordt gebruikt om de benoemde voorbereide instructie te verwijderen.

#### SQL-indeling

```sql
DEALLOCATE {PLAN_NAME}
```

#### Voorbeeld-SQL

```sql
DEALLOCATE test;
```

## Voorbeeld van stroom met voorbereide instructies

Aanvankelijk, kunt u een SQL vraag, zoals hieronder hebben:

```sql
SELECT * FROM table WHERE id >= 10000 AND id <= 10005;
```

De bovenstaande SQL-query retourneert de volgende reactie:

| id | firstname | lastname | geboortedatum | email | stad | land |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoïne | duboe | 1967-03-14 | example2@example.com | Parijs | Frankrijk |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japan |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Zweden |
| 10004 | aasir | kwijthaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rio | 2002-07-30 | example6@example.com | Santiago | Chili |

Voor deze SQL-query kan de parameter worden ingesteld met de volgende voorbereide instructie:

```sql
PREPARE getIdRange AS SELECT * FROM table WHERE id >= $1 AND id <= $2; 
```

Nu, kan de voorbereide verklaring worden uitgevoerd door de volgende vraag te gebruiken:

```sql
EXECUTE getIdRange(10000, 10005);
```

Wanneer dit wordt aangeroepen, ziet u precies dezelfde resultaten als voorheen:

| id | firstname | lastname | geboortedatum | email | stad | land |
|--- | --------- | -------- | --------- | ----- | ------- | ---- |
| 10000 | alexander | davis | 1993-09-15 | example@example.com | Vancouver | Canada |
| 10001 | antoïne | duboe | 1967-03-14 | example2@example.com | Parijs | Frankrijk |
| 10002 | kyoko | sakura | 1999-11-26 | example3@example.com | Tokyo | Japan |
| 10003 | linus | pettersson | 1982-06-03 | example4@example.com | Stockholm | Zweden |
| 10004 | aasir | kwijthaka | 1976-12-17 | example5@example.com | Nairobi | Kenia |
| 10005 | fernando | rio | 2002-07-30 | example6@example.com | Santiago | Chili |

Nadat u het gebruiken van de voorbereide verklaring hebt gebeëindigd, kunt u het ombepalen door de volgende vraag te gebruiken:

```sql
DEALLOCATE getIdRange;
```
