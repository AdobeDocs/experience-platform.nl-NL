---
keywords: Experience Platform;home;populaire onderwerpen;Gegevenskwaliteit;Kwaliteit;Ondersteunde validatie;Validatie;ondersteunde validatie;
solution: Experience Platform
title: Gegevenskwaliteit
topic: overview
description: Het volgende document bevat een overzicht van de ondersteunde controles en validatiegedragingen voor batch- en streaming-opname in Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 4%

---


# Gegevenskwaliteit in Adobe Experience Platform

Adobe Experience Platform biedt duidelijk gedefinieerde garanties voor volledigheid, nauwkeurigheid en consistentie voor alle gegevens die via batch- of streaming opname zijn geüpload. Het volgende document bevat een overzicht van de ondersteunde controles en validatiegedragingen voor batch- en streaming-opname in [!DNL Experience Platform].

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

Zowel batch- als streaming-opname voorkomt dat mislukte gegevens stroomafwaarts gaan door onjuiste gegevens te verplaatsen voor ophalen en analyse in [!DNL Data Lake]. Gegevensinvoer biedt de volgende validaties voor batch- en streaming-opname.

### Inname in batch

De volgende validaties worden uitgevoerd voor batchinvoer:

| Validatiegebied | Beschrijving |
| --------------- | ----------- |
| Schema | Zorgt ervoor dat het schema **niet** leeg is en een verwijzing naar het verenigingsschema bevat, als volgt: `"meta:immutableTags": ["union"]` |
| `identityField` | Hiermee zorgt u ervoor dat alle geldige identiteitsbeschrijvingen zijn gedefinieerd. |
| `createdUser` | Zorgt ervoor dat de gebruiker die de partij heeft ingenomen de partij mag innemen. |

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

Meer informatie over de manier waarop [!DNL Platform] gegevens controleert en valideert vindt u in de [documentatie voor gegevensstromen controleren](./monitor-data-ingestion.md).
