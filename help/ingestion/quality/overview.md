---
keywords: Experience Platform;home;populaire onderwerpen;Gegevenskwaliteit;Kwaliteit;Ondersteunde validatie;Validatie;ondersteunde validatie;
solution: Experience Platform
title: Gegevenskwaliteit
topic-legacy: overview
description: Het volgende document bevat een overzicht van de ondersteunde controles en validatiegedragingen voor batch- en streaming-opname in Adobe Experience Platform.
exl-id: 7ef40859-235a-4759-9492-c63e5fd80c8e
source-git-commit: 7857b9a82dc1b5e12c9f8d757f6967b926124ec4
workflow-type: tm+mt
source-wordcount: '425'
ht-degree: 3%

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
| Schema | Zorgt ervoor dat het schema is **niet** leeg en bevat als volgt een verwijzing naar het schema union: `"meta:immutableTags": ["union"]` |
| `identityField` | Hiermee zorgt u ervoor dat alle geldige identiteitsbeschrijvingen zijn gedefinieerd. |
| `createdUser` | Zorgt ervoor dat de gebruiker die de partij heeft ingenomen de partij mag innemen. |

### Streaming opname

De volgende validaties worden uitgevoerd voor streaming invoer:

| Validatiegebied | Beschrijving |
| --------------- | ----------- |
| Schema | Zorgt ervoor dat het schema is **niet** leeg en bevat als volgt een verwijzing naar het schema union: `"meta:immutableTags": ["union"]` |
| `identityField` | Hiermee zorgt u ervoor dat alle geldige identiteitsbeschrijvingen zijn gedefinieerd. |
| JSON | Zorgt ervoor dat de JSON geldig is. |
| IMS-organisatie | Zorgt ervoor dat de vermelde IMS-organisatie een geldige organisatie is. |
| Bronnaam | Zorgt ervoor dat de naam van de gegevensbron wordt gespecificeerd. |
| Gegevensset | Zorgt ervoor dat de dataset wordt gespecificeerd, toegelaten en niet is verwijderd. |
| Koptekst | Zorgt ervoor dat de kopbal wordt gespecificeerd en geldig is. |

Meer informatie over hoe [!DNL Platform] kunt u vinden in de [documentatie over gegevensstromen bewaken](./monitor-data-ingestion.md).

## Validatie van identiteitswaarden

In de volgende tabel worden de bestaande regels beschreven die u moet volgen om ervoor te zorgen dat uw identiteitswaarde correct wordt gevalideerd.

| Naamruimte | Validatieregel | Systeemgedrag wanneer regel wordt overtreden |
| --- | --- | --- |
| ECID | <ul><li>De identiteitswaarde van een ECID moet precies 38 tekens zijn.</li><li>De identiteitswaarde van een ECID mag alleen uit getallen bestaan.</li></ul> | <ul><li>Als de identiteitswaarde van ECID niet precies 38 tekens is, wordt de record overgeslagen.</li><li>Als de identiteitswaarde van ECID niet-numerieke tekens bevat, wordt de record overgeslagen.</li></ul> |
| Niet-ECID | De identiteitswaarde mag niet langer zijn dan 1024 tekens. | Als de identiteitswaarde meer dan 1024 tekens bevat, wordt de record overgeslagen. |

Voor meer informatie over [!DNL Identity Service] zie de [[!DNL Identity Service] guardrails, overzicht](../../identity-service/guardrails.md).
