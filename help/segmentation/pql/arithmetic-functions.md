---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;De Taal van de Vraag van het profiel;rekenkundige functies;rekenkunde;
solution: Experience Platform
title: Rekenkundige functies van PAL
topic: developer guide
description: De rekenkundige functies worden gebruikt om basisberekeningen op waarden in de Taal van de Vraag van het Profiel (PQL) uit te voeren.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 2%

---


# Rekenkundige functies

Rekenkundige functies worden gebruikt voor het uitvoeren van basisberekeningen op waarden in [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Toevoegen

De functie `+` (optellen) wordt gebruikt om de som twee argumentuitdrukkingen te vinden.

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

De functie `*` (vermenigvuldiging) wordt gebruikt om het product van twee argumentuitdrukkingen te vinden.

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

De functie `-` (aftrekken) wordt gebruikt om het verschil van twee argumentuitdrukkingen te vinden.

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

De functie `/` (delen) wordt gebruikt om het quotiënt van twee argumentuitdrukkingen te vinden.

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

Nu u over rekenkundige functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
