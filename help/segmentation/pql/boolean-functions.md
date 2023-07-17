---
solution: Experience Platform
title: Booleaanse functies PQL
description: Booleaanse functies worden gebruikt voor het uitvoeren van Booleaanse logica op verschillende elementen in PQL (Profile Query Language).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 2%

---

# Booleaanse functies

Booleaanse functies worden gebruikt voor het uitvoeren van Booleaanse logica op verschillende elementen in [!DNL Profile Query Language] (PQL).  Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## en

De `and` Deze functie wordt gebruikt om een logische combinatie te maken.

**Indeling**

```sql
{QUERY} and {QUERY}
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen met het thuisland als Canada en het geboortejaar 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## of

De `or` Deze functie wordt gebruikt om een logische scheiding te maken.

**Indeling**

```sql
{QUERY} or {QUERY}
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen met het thuisland als Canada of geboortejaar 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Niet

De `not` (of `!`) wordt gebruikt om een logische negatie te maken.

**Indeling**

```sql
not ({QUERY})
!({QUERY})
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen die hun thuisland niet als Canada hebben.

```sql
not (homeAddress.countryISO = "CA")
```

## Indien

De `if` wordt gebruikt om een expressie op te lossen, afhankelijk van het feit of een opgegeven voorwaarde waar is.

**Indeling**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | De booleaanse expressie die wordt getest. |
| `{TRUE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` is waar. |
| `{FALSE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` is false. |

**Voorbeeld**

De volgende PQL-query stelt de waarde in als `1` als het land van herkomst Canada is en `2` als het land van herkomst geen Canada is.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Volgende stappen

Nu u over booleaanse functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
