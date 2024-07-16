---
solution: Experience Platform
title: PQL Map-functies
description: Profile Query Language (PQL) biedt functies om interactie met kaarten eenvoudiger te maken.
exl-id: f23616f2-c0dd-40ce-8cfc-c757542fbd05
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---

# Toewijzingsfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met kaarten eenvoudiger te maken. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht ](./overview.md) worden gevonden.

## Get

De functie `get` wordt gebruikt om de waarde van een kaart voor een bepaalde sleutel terug te winnen.

**Formaat**

```sql
{MAP}.get({STRING})
```

**Voorbeeld**

Met de volgende PQL-query wordt de waarde van de identiteitskaart voor de sleutel `example@example.com` opgehaald.

```sql
identityMap.get("example@example.com")
```

## Toetsen

De functie `keys` wordt gebruikt om alle sleutels voor een bepaalde kaart terug te winnen.

**Formaat**

```sql
{MAP}.keys()
```

**Voorbeeld**

Met de volgende PQL-query worden alle toetsen voor de kaart `identityMap` opgehaald.

```sql
identityMap.keys()
```

## Waarden

De functie `values` wordt gebruikt om alle waarden van een bepaalde kaart op te halen.

**Formaat**

```sql
{MAP}.values()
```

**Voorbeeld**

De volgende PQL-query haalt alle waarden voor de kaart `identityMap` op.

```sql
identityMap.values()
```

## Volgende stappen

Nu u over kaartfuncties hebt geleerd, kunt u deze gebruiken binnen uw PQL-query&#39;s. Voor meer informatie over andere functies van PQL, te lezen gelieve het [ overzicht van Profile Query Language ](./overview.md).
