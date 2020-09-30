---
keywords: Experience Platform;home;popular topics;segmentation;Segmentation;Segmentation Service;pql;PQL;Profile Query Language;map functions;map;
solution: Experience Platform
title: Toewijzingsfuncties
topic: developer guide
description: De Taal van de Vraag van het profiel (PQL) biedt functies om interactie met kaarten gemakkelijker te maken.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 3%

---


# Toewijzingsfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met kaarten eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het [[!DNL Profile Query Language] overzicht](./overview.md).

## Get

De `get` functie wordt gebruikt om de waarde van een kaart voor een bepaalde sleutel terug te winnen.

**Indeling**

```sql
{MAP}.get({STRING})
```

**Voorbeeld**

Met de volgende PQL-query wordt de waarde van de identiteitskaart voor de sleutel opgehaald `example@example.com`.

```sql
identityMap.get("example@example.com")
```

## Toetsen

De `keys` functie wordt gebruikt om alle sleutels voor een bepaalde kaart terug te winnen.

**Indeling**

```sql
{MAP}.keys()
```

**Voorbeeld**

Met de volgende PQL-query worden alle toetsen voor de kaart opgehaald `identityMap`.

```sql
identityMap.keys()
```

## Waarden

De `values` functie wordt gebruikt om alle waarden van een bepaalde kaart terug te winnen.

**Indeling**

```sql
{MAP}.values()
```

**Voorbeeld**

Met de volgende PQL-query worden alle waarden voor de kaart opgehaald `identityMap`.

```sql
identityMap.values()
```

## Volgende stappen

Nu u over kaartfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.
