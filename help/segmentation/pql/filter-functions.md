---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Filterfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 6a0a9b020b0dc89a829c557bdf29b66508a10333
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 2%

---


# Filterfuncties

Filterfuncties worden gebruikt om gegevens te filteren binnen arrays in [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## Filter

Met de functie `[]` (filter) kunnen filters worden toegepast op een array en wordt een subset van de array geretourneerd die overeenkomt met de opgegeven voorwaarde.

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

Met de operator `^` (up) kunt u naar eigenschappen in de bovenste niveaus van filters verwijzen.

**Indeling**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beschrijving |
| -------- | ----------- |
| `{ARRAY}` | De array die wordt gefilterd. |
| `{FILTER_1}` | De buitenste laag van het filtreren. |
| `{FILTER_2}` | De binnenlaag van het filtreren |
| `^{PROPERTY}` | De eigenschap waarop ook wordt gefilterd. Vanwege de fout `^`controleert het een eigenschap op basis van filter1. |

**Voorbeeld**

De volgende PQL-query krijgt alle gebeurtenissen die ten minste één product-item hebben met een SKU gelijk aan &quot;PS&quot; **of** een persoon hebben met een vrouwelijk geslacht.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Volgende stappen

Nu u over filterfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
