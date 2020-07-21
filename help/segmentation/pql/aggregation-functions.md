---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Samenvoegingsfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 3%

---


# Samenvoegingsfuncties

Samenvoegfuncties worden gebruikt om meerdere waarden binnen [!DNL Profile Query Language] (PQL)-arrays te groeperen en één samenvattingswaarde te vormen. Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

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
