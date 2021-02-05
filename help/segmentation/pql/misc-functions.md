---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;overige functies;misc;
solution: Experience Platform
title: PQL Overige functies
topic: developer guide
description: De volgende functie is een diverse functie voor de Taal van de Vraag van het Profiel (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 2%

---


# Diverse functies

De volgende functie is een diverse functie voor [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Laat

Met de functie `let` kan een expressie worden opgeslagen als een variabele die later in een query moet worden gebruikt.

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

Nu u over diverse functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
