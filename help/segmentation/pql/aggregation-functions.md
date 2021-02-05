---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;De Taal van de Vraag van het profiel;samenvoegingsfuncties;samenvoeging;
solution: Experience Platform
title: PQL-aggregatiefuncties
topic: developer guide
description: 'Samenvoegfuncties worden gebruikt om meerdere waarden binnen PQL-arrays (Profile Query Language) te groeperen en één samenvattingswaarde te maken. '
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 2%

---


# Samenvoegingsfuncties

Samenvoegfuncties worden gebruikt om meerdere waarden binnen [!DNL Profile Query Language] (PQL) arrays te groeperen en één samenvattingswaarde te vormen. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Aantal

De functie `count` retourneert het aantal elementen binnen de opgegeven array.

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

De functie `sum` retourneert de som van alle geselecteerde waarden binnen de array.

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

De functie `average` retourneert het rekenkundig gemiddelde van alle geselecteerde waarden binnen de array.

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

De functie `min` retourneert de kleinste van alle geselecteerde waarden binnen de array.

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

De functie `max` retourneert de grootste van alle geselecteerde waarden binnen de array.

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

Nu u over samenvoegingsfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
