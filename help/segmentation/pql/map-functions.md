---
keywords: Experience Platform;thuis;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;De Taal van de Vraag van het profiel;kaartfuncties;kaart;
solution: Experience Platform
title: PQL-mapfuncties
description: De Taal van de Vraag van het profiel (PQL) biedt functies om interactie met kaarten gemakkelijker te maken.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 2%

---

# Toewijzingsfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met kaarten eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## Get

De `get` wordt gebruikt om de waarde van een kaart voor een bepaalde sleutel terug te winnen.

**Indeling**

```sql
{MAP}.get({STRING})
```

**Voorbeeld**

De volgende PQL-query haalt de waarde van de identiteitskaart voor de sleutel op `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Toetsen

De `keys` wordt gebruikt om alle sleutels voor een bepaalde kaart terug te winnen.

**Indeling**

```sql
{MAP}.keys()
```

**Voorbeeld**

De volgende PQL-query haalt alle sleutels voor de kaart op `identityMap`.

```sql
identityMap.keys()
```

## Waarden

De `values` wordt gebruikt om alle waarden van een bepaalde kaart op te halen.

**Indeling**

```sql
{MAP}.values()
```

**Voorbeeld**

De volgende PQL-query haalt alle waarden voor de kaart op `identityMap`.

```sql
identityMap.values()
```

## Volgende stappen

Nu u over kaartfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
