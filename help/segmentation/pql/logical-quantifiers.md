---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;De Taal van de Vraag van het profiel;logische kwantoren;logische kwantor;
solution: Experience Platform
title: Logische kwantoren van PQL
description: Logische kwantoren kunnen worden gebruikt om voorwaarden met arrays in Profile Query Language (PQL) te bepalen.
exl-id: 8b1c9560-02e2-46e0-9646-c64dd4a15df1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 2%

---

# Logische kwantor-functies

Logische kwantoren kunnen worden gebruikt om voorwaarden met arrays in te stellen [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

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

De `forall` Deze functie bepaalt alle items in een array die aan alle opgegeven voorwaarden voldoen.

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

Nu u over logische kwantoren hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
