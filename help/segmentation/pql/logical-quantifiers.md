---
solution: Experience Platform
title: Logische PQL-kwantoren
description: Logische kwantoren kunnen worden gebruikt om omstandigheden met arrays in Profile Query Language (PQL) te bevestigen.
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Logische kwantor-functies

Logische kwantoren kunnen worden gebruikt om voorwaarden met arrays in [!DNL Profile Query Language] (PQL) te bevestigen. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht &#x200B;](./overview.md) worden gevonden.

## Exists

De functie `exists` bepaalt het bestaan van een item in een array, op voorwaarde dat dit item voldoet aan de opgegeven voorwaarde.

**Formaat**

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

De volgende PQL-query haalt alle gebeurtenissen op met een prijs hoger dan $50 of met een SKU van &#39;PS&#39;.

```sql
exists E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Voor alles

De functie `forall` bepaalt alle items in een array die aan alle opgegeven voorwaarden voldoen.

**Formaat**

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

De volgende PQL-query haalt alle gebeurtenissen op met een prijs hoger dan $50 en een SKU van &#39;PS&#39;.

```sql
forall E from xEvent where (E.commerce.item.price > 50), I from E.productListItems where I.SKU = "PS"
```

## Volgende stappen

Nu u over logische kwantoren hebt geleerd, kunt u hen binnen uw vragen van PQL gebruiken. Voor meer informatie over andere functies van PQL, te lezen gelieve het [&#x200B; overzicht van Profile Query Language &#x200B;](./overview.md).
