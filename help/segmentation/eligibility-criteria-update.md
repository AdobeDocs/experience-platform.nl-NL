---
title: Update voor subsidiabiliteitscriteria voor segmentering
description: Leer over de updates van de segmenteringsgeschiktheidscriteria die de types van publiek beïnvloeden die kunnen worden geëvalueerd gebruikend het stromen en randsegmentatie.
hide: true
hidefromtoc: true
exl-id: c91c0f75-9bc8-4fa7-9d27-9b07d0ea560c
source-git-commit: eafb7337edacc5d2b2aa9c38540aff946c8d39c0
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 0%

---

# Update voor subsidiabiliteitscriteria voor segmentering

>[!IMPORTANT]
>
>Alle bestaande segmentdefinities die momenteel worden geëvalueerd met behulp van streaming of randsegmentatie, blijven werken zoals ze zijn, tenzij ze worden bewerkt of bijgewerkt.

Vanaf 20 mei 2025 zullen drie updates worden uitgevoerd die van invloed zijn op de segmenteringsgeschiktheid.

1. In aanmerking komende regels
2. Geschiktheid tijdvenster
3. Batchgegevens opnemen in streaming publiek
4. Actief samenvoegbeleid

## Regelset {#ruleset}

Om het even welke **nieuwe of uitgegeven** segmentdefinities die de volgende heersers aanpassen zullen **niet meer** worden geëvalueerd gebruikend het stromen of randsegmentatie. In plaats daarvan worden ze geëvalueerd met behulp van batchsegmentatie.

- Eén gebeurtenis met een tijdvenster van meer dan 24 uur
   - Activeer een publiek met alle profielen die een webpagina in de afgelopen 3 dagen hebben bekeken.
- Eén gebeurtenis zonder tijdvenster
   - Activeer een publiek met alle profielen die een webpagina hebben weergegeven.

## Tijdvenster {#time-window}

Om een publiek met het stromen segmentatie te evalueren, moet het **&#x200B;**&#x200B;binnen een 24 uurstijdvenster worden beperkt.

## Batchgegevens opnemen in streaming publiek {#include-batch-data}

Voorafgaand aan deze update kunt u een definitie voor streaming publiek maken die zowel batch- als streaming gegevensbronnen combineert. Met de nieuwste update wordt het maken van een publiek met zowel batch- als streaming-gegevensbronnen echter geëvalueerd aan de hand van batchsegmentatie.

Als u een segmentdefinitie moet evalueren met behulp van streaming of randsegmentatie die overeenkomt met de bijgewerkte linialen, moet u expliciet een batch- en streaming liniaal maken en deze combineren met behulp van segmentsegmenten. Deze partijheersers **moeten** op een profielschema worden gebaseerd.

Bijvoorbeeld, laten wij zeggen u twee publiek hebt, met één publiek die het schemagegevens van het profiel en de andere gegevens van het de gebeurtenisschema van de huisvestingservaring huisvesten:

| Doelgroep | Schema | Source-type | Query-definitie | Id van publiek |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Inwoners uit Californië | Profiel | Batch | Het adres van het huis is in de staat van Californië | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Recente controles | Experience Event | Streaming | Heeft in de laatste 24 uur ten minste één afhandeling | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

Als u de partijcomponent in uw het stromen publiek wilt gebruiken, zult u een verwijzing naar het partijpubliek moeten maken gebruikend segment van segmenten.

Een voorbeeldregel die de twee soorten publiek samenvoegt, ziet er als volgt uit:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and 
CHAIN(xEvent, timestamp, [C0: WHAT(eventType.equals("commerce.checkouts", false)) 
WHEN(<= 24 hours before now)])
```

Het resulterende publiek *zal* worden geëvalueerd gebruikend het stromen segmentatie, aangezien het hefboomwerkingen het lidmaatschap van het partijpubliek door naar de component van het partijpubliek te verwijzen.

Nochtans, als u twee publiek met gebeurtenisgegevens wilt combineren, kunt u **niet** enkel de twee gebeurtenissen combineren. U moet beide soorten publiek maken en vervolgens een ander publiek maken dat `inSegment` gebruikt om naar beide soorten publiek te verwijzen.

Bijvoorbeeld, laten wij zeggen u twee publiek hebt, met beide publiek woonachtig gebeurtenisschemagegevens:

| Doelgroep | Schema | Source-type | Query-definitie | Id van publiek |
| -------- | ------ | ----------- | ---------------- | ----------- |
| Recente verlaten | Gebeurtenis Experience | Batch | Heeft ten minste één gebeurtenis voor verlaten in de afgelopen 24 uur | `e3be6d7f-1727-401f-a41e-c296b45f607a` |
| Recente controles | Experience Event | Streaming | Heeft in de laatste 24 uur ten minste één afhandeling | `9e1646bb-57ff-4309-ba59-17d6c5bab6a1` |

In deze situatie, zou u een derde publiek als volgt moeten creëren:

```
inSegment("e3be6d7f-1727-401f-a41e-c296b45f607a") and inSegment("9e1646bb-57ff-4309-ba59-17d6c5bab6a1")
```

>[!IMPORTANT]
>
>Alle bestaande segmentdefinities die overeenkomen met de regels, blijven geëvalueerd met streaming of randsegmentatie totdat ze worden bewerkt.
>
>Bovendien, zullen alle bestaande segmentdefinities die momenteel aan de andere het stromen of de evaluatiecriteria van de randsegmentatie voldoen geëvalueerd met het stromen of randsegmentatie blijven.

## Samenvoegbeleid {#merge-policy}

Om het even welke **nieuwe of uitgegeven** segmentdefinities die voor het stromen of randsegmentatie **kwalificeren moeten** op &quot;Actief op Edge&quot;fusiebeleid zijn.

Als er geen actieve reeks van het fusiebeleid is, zult u uw fusiebeleid [&#128279;](../profile/merge-policies/ui-guide.md#configure) moeten vormen en het plaatsen om op rand actief te zijn.
