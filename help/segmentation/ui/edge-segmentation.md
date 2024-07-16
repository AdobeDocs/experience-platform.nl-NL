---
solution: Experience Platform
title: UI-gids Edge Segmentation
description: Leer hoe te om randsegmentatie te gebruiken om segmentdefinities in Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c14c6b8037993b3696b4a99633c80c6ee9679399
workflow-type: tm+mt
source-wordcount: '970'
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

| Type query | Details | Voorbeeld | PQL-voorbeeld |
| ---------- | ------- | ------- | ----------- |
| Eén gebeurtenis | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die een artikel aan hun winkelwagentje hebben toegevoegd. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| Eén profiel | Alle segmentdefinities die verwijzen naar één kenmerk met alleen profiel | Mensen die in de VS wonen. | `homeAddress.countryCode = "US"` |
| Eén gebeurtenis die naar een profiel verwijst | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en één binnenkomende gebeurtenis zonder tijdbeperking. | Mensen die in de VS wonen en die de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| Een enkele gebeurtenis met een profielkenmerk negeren | Elke segmentdefinitie die verwijst naar een negatiefunctie van één binnenkomende gebeurtenis en een of meer profielkenmerken | De mensen die in de V.S. wonen en **niet** hebben de homepage bezocht. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Eén gebeurtenis binnen een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een ingestelde periode. | Mensen die de laatste 24 uur de homepage hebben bezocht. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | Mensen die in de VS wonen en de laatste 24 uur de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis die binnen een tijdvenster is genegeerd met een profielkenmerk | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen een tijdsperiode. | De mensen die in de V.S. wonen en **** hebben niet de homepage in de laatste 24 uren bezocht. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]))` |
| Frequentiegebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een gebeurtenis die een bepaald aantal keren binnen een tijdvenster van 24 uur plaatsvindt. | De mensen die de homepage **minstens** vijf keer in de laatste 24 uren bezochten. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Frequentiegebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | De mensen van de V.S. die de homepage **minstens** vijf keer in de laatste 24 uren bezochten. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Gebeurtenis met een negatieve frequentie binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | De mensen die niet de homepage **meer** meer dan vijf keer in de laatste 24 uren hebben bezocht. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Meerdere inkomende treffers binnen een tijdprofiel van 24 uur | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | De mensen die de homepage **of** bezochten de controlepagina binnen de laatste 24 uren. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Meerdere gebeurtenissen met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | De mensen van de V.S. die de homepage **bezochten en** bezochten de controlepagina binnen de laatste 24 uren. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. | Mensen die in de VS wonen en in het segment &quot;bestaand&quot; zitten. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Query die verwijst naar een kaart | Elke segmentdefinitie die verwijst naar een kaart met eigenschappen. | Personen die aan hun winkelwagentje hebben toegevoegd op basis van externe segmentgegevens. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

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
