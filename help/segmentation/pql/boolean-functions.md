---
solution: Experience Platform
title: PQL Boolean-functies
description: Booleaanse functies worden gebruikt om booleaanse logica uit te voeren op verschillende elementen in Profile Query Language (PQL).
exl-id: 68a4a8cc-88ad-41b1-b9fc-c2b4ab7d0122
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Booleaanse functies

Booleaanse functies worden gebruikt om booleaanse logica uit te voeren op verschillende elementen in [!DNL Profile Query Language] (PQL).  Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht &#x200B;](./overview.md) worden gevonden.

## en

De functie `and` wordt gebruikt om een logische combinatie als booleaanse waarde te maken.

**Formaat**

```sql
{QUERY} and {QUERY}
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen met het thuisland als Canada en het geboortejaar 1985.

```sql
homeAddress.countryISO = "CA" and person.birthYear = 1985
```

## of

De functie `or` wordt gebruikt om een logische scheiding als booleaanse verbinding te maken.

**Formaat**

```sql
{QUERY} or {QUERY}
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen met het thuisland als Canada of geboortejaar 1985.

```sql
homeAddress.countryISO = "CA" or person.birthYear = 1985
```

## Niet

De functie `not` (of `!` ) wordt gebruikt om een logische negatie te maken.

**Formaat**

```sql
not ({QUERY})
!({QUERY})
```

**Voorbeeld**

De volgende PQL-query retourneert alle mensen die geen thuisland als Canada hebben.

```sql
not (homeAddress.countryISO = "CA")
```

## Indien

De functie `if` wordt gebruikt om een expressie op te lossen, afhankelijk van het feit of een opgegeven voorwaarde true is als een Booleaanse waarde.

**Formaat**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | De booleaanse expressie die wordt getest. |
| `{TRUE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` true is. |
| `{FALSE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` false is. |

**Voorbeeld**

De volgende PQL-query stelt de waarde in als `1` als het thuisland Canada is en `2` als het thuisland geen Canada is.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Volgende stappen

Nu u over booleaanse functies hebt geleerd, kunt u deze gebruiken binnen uw PQL-query&#39;s. Voor meer informatie over andere functies van PQL, te lezen gelieve het [&#x200B; overzicht van Profile Query Language &#x200B;](./overview.md).
