---
keywords: Experience Platform;home;populaire onderwerpen;segmentatie;Segmentatie;Segmenteringsservice;pql;PQL;Profile Query Language;string functies;string;
solution: Experience Platform
title: PQL-tekenreeksfuncties
topic-legacy: developer guide
description: PQL (Profile Query Language) biedt functies om interactie met tekenreeksen eenvoudiger te maken.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: 1c9ed96cdbd9e670bd1f05467e33e8dab5bc2121
workflow-type: tm+mt
source-wordcount: '840'
ht-degree: 3%

---

# Reeksfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met tekenreeksen eenvoudiger te maken. Meer informatie over andere PQL-functies vindt u in de [[!DNL Profile Query Language] overzicht](./overview.md).

## leuk

De `like` wordt gebruikt om te bepalen of een tekenreeks overeenkomt met een opgegeven patroon.

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

## Starts with (Begint met)

De `startsWith` wordt gebruikt om te bepalen of een tekenreeks begint met een opgegeven subtekenreeks.

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

De `doesNotStartWith` wordt gebruikt om te bepalen of een tekenreeks niet begint met een opgegeven subtekenreeks.

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

## Ends with (Eindigt met)

De `endsWith` wordt gebruikt om te bepalen of een tekenreeks eindigt met een opgegeven subtekenreeks.

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

De `doesNotEndWith` wordt gebruikt om te bepalen of een tekenreeks niet eindigt met een opgegeven subtekenreeks.

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

De `contains` wordt gebruikt om te bepalen of een tekenreeks een opgegeven subtekenreeks bevat.

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

De `doesNotContain` wordt gebruikt om te bepalen of een tekenreeks geen opgegeven subtekenreeks bevat.

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

## Equals (Is gelijk aan)

De `equals` wordt gebruikt om te bepalen of een tekenreeks gelijk is aan de opgegeven tekenreeks.

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

De `notEqualTo` wordt gebruikt om te bepalen of een tekenreeks niet gelijk is aan de opgegeven tekenreeks.

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

De `matches` wordt gebruikt om te bepalen of een tekenreeks overeenkomt met een specifieke reguliere expressie. Zie [dit document](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) voor meer informatie over overeenkomende patronen in reguliere expressies.

**Indeling**

```sql
{STRING_1}.matches(STRING_2})
```

**Voorbeeld**

De volgende vraag PQL bepaalt, zonder case sensitive te zijn, als de naam van de persoon met &quot;John&quot;begint.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Als u reguliere-expressiefuncties gebruikt, zoals `\w`, u **moet** escape the backslash character. Dus in plaats van alleen maar te schrijven `\w`, moet u een extra backslash en schrijven opnemen `\\w`.

## Groep met reguliere expressies

De `regexGroup` Deze functie wordt gebruikt om specifieke informatie te extraheren op basis van de reguliere expressie die wordt gegeven.

**Indeling**

```sql
{STRING}.regexGroup({EXPRESSION})
```

**Voorbeeld**

De volgende PQL-query wordt gebruikt om de domeinnaam uit een e-mailadres te extraheren.

```sql
emailAddress.regexGroup("@(\\w+)", 1)
```

>[!NOTE]
>
>Als u reguliere-expressiefuncties gebruikt, zoals `\w`, u **moet** escape the backslash character. Dus in plaats van alleen maar te schrijven `\w`, moet u een extra backslash en schrijven opnemen `\\w`.

## Volgende stappen

Nu u over koordfuncties hebt geleerd, kunt u hen binnen uw vragen gebruiken PQL. Voor meer informatie over andere PQL functies, gelieve te lezen [Overzicht van taal voor profielquery](./overview.md).
