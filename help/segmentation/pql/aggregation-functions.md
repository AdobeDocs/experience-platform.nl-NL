---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Samenvoegingsfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Samenvoegingsfuncties

Samenvoegfuncties worden gebruikt om meerdere waarden binnen PQL-arrays (Profile Query Language) te groeperen en één samenvattingswaarde te maken. Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## Aantal

De `count` functie retourneert het aantal elementen binnen de opgegeven array.

**Indeling**

```sql
{ARRAY}.count()
```

**Voorbeeld**

De volgende PQL-query retourneert het aantal orders in de array.

```sql
orders.count()
```

## Som

De `sum` functie retourneert de som van alle geselecteerde waarden binnen de array.

**Indeling**

```sql
{ARRAY}.sum()
```

**Voorbeeld**

De volgende vraag PQL keert de som van alle prijzen van orden terug.

```sql
orders.sum(order.price)
```

## Gemiddeld

De `average` functie retourneert het rekenkundig gemiddelde van alle geselecteerde waarden binnen de array.

**Indeling**

```sql
{ARRAY}.average()
```

**Voorbeeld**

De volgende vraag PQL keert de gemiddelde prijs van alle orden terug.

```sql
orders.average(order.price)
```

## Minimaal

De `min` functie retourneert de kleinste van alle geselecteerde waarden binnen de array.

**Indeling**

```sql
{ARRAY}.min()
```

**Voorbeeld**

De volgende vraag PQL keert de laagste prijs van alle orden terug.

```sql
orders.min(order.price)
```

## Maximum

De `max` functie retourneert de grootste van alle geselecteerde waarden binnen de array.

**Indeling**

```sql
{ARRAY}.max()
```

**Voorbeeld**

De volgende vraag PQL keert de hoogste prijs van alle orden terug.

```sql
orders.max(order.price)
```

## Volgende stappen

Nu u over samenvoegingsfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
