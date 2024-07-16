---
keywords: Experience Platform;home;mapper;mappingset;mapping;
solution: Experience Platform
title: Overzicht van toewijzingssets
description: Leer hoe u toewijzingssets kunt gebruiken met Adobe Experience Platform Data Prep.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 660948b7a43ed3c18feb74cccf8f9c607470759c
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Overzicht van toewijzingssets

Een toewijzingsset is een set toewijzingen waarmee gegevens van het ene schema naar het andere worden getransformeerd. Dit document bevat informatie over de samenstelling van toewijzingssets, zoals invoerschema, uitvoerschema en toewijzingen.

## Aan de slag

Voor dit overzicht is een goed begrip van de volgende Adobe Experience Platform-componenten vereist:

- [ Prep van Gegevens ](./home.md): De Prep van Gegevens staat gegevensingenieurs toe om, gegevens in kaart te brengen om te transformeren en te bevestigen aan en van het Model van Gegevens van de Ervaring (XDM).
- [ Dataflows ](../dataflows/home.md): Dataflows zijn een vertegenwoordiging van gegevensbanen die gegevens over Platform bewegen. Dataflows worden geconfigureerd op verschillende services, waardoor gegevens van bronconnectors naar doelgegevenssets worden verplaatst, naar [!DNL Identity] en [!DNL Profile] en naar [!DNL Destinations] .
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): de methoden waarmee gegevens naar [!DNL Experience Platform] kunnen worden verzonden.
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Het gestandaardiseerde framework waarmee [!DNL Experience Platform] gegevens voor de klantervaring indeelt.

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
| `sourceType` | Voor elke vermelde afbeelding geeft het kenmerk `sourceType` het type bron aan dat moet worden toegewezen. Kan een van `ATTRIBUTE` , `STATIC` of `EXPRESSION` zijn: <ul><li> `ATTRIBUTE` wordt gebruikt voor alle waarden die in het bronpad worden gevonden. </li><li>`STATIC` wordt gebruikt voor waarden die in het doelpad worden geïnjecteerd. Deze waarde blijft constant en wordt niet beïnvloed door het bronschema.</li><li> `EXPRESSION` wordt gebruikt voor een expressie die tijdens runtime wordt opgelost. Een lijst van beschikbare uitdrukkingen kan in de [ handleiding van toewijzingsfuncties ](./functions.md) worden gevonden.</li> </ul> |
| `source` | Voor elke vermelde afbeelding geeft het kenmerk `source` het veld aan dat u wilt toewijzen. Meer informatie over hoe te om uw bron te vormen kan in het [ overzicht van bronnen ](../sources/home.md) worden gevonden. |
| `destination` | Voor elke vermelde toewijzing geeft het kenmerk `destination` het veld aan of het pad naar het veld, waar de waarde die uit het veld `source` is geëxtraheerd, wordt geplaatst. Meer informatie over hoe te om uw bestemmingen te vormen kan in het [ bestemmingsoverzicht ](../destinations/home.md) worden gevonden. |
| `mappings.name` | (*Facultatieve*) een naam voor de afbeelding. |
| `mappings.description` | (*Facultatieve*) een beschrijving van de afbeelding. |

## Toewijzingsbronnen configureren

In een afbeelding kan de `source` een veld, expressie of statische waarde zijn. Op basis van het opgegeven brontype kan de waarde op verschillende manieren worden geëxtraheerd.

### Veld in kolomgegevens

Wanneer u een veld toewijst aan kolomgegevens, zoals een CSV-bestand, gebruikt u het brontype `ATTRIBUTE` . Als het veld `.` in de naam bevat, gebruikt u `\` om de waarde te laten ontsnappen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Csv- dossier van de Steekproef:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**de afbeelding van de Steekproef**

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

Wanneer u een veld toewijst aan geneste gegevens, zoals een JSON-bestand, gebruikt u het brontype `ATTRIBUTE` . Als het veld `.` in de naam bevat, gebruikt u `\` om de waarde te laten ontsnappen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Steekproef JSON- dossier**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**de afbeelding van de Steekproef**

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

**Steekproef JSON- dossier**

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

**de afbeelding van de Steekproef**

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

Met behulp van het brontype `ATTRIBUTE` kunt u een array ook rechtstreeks toewijzen aan een array of een object aan een object. Hieronder vindt u een voorbeeld van deze toewijzing:

**Steekproef JSON- dossier**

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

**de afbeelding van de Steekproef**

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

Met behulp van het brontype `ATTRIBUTE` kunt u arrays doorlopen en toewijzen aan een doelschema met behulp van een jokertekenindex (`[*]` ). Hieronder vindt u een voorbeeld van deze toewijzing:

**Steekproef JSON- dossier**

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

**de afbeelding van de Steekproef**

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

Als u een constante of een statische waarde wilt toewijzen, gebruikt u het brontype `STATIC` .  Wanneer u het brontype `STATIC` gebruikt, vertegenwoordigt `source` de hard-gecodeerde waarde die u aan `destination` wilt toewijzen. Hieronder vindt u een voorbeeld van deze toewijzing:

**Steekproef JSON- dossier**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**de afbeelding van de Steekproef**

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

Als u een expressie wilt toewijzen, gebruikt u het brontype `EXPRESSION` . Een lijst van toegelaten functies kan in de [ handleiding van toewijzingsfuncties ](./functions.md) worden gevonden. Wanneer u het brontype `EXPRESSION` gebruikt, vertegenwoordigt `source` de functie die u wilt omzetten. Hieronder vindt u een voorbeeld van deze toewijzing:

**Steekproef JSON- dossier**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**de afbeelding van de Steekproef**

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

In een toewijzing is `destination` de locatie waar de waarde die uit `source` wordt geëxtraheerd, wordt ingevoegd.

### Veld op hoofdniveau

Wanneer u de `source` -waarde wilt toewijzen aan het hoofdniveau van de getransformeerde gegevens, volgt u het onderstaande voorbeeld:

**Steekproef JSON- dossier**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**de afbeelding van de Steekproef**

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

Wanneer u de waarde `source` wilt toewijzen aan een genest veld in uw getransformeerde gegevens, volgt u het onderstaande voorbeeld:

**Steekproef JSON- dossier**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**de afbeelding van de Steekproef**

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

Wanneer u de `source` -waarde wilt toewijzen aan een specifieke index in een array in uw getransformeerde gegevens, volgt u het onderstaande voorbeeld:

**Steekproef JSON- dossier**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**de afbeelding van de Steekproef**

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

Wanneer u door series wilt herhalen en de waarden aan het doel in kaart brengen, kunt u een vervangingsindex (`[*]`) gebruiken. Hieronder ziet u een voorbeeld:

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

**de afbeelding van de Steekproef**

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

Door dit document te lezen, zou u nu moeten begrijpen hoe de kaartreeksen worden geconstrueerd, met inbegrip van hoe te om individuele afbeeldingen binnen een mappenset te vormen. Voor meer informatie over andere eigenschappen van de Prep van Gegevens, te lezen gelieve het [ overzicht van de Prep van Gegevens ](./home.md). Leren hoe te om kaartreeksen binnen de Prep API van Gegevens te gebruiken, gelieve de [ ontwikkelaarsgids van de Prep van Gegevens ](./api/overview.md) te lezen.
