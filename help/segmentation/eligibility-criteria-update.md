---
title: Update voor subsidiabiliteitscriteria voor segmentering
description: Leer over de updates van de segmenteringsgeschiktheidscriteria die de types van publiek beïnvloeden die kunnen worden geëvalueerd gebruikend het stromen en randsegmentatie.
hide: true
hidefromtoc: true
source-git-commit: 0bbee2100ed6fdc0f40457965e195d07de6eb2a1
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Update voor subsidiabiliteitscriteria voor segmentering

Vanaf 24 september 2024 zullen twee updates worden uitgevoerd die van invloed zijn op de segmenteringsgeschiktheid.

1. querytypen voor streaming en randsegmentatie
2. Samenvoegbeleid voor streaming en randsegmentatie

## Type query

Om het even welke **nieuwe of uitgegeven** segmentdefinities die de volgende vraagtypes aanpassen zullen **niet meer** worden geëvalueerd gebruikend het stromen of randsegmentatie. In plaats daarvan worden ze geëvalueerd met behulp van batchsegmentatie.

- Eén gebeurtenis met een tijdvenster van meer dan 24 uur
   - Activeer een publiek met alle profielen die een webpagina in de afgelopen 3 dagen hebben bekeken.
- Eén gebeurtenis zonder tijdvenster
   - Activeer een publiek met alle profielen die een webpagina hebben weergegeven.

Als u een segmentdefinitie gebruikend het stromen of randsegmentatie moet evalueren die het bijgewerkte vraagtype aanpast, kunt u een partij en het stromen vraag uitdrukkelijk tot stand brengen en hen combineren gebruikend segment van segmenten.

Als u bijvoorbeeld een publiek wilt activeren met alle profielen die een webpagina in de afgelopen 3 dagen hebben weergegeven met streaming segmentatie, kunt u de volgende query&#39;s maken:

- Q1 (Streaming): alle profielen die een webpagina in de afgelopen 24 uur hebben weergegeven
- Q2 (batch): alle profielen die de laatste drie dagen een webpagina hebben weergegeven

Vervolgens kunt u ze combineren door te verwijzen naar Q1 of Q2.

Op dezelfde manier kunt u de volgende query&#39;s maken als u een publiek wilt activeren met alle profielen die een webpagina weergeven:

- Vraag 3 (Streaming): Alle profielen die een webpagina in de afgelopen 24 uur hebben weergegeven
- V4 (batch): alle profielen die een webpagina hebben weergegeven.

Vervolgens kunt u ze combineren door naar Q3 of Q4 te verwijzen.

>[!IMPORTANT]
>
>Alle bestaande segmentdefinities die de vraagtypes aanpassen zullen geëvalueerd blijven gebruikend het stromen of randsegmentatie tot zij worden uitgegeven.
>
>Bovendien, zullen alle bestaande segmentdefinities die momenteel aan de andere het stromen of de evaluatiecriteria van de randsegmentatie voldoen geëvalueerd met het stromen of randsegmentatie blijven.

## Samenvoegbeleid

Om het even welke **nieuwe of uitgegeven** segmentdefinities die voor het stromen of randsegmentatie **kwalificeren moeten** op &quot;Actief op Edge&quot;fusiebeleid zijn.

Alle bestaande segmentdefinities die met streaming of randsegmentatie worden geëvalueerd, blijven werken zoals ze zijn.
