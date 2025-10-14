---
solution: Experience Platform
title: Array-, List- en PQL-functies instellen
description: Profile Query Language (PQL) biedt functies om interactie met arrays, lijsten en tekenreeksen eenvoudiger te maken.
exl-id: 5ff2b066-8857-4cde-9932-c8bf09e273d3
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '820'
ht-degree: 0%

---

# Array, list en set-functies

[!DNL Profile Query Language] (PQL) biedt functies om interactie met arrays, lijsten en tekenreeksen eenvoudiger te maken. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht &#x200B;](./overview.md) worden gevonden.

## In

De functie `in` wordt gebruikt om te bepalen of een item lid is van een array of lijst als een booleaanse waarde.

**Formaat**

```sql
{VALUE} in {ARRAY}
```

**Voorbeeld**

De volgende PQL-query definieert personen met verjaardagen in maart, juni of september.

```sql
person.birthMonth in [3, 6, 9]
```

## Niet in

De functie `notIn` wordt gebruikt om te bepalen of een item geen lid is van een array of lijst als een booleaanse waarde.

>[!NOTE]
>
>De `notIn` functie ** zorgt ook ervoor dat geen van beide waarde aan ongeldig is. Daarom zijn de resultaten geen exacte negatie van de functie `in` .

**Formaat**

```sql
{VALUE} notIn {ARRAY}
```

**Voorbeeld**

De volgende PQL-query definieert personen met verjaardagen die zich niet in maart, juni of september bevinden.

```sql
person.birthMonth notIn [3, 6, 9]
```

## Doorsnede

De functie `intersects` wordt gebruikt om te bepalen of twee arrays of lijsten ten minste één gemeenschappelijk lid als een booleaanse waarde hebben.

**Formaat**

```sql
{ARRAY}.intersects({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert personen van wie de favoriete kleuren ten minste een van de kleuren rood, blauw of groen zijn.

```sql
person.favoriteColors.intersects(["red", "blue", "green"])
```

## Doorsnede

De functie `intersection` wordt gebruikt om de algemene leden van twee arrays of lijsten als een lijst te bepalen.

**Formaat**

```sql
{ARRAY}.intersection({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert of persoon 1 en persoon 2 beide favoriete kleuren rood, blauw en groen hebben.

```sql
person1.favoriteColors.intersection(person2.favoriteColors) = ["red", "blue", "green"]
```

## Subset van

De functie `subsetOf` wordt gebruikt om te bepalen of een specifieke array (array A) een subset is van een andere array (array B). Met andere woorden, alle elementen in array A zijn elementen van array B als een booleaanse waarde.

**Formaat**

```sql
{ARRAY}.subsetOf({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert mensen die al hun favoriete steden hebben bezocht.

```sql
person.favoriteCities.subsetOf(person.visitedCities)
```

## Superset van

De functie `supersetOf` wordt gebruikt om te bepalen of een specifieke array (array A) een superset is van een andere array (array B). Met andere woorden, die array A bevat alle elementen in array B als een booleaanse waarde.

**Formaat**

```sql
{ARRAY}.supersetOf({ARRAY})
```

**Voorbeeld**

De volgende PQL-query definieert mensen die sushi en pizza ten minste één keer hebben gegeten.

```sql
person.eatenFoods.supersetOf(["sushi", "pizza"])
```

## Inclusief

De functie `includes` wordt gebruikt om te bepalen of een array of lijst een bepaald item als een booleaanse waarde bevat.

**Formaat**

```sql
{ARRAY}.includes({ITEM})
```

**Voorbeeld**

De volgende PQL-query definieert personen van wie de favoriete kleur rood bevat.

```sql
person.favoriteColors.includes("red")
```

## Afzonderlijk

De functie `distinct` wordt gebruikt om dubbele waarden uit een array of lijst als een array te verwijderen.

**Formaat**

```sql
{ARRAY}.distinct()
```

**Voorbeeld**

Met de volgende PQL-query worden personen opgegeven die orders in meer dan één winkel hebben geplaatst.

```sql
person.orders.storeId.distinct().count() > 1
```

## Groeperen op

De functie `groupBy` wordt gebruikt om waarden van een array of lijst te verdelen in een groep op basis van de waarde van de expressie als een kaart van unieke waarden van de groeperingsexpressie naar arrays die partities zijn van de waarde van de arrayexpressie.

**Formaat**

```sql
{ARRAY}.groupBy({EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{ARRAY}` | De array of lijst die moet worden gegroepeerd. |
| `{EXPRESSION}` | Een expressie die elk item in de array of lijst die wordt geretourneerd, koppelt. |

**Voorbeeld**

De volgende PQL-query groepeert alle bestellingen waarmee de bestelling is opgeslagen.

```sql
xEvent[type="order"].groupBy(storeId)
```

## Filter

De functie `filter` wordt gebruikt om een array of lijst te filteren op basis van een expressie als een array of lijst, afhankelijk van de invoer.

**Formaat**

```sql
{ARRAY}.filter({EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{ARRAY}` | De array of lijst die moet worden gefilterd. |
| `{EXPRESSION}` | Een expressie waarop moet worden gefilterd. |

**Voorbeeld**

De volgende PQL-query definieert alle personen die 21 jaar of ouder zijn.

```sql
person.filter(age >= 21)
```

## Kaart

De functie `map` wordt gebruikt om een nieuwe array te maken door een expressie toe te passen op elk item in een bepaalde array als een array.

**Formaat**

```sql
array.map(expression)
```

**Voorbeeld**

Met de volgende PQL-query wordt een nieuwe array met getallen gemaakt en wordt de waarde van de oorspronkelijke getallen in vierkantjes weergegeven.

```sql
numbers.map(square)
```

## Eerste `n` in array {#first-n}

De functie `topN` wordt gebruikt om de eerste `N` -items in een array te retourneren, wanneer deze in oplopende volgorde worden gesorteerd op basis van de opgegeven numerieke expressie als een array.

**Formaat**

```sql
{ARRAY}.topN({VALUE}, {AMOUNT})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{ARRAY}` | De array of lijst die moet worden gesorteerd. |
| `{VALUE}` | De eigenschap waarin de array of de lijst moet worden gesorteerd. |
| `{AMOUNT}` | Het aantal objecten dat moet worden geretourneerd. |

**Voorbeeld**

De volgende PQL-query retourneert de bovenste vijf bestellingen met de hoogste prijs.

```sql
orders.topN(price, 5)
```

## Laatste `n` in array

De functie `bottomN` wordt gebruikt om de laatste `N` -items in een array te retourneren, wanneer deze in oplopende volgorde worden gesorteerd op basis van de opgegeven numerieke expressie als een array.

**Formaat**

```sql
{ARRAY}.bottomN({VALUE}, {AMOUNT})
```

| Argument | Beschrijving |
| --------- | ----------- | 
| `{ARRAY}` | De array of lijst die moet worden gesorteerd. |
| `{VALUE}` | De eigenschap waarin de array of de lijst moet worden gesorteerd. |
| `{AMOUNT}` | Het aantal objecten dat moet worden geretourneerd. |

**Voorbeeld**

De volgende PQL-query retourneert de bovenste vijf bestellingen met de laagste prijs.

```sql
orders.bottomN(price, 5)
```

## Eerste object

De functie `head` wordt gebruikt om het eerste item in de array of lijst als een object te retourneren.

**Formaat**

```sql
{ARRAY}.head()
```

**Voorbeeld**

De volgende PQL-query retourneert de eerste van de bovenste vijf bestellingen met de hoogste prijs. Meer informatie over de `topN` functie kan in [&#x200B; eerst `n` in serie &#x200B;](#first-n) sectie worden gevonden.

```sql
orders.topN(price, 5).head()
```

## Volgende stappen

Nu u over serie, lijst, en vastgestelde functies hebt geleerd, kunt u hen binnen uw vragen van PQL gebruiken. Voor meer informatie over andere functies van PQL, te lezen gelieve het [&#x200B; overzicht van Profile Query Language &#x200B;](./overview.md).
