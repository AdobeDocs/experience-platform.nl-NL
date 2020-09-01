---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;object functions;object;
solution: Experience Platform
title: Objectfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 17ef6c1c6ce58db2b65f1769edf719b98d260fc6
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 3%

---


# Objectfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met objecten eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Is null

De `isNull` functie bepaalt of een objectverwijzing niet bestaat.

**Indeling**

```sql
{OBJECT}.isNull()
```

**Voorbeeld**

De volgende vraag PQL controleert als het huisadres van de persoon niet bestaat.

```sql
person.homeAddress.isNull()
```

## Is niet null

De `isNotNull` functie bepaalt of een objectverwijzing bestaat.

**Indeling**

```sql
{OBJECT}.isNotNull()
```

**Voorbeeld**

De volgende vraag PQL controleert als het huisadres van de persoon bestaat.

```sql
person.homeAddress.isNotNull()
```

## Volgende stappen

Nu u over objecten functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.