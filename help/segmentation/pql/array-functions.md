---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;array-functies;array;
solution: Experience Platform
title: Array, List en Set PQL-functies
topic: developer guide
description: De Taal van de Vraag van het profiel (PQL) biedt functies om interactie met series, lijsten, en koorden gemakkelijker te maken.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '767'
ht-degree: 2%

---


# Array, list en set-functies

[!DNL Profile Query Language] (PQL) biedt functies om interactie met arrays, lijsten en tekenreeksen eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## In

De functie `in` wordt gebruikt om te bepalen of een punt een lid van een serie of een lijst is.

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

De functie `notIn` wordt gebruikt om te bepalen als een punt geen lid van een serie of een lijst is.

>[!NOTE]
>
>De `notIn` functie *also* zorgt ervoor dat geen van beide waarden gelijk aan null is. Daarom zijn de resultaten geen exacte negatie van de functie `in`.

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

De functie `intersects` wordt gebruikt om te bepalen of twee series of lijsten minstens één gemeenschappelijk lid hebben.

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

De functie `intersection` wordt gebruikt om de gemeenschappelijke leden van twee series of lijsten te bepalen.

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

De functie `subsetOf` wordt gebruikt om te bepalen of een specifieke array (array A) een subset is van een andere array (array B). Met andere woorden, alle elementen in array A zijn elementen van array B.

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

De functie `supersetOf` wordt gebruikt om te bepalen of een specifieke array (array A) een superset is van een andere array (array B). Met andere woorden, die array A bevat alle elementen in array B.

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

De functie `includes` wordt gebruikt om te bepalen of een serie of een lijst een bepaald punt bevat.

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

De functie `distinct` wordt gebruikt om dubbele waarden uit een serie of een lijst te verwijderen.

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

De functie `groupBy` wordt gebruikt om waarden van een serie of lijst in een groep te verdelen die op de waarde van de uitdrukking wordt gebaseerd.

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

De functie `filter` wordt gebruikt om een serie of een lijst te filtreren die op een uitdrukking wordt gebaseerd.

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

De functie `map` wordt gebruikt om een nieuwe serie tot stand te brengen door een uitdrukking op elk punt in een bepaalde serie toe te passen.

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

De functie `topN` wordt gebruikt om de eerste `N` punten in een serie terug te keren, wanneer gesorteerd in oplopende orde die op de bepaalde numerieke uitdrukking wordt gebaseerd.

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

De functie `bottomN` wordt gebruikt om de laatste `N` punten in een serie terug te keren, wanneer gesorteerd in oplopende orde die op de bepaalde numerieke uitdrukking wordt gebaseerd.

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

De functie `head` wordt gebruikt om het eerste item in de array of lijst te retourneren.

**Indeling**

```sql
{ARRAY}.head()
```

**Voorbeeld**

De volgende vraag PQL keert eerste van de hoogste vijf orden met de hoogste prijs terug. Meer informatie over de functie `topN` vindt u in de sectie [first `n` in array](#first-n).

```sql
orders.topN(price, 5).head()
```

## Volgende stappen

Nu u over serie, lijst, en vastgestelde functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
