---
solution: Experience Platform
title: PQL Overige functies
description: De volgende functie is een overige functie voor Profile Query Language (PQL).
exl-id: a6ed31a2-a649-4dc8-89b1-48c1170b7f16
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Diverse functies

De volgende functie is een overige functie voor [!DNL Profile Query Language] (PQL). Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht &#x200B;](./overview.md) worden gevonden.

## Laat

Met de functie `let` kan een expressie worden opgeslagen als een variabele die later in een query moet worden gebruikt.

**Formaat**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Voorbeeld**

De volgende PQL-query krijgt alle bedragen van de producttotalen met de transactie in USD waar de som groter is dan $100 en kleiner dan $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Volgende stappen

Nu u over diverse functies hebt geleerd, kunt u deze gebruiken binnen uw PQL-query&#39;s. Voor meer informatie over andere functies van PQL, te lezen gelieve het [&#x200B; overzicht van Profile Query Language &#x200B;](./overview.md).
