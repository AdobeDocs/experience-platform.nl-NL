---
solution: Experience Platform
title: PQL-aggregatiefuncties
description: Samenvoegfuncties worden gebruikt om meerdere waarden binnen Profile Query Language (PQL)-arrays te groeperen en één samenvattingswaarde te maken.
exl-id: 6c0c0f6d-98c5-4b5d-b440-3e5e18c0f34b
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%

---

# Samenvoegingsfuncties

Samenvoegfuncties worden gebruikt om meerdere waarden binnen [!DNL Profile Query Language] (PQL) -arrays te groeperen en één samenvattingswaarde te maken. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht ](./overview.md) worden gevonden.

## Aantal

De functie `count` retourneert het aantal elementen binnen de opgegeven array.

**Formaat**

```sql
{ARRAY}.count()
```

**Voorbeeld**

De volgende PQL-query retourneert het aantal orders in de array.

```sql
orders.count()
```

## Som

De functie `sum` retourneert de som van alle geselecteerde waarden binnen de array.

**Formaat**

```sql
{ARRAY}.sum()
```

**Voorbeeld**

De volgende PQL-query retourneert de som van de prijzen van alle orders.

```sql
orders.sum(order.price)
```

## Gemiddelde

De functie `average` retourneert het rekenkundig gemiddelde van alle geselecteerde waarden binnen de array.

**Formaat**

```sql
{ARRAY}.average()
```

**Voorbeeld**

De volgende PQL-query retourneert de gemiddelde prijs van alle bestellingen.

```sql
orders.average(order.price)
```

## Minimaal

De functie `min` retourneert het laagste van alle geselecteerde waarden binnen de array.

**Formaat**

```sql
{ARRAY}.min()
```

**Voorbeeld**

De volgende PQL-query retourneert de laagste prijs van alle bestellingen.

```sql
orders.min(order.price)
```

## Maximum

De functie `max` retourneert de grootste van alle geselecteerde waarden binnen de array.

**Formaat**

```sql
{ARRAY}.max()
```

**Voorbeeld**

De volgende PQL-query retourneert de hoogste prijs voor alle bestellingen.

```sql
orders.max(order.price)
```

## Volgende stappen

Nu u over samenvoegingsfuncties hebt geleerd, kunt u hen binnen uw vragen van PQL gebruiken. Voor meer informatie over andere functies van PQL, te lezen gelieve het [ overzicht van Profile Query Language ](./overview.md).
