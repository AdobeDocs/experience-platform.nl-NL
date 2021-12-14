---
keywords: Experience Platform;home;mapper;mappingset;mapping;
solution: Experience Platform
title: Overzicht van toewijzingssets
topic-legacy: overview
description: Leer hoe u toewijzingssets kunt gebruiken met Adobe Experience Platform Data Prep.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Overzicht van toewijzingssets

Een toewijzingsset is een set toewijzingen waarmee gegevens van het ene schema naar het andere worden getransformeerd. Dit document bevat informatie over de samenstelling van toewijzingssets, zoals invoerschema, uitvoerschema en toewijzingen.

## Aan de slag

Voor dit overzicht is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

- [Gegevensprep](./home.md): Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).
- [Gegevensstromen](../dataflows/home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden gevormd over verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, aan [!DNL Identity] en [!DNL Profile]en [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): De methoden waarmee gegevens kunnen worden verzonden naar [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde kader waardoor [!DNL Experience Platform] organiseert de gegevens van de klantenervaring.

## Syntaxis toewijzingsset

Een toewijzingsset bestaat uit een id, naam, invoerschema, uitvoerschema en een lijst met gekoppelde toewijzingen.

De volgende JSON is een voorbeeld van een typische toewijzingenset:

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name": "Id",
            "description": "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Eigenschap | Beschrijving |
| -------- | ----------- |
| `id` | Een unieke id voor de toewijzingsset. |
| `name` | De naam van de toewijzingsset. |
| `inputSchema` | Het XDM-schema voor de binnenkomende gegevens. |
| `outputSchema` | Het XDM-schema waaraan de invoergegevens moeten voldoen, wordt getransformeerd. |
| `mappings` | Een serie van gebied aan gebied afbeeldingen van het bronschema aan het bestemmingsschema. |
| `sourceType` | Voor elke vermelde afbeelding, zijn `sourceType` kenmerk geeft het type bron aan dat moet worden toegewezen. Kan één van `ATTRIBUTE`, `STATIC`, of `EXPRESSION`: <ul><li> `ATTRIBUTE` wordt gebruikt voor alle waarden die in het bronpad worden gevonden. </li><li>`STATIC` wordt gebruikt voor waarden die in het bestemmingspad worden geïnjecteerd. Deze waarde blijft constant en wordt niet beïnvloed door het bronschema.</li><li> `EXPRESSION` wordt gebruikt voor een expressie die tijdens runtime wordt opgelost. Een lijst met beschikbare expressies vindt u in het dialoogvenster [handleiding voor toewijzingsfuncties](./functions.md).</li> </ul> |
| `source` | Voor elke vermelde afbeelding wordt de `source` Dit kenmerk geeft het veld aan dat u wilt toewijzen. Meer informatie over hoe te om uw bron te vormen kan in worden gevonden [bronsectie](#sources). |
| `destination` | Voor elke vermelde afbeelding wordt de `destination` kenmerk geeft het veld aan, of het pad naar het veld, waar de waarde wordt geëxtraheerd uit het `source` wordt geplaatst. Meer informatie over hoe te om uw bestemmingen te vormen kan in worden gevonden [doelsectie](#destination). |
| `mappings.name` | (*Optioneel*) Een naam voor de toewijzing. |
| `mappings.description` | (*Optioneel*) Een beschrijving van de toewijzing. |

## Toewijzingsbronnen configureren

In een afbeelding worden de `source` Dit kan een veld, expressie of statische waarde zijn. Op basis van het opgegeven brontype kan de waarde op verschillende manieren worden geëxtraheerd.

### Veld in kolomgegevens

Wanneer u een veld toewijst aan kolomgegevens, zoals een CSV-bestand, gebruikt u de opdracht `ATTRIBUTE` brontype. Als het veld `.` binnen de naam ervan gebruiken `\` om aan de waarde te ontsnappen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-CSV-bestand:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Voorbeeldtoewijzing**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Veld in geneste gegevens

Wanneer u een veld in geneste gegevens toewijst, zoals een JSON-bestand, gebruikt u de opdracht `ATTRIBUTE` brontype. Als het veld `.` binnen de naam ervan gebruiken `\` om aan de waarde te ontsnappen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-JSON-bestand**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Veld binnen een array

Wanneer u een veld in een array toewijst, kunt u een specifieke waarde ophalen met een index. Om dit te doen, gebruik `ATTRIBUTE` Het brontype en de index van de waarde die u wilt toewijzen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-JSON-bestand**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Array naar array of object naar object

Met de `ATTRIBUTE` brontype, kunt u een array ook rechtstreeks toewijzen aan een array of een object aan een object. Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-JSON-bestand**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Interactieve bewerkingen op arrays

Met de `ATTRIBUTE` brontype, kunt u door series herhaling en kaart hen aan een doelschema door een vervangingsindex te gebruiken (`[*]`). Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-JSON-bestand**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Constante waarde

Als u een constante of een statische waarde wilt toewijzen, gebruikt u de opdracht `STATIC` brontype.  Wanneer u de `STATIC` brontype, de `source` vertegenwoordigt de hard-gecodeerde waarde die u aan wilt toewijzen `destination`. Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-JSON-bestand**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Getransformeerde gegevens**

```json
{
    "userType:": "CUSTOMER"
}
```

### Expressies

Als u een expressie wilt toewijzen, gebruikt u de opdracht `EXPRESSION` brontype. Een lijst met geaccepteerde functies vindt u in de [handleiding voor toewijzingsfuncties](./functions.md). Wanneer u de `EXPRESSION` brontype, de `source` vertegenwoordigt de functie u wilt oplossen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Voorbeeld-JSON-bestand**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Toewijzingsdoelen configureren

In een afbeelding worden de `destination` is de locatie waar de waarde uit de `source` wordt ingevoegd.

### Veld op hoofdniveau

Wanneer u de `source` de waarde tot het wortelniveau van uw getransformeerde gegevens, volgt het voorbeeld hieronder:

**Voorbeeld-JSON-bestand**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "name": "John Smith"
}
```

### Geneste veld

Wanneer u de `source` volgt u het onderstaande voorbeeld om een waarde toe te voegen aan een genest veld in uw getransformeerde gegevens:

**Voorbeeld-JSON-bestand**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Veld bij een specifieke arrayindex

Wanneer u de `source` Volg het onderstaande voorbeeld voor een waarde van een specifieke index in een array in uw getransformeerde gegevens:

**Voorbeeld-JSON-bestand**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "piList": ["John Smith"]
}
```

### Iteratieve arraybewerking

Wanneer u arrays herhaaldelijk wilt doorlopen en de waarden aan het doel wilt toewijzen, kunt u een jokertekenindex gebruiken (`[*]`). Hieronder ziet u een voorbeeld:

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Voorbeeldtoewijzing**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Getransformeerde gegevens**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Volgende stappen

Door dit document te lezen, zou u nu moeten begrijpen hoe de kaartreeksen worden geconstrueerd, met inbegrip van hoe te om individuele afbeeldingen binnen een mappenset te vormen. Lees voor meer informatie over andere functies van Data Prep de [Overzicht van Data Prep](./home.md). Als u wilt weten hoe u toewijzingssets kunt gebruiken in de Data Prep API, leest u de [Handleiding voor ontwikkelaars van Data Prep](./api/overview.md).
