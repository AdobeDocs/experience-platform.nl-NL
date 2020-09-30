---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;miscellaneous functions;misc;
solution: Experience Platform
title: Diverse functies
topic: developer guide
description: De volgende functie is een diverse functie voor de Taal van de Vraag van het Profiel (PQL).
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 2%

---


# Diverse functies

De volgende functie is een overige functie voor [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Laat

Met de `let` functie kan een expressie worden opgeslagen als een variabele die later in een query moet worden gebruikt.

**Indeling**

```sql
let {VARIABLE} = {EXPRESSION}
```

**Voorbeeld**

De volgende vraag PQL krijgt alle sommen producttotalen met de transactie in USD waar de som groter is dan $100 en minder dan $1000.

```sql
let S = (sum X.commerce.order.priceTotal over X from xEvent where X.commerce.order.currencyCode = "USD") in (S > 100 and S < 1000)
```

## Volgende stappen

Nu u over diverse functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
