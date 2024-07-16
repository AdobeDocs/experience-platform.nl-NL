---
keywords: Experience Platform;ontwikkelaarshandleiding;eindpunt;Data Science Workspace;populaire onderwerpen;
solution: Experience Platform
title: Bijlage API-handleiding voor leren van Sensei
description: In de volgende secties vindt u informatie over verschillende functies van de API voor leren van Sensei Machine.
role: Developer
exl-id: 2c8d3ae8-7ad7-4ff6-8d6b-3a42d3eccdff
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 1%

---

# [!DNL Sensei Machine Learning] API-hulplijnbijlage

In de volgende secties vindt u informatie over diverse functies van de API van [!DNL Sensei Machine Learning] .

## Zoekparameters voor ophalen van elementen {#query}

De API van [!DNL Sensei Machine Learning] biedt ondersteuning voor queryparameters met het ophalen van elementen. De beschikbare vraagparameters en hun gebruik worden beschreven in de volgende lijst:

| Query-parameter | Beschrijving | Standaardwaarde |
| --------------- | ----------- | ------- |
| `start` | Geeft de beginindex voor paginering aan. | `start=0` |
| `limit` | Geeft het maximale aantal resultaten aan dat moet worden geretourneerd. | `limit=25` |
| `orderby` | Geeft de eigenschappen aan die moeten worden gebruikt voor sorteren in de volgorde van prioriteit. Omvat een streepje (**-**) vóór een bezitsnaam om in dalende orde te sorteren, anders worden de resultaten gesorteerd in het stijgen orde. | `orderby=created` |
| `property` | Hiermee wordt de vergelijkingsexpressie aangegeven waaraan een object moet voldoen om te worden geretourneerd. | `property=deleted==false` |

>[!NOTE]
>
>Wanneer het combineren van veelvoudige vraagparameters, moeten zij door ampersands (**&amp;**) worden gescheiden.

## Python CPU- en GPU-configuraties {#cpu-gpu-config}

De Motoren van de Python hebben de capaciteit om tussen of cpu of een GPU voor zijn opleiding of het scoren doeleinden te kiezen, en op een [ MLInstance ](./mlinstances.md) als taakspecificatie (`tasks.specification`) bepaald.

Hieronder volgt een voorbeeldconfiguratie die het gebruik van een CPU voor training en een GPU voor scoring opgeeft:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "training parameter",
                "value": "parameter value"
            }    
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "cpus": "1"
        }
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value" 
            }
        ],
        "specification": {
            "type": "ContainerTaskSpec",
            "gpus": "1"
        }
    }
]
```

>[!NOTE]
>
>De waarden van `cpus` en `gpus` geven niet het aantal CPU&#39;s of GPU&#39;s aan, maar het aantal fysieke machines. Deze waarden zijn toelaatbaar `"1"` en zullen anders een uitzondering genereren.

## PySpark- en Spark-bronconfiguraties {#resource-config}

De Motoren van de Vonk hebben de capaciteit om computermiddelen voor opleiding en het scoren te wijzigen. Deze bronnen worden in de volgende tabel beschreven:

| Bron | Beschrijving | Type |
| -------- | ----------- | ---- |
| driverMemory | Geheugen voor stuurprogramma in megabytes | int |
| driverCores | Aantal door de bestuurder gebruikte kernen | int |
| executeMemory | Geheugen voor uitvoerder in megabytes | int |
| executorCores | Aantal door de uitvoerder gebruikte kernen | int |
| numExecutors | Aantal executoren | int |

De middelen kunnen op een [ MLInstance ](./mlinstances.md) als of (A) individuele opleiding of het scoren parameters, of (B) binnen een extra specificatievoorwerp (`specification`) worden gespecificeerd. De volgende bronnenconfiguraties zijn bijvoorbeeld hetzelfde voor zowel training als scoring:

```json
[
    {
        "name": "train",
        "parameters": [
            {
                "key": "driverMemory",
                "value": "2048"
            },
            {
                "key": "driverCores",
                "value": "1"
            },
            {
                "key": "executorMemory",
                "value": "2048"
            },
            {
                "key": "executorCores",
                "value": "2"
            },
            {
                "key": "numExecutors",
                "value": "3"
            }
        ]
    },
    {
        "name": "score",
        "parameters": [
            {
                "key": "scoring parameter",
                "value": "parameter value"
            }
        ],
        "specification": {
            "type": "SparkTaskSpec",
            "name": "Spark Task name",
            "className": "Class name",
            "driverMemoryInMB": 2048,
            "driverCores": 1,
            "executorMemoryInMB": 2048,
            "executorCores": 2,
            "numExecutors": 3
        }
    }
]
```
