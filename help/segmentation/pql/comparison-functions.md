---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;vergelijkingsfuncties;vergelijking;
solution: Experience Platform
title: PQL-vergelijkingsfuncties
topic: developer guide
description: Vergelijkingsfuncties worden gebruikt om verschillende expressies en waarden met elkaar te vergelijken, waarbij "true" of "false" overeenkomstig wordt geretourneerd.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 7%

---


# Vergelijkingsfuncties

Vergelijkingsfuncties worden gebruikt om tussen verschillende expressies en waarden te vergelijken en `true` of `false` dienovereenkomstig te retourneren. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Equals (Is gelijk aan)

De functie `=` (equals) controleert of één waarde of expressie gelijk is aan een andere waarde of expressie.

**Indeling**

```sql
{EXPRESSION} = {VALUE}
```

**Voorbeeld**

De volgende vraag PQL controleert als het land van het huisadres in Canada is.

```sql
homeAddress.countryISO = "CA"
```

## Niet gelijk

De functie `!=` (niet gelijk aan) controleert of één waarde of expressie **niet** gelijk is aan een andere waarde of expressie.

**Indeling**

```sql
{EXPRESSION} != {VALUE}
```

**Voorbeeld**

De volgende vraag PQL controleert als het land van het huisadres niet in Canada is.

```sql
homeAddress.countryISO != "CA"
```

## Greater than

De functie `>` (groter dan) wordt gebruikt om te controleren of de eerste waarde groter is dan de tweede waarde.

**Indeling**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Voorbeeld**

De volgende PQL-query definieert personen wier verjaardagen niet in januari of februari vallen.

```sql
person.birthMonth > 2
```

## Greater than or equal to

De functie `>=` (groter dan of gelijk aan) wordt gebruikt om te controleren of de eerste waarde groter dan of gelijk aan de tweede waarde is.

**Indeling**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Voorbeeld**

De volgende PQL-query definieert personen wier verjaardagen niet in januari of februari vallen.

```sql
person.birthMonth >= 3
```

## Less than

De vergelijkingsfunctie `<` (kleiner dan) wordt gebruikt om te controleren of de eerste waarde minder is dan de tweede waarde.

**Indeling**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Voorbeeld**

De volgende vraag PQL bepaalt mensen van wie verjaardag in Januari is.

```sql
person.birthMonth < 2
```

## Less than or equal to

De vergelijkingsfunctie `<=` (kleiner dan of gelijk aan) wordt gebruikt om te controleren of de eerste waarde kleiner dan of gelijk aan de tweede waarde is.

**Indeling**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Voorbeeld**

De volgende vraag PQL bepaalt mensen van wie verjaardag in Januari of Februari is.

```sql
person.birthMonth <= 2
```

## Volgende stappen

Nu u over vergelijkingsfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
