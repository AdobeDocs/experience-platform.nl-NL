---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Kwaliteit van gegevensinvoer
topic: overview
translation-type: tm+mt
source-git-commit: 24df962656706d769a7034020d96a545e8f905ca

---


# Gegevenskwaliteit in het Adobe Experience Platform

Het Adobe Experience Platform biedt duidelijk gedefinieerde garanties voor de volledigheid, nauwkeurigheid en consistentie voor alle gegevens die via batch- of streaming opname zijn geüpload. Het volgende document bevat een overzicht van de ondersteunde controles en validatiegedragingen voor batch- en streaming-opname in het Experience Platform.

## Ondersteunde controles

|   | Batchinname | Streaming insluiting |
| ------ | --------------- | ------------------- |
| Gegevenstype controleren | Ja | Ja |
| Enumcontrole | Ja | Ja |
| Bereik controleren (min, max) | Ja | Ja |
| Vereiste veldcontrole | Ja | Ja |
| Patrooncontrole | Nee | Ja |
| Indelingscontrole | Nee | Ja |

## Ondersteund validatiegedrag

Zowel partij als het stromen ingestie verhinderen ontbroken gegevens stroomafwaarts te gaan door slechte gegevens voor herwinning en analyse in het meer van Gegevens te bewegen. Gegevensinvoer biedt de volgende validaties voor batch- en streaming-opname.

### Inname in batch

De volgende validaties worden uitgevoerd voor batchinvoer:

| Validatiegebied | Beschrijving |
| --------------- | ----------- |
| Schema | Zorgt ervoor dat het schema **niet** leeg is en een verwijzing naar het verenigingsschema bevat, als volgt: `"meta:immutableTags": ["union"]` |
| `identityField` | Hiermee zorgt u ervoor dat alle geldige identiteitsbeschrijvingen zijn gedefinieerd. |
| `createdUser` | Hiermee zorgt u ervoor dat de gebruiker die de batch heeft ingeslikt, de batch mag innemen. |

### Streaming opname

De volgende validaties worden uitgevoerd voor streaming invoer:

| Validatiegebied | Beschrijving |
| --------------- | ----------- |
| Schema | Zorgt ervoor dat het schema **niet** leeg is en een verwijzing naar het verenigingsschema bevat, als volgt: `"meta:immutableTags": ["union"]` |
| `identityField` | Hiermee zorgt u ervoor dat alle geldige identiteitsbeschrijvingen zijn gedefinieerd. |
| JSON | Zorgt ervoor dat de JSON geldig is. |
| IMS-organisatie | Zorgt ervoor dat de vermelde IMS-organisatie een geldige organisatie is. |
| Bronnaam | Zorgt ervoor dat de naam van de gegevensbron wordt gespecificeerd. |
| Gegevensset | Zorgt ervoor dat de dataset wordt gespecificeerd, toegelaten en niet is verwijderd. |
| Koptekst | Zorgt ervoor dat de kopbal wordt gespecificeerd en geldig is. |

Meer informatie over hoe het Platform gegevens controleert en bevestigt kan in de documentatie [van de](./monitor-data-flows.md)controlegegevensstromen worden gevonden.
