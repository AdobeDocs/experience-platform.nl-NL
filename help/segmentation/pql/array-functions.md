---
solution: Experience Platform
title: Array, List en Set PQL-functies
description: De Taal van de Vraag van het profiel (PQL) biedt functies om interactie met series, lijsten, en koorden gemakkelijker te maken.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '750'
ht-degree: 3%

---

# Array, list en set-functies

[!DNL Profile Query Language] (PQL) biedt functies om interactie met arrays, lijsten en tekenreeksen eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## In

De `in` wordt gebruikt om te bepalen of een punt een lid van een serie of een lijst is.

**Indeling**

```sql
{VALUE} in {ARRAY}
```

**Voorbeeld**

De volgende vraag PQL bepaalt mensen met verjaardagen in Maart, Juni, of September.

```sql
person.birthMonth in [3, 6, 9]
```

## Niet in

De `notIn` wordt gebruikt om te bepalen of een item geen lid is van een array of lijst.

>[!NOTE]
>
>De `notIn` function *ook* zorgt ervoor dat geen van beide waarden gelijk is aan null. Daarom zijn de resultaten geen exacte ontkenning van de `in` functie.

**Indeling**

```sql
{VALUE} notIn {ARRAY}
```

**Voorbeeld**

De volgende vraag PQL bepaalt mensen met verjaardagen die niet in Maart, Juni, of September zijn.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Doorsnede

De `intersects` functie wordt gebruikt om te bepalen of twee series of lijsten minstens één gemeenschappelijk lid hebben.

**Indeling**

```sql
{ARRAY}.intersects({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert personen van wie de favoriete kleuren ten minste een van de kleuren rood, blauw of groen zijn.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Doorsnede

De `intersection` wordt gebruikt om de gemeenschappelijke leden van twee series of lijsten te bepalen.

**Indeling**

```sql
{ARRAY}.intersection({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert of persoon 1 en persoon 2 beide favoriete kleuren rood, blauw en groen hebben.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subset van

De `subsetOf` wordt gebruikt om te bepalen of een specifieke array (array A) een subset is van een andere array (array B). Met andere woorden, alle elementen in array A zijn elementen van array B.

**Indeling**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Voorbeeld**

De volgende vraag PQL bepaalt mensen die elk van hun favoriete steden hebben bezocht.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset van

De `supersetOf` wordt gebruikt om te bepalen of een specifieke array (array A) een superset is van een andere array (array B). Met andere woorden, die array A bevat alle elementen in array B.

**Indeling**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert mensen die sushi en pizza ten minste één keer hebben gegeten.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inclusief

De `includes` wordt gebruikt om te bepalen of een array of lijst een bepaald item bevat.

**Indeling**

```sql
{ARRAY}.includes({ITEM})
```

**Voorbeeld**

De volgende PQL-query definieert personen met de favoriete kleur rood.

```sql
person.favoriteColors.includes("red")
```

## Afzonderlijk

De `distinct` wordt gebruikt om dubbele waarden uit een array of lijst te verwijderen.

**Indeling**

```sql
{ARRAY}.distinct()
```

**Voorbeeld**

De volgende vraag PQL specificeert mensen die orden in meer dan één opslag hebben geplaatst.

```sql
person.orders.storeId.distinct().count() > 1
```

## Groeperen op

De `groupBy` Deze functie wordt gebruikt om waarden van een array of lijst op te delen in een groep op basis van de waarde van de expressie.

**Indeling**

```sql
{ARRAY}.groupBy({EXPRESSION)
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{ARRAY}` | De array of lijst die moet worden gegroepeerd. |
| `{EXPRESSION}` | Een expressie die elk item in de array of lijst die wordt geretourneerd, koppelt. |

**Voorbeeld**

De volgende vraag PQL groepeert alle orden waardoor opslag de orde werd geplaatst bij.

```sql
orders.groupBy(storeId)
```

## Filter

De `filter` wordt gebruikt om een array of lijst te filteren op basis van een expressie.

**Indeling**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{ARRAY}` | De array of lijst die moet worden gefilterd. |
| `{EXPRESSION}` | Een expressie waarop moet worden gefilterd. |

**Voorbeeld**

De volgende vraag PQL bepaalt alle mensen die 21 of ouder zijn.

```sql
person.filter(age >= 21)
```

## Kaart

De `map` wordt gebruikt om een nieuwe array te maken door een expressie toe te passen op elk item in een bepaalde array.

**Indeling**

```sql
array.map(expression)
```

**Voorbeeld**

Met de volgende PQL-query wordt een nieuwe array met getallen gemaakt en wordt de waarde van de oorspronkelijke getallen in vierkantjes geplaatst.

```sql
numbers.map(square)
```

## Eerste `n` in array {#first-n}

De `topN` function wordt gebruikt om de eerste te retourneren `N` items in een array, indien gesorteerd in oplopende volgorde op basis van de opgegeven numerieke expressie.

**Indeling**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{ARRAY}` | De array of lijst die moet worden gesorteerd. |
| `{VALUE}` | De eigenschap waarin de array of de lijst moet worden gesorteerd. |
| `{AMOUNT}` | Het aantal objecten dat moet worden geretourneerd. |

**Voorbeeld**

De volgende vraag PQL keert de hoogste vijf orden met de hoogste prijs terug.

```sql
orders.topN(price, 5)
```

## Laatste `n` in array

De `bottomN` function wordt gebruikt om de laatste te retourneren `N` items in een array, indien gesorteerd in oplopende volgorde op basis van de opgegeven numerieke expressie.

**Indeling**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Beschrijving |
| --------- | ----------- | 
| `{ARRAY}` | De array of lijst die moet worden gesorteerd. |
| `{VALUE}` | De eigenschap waarin de array of de lijst moet worden gesorteerd. |
| `{AMOUNT}` | Het aantal objecten dat moet worden geretourneerd. |

**Voorbeeld**

De volgende vraag PQL keert de hoogste vijf orden met de laagste prijs terug.

```sql
orders.bottomN(price, 5)
```

## Eerste object

De `head` functie wordt gebruikt om het eerste item in de array of lijst te retourneren.

**Indeling**

```sql
{ARRAY}.head()
```

**Voorbeeld**

De volgende vraag PQL keert eerste van de hoogste vijf orden met de hoogste prijs terug. Meer informatie over de `topN` kan worden gevonden in de [first `n` in array](#first-n) sectie.

```sql
orders.topN(price, 5).head()
```

## Volgende stappen

Nu u over serie, lijst, en vastgestelde functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
