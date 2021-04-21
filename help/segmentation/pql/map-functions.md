---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;De Taal van de Vraag van het profiel;kaartfuncties;kaart;
solution: Experience Platform
title: PQL-mapfuncties
topic-legacy: developer guide
description: De Taal van de Vraag van het profiel (PQL) biedt functies om interactie met kaarten gemakkelijker te maken.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# Toewijzingsfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met kaarten eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Get

De functie `get` wordt gebruikt om de waarde van een kaart voor een bepaalde sleutel terug te winnen.

**Indeling**

```sql
{MAP}.get({STRING})
```

**Voorbeeld**

De volgende vraag PQL krijgt de waarde van de identiteitskaart voor sleutel `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Toetsen

De functie `keys` wordt gebruikt om alle sleutels voor een bepaalde kaart terug te winnen.

**Indeling**

```sql
{MAP}.keys()
```

**Voorbeeld**

De volgende vraag PQL krijgt alle sleutels voor de kaart `identityMap`.

```sql
identityMap.keys()
```

## Waarden

De functie `values` wordt gebruikt om alle waarden van een bepaalde kaart terug te winnen.

**Indeling**

```sql
{MAP}.values()
```

**Voorbeeld**

De volgende vraag PQL krijgt alle waarden voor de kaart `identityMap`.

```sql
identityMap.values()
```

## Volgende stappen

Nu u over kaartfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere functies PQL, te lezen gelieve [het Taal van de Vraag van het Profiel](./overview.md).
