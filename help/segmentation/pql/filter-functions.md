---
solution: Experience Platform
title: PQL-filterfuncties
description: Filterfuncties worden gebruikt om gegevens te filteren binnen arrays in Profile Query Language (PQL).
exl-id: 09d66be3-30dc-4488-84a1-cfd09c44470d
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---

# Filterfuncties

Filterfuncties worden gebruikt om gegevens te filteren binnen arrays in [!DNL Profile Query Language] (PQL). Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht ](./overview.md) worden gevonden.

## Filter

Met de functie `[]` (filter) kunnen filters worden toegepast op een array en wordt een subset van de array geretourneerd die overeenkomt met de opgegeven voorwaarde.

**Formaat**

```sql
{ARRAY}[filter]
```

**Voorbeeld**

Met de volgende PQL-query worden alle gebeurtenissen opgehaald die ten minste één productitem hebben met een SKU gelijk aan &quot;PS&quot;.

```sql
xEvent[productListItems[SKU="PS"]]
```

## Omhoog, operator

Met de operator `^` (up) kunt u naar eigenschappen in de bovenste niveaus van filters verwijzen.

**Formaat**

```sql
{ARRAY}[{FILTER_1}[{FILTER_2} or ^{PROPERTY}]]
```

| Argument | Beschrijving |
| -------- | ----------- |
| `{ARRAY}` | De array die wordt gefilterd. |
| `{FILTER_1}` | De buitenste laag van het filtreren. |
| `{FILTER_2}` | De binnenlaag van het filtreren |
| `^{PROPERTY}` | De eigenschap waarop ook wordt gefilterd. Door de `^` wordt een eigenschap gecontroleerd op basis van filter1. |

**Voorbeeld**

De volgende vraag van PQL krijgt alle gebeurtenissen die minstens één productpunt met SKU gelijk aan &quot;PS&quot; **hebben of** een persoon hebben van wie geslacht vrouwelijk is.

```sql
xEvent[productListItems[SKU="PS" or ^^.person.gender="female"]]
```

## Volgende stappen

Nu u over filterfuncties hebt geleerd, kunt u deze gebruiken binnen uw PQL-query&#39;s. Voor meer informatie over andere functies van PQL, te lezen gelieve het [ overzicht van Profile Query Language ](./overview.md).
