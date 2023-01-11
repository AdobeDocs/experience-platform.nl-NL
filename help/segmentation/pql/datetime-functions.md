---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsdienst;pql;PQL;De Taal van de Vraag van het profiel;datum en tijdfuncties;datetime functies;datetime;date;time;
solution: Experience Platform
title: PQL Datum- en tijdfuncties
description: Datum- en tijdfuncties worden gebruikt om datum- en tijdbewerkingen uit te voeren op waarden in de taal van de profielquery (PQL).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 2%

---

# Datum- en tijdfuncties

Datum- en tijdfuncties worden gebruikt voor het uitvoeren van datum- en tijdbewerkingen op waarden binnen [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## Huidige maand

De `currentMonth` Deze functie retourneert de huidige maand als een geheel getal.

**Indeling**

```sql
currentMonth()
```

**Voorbeeld**

De volgende vraag PQL controleert als de geboortemaand van de persoon de huidige maand is.

```sql
person.birthMonth = currentMonth()
```

## Maand ophalen

De `getMonth` Deze functie retourneert de maand als een geheel getal op basis van een opgegeven tijdstempel.

**Indeling**

```sql
{TIMESTAMP}.getMonth()
```

**Voorbeeld**

De volgende vraag PQL controleert als de geboortemaand van de persoon in Juni is.

```sql
person.birthdate.getMonth() = 6
```

## Huidig jaar

De `currentYear` functie retourneert het huidige jaar als een geheel getal.

**Indeling**

```sql
currentYear()
```

**Voorbeeld**

De volgende PQL-query controleert of het product in het huidige jaar is verkocht.

```sql
product.saleYear = currentYear()
```

## Jaar ophalen

De `getYear` Deze functie retourneert het jaar, als een geheel getal, op basis van een opgegeven tijdstempel.

**Indeling**

```sql
{TIMESTAMP}.getYear()
```

**Voorbeeld**

De volgende PQL-query controleert of het geboortejaar van de persoon in 1991, 1992, 1993, 1994 of 1995 valt.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Huidige dag van de maand

De `currentDayOfMonth` Deze functie retourneert de huidige dag van de maand als een geheel getal.

**Indeling**

```sql
currentDayOfMonth()
```

**Voorbeeld**

De volgende PQL-query controleert of de geboortedag van de persoon overeenkomt met de huidige dag van de maand.

```sql
person.birthDay = currentDayOfMonth()
```

## Dag van de maand ophalen

De `getDayOfMonth` Deze functie retourneert de dag als een geheel getal op basis van een opgegeven tijdstempel.

**Indeling**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Voorbeeld**

De volgende PQL-query controleert of het object binnen de eerste 15 dagen van de maand is verkocht.

```sql
product.sale.getDayOfMonth() <= 15
```

## Occurs

De `occurs` Deze functie vergelijkt de opgegeven tijdstempelfunctie met een vaste tijdsperiode.

**Indeling**

De `occurs` Deze functie kan in een van de volgende indelingen worden geschreven:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{COMPARISON}` | Een vergelijkingsoperator. Kan een van de volgende operatoren zijn: `>`, `>=`, `<`, `<=`, `=`, `!=`. Meer informatie over de vergelijkingsfuncties vindt u in het gedeelte [document met vergelijkingsfuncties](./comparison-functions.md). |
| `{INTEGER}` | Een positief geheel getal. |
| `{TIME_UNIT}` | Een tijdseenheid. Kan een van de volgende woorden zijn: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia`. |
| `{DIRECTION}` | Een voorstelling waarin wordt beschreven wanneer de datum moet worden vergeleken met. Kan een van de volgende woorden zijn: `before`, `after`, `from`. |
| `{TIME}` | Kan een letterlijke tijdstempel zijn (`today`, `now`, `yesterday`, `tomorrow`), een relatieve tijdeenheid (een van de `this`, `last`, of `next` gevolgd door een tijdeenheid) of een tijdstempelkenmerk. |

>[!NOTE]
>
>Gebruik van het woord `on` is optioneel. Het is mogelijk de leesbaarheid van bepaalde combinaties te verbeteren, zoals `timestamp occurs on date(2019,12,31)`.

**Voorbeeld**

De volgende PQL-query controleert of het item vorige week is verkocht.

```sql
product.saleDate occurs last week
```

De volgende PQL-query controleert of een item is verkocht tussen 8 januari 2015 en 1 juli 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Nu

`now` is een gereserveerd woord dat het tijdstempel van de uitvoering van de PQL vertegenwoordigt.

**Voorbeeld**

De volgende PQL-query controleert of een item precies drie uur eerder is verkocht.

```sql
product.saleDate occurs = 3 hours before now
```

## Vandaag

`today` is een gereserveerd woord dat de tijdstempel vertegenwoordigt van het begin van de dag van de PQL-uitvoering.

**Voorbeeld**

De volgende PQL-query controleert of een persoon drie dagen geleden jarig was.

```sql
person.birthday occurs = 3 days before today
```

## Volgende stappen

Nu u over datum en tijdfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
