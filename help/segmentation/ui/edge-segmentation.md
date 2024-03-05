---
solution: Experience Platform
title: gebruikersgids voor Edge Segmentation
description: Leer hoe te om randsegmentatie te gebruiken om segmentdefinities in Platform onmiddellijk op de rand te evalueren, toelatend de zelfde pagina en volgende de gebruikscituaties van de paginagrootte.
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Edge segmentation UI-hulplijn

>[!NOTE]
>
>De segmentatie van de rand is nu over het algemeen beschikbaar aan alle gebruikers van het Platform. Als u de definities van het randsegment tijdens bèta creeerde, zullen deze segmentdefinities operationeel blijven.

Randsegmentatie is de mogelijkheid om segmenten in Adobe Experience Platform ogenblikkelijk te evalueren [op de rand](../../web-sdk/home.md)en de volgende pagina&#39;s aanpassen.

>[!IMPORTANT]
>
> De Edge-gegevens worden opgeslagen op een locatie op de Edge-server die het dichtst bij de locatie ligt waar ze zijn verzameld en kunnen worden opgeslagen op een andere locatie dan die welke is aangewezen als het Adobe Experience Platform-datacenter in de hub (of principal).
>
> Bovendien zal de engine voor randsegmentatie alleen aanvragen aan de rand uitvoeren waar deze zich bevindt **één** primaire gemarkeerde identiteit, die consistent is met niet-Edge-primaire identiteiten.

## Type Edge-segmenteringsquery {#query-types}

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
| Een enkele gebeurtenis met een profielkenmerk negeren | Elke segmentdefinitie die verwijst naar een negatiefunctie van één binnenkomende gebeurtenis en een of meer profielkenmerken | Mensen die in de VS wonen en **niet** heeft de homepage bezocht. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| Eén gebeurtenis binnen een tijdvenster | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis binnen een ingestelde periode. | Mensen die de laatste 24 uur de homepage hebben bezocht. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis met een profielkenmerk binnen een relatief tijdvenster van minder dan 24 uur | Elke segmentdefinitie die verwijst naar één binnenkomende gebeurtenis, met een of meer profielkenmerken, en die optreedt binnen een relatief tijdvenster van minder dan 24 uur. | Mensen die in de VS wonen en de laatste 24 uur de homepage hebben bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)])` |
| Eén gebeurtenis die binnen een tijdvenster is genegeerd met een profielkenmerk | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde enkele binnenkomende gebeurtenis binnen een tijdsperiode. | Mensen die in de VS wonen en **niet** heeft de laatste 24 uur de homepage bezocht. | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]))` |
| Frequentiegebeurtenis binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een gebeurtenis die een bepaald aantal keren binnen een tijdvenster van 24 uur plaatsvindt. | Personen die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Frequentiegebeurtenis met een profielkenmerk binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen uit de VS die de homepage hebben bezocht **ten minste** vijf keer in de laatste 24 uur. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| Gebeurtenis met een negatieve frequentie binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en een genegeerde gebeurtenis die een bepaald aantal keren plaatsvindt binnen een tijdvenster van 24 uur. | Personen die de homepage niet hebben bezocht **meer** meer dan vijf keer in de laatste 24 uur. | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| Meerdere inkomende treffers binnen een tijdprofiel van 24 uur | Elke segmentdefinitie die verwijst naar meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen die de homepage hebben bezocht **of** heeft de laatste 24 uur de afhandelingspagina bezocht. | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Meerdere gebeurtenissen met een profiel binnen een tijdvenster van 24 uur | Elke segmentdefinitie die verwijst naar een of meer profielkenmerken en meerdere gebeurtenissen die binnen een tijdsvenster van 24 uur optreden. | Personen uit de VS die de homepage hebben bezocht **en** heeft de laatste 24 uur de afhandelingspagina bezocht. | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| Segment van segmenten | Elke segmentdefinitie die een of meer batch- of streaming segmenten bevat. | Mensen die in de VS wonen en in het segment &quot;bestaand&quot; zitten. | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| Query die verwijst naar een kaart | Elke segmentdefinitie die verwijst naar een kaart met eigenschappen. | Personen die aan hun winkelwagentje hebben toegevoegd op basis van externe segmentgegevens. | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

Een segmentdefinitie zal **niet** voor randsegmentatie in het volgende scenario worden toegelaten:

- De segmentdefinitie omvat een combinatie van één gebeurtenis en een `inSegment` gebeurtenis.
   - Als de segmentdefinitie in de `inSegment` gebeurtenis is alleen profiel, de segmentdefinitie **zal** worden ingeschakeld voor randsegmentatie.

## Volgende stappen

In deze handleiding wordt uitgelegd hoe u segmentatiedefinities met randsegmentatie op Adobe Experience Platform kunt evalueren. Voor meer informatie over het gebruik van de gebruikersinterface van het Experience Platform leest u de [Gebruikershandleiding voor segmentatie](./overview.md). Ga voor meer informatie over het uitvoeren van vergelijkbare acties en het werken met segmentdefinities met Experience Platform-API&#39;s naar de [hulplijn voor Edge segmentation-API](../api/edge-segmentation.md).

## Bijlage

In de volgende sectie worden veelgestelde vragen over de segmentatie van randen weergegeven:

### Hoe lang duurt het voor een segmentdefinitie beschikbaar is op het Netwerk van de Rand?

Het duurt tot één uur voor een segmentdefinitie beschikbaar is in het Edge-netwerk.
