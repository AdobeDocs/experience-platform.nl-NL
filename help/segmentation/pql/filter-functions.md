---
solution: Experience Platform
title: PQL-filterfuncties
description: Filterfuncties worden gebruikt voor het filteren van gegevens binnen arrays in Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 2%

---

# Filterfuncties

Filterfuncties worden gebruikt om gegevens binnen arrays te filteren in [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## Filter

De `[]` (filter) laat filters toe om op een serie worden toegepast en keert een ondergroep van de serie terug die de gespecificeerde voorwaarde aanpast.

**Indeling**

```sql
{ARRAY}[filter]
```

**Voorbeeld**

De volgende PQL-query krijgt alle gebeurtenissen die ten minste één product-item hebben met een SKU gelijk aan &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Omhoog, operator

De `^` (up) operator staat u toe te verwijzen naar eigenschappen in de bovenste niveaus van filters.

**Indeling**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beschrijving |
| -------- | ----------- |
| `{ARRAY}` | De array die wordt gefilterd. |
| `{FILTER_1}` | De buitenste laag van het filtreren. |
| `{FILTER_2}` | De binnenlaag van het filtreren |
| `^{PROPERTY}` | De eigenschap waarop ook wordt gefilterd. Door de `^`, controleert deze een eigenschap op basis van filter1. |

**Voorbeeld**

De volgende PQL-query krijgt alle gebeurtenissen die ten minste één product-item hebben met een SKU die gelijk is aan &quot;PS&quot; **of** een persoon hebben van wie het geslacht vrouwelijk is.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Volgende stappen

Nu u over filterfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
