---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;object-functies;object;
solution: Experience Platform
title: PQL-objectfuncties
topic: developer guide
description: PQL (Profile Query Language) biedt functies om interactie met objecten eenvoudiger te maken.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# Objectfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met objecten eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Is null

De functie `isNull` bepaalt of een objectverwijzing niet bestaat.

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

De functie `isNotNull` bepaalt of een objecten verwijzing bestaat.

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

Nu u over objecten functies hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).