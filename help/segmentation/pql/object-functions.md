---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;object-functies;object;
solution: Experience Platform
title: PQL-objectfuncties
topic-legacy: developer guide
description: PQL (Profile Query Language) biedt functies om interactie met objecten eenvoudiger te maken.
exl-id: e65257d8-5bc8-46c8-8487-33bc7ce4059b
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
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
