---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;De Taal van de Vraag van het profiel;logische kwantoren;logische kwantor;
solution: Experience Platform
title: Logische kwantoren van PQL
topic: developer guide
description: Logische kwantoren kunnen worden gebruikt om voorwaarden met arrays in Profile Query Language (PQL) te bepalen.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---


# Logische kwantor-functies

Logische kwantoren kunnen worden gebruikt om voorwaarden met arrays in [!DNL Profile Query Language] (PQL) te bevestigen. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Exists

De functie `exists` bepaalt het bestaan van een punt in een serie, op voorwaarde dat het aan de verstrekte voorwaarde voldoet.

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

De functie `forall` bepaalt alle items in een array die aan alle opgegeven voorwaarden voldoen.

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

Nu u over logische kwantoren hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
