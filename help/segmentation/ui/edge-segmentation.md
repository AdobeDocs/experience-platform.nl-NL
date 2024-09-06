---
solution: Experience Platform
title: UI-gids Edge Segmentation
description: Leer hoe te om randsegmentatie te gebruiken om segmentdefinities in Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 057db1432493a8443eb91b0fc371d0bdffb3de86
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Handleiding Edge-segmenteringsinterface

>[!NOTE]
>
>Edge-segmentatie is nu algemeen beschikbaar voor alle platformgebruikers. Als u de definities van het randsegment tijdens bèta creeerde, zullen deze segmentdefinities operationeel blijven.

De segmentatie van Edge is de capaciteit om segmenten in Adobe Experience Platform onmiddellijk [ op de rand ](../../web-sdk/home.md) te evalueren, toelatend de zelfde pagina en volgende het gebruikscase van de paginagrootte.

>[!IMPORTANT]
>
> De Edge-gegevens worden opgeslagen op een locatie op de Edge-server die het dichtst bij de locatie ligt waar ze zijn verzameld en kunnen worden opgeslagen op een andere locatie dan die welke is aangewezen als het Adobe Experience Platform-datacenter in de hub (of principal).
>
> Bovendien, zal de motor van de randsegmentatie slechts verzoeken op de rand waar er **één** primaire duidelijke identiteit is, die met niet op rand-gebaseerde primaire identiteiten verenigbaar is.

## Type Edge-segmentquery {#query-types}

Momenteel kunnen alleen bepaalde querytypen worden geëvalueerd met randsegmentatie. De volgende secties verstrekken een lijst van vraagtypes die met randsegmentatie en die kunnen worden geëvalueerd die momenteel niet worden gesteund.

Een vraag kan met randsegmentatie worden geëvalueerd als het aan om het even welke criteria voldoet die in de volgende lijst worden geschetst.

>[!NOTE]
>
>Als de vraag om het even welke vraagtypes in de volgende lijst aanpast, zal het automatisch worden geëvalueerd gebruikend randsegmentatie. Het systeem bepaalt deze mogelijkheid automatisch gebaseerd op de vraaguitdrukking.

| Type query | Details |
| ---------- | ------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. |
| Eén gebeurtenis binnen een relatief tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis. |
| Eén gebeurtenis met een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis met een tijdvenster. |
| Alleen profiel | Elke segmentdefinitie die alleen naar een profielkenmerk verwijst. |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. **Nota:** als een segment van segmenten wordt gebruikt, zal de profielontzetting **elke 24 uren** gebeuren. |
| Meerdere gebeurtenissen met een profielkenmerk | Om het even welke segmentdefinitie die naar veelvoudige gebeurtenissen **binnen de laatste 24 uren** verwijst en (naar keuze) heeft één of meerdere profielattributen. |

Een segmentdefinitie zal **** niet voor randsegmentatie in het volgende scenario worden toegelaten:

- De segmentdefinitie bevat een combinatie van één gebeurtenis en een `inSegment` -gebeurtenis.
   - Nochtans, als de segmentdefinitie in de `inSegment` gebeurtenis profiel slechts is, zal de segmentdefinitie **** voor randsegmentatie worden toegelaten.
- In de segmentdefinitie wordt &quot;Jaar negeren&quot; gebruikt als onderdeel van de tijdbeperkingen.

## Volgende stappen

In deze handleiding wordt uitgelegd hoe u segmentatiedefinities met randsegmentatie op Adobe Experience Platform kunt evalueren. Om meer over het gebruiken van het gebruikersinterface van het Experience Platform te leren, te lezen gelieve de [ gebruikersgids van de Segmentatie ](./overview.md). Leren hoe te om gelijkaardige acties uit te voeren en met segmentdefinities te werken gebruikend Experience Platform APIs, gelieve de [ gids van de randsegmentatie API ](../api/edge-segmentation.md) te bezoeken.

## Bijlage

In de volgende sectie worden veelgestelde vragen over de segmentatie van randen weergegeven:

### Hoe lang duurt het voordat een segmentdefinitie beschikbaar is op de Edge Network?

Het duurt tot één uur voor een segmentdefinitie beschikbaar is op de Edge Network.
