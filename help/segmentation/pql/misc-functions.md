---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Diverse functies
topic: developer guide
translation-type: tm+mt
source-git-commit: d7ec6240864916d3b54db8bd641f4917a38f9480

---


# Diverse functies

De volgende functie is een diverse functie voor de Taal van de Vraag van het Profiel (PQL). Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

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
