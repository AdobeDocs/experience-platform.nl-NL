---
solution: Experience Platform
title: PQL-objectfuncties
description: Profile Query Language (PQL) biedt functies om interactie met objecten eenvoudiger te maken.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---

# Objectfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met objecten eenvoudiger te maken. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht ](./overview.md) worden gevonden.

## Is null

De functie `isNull` bepaalt of een objectverwijzing niet bestaat als een booleaanse verwijzing.

**Formaat**

```sql
{OBJECT}.isNull()
```

**Voorbeeld**

De volgende PQL-query controleert of het huisadres van de persoon niet bestaat.

```sql
person.homeAddress.isNull()
```

## Is niet null

De functie `isNotNull` bepaalt of een objectverwijzing bestaat als een booleaanse verwijzing.

**Formaat**

```sql
{OBJECT}.isNotNull()
```

**Voorbeeld**

De volgende PQL-query controleert of het huisadres van de persoon bestaat.

```sql
person.homeAddress.isNotNull()
```

## Volgende stappen

Nu u over objecten functies hebt geleerd, kunt u hen binnen uw vragen van PQL gebruiken. Voor meer informatie over andere functies van PQL, te lezen gelieve het [ overzicht van Profile Query Language ](./overview.md).
