---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Objectfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Objectfuncties

PQL (Profile Query Language) biedt functies om interactie met objecten eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## Is null

De `isNull` functie bepaalt of een objectverwijzing niet bestaat.

**Indeling**

```sql
{OBJECT}.isNull()
```

**Voorbeeld**

De volgende vraag PQL controleert als het huisadres van de persoon niet bestaat.

```sql
person.homeAddress.isNull()
```

## Is niet null

De `isNotNull` functie bepaalt of een objectverwijzing bestaat.

**Indeling**

```sql
{OBJECT}.isNotNull()
```

**Voorbeeld**

De volgende vraag PQL controleert als het huisadres van de persoon bestaat.

```sql
person.homeAddress.isNotNull()
```

## Volgende stappen

Nu u over objecten functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.