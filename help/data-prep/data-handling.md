---
keywords: Experience Platform;home;populaire onderwerpen;map csv;map csv-bestand;map csv-bestand toewijzen aan xdm;map csv aan xdm;ui guide;mapper;mapping;data prep;data voorbereiden;voorbereiden van gegevens;
solution: Experience Platform
title: Gegevensindelingen verwerken met Data Prep
description: Dit document geeft een overzicht van hoe de verschillende gegevenstypen in de Prep van Gegevens worden behandeld.
exl-id: 4ad253b7-3f83-48cd-9c46-8b5ba627c09e
source-git-commit: a49140853124f4f7beee87a739c8e670838947f4
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 3%

---

# Gegevensindelingen verwerken met Data Prep

Data Prep kan op krachtige wijze verschillende gegevensindelingen verwerken die in Adobe Experience Platform worden ingevoerd. In dit document wordt beschreven hoe verschillende gegevensindelingen worden verwerkt met Data Prep.

## Booleaanse {#booleans}

Als het brontype een tekenreeks is en het doeltype een Booleaanse waarde is, kan de waarde automatisch worden geparseerd met Data Prep en kan de bronwaarde worden omgezet in een booleaanse waarde.

De waarden `y`, `yes`, `Y`, `YES`, `on`, `ON`, `true` en `TRUE` worden automatisch geparseerd om `true` te zijn.

De waarden `n`, `N`, `no`, `NO`, `off`, `OFF`, `false` en `FALSE` worden automatisch geparseerd om `false` te zijn.

## Datums {#dates}

Data Prep ondersteunt datumfuncties, zowel als tekenreeksen als als datetime-objecten.

### Datumfunctie-indeling

De datumfunctie zet tekenreeksen en datetime-objecten om in een ISO 8601-opgemaakt ZonedDateTime-object.

**Formaat**

```http
date({DATE}, {FORMAT}, {DEFAULT_DATE})
```

| Parameter | Beschrijving |
| --------- | ----------- |
| `{DATE}` | Vereist. De tekenreeks die de datum vertegenwoordigt. |
| `{FORMAT}` | Optioneel. De tekenreeks die staat voor de indeling van de brondatum. Meer informatie over koord het formatteren kan in de [ de sectie van het datum/tijdformaat koord ](#format) worden gevonden. |
| `{DEFAULT_DATE}` | Optioneel. De standaarddatum die moet worden geretourneerd als de opgegeven datum null is. |

Met de expressie `date(orderDate, "yyyy-MM-dd")` wordt bijvoorbeeld de `orderDate` waarde &quot;31 december 2020&quot; omgezet in de datetime-waarde &quot;2020-12-31&quot;.

### Datumfunctie converteert

Wanneer de koordgebieden van inkomende gegevens aan datumgebieden in schema&#39;s gebruikend het Model van de Gegevens van de Ervaring (XDM) in kaart worden gebracht, zou het datumformaat uitdrukkelijk moeten worden vermeld. Indien niet expliciet vermeld, probeert Data Prep de invoergegevens om te zetten door deze aan de volgende indelingen aan te passen. Als een overeenkomende indeling wordt gevonden, wordt de evaluatie van alle volgende indelingen stopgezet.

```console
"yyyy-MM-dd HH:mm:ssZ",
"yyyy-MM-dd HH:mm:ss.SSSZ",
"yyyy-MM-dd HH:mm:ss.SSS",
"yyyy-MM-dd'T'HH:mm:ss.SSSX",
"yyyy-MM-dd'T'HH:mm:ss'Z'",
"yyyy-MM-dd",
"yyyy/MM/dd",
"yyyy.MM.dd",
"yyyy-MMM-dd",
"yyyyMMdd",
"MM-dd-yyyy",
"MMddyyyy",
"M/dd/yyyy",
"dd.M.yyyy",
"M/dd/yyyy hh:mm:ss a",
"dd.M.yyyy hh:mm:ss a",
"dd.MMM.yyyy",
"dd-MMM-yyyy"
```

>[!IMPORTANT]
>
> Met Data Prep worden tekenreeksen zo goed mogelijk omgezet in datums. Deze omzettingen kunnen echter tot ongewenste resultaten leiden. De tekenreekswaarde &quot;12112020&quot; komt bijvoorbeeld overeen met het patroon &quot;MMddyy&quot;, maar de gebruiker kan de datum hebben willen lezen met het patroon &quot;ddMMyyyy&quot;. Daarom moeten gebruikers expliciet de datumnotatie voor tekenreeksen vermelden.

### Tekenreeksen voor datum-/tijdnotatie {#format}

>[!TIP]
>
>Momenteel verwijdert de datumfunctie in batch-opname milliseconden als de datumwaarden de volgende notatie hebben: `2024-05-05 20:39:00.005` PST. Gebruik de volgende notatie om milliseconden te behouden: `2024-05-05 20:39:00.005-0800`

In de volgende tabel wordt aangegeven welke patroonletters zijn gedefinieerd voor opmaaktekenreeksen. De letters zijn hoofdlettergevoelig.

| Symbool | Betekenis | Presentatie | Voorbeeld |
| ------ | ------- | ------------ | ------- |
| G | Het tijdperk | Tekst | AD; Anno Domini; A |
| Y | Jaar op basis van de ISO-week | Getal | 1996; 96 |
| y | Het jaar | Getal | 2004; 04 |
| M/L | Maand van het jaar | Getal/tekst | 7; 07; juli; J |
| w | Week in het jaar | Getal | 27 |
| W | Week van de maand | Getal | 3 |
| D | Dag van het jaar | Getal | 189 |
| d | Dag van de maand | Getal | 10 |
| F | Dag van de week in een maand | Getal | 2 |
| E | Naam van de weekdag | Tekst | Dinsdag; Kleurtoon |
| u | Dag van de week, als een getal. 1 staat voor maandag, ..., 7 staat voor zondag | Getal | 1 |
| a | AM/PM-markering | Tekst | PM |
| H | Uur in dag (0-23) | Getal | 0 |
| k | Uur in dag (1-24) | Getal | 24 |
| K | Uur in AM/PM (0-11) | Getal | 0 |
| h | Uur in AM/PM (1-12) | Getal | 12 |
| m | Minuut in uur | Getal | 38 |
| s | Seconde in de minuut | Getal | 44 |
| S | Milliseconde | Getal | 245 |
| z | Tijdzone | Algemene tijdzone | Pacific Standard Time; PST; GMT-08:00 |
| Z | Tijdzone | RFC 822 — Tijdzone | -0800 |
| X | Tijdzone | Tijdzone ISO 8601 | -08; -0800; -08:00 |
| V | Tijdzone-id | Tekst | America/Los_Angeles |
| O | Verschuiving tijdzone | Tekst | GMT+8 |
| Q/q | Kwartaal van het jaar | Getal/tekst | 3; 03; Q3; 3de kwartaal |

## Kaarten {#maps}

Kaarten worden momenteel niet ondersteund in [!DNL Data Prep] .
