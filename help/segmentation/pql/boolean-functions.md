---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;boolean-functies;boolean;
solution: Experience Platform
title: Booleaanse functies PQL
topic: developer guide
description: Booleaanse functies worden gebruikt voor het uitvoeren van Booleaanse logica op verschillende elementen in PQL (Profile Query Language).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 2%

---


# Booleaanse functies

Booleaanse functies worden gebruikt om booleaanse logica uit te voeren op verschillende elementen in [!DNL Profile Query Language] (PQL).  Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## en

De functie `and` wordt gebruikt om een logische samenhang tot stand te brengen.

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

De functie `or` wordt gebruikt om een logische scheiding tot stand te brengen.

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

De functie `not` (of `!`) wordt gebruikt om een logische negatie tot stand te brengen.

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

De functie `if` wordt gebruikt om een uitdrukking op te lossen afhankelijk van of een gespecificeerde voorwaarde waar is.

**Indeling**

```sql
if ({TEST_EXPRESSION}, {TRUE_EXPRESSION}, {FALSE_EXPRESSION})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{TEST_EXPRESSION}` | De booleaanse expressie die wordt getest. |
| `{TRUE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` waar is. |
| `{FALSE_EXPRESSION}` | De expressie waarvan de waarde wordt gebruikt als `{TEST_EXPRESSION}` false is. |

**Voorbeeld**

De volgende PQL-query stelt de waarde in als `1` als het thuisland Canada is en `2` als het thuisland geen Canada is.

```sql
if (homeAddress.countryISO = "CA", 1, 2)
```

## Volgende stappen

Nu u over booleaanse functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
