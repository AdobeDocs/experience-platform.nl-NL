---
keywords: Experience Platform;home;mapper;mappingset;mapping;
solution: Experience Platform
title: Overzicht van toewijzingssets
topic-legacy: overview
description: Leer hoe u toewijzingssets kunt gebruiken met Adobe Experience Platform Data Prep.
source-git-commit: 97f803f649b2c42b0449a2f8f0cff370ed1aba93
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---


# Overzicht van toewijzingssets

Een toewijzingsset is een set toewijzingen waarmee gegevens van het ene schema naar het andere worden getransformeerd. Dit document bevat informatie over de samenstelling van toewijzingssets, zoals invoerschema, uitvoerschema en toewijzingen.

## Aan de slag

Voor dit overzicht is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

- [Gegevensvoorbeeld](./home.md): Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).
- [Gegevensstroom](../dataflows/home.md): Dataflows zijn een voorstelling van gegevenstaken die gegevens over het Platform verplaatsen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] worden verplaatst.
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): De methoden waarmee gegevens kunnen worden verzonden naar  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde kader waardoor de gegevens van de  [!DNL Experience Platform] klantenervaring worden georganiseerd.

## Syntaxis toewijzingsset

Een toewijzingsset bestaat uit een id, naam, invoerschema, uitvoerschema en een lijst met gekoppelde toewijzingen.

De volgende JSON is een voorbeeld van een typische toewijzingenset:

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
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
            "name" : "Id",
            "description" : "Identifier field"
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
| `sourceType` | Voor elke vermelde afbeelding, wijst zijn `sourceType` attribuut op het type van bron dat moet worden in kaart gebracht. Kan een van `ATTRIBUTE`, `STATIC`, of `EXPRESSION` zijn: <ul><li> `ATTRIBUTE` wordt gebruikt voor alle waarden die in het bronpad worden gevonden. </li><li>`STATIC` wordt gebruikt voor waarden die in het bestemmingspad worden geïnjecteerd. Deze waarde blijft constant en wordt niet beïnvloed door het bronschema.</li><li> `EXPRESSION` wordt gebruikt voor een expressie die tijdens runtime wordt opgelost. Een lijst met beschikbare expressies vindt u in de handleiding [toewijzingsfuncties](./functions.md).</li> </ul> |
| `source` | Voor elke vermelde afbeelding geeft het kenmerk `source` het veld aan dat u wilt toewijzen. Meer informatie over hoe te om uw bron te vormen kan in [bronnen sectie](#sources) worden gevonden. |
| `destination` | Voor elke vermelde afbeelding geeft het kenmerk `destination` het veld aan of het pad naar het veld, waar de waarde die uit het veld `source` is geëxtraheerd, wordt geplaatst. Meer informatie over hoe te om uw bestemmingen te vormen kan in [bestemmingssectie](#destination) worden gevonden. |
| `mappings.name` | (*Optioneel*) Een naam voor de toewijzing. |
| `mappings.description` | (*Optioneel*) Een beschrijving van de toewijzing. |

## Toewijzingsbronnen configureren

In een afbeelding kan `source` een veld, expressie of statische waarde zijn. Op basis van het opgegeven brontype kan de waarde op verschillende manieren worden geëxtraheerd.

### Veld in kolomgegevens

Wanneer u een veld in kolomgegevens toewijst, zoals een CSV-bestand, gebruikt u het brontype `ATTRIBUTE`. Als het veld `.` binnen de naam bevat, gebruikt u `\` om de waarde te verwijderen. Hieronder vindt u een voorbeeld van deze toewijzing:

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

Wanneer u een veld in geneste gegevens toewijst, zoals een JSON-bestand, gebruikt u het brontype `ATTRIBUTE`. Als het veld `.` binnen de naam bevat, gebruikt u `\` om de waarde te verwijderen. Hieronder vindt u een voorbeeld van deze toewijzing:

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

Wanneer u een veld in een array toewijst, kunt u een specifieke waarde ophalen met een index. Hiervoor gebruikt u het brontype `ATTRIBUTE` en de index van de waarde die u wilt toewijzen. Hieronder vindt u een voorbeeld van deze toewijzing:

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

Met het brontype `ATTRIBUTE` kunt u een array ook rechtstreeks toewijzen aan een array of een object aan een object. Hieronder vindt u een voorbeeld van deze toewijzing:

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

Met het brontype `ATTRIBUTE` kunt u arrays doorlopen en toewijzen aan een doelschema door een jokertekenindex (`[*]`) te gebruiken. Hieronder vindt u een voorbeeld van deze toewijzing:

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

Als u een constante of een statische waarde wilt toewijzen, gebruikt u het brontype `STATIC`.  Wanneer het gebruiken van `STATIC` brontype, `source` vertegenwoordigt de hard-gecodeerde waarde die u aan `destination` wilt toewijzen. Hieronder vindt u een voorbeeld van deze toewijzing:

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

Als u een expressie wilt toewijzen, gebruikt u het brontype `EXPRESSION`. Een lijst met toegestane functies vindt u in de handleiding [toewijzingsfuncties](./functions.md). Wanneer het gebruiken van `EXPRESSION` brontype, `source` vertegenwoordigt de functie u wilt oplossen. Hieronder vindt u een voorbeeld van deze toewijzing:

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

In een afbeelding is `destination` de locatie waar de waarde die uit `source` wordt geëxtraheerd, wordt ingevoegd.

### Veld op hoofdniveau

Wanneer u de waarde `source` aan het wortelniveau van uw getransformeerde gegevens wilt in kaart brengen, volg het onderstaande voorbeeld:

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

Wanneer u de waarde `source` aan een genesteld gebied in uw getransformeerde gegevens wilt in kaart brengen, volg het onderstaande voorbeeld:

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

Wanneer u de waarde `source` aan een specifieke index in een serie in uw getransformeerde gegevens wilt in kaart brengen, volg het onderstaande voorbeeld:

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

Wanneer u herhalende door series wilt herhalen en de waarden aan het doel in kaart brengen, kunt u een vervangingsindex (`[*]`) gebruiken. Hieronder ziet u een voorbeeld:

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

Door dit document te lezen, zou u nu moeten begrijpen hoe de kaartreeksen worden geconstrueerd, met inbegrip van hoe te om individuele afbeeldingen binnen een mappenset te vormen. Voor meer informatie over andere eigenschappen van de Prep van Gegevens, te lezen gelieve [Overzicht van de Prep van Gegevens](./home.md). Lees de [handleiding voor ontwikkelaars van Data Prep](./api/overview.md) voor informatie over het gebruik van toewijzingssets in de Data Prep API.