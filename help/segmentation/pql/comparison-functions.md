---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Vergelijkingsfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Vergelijkingsfuncties

Vergelijkingsfuncties worden gebruikt om verschillende expressies en waarden met elkaar te vergelijken, `true` of `false` op basis daarvan. Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## Gelijk

De functie `=` (equals) controleert of een waarde of expressie gelijk is aan een andere waarde of expressie.

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

De functie `!=` (niet gelijk aan) controleert of een waarde of expressie **niet** gelijk is aan een andere waarde of expressie.

**Indeling**

```sql
{EXPRESSION} != {VALUE}
```

**Voorbeeld**

De volgende vraag PQL controleert als het land van het huisadres niet in Canada is.

```sql
homeAddress.countryISO != "CA"
```

## Groter dan

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

## Groter dan of gelijk aan

De functie `>=` (groter dan of gelijk aan) wordt gebruikt om te controleren of de eerste waarde groter dan of gelijk is aan de tweede waarde.

**Indeling**

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

**Indeling**

```sql
{EXPRESSION} < {EXPRESSION} 
```

**Voorbeeld**

De volgende vraag PQL bepaalt mensen van wie verjaardag in Januari is.

```sql
person.birthMonth < 2
```

## Kleiner dan of gelijk aan

De vergelijkingsfunctie `<=` (kleiner dan of gelijk aan) wordt gebruikt om te controleren of de eerste waarde kleiner dan of gelijk is aan de tweede waarde.

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

Nu u over vergelijkingsfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
