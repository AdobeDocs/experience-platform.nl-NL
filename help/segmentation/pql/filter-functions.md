---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;filter;filter;
solution: Experience Platform
title: PQL-filterfuncties
topic: developer guide
description: Filterfuncties worden gebruikt voor het filteren van gegevens binnen arrays in Profile Query Language (PQL).
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 2%

---


# Filterfuncties

Filterfuncties worden gebruikt om gegevens te filteren binnen arrays in [!DNL Profile Query Language] (PQL). Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

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
| `^{PROPERTY}` | De eigenschap waarop ook wordt gefilterd. Vanwege de `^` controleert het een eigenschap op basis van filter1. |

**Voorbeeld**

De volgende PQL-query krijgt alle gebeurtenissen die ten minste één product-item hebben met een SKU gelijk aan &quot;PS&quot; **of** hebben een persoon met een vrouwelijk geslacht.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Volgende stappen

Nu u over filterfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
