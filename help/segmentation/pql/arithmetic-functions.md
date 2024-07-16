---
solution: Experience Platform
title: Rekenkundige functies van PAL
description: Rekenkundige functies worden gebruikt voor het uitvoeren van basisberekeningen voor waarden in Profile Query Language (PQL).
exl-id: 3540ef7c-dbe4-4302-a414-3cf85618f870
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Rekenkundige functies

Rekenkundige functies worden gebruikt voor het uitvoeren van basisberekeningen voor waarden in [!DNL Profile Query Language] (PQL). Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht ](./overview.md) worden gevonden.

## Toevoegen

De functie `+` (optellen) wordt gebruikt om de som twee argumentuitdrukkingen te vinden.

**Formaat**

```sql
{NUMBER} + {NUMBER}
```

**Voorbeeld**

In de volgende PQL-query wordt de prijs van twee verschillende producten samengevat.

```sql
product1.price + product2.price
```

## Vermenigvuldigen

De functie `*` (vermenigvuldigen) wordt gebruikt om het product van twee argumentexpressies te vinden.

**Formaat**

```sql
{NUMBER} * {NUMBER}
```

**Voorbeeld**

In de volgende PQL-query worden het product van de voorraad en de prijs van een product gevonden om de brutowaarde van het product te vinden.

```sql
product.inventory * product.price
```

## Aftrekken

De functie `-` (aftrekken) wordt gebruikt om het verschil tussen twee argumentexpressies te zoeken.

**Formaat**

```sql
{NUMBER} - {NUMBER}
```

**Voorbeeld**

Met de volgende PQL-query wordt het prijsverschil tussen twee verschillende producten gevonden.

```sql
product1.price - product2.price
```

## Splitsen

De functie `/` (delen) wordt gebruikt om het quotiënt van twee argumentuitdrukkingen te vinden.

**Formaat**

```sql
{NUMBER} / {NUMBER}
```

**Voorbeeld**

In de volgende PQL-query wordt het quotiënt gevonden tussen de totale verkochte producten en het totale verdiende geld om de gemiddelde kosten per object te zien.

```sql
totalProduct.price / totalProduct.sold
```

## Herinnering

De functie `%` (restbepaling bij deling/restbepaling) wordt gebruikt om de rest te zoeken na het delen van de twee argumentexpressies.

**Formaat**

```sql
{NUMBER} % {NUMBER}
```

**Voorbeeld**

De volgende PQL-query controleert of de leeftijd van de persoon door vijf kan worden gedeeld.

```sql
person.age % 5 = 0
```

## Volgende stappen

Nu u over rekenkundige functies hebt geleerd, kunt u deze gebruiken binnen uw PQL-query&#39;s. Voor meer informatie over andere functies van PQL, te lezen gelieve het [ overzicht van Profile Query Language ](./overview.md).
