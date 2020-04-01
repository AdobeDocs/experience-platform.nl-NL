---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Datum- en tijdfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Datum- en tijdfuncties

Datum- en tijdfuncties worden gebruikt om datum- en tijdbewerkingen uit te voeren op waarden in de taal van de profielquery (PQL). Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## Huidige maand

De `currentMonth` functie retourneert de huidige maand als een geheel getal.

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

De `getMonth` functie retourneert de maand als een geheel getal op basis van een opgegeven tijdstempel.

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

De `getYear` functie retourneert het jaar als een geheel getal op basis van een opgegeven tijdstempel.

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

De `currentDayOfMonth` functie retourneert de huidige dag van de maand als een geheel getal.

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

De `getDayOfMonth` functie retourneert de dag als een geheel getal op basis van een opgegeven tijdstempel.

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

De `occurs` functie vergelijkt de opgegeven tijdstempelfunctie met een vaste tijdsperiode.

**Indeling**

De `occurs` functie kan worden geschreven met een van de volgende indelingen:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{COMPARISON}` | Een vergelijkingsoperator. Kan een van de volgende operatoren zijn: `>`, `>=`, `<`, `<=`, `=`, `!=`. Meer informatie over de vergelijkingsfuncties vindt u in het document [met](./comparison-functions.md)vergelijkingsfuncties. |
| `{INTEGER}` | Een positief geheel getal. |
| `{TIME_UNIT}` | Een tijdseenheid. Kan een van de volgende woorden zijn: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century``centuries``millennium``millennia`, . |
| `{DIRECTION}` | Een voorstelling waarin wordt beschreven wanneer de datum moet worden vergeleken met. Kan een van de volgende woorden zijn: `before`, `after`, `from`. |
| `{TIME}` | Dit kan een letterlijke tijdstempel (`today`, `now`, `yesterday`, `tomorrow`), een relatieve tijdeenheid (een van `this`, `last`of `next` gevolgd door een tijdeenheid) of een tijdstempelkenmerk zijn. |

>[!NOTE] Het gebruik van het woord `on` is optioneel. Het is nodig om de leesbaarheid van bepaalde combinaties, zoals `timestamp occurs on date(2019,12,31)`bijvoorbeeld, te verbeteren.

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

Nu u over datum en tijdfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
