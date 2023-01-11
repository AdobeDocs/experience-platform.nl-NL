---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;vergelijkingsfuncties;vergelijking;
solution: Experience Platform
title: PQL-vergelijkingsfuncties
description: Vergelijkingsfuncties worden gebruikt om verschillende expressies en waarden met elkaar te vergelijken, waarbij "true" of "false" overeenkomstig wordt geretourneerd.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 7%

---

# Vergelijkingsfuncties

Vergelijkingsfuncties worden gebruikt om verschillende expressies en waarden met elkaar te vergelijken en retourneren `true` of `false` dienovereenkomstig. Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## Equals (Is gelijk aan)

De `=` (equals) functie controleert of één waarde of expressie gelijk is aan een andere waarde of expressie.

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

De `!=` (niet gelijk aan) functie controleert of één waarde of expressie **niet** gelijk aan een andere waarde of expressie.

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

De `>` (groter dan) wordt gebruikt om te controleren of de eerste waarde groter is dan de tweede waarde.

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

De `>=` (groter dan of gelijk aan) functie wordt gebruikt om te controleren of de eerste waarde groter dan of gelijk aan de tweede waarde is.

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

De `<` (kleiner dan) vergelijkingsfunctie wordt gebruikt om te controleren of de eerste waarde kleiner is dan de tweede waarde.

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

De `<=` (kleiner dan of gelijk aan) vergelijkingsfunctie wordt gebruikt om te controleren of de eerste waarde kleiner dan of gelijk is aan de tweede waarde.

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

Nu u over vergelijkingsfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
