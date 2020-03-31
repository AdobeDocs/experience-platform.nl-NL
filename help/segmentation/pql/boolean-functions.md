---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Booleaanse functies
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Booleaanse functies

Booleaanse functies worden gebruikt voor het uitvoeren van Booleaanse logica op verschillende elementen in PQL (Profile Query Language).  Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## en

De `and` functie wordt gebruikt om een logische verbinding tot stand te brengen.

**Indeling**

```sql
{QUERY} and {QUERY}
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen met het thuisland als Canada en het geboortejaar 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## of

De `or` functie wordt gebruikt om een logische scheiding te maken.

**Indeling**

```sql
{QUERY} or {QUERY}
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen met het thuisland als Canada of geboortejaar 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Niet

De functie `not` (of `!`) wordt gebruikt om een logische negatie te maken.

**Indeling**

```sql
not ({QUERY})
!({QUERY})
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen die hun thuisland niet als Canada hebben.

```sql
not (homeAddress.countryISO = "CA")
```

## Indien

De `if` functie wordt gebruikt om een expressie op te lossen, afhankelijk van het feit of een opgegeven voorwaarde waar is.

**Indeling**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | De booleaanse expressie die wordt getest. |
| `{TRUE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` true is. |
| `{FALSE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als deze false `{TEST_EXPRESSION}` is. |

**Voorbeeld**

De volgende PQL-query stelt de waarde in alsof `1` het thuisland Canada is en `2` als het thuisland geen Canada is.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Volgende stappen

Nu u over booleaanse functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
