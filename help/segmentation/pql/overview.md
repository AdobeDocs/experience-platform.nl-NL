---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van PQL (Profile Query Language)
topic: developer guide
translation-type: tm+mt
source-git-commit: 902ba5efbb5f18a2de826fffd023195d804309cc

---


# Overzicht van PQL (Profile Query Language)

De Taal van de Vraag van het profiel (PQL) is een van het Model van de Gegevens van de Ervaring (XDM) volgzame vraagtaal die wordt ontworpen om de definitie en de uitvoering van segmenteringsvragen voor de gegevens van het Profiel van de Klant in real time te steunen.

Deze handleiding biedt een algemeen overzicht van PQL, met opmaakrichtlijnen en voorbeelden van PQL-expressies.

## PQL-queryopmaak

PQL-query&#39;s hebben de volgende handtekening:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

De invoerparameter kan een eenvoudige primitieve parameter zijn, zoals een booleaanse tekenreeks of een complexer type, zoals een object, array of kaart.

Er zijn **drie** verschillende manieren om naar inputparameters binnen het lichaam van een uitdrukking te verwijzen PQL:

### Impliciete verwijzing naar de eerste parameter

In het onderstaande voorbeeld, omdat de eerste parameter altijd in context staat, kan er rechtstreeks een eigenschapverwijzing (`homeAddress`) naar worden gemaakt.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Expliciete verwijzing naar de eerste parameter

In het onderstaande voorbeeld `$1` wordt naar de eerste parameter verwezen. Als gevolg hiervan `$2` zou ik verwijzen naar de tweede parameter, enz.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Gebruik van benoemde variabelen met de lambda-notatie

In het onderstaande voorbeeld `Profile` is dit een variabelenaam die door de auteur van de query kan worden gekozen.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL-literalen

PQL biedt ondersteuning voor de volgende letterlijke typen:

| Letterlijk | Definitie | Voorbeeld |
| ------- | ---------- | ------- |
| String | Een gegevenstype dat bestaat uit tekens die tussen dubbele aanhalingstekens staan. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolean | Een gegevenstype dat waar of onwaar is. | `true`, `false` |
| Geheel | Een gegevenstype dat een geheel getal vertegenwoordigt. Het kan positief, negatief, of nul zijn. | `-201`, `0`, `412` |
| Dubbel | A data type representing any real number. Het kan positief, negatief, of nul zijn. | `-51.24`, `3.14`, `0.6942058` |
| Datum | Een gegevenstype dat kan worden gebruikt om datums te maken op basis van het jaar, de maand en de dag als parameters van gehele getallen. Het is opgemaakt als `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Een gegevenstype dat is samengesteld als een groep andere letterlijke waarden. Er worden vierkante haakjes gebruikt om te groeperen en komma&#39;s om te scheiden tussen verschillende waarden. <br> **Opmerking:** U hebt niet rechtstreeks toegang tot eigenschappen van items binnen een array. Dus als u toegang moet krijgen tot een eigenschap binnen een array, is de ondersteunde methode `select X from array where X.item = ...`. <br> PQL behoudt zich het woord voor `xEvent` te verwijzen naar een array van ervaringsgebeurtenissen die aan een profiel zijn gekoppeld. | `[1, 4, 7]`, `["US", "CA"]` |
| Relatieve tijdverwijzingen | Gereserveerde woorden die kunnen worden gebruikt om tijdstempel en tijdinterval verwijzingen te vormen. <ul><li>nu, vandaag, gisteren, morgen</li><li>dit, laatste, volgende</li><li>voor, na, van</li><li>millisecond(en), seconde(n), minuut(n), uur, dag(en), week(en), maand(en), jaar(en), decennium(en), eeuw/eeuwen, millennium/millennium</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |


## PQL-functies

In de volgende tabel worden de verschillende categorieën ondersteunde PQL-functies beschreven, waaronder koppelingen naar verdere documentatie voor meer informatie.

| Categorie | Definitie |
| -------- | ---------- |
| Boolean | Wordt gebruikt om booleaanse algebra te implementeren in PQL. Meer informatie over deze functies vindt u in het document [met](./boolean-functions.md)booleaanse functies. |
| Vergelijking | Wordt gebruikt om verschillende PQL-elementen te vergelijken. Meer informatie over deze functies vindt u in het document [met](./comparison-functions.md)vergelijkingsfuncties. |
| Array, list en set | Wordt gebruikt voor interactie met arrays, lijsten en sets. Meer informatie over deze functies vindt u in het document met [arrays, lijsten en ingestelde functies](./array-functions.md). |
| Kaart | Wordt gebruikt voor interactie met kaarten. Meer informatie over deze functies vindt u in het document met [kaartfuncties](./map-functions.md). |
| String | Wordt gebruikt voor interactie met tekenreeksen. Meer informatie over deze functies vindt u in het document [met](./string-functions.md)tekenreeksfuncties. |
| Rekenkundig | Wordt gebruikt voor het uitvoeren van rekenkundige basisbewerkingen op PQL-elementen. Meer informatie over deze functies vindt u in het document met [rekenkundige functies](./arithmetic-functions.md) |
| Samenvoeging | Wordt gebruikt om resultaten van een array te combineren in een enkel resultaat. Meer informatie over samenvoegingsfuncties vindt u in het document [met](./aggregation-functions.md)aggregatiefuncties. |
| Datum en tijd | Wordt gebruikt in combinatie met datum-, tijd- en datetime-objecten. Meer informatie over deze functies vindt u in het document met [datum-/tijdfuncties](./datetime-functions.md). |
| Filter | Wordt gebruikt om gegevens binnen arrays te filteren. Meer informatie over deze functies vindt u in het document [met](./filter-functions.md)filterfuncties. |
| Logische kwantoren | Wordt gebruikt om voorwaarden binnen een array te bevestigen. Meer informatie vindt u in het document [met](./logical-quantifiers.md)logische kwantoren. |
| Diversen | Functies die niet in een van de bovenstaande categorieën passen, vindt u in het document [met](./misc-functions.md)diverse functies. |

## Volgende stappen

Nu u hebt geleerd hoe te om de Taal van de Vraag van het Profiel te gebruiken, kunt u PQL gebruiken wanneer het creëren van en het wijzigen van segmenten. Lees het [segmentatieoverzicht](../home.md)voor meer informatie over segmentatie.