---
keywords: Experience Platform;thuis;populaire onderwerpen;de vraagdienst;de dienst van de vraag;voorbereide verklaringen;voorbereid;sql;
solution: Experience Platform
title: Bereide verklaringen in de Dienst van de Vraag
description: In SQL, worden de voorbereide verklaringen gebruikt aan malplaatje gelijkaardige vragen of updates. De Dienst van de Vraag van Adobe Experience Platform steunt voorbereide verklaringen door een parameterized vraag te gebruiken.
exl-id: 7ee4a10e-2bfe-487f-a8c5-f03b5b1d77e3
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 3%

---

# Vooraf voorbereide instructies

In SQL, worden de voorbereide verklaringen gebruikt om gelijkaardige vragen of updates te templatiseren. Adobe Experience Platform [!DNL Query Service] ondersteunt voorbereide instructies met behulp van een geparametriseerde query. Hierdoor kunnen de prestaties worden geoptimaliseerd, omdat u een query niet langer herhaaldelijk opnieuw hoeft te parseren.

## Vooraf voorbereide instructies gebruiken

Wanneer u kant-en-klare instructies gebruikt, worden de volgende syntaxis ondersteund:

- [PREPARE](#prepare)
- [UITVOEREN](#execute)
- [VERWIJDEREN](#deallocate)

### Een voorbereide instructie voorbereiden {#prepare}

Deze SQL-query slaat de geschreven SELECT-query op onder de naam `PLAN_NAME` . U kunt variabelen, zoals `$1`, gebruiken in plaats van werkelijke waarden. Deze voorbereide instructie wordt opgeslagen tijdens de huidige sessie. Gelieve te merken op dat de plannamen **niet** gevoelig geval zijn.

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

Voor deze SQL-query kan de parameter worden ingesteld met behulp van de volgende voorbereide instructie:

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
