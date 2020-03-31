---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Reeksfuncties
topic: developer guide
translation-type: tm+mt
source-git-commit: 92f92f480f29f7d6440f4e90af3225f9a1fcc3d0

---


# Reeksfuncties

PQL (Profile Query Language) biedt functies om interactie met tekenreeksen eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in het overzicht [Taal van](./overview.md)profielquery.

## leuk

De `like` functie wordt gebruikt om te bepalen of een tekenreeks overeenkomt met een opgegeven patroon.

**Indeling**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De expressie die moet overeenkomen met de eerste tekenreeks. Er zijn twee ondersteunde speciale tekens voor het maken van een expressie: `%` en `_`. <ul><li>`%` wordt gebruikt om nul of meer tekens te vertegenwoordigen.</li><li>`_` wordt gebruikt om precies één teken te vertegenwoordigen.</li></ul> |

**Voorbeeld**

Met de volgende PQL-query worden alle steden opgehaald die het patroon &quot;es&quot; bevatten.

```sql
city like "%es%"
```

## Begint met

De `startsWith` functie wordt gebruikt om te bepalen of een tekenreeks begint met een opgegeven subtekenreeks.

**Indeling**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende vraag PQL bepaalt, met case gevoeligheid, als de naam van de persoon met &quot;Joe&quot;begint.

```sql
person.name.startsWith("Joe")
```

## Begint niet met

De `doesNotStartWith` functie wordt gebruikt om te bepalen of een tekenreeks niet begint met een opgegeven subtekenreeks.

**Indeling**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende vraag PQL bepaalt, met case gevoeligheid, als de naam van de persoon niet met &quot;Joe&quot;begint.

```sql
person.name.doesNotStartWith("Joe")
```

## Eindigt met

De `endsWith` functie wordt gebruikt om te bepalen of een tekenreeks eindigt met een opgegeven subtekenreeks.

**Indeling**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of het e-mailadres van de persoon eindigt met &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Eindigt niet met

De `doesNotEndWith` functie wordt gebruikt om te bepalen of een tekenreeks niet eindigt met een opgegeven subtekenreeks.

**Indeling**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of het e-mailadres van de persoon niet eindigt met &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Bevat

De `contains` functie wordt gebruikt om te bepalen of een tekenreeks een opgegeven subtekenreeks bevat.

**Indeling**

```sql
{STRING_1}.contains({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of het e-mailadres van de persoon de tekenreeks &quot;2010@gm&quot; bevat.

```sql
person.emailAddress.contains("2010@gm")
```

## Bevat niet

De `doesNotContain` functie wordt gebruikt om te bepalen of een tekenreeks geen opgegeven subtekenreeks bevat.

**Indeling**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of het e-mailadres van de persoon de tekenreeks &quot;2010@gm&quot; niet bevat.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Gelijk

De `equals` functie wordt gebruikt om te bepalen of een tekenreeks gelijk is aan de opgegeven tekenreeks.

**Indeling**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks die met de eerste tekenreeks moet worden vergeleken. |

**Voorbeeld**

De volgende vraag PQL bepaalt, met gevalgevoeligheid, als de naam van de persoon &quot;John&quot;is.

```sql
person.name.equals("John")
```

## Niet gelijk aan

De `notEqualTo` functie wordt gebruikt om te bepalen of een tekenreeks niet gelijk is aan de opgegeven tekenreeks.

**Indeling**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks die met de eerste tekenreeks moet worden vergeleken. |

**Voorbeeld**

De volgende vraag PQL bepaalt, met case gevoeligheid, als de naam van de persoon niet &quot;John&quot; is.

```sql
person.name.notEqualTo("John")
```

## Overeenkomsten

De `matches` functie wordt gebruikt om te bepalen of een tekenreeks overeenkomt met een specifieke reguliere expressie. Raadpleeg [dit document](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) voor meer informatie over overeenkomende patronen in reguliere expressies.

**Indeling**

```sql
{STRING_1}.matches(STRING_2})
```

**Voorbeeld**

De volgende vraag PQL bepaalt, zonder case sensitive te zijn, als de naam van de persoon met &quot;John&quot;begint.

```sql
person.name.matches("(?i)^John")
```

## Groep met reguliere expressies

De `regexGroup` functie wordt gebruikt om specifieke informatie te extraheren, gebaseerd op de regelmatige verstrekte uitdrukking.

**Indeling**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Voorbeeld**

De volgende PQL-query wordt gebruikt om de domeinnaam uit een e-mailadres te extraheren.

```sql
emailAddress.regexGroup("@(\w+)", 1)
```

## Volgende stappen

Nu u over koordfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Lees voor meer informatie over andere PQL-functies het overzicht [van de](./overview.md)profielquery.

