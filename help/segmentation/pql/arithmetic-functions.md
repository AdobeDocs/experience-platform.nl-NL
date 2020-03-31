---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Rekenkundige functies
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Rekenkundige functies

De rekenkundige functies worden gebruikt om basisberekeningen op waarden in de Taal van de Vraag van het Profiel (PQL) uit te voeren. Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## Toevoegen

De functie `+` (optellen) wordt gebruikt om de som van twee argumentuitdrukkingen te vinden.

**Indeling**

```sql
{NUMBER} + {NUMBER}
```

**Voorbeeld**

De volgende vraag PQL sommen de prijs van twee verschillende producten.

```sql
product1.price + product2.price
```

## Vermenigvuldigen

De functie `*` (vermenigvuldigen) wordt gebruikt om het product van twee argumentexpressies te zoeken.

**Indeling**

```sql
{NUMBER} * {NUMBER}
```

**Voorbeeld**

De volgende vraag PQL vindt het product van de inventaris en de prijs van een product om de bruto waarde van het product te vinden.

```sql
product.inventory * product.price
```

## Aftrekken

De functie `-` (aftrekken) wordt gebruikt om het verschil tussen twee argumentexpressies te vinden.

**Indeling**

```sql
{NUMBER} - {NUMBER}
```

**Voorbeeld**

De volgende vraag PQL vindt het verschil in prijs tussen twee verschillende producten.

```sql
product1.price - product2.price
```

## Verdelen

De functie `/` (delen) wordt gebruikt om het quotiënt van twee argumentexpressies te vinden.

**Indeling**

```sql
{NUMBER} / {NUMBER}
```

**Voorbeeld**

Met de volgende PQL-query wordt het quotiënt gevonden tussen de totale verkochte producten en het totale verdiende geld om de gemiddelde kosten per object te zien.

```sql
totalProduct.price / totalProduct.sold
```

## Herinnering

De functie `%` (restbepaling bij deling/restbepaling) wordt gebruikt om de rest te zoeken na het delen van de twee argumentexpressies.

**Indeling**

```sql
{NUMBER} % {NUMBER}
```

**Voorbeeld**

De volgende vraag PQL controleert als de leeftijd van de persoon door vijf deelbaar is.

```sql
person.age % 5 = 0
```

## Volgende stappen

Nu u over rekenkundige functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
