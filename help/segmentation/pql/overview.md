---
solution: Experience Platform
title: Overzicht van Profile Query Language (PQL)
description: Deze handleiding biedt een algemeen overzicht van PQL, met opmaakrichtlijnen en voorbeelden van PQL-expressies.
exl-id: 4f7ab50e-89a3-42db-b74a-c6f2d86c9bcb
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Overzicht van [!DNL Profile Query Language] (PQL)

[!DNL Profile Query Language] (PQL) is een [!DNL Experience Data Model] (XDM) compatibele querytaal die is ontworpen om de definitie en uitvoering van segmenteringsquery&#39;s voor [!DNL Real-Time Customer Profile] -gegevens te ondersteunen.

Deze handleiding biedt een algemeen overzicht van PQL, met opmaakrichtlijnen en voorbeelden van PQL-expressies.

## PQL-queryopmaak

PQL-query&#39;s hebben de volgende handtekening:

```sql
({INPUT_PARAMETER_1}, {INPUT_PARAMETER_2}, ...) => {RESULT_TYPE}
```

De invoerparameter kan een eenvoudige primitieve parameter zijn, zoals een booleaanse tekenreeks of een complexer type, zoals een object, array of kaart.

Er zijn drie verschillende manieren om naar invoerparameters binnen de hoofdtekst van een PQL-expressie te verwijzen:

### Impliciete verwijzing naar de eerste parameter

In het onderstaande voorbeeld, aangezien de eerste parameter altijd in context is, kan een bezitsverwijzing (`homeAddress`) direct aan het worden gemaakt.

```sql
homeAddress.stateProvince = workAddress.stateProvince
```

### Expliciete verwijzing naar de eerste parameter

In het onderstaande voorbeeld verwijst `$1` naar de eerste parameter. Als gevolg hiervan verwijst `$2` bijvoorbeeld naar de tweede parameter.

```sql
$1.homeAddress.stateProvince = $1.homeAddress.stateProvince
```

### Gebruik van benoemde variabelen met de lambda-notatie

In het onderstaande voorbeeld is `Profile` een variabelenaam die door de auteur van de query kan worden gekozen.

```sql
(Profile) => Profile.homeAddress.stateProvince = Profile.workAddress.stateProvince
```

## PQL literals

PQL biedt ondersteuning voor de volgende letterlijke typen:

| Letterlijk | Definitie | Voorbeeld |
| ------- | ---------- | ------- |
| String | Een gegevenstype dat bestaat uit tekens die worden omringd door dubbele aanhalingstekens. | `"pizza"`, `"jobs"`, `"antidisestablishmentarianism"` |
| Boolean | Een gegevenstype dat waar of onwaar is. | `true`, `false` |
| Geheel | Een gegevenstype dat een geheel getal vertegenwoordigt. Het kan positief, negatief, of nul zijn. | `-201`, `0`, `412` |
| Dubbel | A data type representing any real number. Het kan positief, negatief, of nul zijn. | `-51.24`, `3.14`, `0.6942058` |
| Datum | Een gegevenstype dat kan worden gebruikt om datums te maken op basis van het jaar, de maand en de dag als parameters van gehele getallen. Het is opgemaakt als `date(year, month, day)` | `date(2020, 3, 14)` |
| Array | Een gegevenstype dat is samengesteld als een groep andere letterlijke waarden. Er worden vierkante haakjes gebruikt om te groeperen en komma&#39;s om te scheiden tussen verschillende waarden. <br> **Nota:** u kunt tot eigenschappen van punten binnen een serie direct toegang hebben. Dus als u toegang moet krijgen tot een eigenschap binnen een array, is de ondersteunde methode `select X from array where X.item = ...` . <br> PQL behoudt zich het woord `xEvent` voor om te verwijzen naar een array van ervaringsgebeurtenissen die aan een profiel zijn gekoppeld. | `[1, 4, 7]`, `["US", "CA"]` |
| Relatieve tijdverwijzingen | Gereserveerde woorden die kunnen worden gebruikt om tijdstempel en tijdinterval verwijzingen te vormen. <ul><li>nu, vandaag, gisteren, morgen</li><li>dit, laatste, volgende</li><li>voor, na, van</li><li>millisecond(en), seconde(n), minuut(n), uur, dag(en), week(en), maand(en), jaar(en), decennium(en), eeuw/eeuwen, millennium/millennium</li></ul> | `X.timestamp occurs before today`, `X.timestamp occurs last month`, `X.timestamp occurs <= 3 days before now` |

## PQL-functies

In de volgende tabel worden de verschillende categorieën ondersteunde PQL-functies beschreven, waaronder koppelingen naar verdere documentatie voor meer informatie.

| Categorie | Definitie |
| -------- | ---------- |
| Boolean | Wordt gebruikt om Booleaanse algebra te implementeren in PQL. Meer informatie over deze functies kan in het [&#x200B; worden gevonden booleaanse functiedocument &#x200B;](./boolean-functions.md). |
| Vergelijking | Wordt gebruikt om verschillende PQL-elementen te vergelijken. Meer informatie over deze functies kan in het [&#x200B; document van vergelijkingsfuncties worden gevonden &#x200B;](./comparison-functions.md). |
| Array, list en set | Wordt gebruikt voor interactie met arrays, lijsten en sets. Meer informatie over deze functies kan in de [&#x200B; serie worden gevonden, lijst, en reeks functies document &#x200B;](./array-functions.md). |
| Kaart | Wordt gebruikt voor interactie met kaarten. Meer informatie over deze functies kan in het [&#x200B; document van kaartfuncties worden gevonden &#x200B;](./map-functions.md). |
| String | Wordt gebruikt voor interactie met tekenreeksen. Meer informatie over deze functies kan in het [&#x200B; document van de koordfuncties worden gevonden &#x200B;](./string-functions.md). |
| Object | Wordt gebruikt voor interactie met objecten. Meer informatie over deze functies kan in het [&#x200B; document van objecten functies &#x200B;](./object-functions.md) worden gevonden. |
| Rekenkundig | Wordt gebruikt voor het uitvoeren van rekenkundige basisbewerkingen op PQL-elementen. Meer informatie over deze functies kan in het [&#x200B; rekenkundige functiedocument &#x200B;](./arithmetic-functions.md) worden gevonden |
| Samenvoeging | Wordt gebruikt om resultaten van een array te combineren in een enkel resultaat. Meer informatie over samenvoegingsfuncties kan in het [&#x200B; document van de samenvoegingsfuncties worden gevonden &#x200B;](./aggregation-functions.md). |
| Datum en tijd | Wordt gebruikt in combinatie met datum-, tijd- en datetime-objecten. Meer informatie over deze functies kan in het [&#x200B; datum/tijdfunctiedocument &#x200B;](./datetime-functions.md) worden gevonden. |
| Filter | Wordt gebruikt om gegevens binnen arrays te filteren. Meer informatie over deze functies kan in het [&#x200B; document van de filterfuncties worden gevonden &#x200B;](./filter-functions.md). |
| Logische kwantoren | Wordt gebruikt om voorwaarden binnen een array te bevestigen. Meer informatie kan in het [&#x200B; logische kwantoren document &#x200B;](./logical-quantifiers.md) worden gevonden. |
| Overige | De functies die niet in om het even welke bovengenoemde categorieën passen kunnen in het [&#x200B; diverse functiedocument &#x200B;](./misc-functions.md) worden gevonden. |

## Volgende stappen

Nu u hebt geleerd hoe u [!DNL Profile Query Language] kunt gebruiken, kunt u PQL gebruiken bij het maken en wijzigen van segmentdefinities. Voor meer informatie over segmentatie, gelieve het [&#x200B; segmentatieoverzicht &#x200B;](../home.md) te lezen.
