---
solution: Experience Platform
title: Datum- en tijdfuncties van PQL
description: Datum- en tijdfuncties worden gebruikt om datum- en tijdbewerkingen uit te voeren op waarden in Profile Query Language (PQL).
exl-id: 8cbffcb6-1c25-454f-8f02-eca602318e5e
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Datum- en tijdfuncties

Datum- en tijdfuncties worden gebruikt om datum- en tijdbewerkingen uit te voeren op waarden binnen [!DNL Profile Query Language] (PQL). Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht &#x200B;](./overview.md) worden gevonden.

## Huidige maand

De functie `currentMonth` retourneert de huidige maand als een geheel getal.

**Formaat**

```sql
currentMonth()
```

**Voorbeeld**

De volgende PQL-query controleert of de geboortemaand van de persoon de huidige maand is.

```sql
person.birthMonth = currentMonth()
```

## Maand ophalen

De functie `getMonth` retourneert de maand als een geheel getal op basis van een opgegeven tijdstempel.

**Formaat**

```sql
{TIMESTAMP}.getMonth()
```

**Voorbeeld**

De volgende PQL-query controleert of de geboortemaand van de persoon in juni is.

```sql
person.birthdate.getMonth() = 6
```

## Huidig jaar

De functie `currentYear` retourneert het huidige jaar als een geheel getal.

**Formaat**

```sql
currentYear()
```

**Voorbeeld**

De volgende PQL-query controleert of het product in het huidige jaar is verkocht.

```sql
product.saleYear = currentYear()
```

## Jaar ophalen

De functie `getYear` retourneert het jaar, als een geheel getal, op basis van een opgegeven tijdstempel.

**Formaat**

```sql
{TIMESTAMP}.getYear()
```

**Voorbeeld**

De volgende PQL controleert of het geboortejaar van de persoon in 1991, 1992, 1993, 1994 of 1995 valt.

```sql
person.birthday.getYear() in [1991, 1992, 1993, 1994, 1995]
```

## Huidige dag van maand

De functie `currentDayOfMonth` retourneert de huidige dag van de maand als een geheel getal.

**Formaat**

```sql
currentDayOfMonth()
```

**Voorbeeld**

De volgende PQL-query controleert of de geboortedag van de persoon overeenkomt met de huidige dag van de maand.

```sql
person.birthDay = currentDayOfMonth()
```

## Dag van de maand ophalen

De functie `getDayOfMonth` retourneert de dag als een geheel getal op basis van een opgegeven tijdstempel.

**Formaat**

```sql
{TIMESTAMP}.getDayOfMonth()
```

**Voorbeeld**

De volgende PQL-query controleert of het object binnen de eerste 15 dagen van de maand is verkocht.

```sql
product.sale.getDayOfMonth() <= 15
```

## Occurs

De functie `occurs` vergelijkt de opgegeven tijdstempelfunctie met een vaste tijdsperiode als een booleaanse functie.

**Formaat**

De functie `occurs` kan met een van de volgende indelingen worden geschreven:

```sql
{TIMESTAMP} occurs {COMPARISON} {INTEGER} {TIME_UNIT} {DIRECTION} {TIME}
{TIMESTAMP} occurs {DIRECTION} {TIME}
{TIMESTAMP} occurs (on) {TIME}
{TIMESTAMP} occurs between {TIME} and {TIME}
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{COMPARISON}` | Een vergelijkingsoperator. Kan een van de volgende operatoren zijn: `>`, `>=`, `<`, `<=`, `=`, `!=` . Meer informatie over de vergelijkingsfuncties kan in het [&#x200B; document van vergelijkingsfuncties worden gevonden &#x200B;](./comparison-functions.md). |
| `{INTEGER}` | Een positief geheel getal. |
| `{TIME_UNIT}` | Een tijdseenheid. Kan een van de volgende woorden zijn: `millisecond(s)`, `second(s)`, `minute(s)`, `hour(s)`, `day(s)`, `week(s)`, `month(s)`, `year(s)`, `decade(s)`, `century`, `centuries`, `millennium`, `millennia` . |
| `{DIRECTION}` | Een voorstelling waarin wordt beschreven wanneer de datum moet worden vergeleken met. Kan een van de volgende woorden zijn: `before`, `after`, `from` . |
| `{TIME}` | Dit kan een letterlijke tijdstempel (`today`, `now`, `yesterday`, `tomorrow`), een relatieve tijdeenheid (een van `this`, `last` of `next` gevolgd door een tijdstempelkenmerk) of een tijdstempelkenmerk zijn. |

>[!NOTE]
>
>Het gebruik van het woord `on` is optioneel. Er is een functie waarmee bepaalde combinaties, zoals `timestamp occurs on date(2019,12,31)`, beter leesbaar kunnen worden gemaakt.

**Voorbeeld**

De volgende PQL-query controleert of het object vorige week is verkocht.

```sql
product.saleDate occurs last week
```

De volgende PQL-query controleert of een object is verkocht tussen 8 januari 2015 en 1 juli 2017.

```sql
product.saleDate occurs between date(2015, 1, 8) and date(2017, 7, 1)
```

## Nu

`now` is een gereserveerd woord dat het tijdstempel van de PQL-uitvoering vertegenwoordigt.

**Voorbeeld**

De volgende PQL-query controleert of een object precies drie uur eerder is verkocht.

```sql
product.saleDate occurs = 3 hours before now
```

## Vandaag

`today` is een gereserveerd woord dat staat voor het tijdstempel van het begin van de dag waarop de PQL wordt uitgevoerd.

**Voorbeeld**

De volgende PQL-query controleert of iemand drie dagen geleden jarig was.

```sql
person.birthday occurs = 3 days before today
```

## Volgende stappen

Nu u over datum en tijdfuncties hebt geleerd, kunt u deze gebruiken in uw PQL-query&#39;s. Voor meer informatie over andere functies van PQL, te lezen gelieve het [&#x200B; overzicht van Profile Query Language &#x200B;](./overview.md).
