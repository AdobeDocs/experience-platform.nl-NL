---
title: Berekende kenmerken Veelgestelde vragen
description: Ontdek antwoorden op veelgestelde vragen over het gebruik van berekende kenmerken.
badge: "Bèta"
source-git-commit: 3b4e1e793a610c9391b3718584a19bd11959e3be
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---


# Veelgestelde vragen

>[!IMPORTANT]
>
>De berekende kenmerken staan momenteel in **bèta** en is **niet** beschikbaar voor alle gebruikers.

In Adobe Experience Platform zijn berekende kenmerken functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Hieronder volgt een lijst met veelgestelde vragen over berekende kenmerken.

## Welke datasets dragen bij tot berekende attributenberekeningen?

Bij berekende kenmerken wordt rekening gehouden met de gegevenssets van Experience Event voor het berekenen van berekende kenmerken die zijn ingesteld op realtime klantprofiel.

## Welke gebieden van het Gegevensmodel van de Ervaring (XDM) kunnen voor het creëren van gegevens verwerkte attributen worden gebruikt?

Alle XDM-velden in het schema Experience Event union kunnen worden gebruikt om berekende kenmerken te maken.

## Wat vertegenwoordigt de &quot;laatste evaluatietijd&quot;?

De laatste evaluatietijd betekent dat de gebeurtenissen **voorafgaand** naar die tijdstempel zijn doorgevoerd in de laatste geslaagde vernieuwing van het berekende kenmerk.

## Kan ik de vernieuwingsfrequentie kiezen? Hoe wordt dit besloten?

De vernieuwingsfrequentie wordt automatisch bepaald op basis van de terugzoekperiode van uw berekende kenmerk. Lees voor meer informatie hierover de [sectie terugzoekperiode](./overview.md#lookback-periods) van het berekende kenmerkenoverzicht.

## Hoe worden berekeningen beïnvloed door de gegevensvervaltijden van de Gebeurtenis van de Ervaring?

Berekende kenmerkberekeningen zijn gebaseerd op de gedefinieerde terugzoekperiode en de Experience Events die binnen die periode vallen. Deze berekeningen zijn dus: **niet** beïnvloed door het verlopen van de gegevens van de Gebeurtenis van de Ervaring. Maar om de nauwkeurigheid van uw berekende kenmerken te garanderen, moet uw terugzoekperiode **binnen** de grenzen van uw gegevens verlopen.

## Kan ik een gegevens verwerkt attribuut tot stand brengen dat op een ander gegevens verwerkt attribuut wordt gebaseerd?

Aangezien berekende kenmerken worden gemaakt met de velden Experience Event en zich in een Profile-veld bevinden, is het niet mogelijk om een berekend kenmerk rechtstreeks te gebruiken om een ander berekend kenmerk te maken.

## Zijn er grenzen aan het aantal gegevens verwerkte attributen ik kan creëren?

Het huidige maximumaantal van **gepubliceerd** berekende kenmerken zijn 25.

## Zijn er om het even welke stroomafwaartse implicaties voor het onbruikbaar maken van een gegevens verwerkt attribuut?

Voordat u het berekende kenmerk uitschakelt, **moet** ze uit uw downstreamsystemen verwijderen (zoals segmentatie, reizen of bestemmingen), omdat er complicaties kunnen optreden als ze niet worden verwijderd.

## Wat gebeurt wanneer ik een gegevens verwerkt attribuut onbruikbaar maak? {#inactive-status}

Wanneer een berekend kenmerk is uitgeschakeld of inactief wordt gemaakt, wordt het niet meer bijgewerkt. Dientengevolge, dit gegevens verwerkte attribuut **kan** worden gebruikt in het opzoeken van profielen of andere downstreamtoepassingen.

## Hoe kunnen berekende kenmerken de betrokkenheid stimuleren?

Met berekende kenmerken wordt de profielverrijking bevorderd door de gebeurteniskenmerken samen te voegen op het niveau van het samengevoegde profiel. U kunt bijvoorbeeld marketingberichten aanpassen met het meest recente weergegeven product.
