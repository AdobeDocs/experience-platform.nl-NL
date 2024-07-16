---
solution: Experience Platform
title: Vergelijkingsfuncties van PQL
description: Vergelijkingsfuncties worden gebruikt om verschillende expressies en waarden met elkaar te vergelijken, waarbij "true" of "false" overeenkomstig wordt geretourneerd.
exl-id: 15f106c7-b88b-4042-b925-703e2a309573
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Vergelijkingsfuncties

Vergelijkingsfuncties worden gebruikt om verschillende expressies en waarden met elkaar te vergelijken en `true` of `false` dienovereenkomstig te retourneren. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht ](./overview.md) worden gevonden.

## Gelijk

De functie `=` (equals) controleert of een waarde of expressie gelijk is aan een andere waarde of expressie.

**Formaat**

```sql
{EXPRESSION} = {VALUE}
```

**Voorbeeld**

De volgende PQL-query controleert of het thuisadresland zich in Canada bevindt.

```sql
homeAddress.countryISO = "CA"
```

## Niet gelijk

De `!=` (niet gelijk aan) functie controleert of één waarde of uitdrukking **** niet gelijk aan een andere waarde of een uitdrukking is.

**Formaat**

```sql
{EXPRESSION} != {VALUE}
```

**Voorbeeld**

De volgende PQL-query controleert of het thuisadresland zich niet in Canada bevindt.

```sql
homeAddress.countryISO != "CA"
```

## Groter dan

De functie `>` (groter dan) wordt gebruikt om te controleren of de eerste waarde groter is dan de tweede waarde.

**Formaat**

```sql
{EXPRESSION} > {EXPRESSION} 
```

**Voorbeeld**

De volgende PQL-query definieert personen wier verjaardagen niet in januari of februari vallen.

```sql
person.birthMonth > 2
```

## Groter dan of gelijk aan

De functie `>=` (groter dan of gelijk aan) wordt gebruikt om te controleren of de eerste waarde groter dan of gelijk is aan de tweede waarde.

**Formaat**

```sql
{EXPRESSION} >= {EXPRESSION} 
```

**Voorbeeld**

De volgende PQL-query definieert personen wier verjaardagen niet in januari of februari vallen.

```sql
person.birthMonth >= 3
```

## Minder dan

De vergelijkingsfunctie `<` (kleiner dan) wordt gebruikt om te controleren of de eerste waarde kleiner is dan de tweede waarde.

**Formaat**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Voorbeeld**

In de volgende PQL-query worden personen gedefinieerd die in januari jarig zijn.

```sql
person.birthMonth < 2
```

## Kleiner dan of gelijk aan

De vergelijkingsfunctie `<=` (kleiner dan of gelijk aan) wordt gebruikt om te controleren of de eerste waarde kleiner dan of gelijk is aan de tweede waarde.

**Formaat**

```sql
{EXPRESSION} <= {EXPRESSION} 
```

**Voorbeeld**

De volgende PQL-query definieert personen van wie de geboortedatum in januari of februari is.

```sql
person.birthMonth <= 2
```

## Volgende stappen

Nu u over vergelijkingsfuncties hebt geleerd, kunt u hen binnen uw vragen van PQL gebruiken. Voor meer informatie over andere functies van PQL, te lezen gelieve het [ overzicht van Profile Query Language ](./overview.md).
