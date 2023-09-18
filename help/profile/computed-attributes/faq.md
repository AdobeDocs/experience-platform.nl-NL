---
title: Berekende kenmerken Veelgestelde vragen
description: Ontdek antwoorden op veelgestelde vragen over het gebruik van berekende kenmerken.
source-git-commit: fb5d3088b9fb330153bf64125df2f739eee80518
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---


# Veelgestelde vragen

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

Berekende kenmerkberekeningen worden teruggevuld voor de bepaalde terugzoekduur in de eerste tijdevaluatie en bijgewerkt op basis van incrementele gebeurtenissen voor volgende updates. Deze berekeningen zijn dus: **niet** beïnvloed door de gegevensvervaltijden van de Gebeurtenis van de Ervaring van de oude gegevens na de eerste evaluatie.

Bijvoorbeeld, als u een gegevens verwerkt attribuut creeert dat maandelijks met een periode van drie maanden terugblik, voor de eerste evaluatie wordt geëvalueerd, zal het gegevens verwerkte attribuut voor alle gebeurtenissen binnen die periode van drie maanden raadplegingen gegevens verwerken. Zelfs als de dataset van de Gebeurtenis van de Ervaring een gegevensvervaldatum één maand heeft, zal deze gegevensvervaldatum **niet** beïnvloedt maandelijks gegevens verwerkte attribuut zich verfrist, aangezien de evaluatieronde van de volgende maand incrementeel gebeurtenissen bijeenvoegt en de berekening bijwerkt.

>[!NOTE]
>
>Verlopen gegevens **kan** later worden teruggevuld door een berekend kenmerk. Vervaldatum gegevensset voor gebeurtenis **kan** beperkte de mogelijkheid om de waarde van het berekende kenmerk op een later tijdstip te valideren. Om de berekende kenmerkwaarde te bevestigen, zou uw raadplegingsperiode moeten blijven **binnen** de grenzen van de gegevensvervaldata.

## Kan ik een gegevens verwerkt attribuut tot stand brengen dat op een ander gegevens verwerkt attribuut wordt gebaseerd?

Aangezien berekende kenmerken worden gemaakt met de velden Experience Event en zich in een Profile-veld bevinden, is het niet mogelijk om een berekend kenmerk rechtstreeks te gebruiken om een ander berekend kenmerk te maken.

## Zijn er grenzen aan het aantal gegevens verwerkte attributen ik kan creëren?

Ja, er geldt een limiet voor het aantal berekende kenmerken dat u kunt maken. Raadpleeg de productbeschrijving of neem contact op met het accountteam van de Adobe voor meer informatie.

## Zijn er om het even welke stroomafwaartse implicaties voor het onbruikbaar maken van een gegevens verwerkt attribuut?

Voordat u het berekende kenmerk uitschakelt, **moet** ze uit uw downstreamsystemen verwijderen (zoals segmentatie, reizen of bestemmingen), omdat er complicaties kunnen optreden als ze niet worden verwijderd.

## Wat gebeurt wanneer ik een gegevens verwerkt attribuut onbruikbaar maak? {#inactive-status}

Wanneer een berekend kenmerk is uitgeschakeld of inactief wordt gemaakt, wordt het niet meer bijgewerkt. Dientengevolge, dit gegevens verwerkte attribuut **kan** worden gebruikt in het opzoeken van profielen of andere downstreamtoepassingen.

## Hoe kunnen berekende kenmerken de betrokkenheid stimuleren?

Met berekende kenmerken wordt de profielverrijking bevorderd door de gebeurteniskenmerken samen te voegen op het niveau van het samengevoegde profiel. U kunt bijvoorbeeld marketingberichten personaliseren met het meest recente weergegeven product.

## Hoe vaak worden berekende kenmerken geëvalueerd? Heeft dit betrekking op het beoordelingsschema voor de doelgroep?

De berekende attributen worden geëvalueerd in partijen onafhankelijk van het segmenteringsprogramma. Dit betekent dat, ongeacht het segmentatietype (batchsegmentatie of streamingsegmentatie), het berekende kenmerk volgens zijn eigen schema (per uur, per dag, per week of per maand) wordt geëvalueerd.

Wanneer het publiek wordt geëvalueerd, gebruikt het de **nieuwste** waarde van het berekende beschikbare kenmerk.

## Hoe beïnvloeden de gegevens verwerkte attributen met publiek geëvalueerd gebruikend het stromen segmentatie?

Als een streaming-segmentatie-geëvalueerd publiek een gegevens verwerkt attribuut gebruikt, zal het nemen **nieuwste waarde** van het berekende attribuut terwijl het publiek wordt geëvalueerd. Als het publiek bijvoorbeeld op zoek is naar aankoopgebeurtenissen, verwijst het publiek naar de laatst berekende waarde van het kenmerk wanneer de aankoopgebeurtenis plaatsvindt.

## Kan ik berekende kenmerken gebruiken op Edge?

Net als andere profielkenmerken zijn berekende kenmerken beschikbaar en kunnen deze worden gebruikt aan de randen. De berekende kenmerken zijn **niet** berekend aan de rand.

## Hoe worden labels voor gegevensgebruik toegepast op berekende kenmerken?

De gegevens verwerkte attributen leiden automatisch de etiketten van het gegevensgebruik van de brongebieden en datasets af die werden gebruikt om de gegevens verwerkte attributen te bepalen. Dit zorgt ervoor dat uw gedragsgegevens correct worden gebruikt.

## Hoe krijg ik toegang tot berekende kenmerken?

Om toegang te krijgen tot gegevens verwerkte attributen, zult u de aangewezen toestemmingen moeten hebben. Lees voor meer informatie over de vereiste machtigingen de [toegangsbeheerdocumentatie](../../access-control/home.md).

## Hoe gebruik ik berekende kenmerken met Adobe Journey Optimizer?

Als u berekende kenmerken wilt gebruiken tijdens reizen, moet u de opdracht `SystemComputedAttributes` veldgroep naar de gegevensbron van het Experience Platform. Voor meer informatie bij het vormen van de gegevensbron van het Experience Platform, gelieve te lezen [Adobe Experience Platform-gegevensbrongids](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html?lang=en).
