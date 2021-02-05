---
keywords: Experience Platform;home;populaire onderwerpen;PQL;pql;taal voor profielquery
solution: Experience Platform
title: Overzicht van de profielquery Language (PQL)
topic: developer guide
description: Deze handleiding biedt een algemeen overzicht van PQL, met opmaakrichtlijnen en voorbeelden van PQL-expressies.
translation-type: tm+mt
source-git-commit: b3defc3e33a55855e307ab70b9797d985d5719e3
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 1%

---


# [!DNL Profile Query Language] (PQL) - overzicht

[!DNL Profile Query Language] (PQL) is een  [!DNL Experience Data Model] (XDM) volgzame vraagtaal die wordt ontworpen om de definitie en de uitvoering van segmenteringsvragen voor  [!DNL Real-time Customer Profile] gegevens te steunen.

Deze handleiding biedt een algemeen overzicht van PQL, met opmaakrichtlijnen en voorbeelden van PQL-expressies.

## PQL-queryopmaak

PQL-query&#39;s hebben de volgende handtekening:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

De invoerparameter kan een eenvoudige primitieve parameter zijn, zoals een booleaanse tekenreeks of een complexer type, zoals een object, array of kaart.

Er zijn drie verschillende manieren om naar inputparameters binnen het lichaam van een uitdrukking te verwijzen PQL:

### Impliciete verwijzing naar de eerste parameter

In het onderstaande voorbeeld, aangezien de eerste parameter altijd in context is, kan een bezitsverwijzing (`homeAddress`) direct aan het worden gemaakt.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Expliciete verwijzing naar de eerste parameter

In het onderstaande voorbeeld verwijst `$1` naar de eerste parameter. Als gevolg hiervan verwijst `$2` naar de tweede parameter, enz.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Gebruik van benoemde variabelen met de lambda-notatie

In het onderstaande voorbeeld is `Profile` een variabelenaam, die door de vraagauteur kan worden gekozen.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL-literalen

PQL biedt ondersteuning voor de volgende letterlijke typen:

| Letterlijk | Definitie | Voorbeeld |
| ------- | ---------- | ------- |
| Tekenreeks | Een gegevenstype dat bestaat uit tekens die tussen dubbele aanhalingstekens staan. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolean | Een gegevenstype dat waar of onwaar is. | `true`, `false` |
| Geheel | Een gegevenstype dat een geheel getal vertegenwoordigt. Het kan positief, negatief, of nul zijn. | `-201`,  `0`,  `412` |
| Dubbel | A data type representing any real number. Het kan positief, negatief, of nul zijn. | `-51.24`,  `3.14`,  `0.6942058` |
| Datum | Een gegevenstype dat kan worden gebruikt om datums te maken op basis van het jaar, de maand en de dag als parameters van gehele getallen. Het is opgemaakt als `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Een gegevenstype dat is samengesteld als een groep andere letterlijke waarden. Er worden vierkante haakjes gebruikt om te groeperen en komma&#39;s om te scheiden tussen verschillende waarden. <br> **Opmerking:** u hebt niet rechtstreeks toegang tot eigenschappen van items binnen een array. Dus als u toegang moet krijgen tot een eigenschap binnen een array, is de ondersteunde methode `select X from array where X.item = ...`. <br> PQL behoudt zich het woord voor  `xEvent` te verwijzen naar een array van ervaringsgebeurtenissen die aan een profiel zijn gekoppeld. | `[1, 4, 7]`,  `["US", "CA"]` |
| Relatieve tijdverwijzingen | Gereserveerde woorden die kunnen worden gebruikt om tijdstempel en tijdinterval verwijzingen te vormen. <ul><li>nu, vandaag, gisteren, morgen</li><li>dit, laatste, volgende</li><li>voor, na, van</li><li>millisecond(en), seconde(n), minuut(n), uur, dag(en), week(en), maand(en), jaar(en), decennium(en), eeuw/eeuwen, millennium/millennium</li></ul> | `X.timestamp occurs before today`,  `X.timestamp occurs last month`,  `X.timestamp occurs <= 3 days before now` |


## PQL-functies

In de volgende tabel worden de verschillende categorieën ondersteunde PQL-functies beschreven, waaronder koppelingen naar verdere documentatie voor meer informatie.

| Categorie | Definitie |
| -------- | ---------- |
| Boolean | Wordt gebruikt om booleaanse algebra te implementeren in PQL. Meer informatie over deze functies vindt u in het document [booleaanse functies](./boolean-functions.md). |
| Vergelijking | Wordt gebruikt om verschillende PQL-elementen te vergelijken. Meer informatie over deze functies vindt u in het document [vergelijkingsfuncties](./comparison-functions.md). |
| Array, list en set | Wordt gebruikt voor interactie met arrays, lijsten en sets. Meer informatie over deze functies vindt u in het document [array, list en set functions](./array-functions.md). |
| Kaart | Wordt gebruikt voor interactie met kaarten. Meer informatie over deze functies vindt u in het document [kaartfuncties](./map-functions.md). |
| Tekenreeks | Wordt gebruikt voor interactie met tekenreeksen. Meer informatie over deze functies vindt u in het document [tekenreeksfuncties](./string-functions.md). |
| Object | Wordt gebruikt voor interactie met objecten. Meer informatie over deze functies vindt u in het document [objectfuncties](./object-functions.md). |
| Rekenkundig | Wordt gebruikt voor het uitvoeren van rekenkundige basisbewerkingen op PQL-elementen. Meer informatie over deze functies vindt u in het document [rekenkundige functies](./arithmetic-functions.md) |
| Samenvoeging | Wordt gebruikt om resultaten van een array te combineren in een enkel resultaat. Meer informatie over samenvoegingsfuncties vindt u in het document [aggregatiefuncties](./aggregation-functions.md). |
| Datum en tijd | Wordt gebruikt in combinatie met datum-, tijd- en datetime-objecten. Meer informatie over deze functies vindt u in het document [datum-/tijdfuncties](./datetime-functions.md). |
| Filter | Wordt gebruikt om gegevens binnen arrays te filteren. Meer informatie over deze functies vindt u in het document [filterfuncties](./filter-functions.md). |
| Logische kwantoren | Wordt gebruikt om voorwaarden binnen een array te bevestigen. Meer informatie vindt u in het document [logische kwantoren](./logical-quantifiers.md). |
| Diversen | Functies die niet in een van de bovenstaande categorieën passen, vindt u in het [document met diverse functies](./misc-functions.md). |

## Volgende stappen

Nu u hebt geleerd hoe te om [!DNL Profile Query Language] te gebruiken, kunt u PQL gebruiken wanneer het creëren van en het wijzigen van segmenten. Lees voor meer informatie over segmentatie het [segmentatieoverzicht](../home.md).