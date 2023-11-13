---
solution: Experience Platform
title: Rekenkundige functies van PAL
description: De rekenkundige functies worden gebruikt om basisberekeningen op waarden in de Taal van de Vraag van het Profiel (PQL) uit te voeren.
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 2%

---

# Rekenkundige functies

Rekenkundige functies worden gebruikt voor het uitvoeren van basisberekeningen voor waarden in [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## Toevoegen

De `+` (optellen) functie wordt gebruikt om de som twee argumentuitdrukkingen te vinden.

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

De `*` (vermenigvuldigen) functie wordt gebruikt om het product van twee argument uitdrukkingen te vinden.

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

De `-` (aftrekken) functie wordt gebruikt om het verschil tussen twee argument expressies te vinden.

**Indeling**

```sql
{NUMBER} - {NUMBER}
```

**Voorbeeld**

De volgende vraag PQL vindt het verschil in prijs tussen twee verschillende producten.

```sql
product1.price - product2.price
```

## Splitsen

De `/` (delen) wordt gebruikt om het quotiënt van twee argumentuitdrukkingen te vinden.

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

De `%` (restbepaling bij deling/rest) wordt gebruikt om de rest te zoeken na het delen van de twee argumentexpressies.

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

Nu u over rekenkundige functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
