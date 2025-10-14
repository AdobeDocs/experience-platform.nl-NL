---
solution: Experience Platform
title: PQL String-functies
description: Profile Query Language (PQL) biedt functies om interactie met tekenreeksen eenvoudiger te maken.
exl-id: 9fd79d86-0802-4312-abce-f6ef5ba5bb34
source-git-commit: c4d034a102c33fda81ff27bee73a8167e9896e62
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 1%

---

# Reeksfuncties

[!DNL Profile Query Language] (PQL) biedt functies om interactie met tekenreeksen eenvoudiger te maken. Meer informatie over andere functies van PQL kan in het [[!DNL Profile Query Language]  overzicht &#x200B;](./overview.md) worden gevonden.

## leuk

De functie `like` wordt gebruikt om te bepalen of een tekenreeks overeenkomt met een opgegeven patroon als een Booleaanse waarde.

**Formaat**

```sql
{STRING_1} like {STRING_2}
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De expressie die moet overeenkomen met de eerste tekenreeks. Er zijn twee ondersteunde speciale tekens voor het maken van een expressie: `%` en `_` . <ul><li>`%` wordt gebruikt om nul of meer tekens te vertegenwoordigen.</li><li>`_` wordt gebruikt om precies één teken te vertegenwoordigen.</li></ul> |

**Voorbeeld**

Met de volgende PQL-query worden alle steden opgehaald die het patroon &quot;es&quot; bevatten.

```sql
city like "%es%"
```

## Begint met

De functie `startsWith` wordt gebruikt om te bepalen of een tekenreeks begint met een opgegeven subtekenreeks als een booleaanse tekenreeks.

**Formaat**

```sql
{STRING_1}.startsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of de naam van de persoon begint met &quot;Joe&quot;.

```sql
person.name.startsWith("Joe")
```

## Begint niet met

De functie `doesNotStartWith` wordt gebruikt om te bepalen of een tekenreeks niet begint met een opgegeven subtekenreeks als een booleaanse tekenreeks.

**Formaat**

```sql
{STRING_1}.doesNotStartWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of de naam van de persoon niet begint met &quot;Joe&quot;.

```sql
person.name.doesNotStartWith("Joe")
```

## Eindigt met

De functie `endsWith` wordt gebruikt om te bepalen of een tekenreeks eindigt met een opgegeven subtekenreeks als een booleaanse tekenreeks.

**Formaat**

```sql
{STRING_1}.endsWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt met hoofdlettergevoeligheid of het e-mailadres van de persoon eindigt op &quot;.com&quot;.

```sql
person.emailAddress.endsWith(".com")
```

## Eindigt niet met

De functie `doesNotEndWith` wordt gebruikt om te bepalen of een tekenreeks niet eindigt met een opgegeven subtekenreeks als een booleaanse tekenreeks.

**Formaat**

```sql
{STRING_1}.doesNotEndWith({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt met hoofdlettergevoeligheid of het e-mailadres van de persoon niet eindigt met &quot;.com&quot;.

```sql
person.emailAddress.doesNotEndWith(".com")
```

## Bevat

De functie `contains` wordt gebruikt om te bepalen of een tekenreeks een opgegeven subtekenreeks als een booleaanse tekenreeks bevat.

**Formaat**

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

De functie `doesNotContain` wordt gebruikt om te bepalen of een tekenreeks geen opgegeven subtekenreeks als een booleaanse tekenreeks bevat.

**Formaat**

```sql
{STRING_1}.doesNotContain({STRING_2}, {BOOLEAN})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks waarnaar moet worden gezocht binnen de eerste tekenreeks. |
| `{BOOLEAN}` | Een optionele parameter om te bepalen of de controle hoofdlettergevoelig is. Standaard is dit ingesteld op true. |

**Voorbeeld**

De volgende PQL-query bepaalt met hoofdlettergevoeligheid of het e-mailadres van de persoon de tekenreeks &quot;2010@gm&quot; niet bevat.

```sql
person.emailAddress.doesNotContain("2010@gm")
```

## Gelijk

De functie `equals` wordt gebruikt om te bepalen of een tekenreeks gelijk is aan de opgegeven tekenreeks als een booleaanse tekenreeks.

**Formaat**

```sql
{STRING_1}.equals({STRING_2})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks die met de eerste tekenreeks moet worden vergeleken. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of de naam van de persoon &quot;John&quot; is.

```sql
person.name.equals("John")
```

## Niet gelijk aan

De functie `notEqualTo` wordt gebruikt om te bepalen of een tekenreeks niet gelijk is aan de opgegeven tekenreeks als een booleaanse tekenreeks.

**Formaat**

```sql
{STRING_1}.notEqualTo({STRING_2})
```

| Argument | Beschrijving |
| --------- | ----------- |
| `{STRING_1}` | De tekenreeks die de controle moet uitvoeren. |
| `{STRING_2}` | De tekenreeks die met de eerste tekenreeks moet worden vergeleken. |

**Voorbeeld**

De volgende PQL-query bepaalt, met hoofdlettergevoeligheid, of de naam van de persoon niet &quot;John&quot; is.

```sql
person.name.notEqualTo("John")
```

## Overeenkomsten

De functie `matches` wordt gebruikt om te bepalen of een tekenreeks overeenkomt met een specifieke reguliere expressie. Gelieve te verwijzen naar [&#x200B; dit document &#x200B;](https://docs.oracle.com/javase/8/docs/api/java/util/regex/Pattern.html) voor meer informatie over passende patronen in regelmatige uitdrukkingen als boolean.

**Formaat**

```sql
{STRING_1}.matches(STRING_2})
```

**Voorbeeld**

De volgende PQL-query bepaalt, zonder onderscheid tussen hoofdletters en kleine letters, of de naam van de persoon begint met &quot;John&quot;.

```sql
person.name.matches("(?i)^John")
```

>[!NOTE]
>
>Als u regelmatige uitdrukkingsfuncties zoals `\w` gebruikt, moet u **&#x200B;**&#x200B;ontsnappen backslash karakter. Dus in plaats van alleen te schrijven `\w` moet u een extra backslash en schrijven `\\w` opnemen.

## Groep met reguliere expressies

De functie `regexGroup` wordt gebruikt om specifieke informatie te extraheren, op basis van de reguliere expressie die als een tekenreeks wordt opgegeven.

**Formaat**

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
>Als u regelmatige uitdrukkingsfuncties zoals `\w` gebruikt, moet u **&#x200B;**&#x200B;ontsnappen backslash karakter. Dus in plaats van alleen te schrijven `\w` moet u een extra backslash en schrijven `\\w` opnemen.

## Volgende stappen

Nu u over koordfuncties hebt geleerd, kunt u hen binnen uw vragen van PQL gebruiken. Voor meer informatie over andere functies van PQL, te lezen gelieve het [&#x200B; overzicht van Profile Query Language &#x200B;](./overview.md).
