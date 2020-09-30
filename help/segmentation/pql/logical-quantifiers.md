---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;logical quantifiers;logical quantifier;
solution: Experience Platform
title: Logische kwantoren
topic: developer guide
description: Logische kwantoren kunnen worden gebruikt om voorwaarden met arrays in Profile Query Language (PQL) te bepalen.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 3%

---


# Logische kwantor-functies

Logische kwantoren kunnen worden gebruikt om omstandigheden met arrays in [!DNL Profile Query Language] (PQL) te bevestigen. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Exists

De `exists` functie bepaalt het bestaan van een item in een array, op voorwaarde dat het aan de opgegeven voorwaarde voldoet.

**Indeling**

```sql
exists {VARIABLE} from {EXPRESSION} where {CONDITION}
exists {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschrijving |
| ---------- | ----------- |
| `{VARIABLE}` | Een naam van een variabele. |
| `{EXPRESSION}` | De array die wordt gecontroleerd. |
| `{CONDITION}` | Een optionele expressie die de waarden in de geretourneerde array filtert. |

**Voorbeeld**

De volgende PQL-query krijgt alle gebeurtenissen met een prijs hoger dan $50 of met een SKU van &#39;PS&#39;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Voor alles

De `forall` functie bepaalt alle items in een array die aan alle opgegeven voorwaarden voldoen.

**Indeling**

```sql
forall {VARIABLE} from {EXPRESSION} where {CONDITION}
forall {VARIABLE} from {EXPRESSION} : {CONDITION}
```

| Argument | Beschrijving |
| ---------- | ----------- |
| `{VARIABLE}` | Een naam van een variabele. |
| `{EXPRESSION}` | De array die wordt gecontroleerd. |
| `{CONDITION}` | Een optionele expressie die de waarden in de geretourneerde array filtert. |

**Voorbeeld**

De volgende PQL-query krijgt alle gebeurtenissen met een prijs hoger dan $50 en een SKU van &#39;PS&#39;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Volgende stappen

Nu u over logische kwantoren hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
