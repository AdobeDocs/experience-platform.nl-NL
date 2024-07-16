---
title: Berekende kenmerken Veelgestelde vragen
description: Ontdek antwoorden op veelgestelde vragen over het gebruik van berekende kenmerken.
exl-id: a4d3c06a-d135-453b-9637-4f98e62737a7
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Veelgestelde vragen

In Adobe Experience Platform zijn berekende kenmerken functies die worden gebruikt om gegevens op gebeurtenisniveau samen te voegen tot kenmerken op profielniveau. Deze functies worden automatisch berekend zodat zij over segmentatie, activering, en verpersoonlijking kunnen worden gebruikt. Hieronder volgt een lijst met veelgestelde vragen over berekende kenmerken.

## Hoe krijg ik toegang tot berekende kenmerken?

Om toegang tot gegevens verwerkte attributen te krijgen, zult u de aangewezen toestemmingen moeten hebben (**Mening Berekende attributen** en **beheert Gedetailleerde attributen**). Voor meer informatie over de vereiste toestemmingen, te lezen gelieve de [ documentatie van de toegangscontrole ](../../access-control/home.md). Leren hoe te om deze toestemmingen toe te passen, te lezen gelieve [ het leiden toestemmingengids ](../../access-control/ui/permissions.md).

## Welke datasets dragen bij tot berekende attributenberekeningen?

Bij berekende kenmerken wordt rekening gehouden met de gegevenssets van Experience Event voor het berekenen van berekende kenmerken die zijn ingesteld op realtime klantprofiel.

## Welke gebieden van het Gegevensmodel van de Ervaring (XDM) kunnen voor het creëren van gegevens verwerkte attributen worden gebruikt?

Alle XDM-velden in het schema Experience Event union kunnen worden gebruikt om berekende kenmerken te maken.

## Wat vertegenwoordigen &quot;laatste evaluatie&quot; en &quot;laatste evaluatiestatus&quot;?

Laatst geëvalueerd verwijst naar de tijdstempel tot welke gebeurtenissen worden beschouwd in de laatste succesvolle run. De laatste evaluatiestatus heeft betrekking op de vraag of de laatste evaluatieronde succesvol was.

## Kan ik de vernieuwingsfrequentie kiezen? Hoe wordt dit besloten?

De vernieuwingsfrequentie wordt automatisch bepaald op basis van de terugzoekperiode van uw berekende kenmerk. Voor meer informatie over dit, te lezen gelieve de [ sectie van de raadplegingsperiode ](./overview.md#lookback-periods) van het gegevens verwerkte attributenoverzicht.

## Hoe worden berekeningen beïnvloed door de gegevensvervaltijden van de Gebeurtenis van de Ervaring?

Berekende kenmerkberekeningen worden teruggevuld voor de bepaalde terugzoekduur in de eerste tijdevaluatie en bijgewerkt op basis van incrementele gebeurtenissen voor volgende updates. Dientengevolge, worden deze berekeningen **niet** beïnvloed door de gegevensvervalsing van de Gebeurtenis van de Ervaring van de oude gegevens na de eerste evaluatie.

Bijvoorbeeld, als u een gegevens verwerkt attribuut creeert dat maandelijks met een periode van drie maanden terugblik, voor de eerste evaluatie wordt geëvalueerd, zal het gegevens verwerkte attribuut voor alle gebeurtenissen binnen die periode van drie maanden raadplegingen gegevens verwerken. Zelfs als de dataset van de Gebeurtenis van de Ervaring een gegevensvervaldatum van één maand heeft, zal deze gegevensvervaldatum **niet** beïnvloeden de maandelijkse gegevens verwerkte attributen verfrissen zich, aangezien de de evaluatiereeks van de volgende maand incrementeel gebeurtenissen bijeenvoegen en de berekening bijwerken.

>[!NOTE]
>
>De verlopen gegevens **kunnen** niet later door een gegevens verwerkt attribuut worden teruggevuld. De gegevensvervaldatum van de dataset van de gebeurtenis **kan** de capaciteit beperken om de gegevens verwerkte waarde van attributen op een later punt in tijd te bevestigen. Om de gegevens verwerkte attributenwaarde te bevestigen, zou uw raadplegingsperiode **binnen** de grenzen van de gegevensvervalsingen moeten blijven.

## Kan ik een gegevens verwerkt attribuut tot stand brengen dat op een ander gegevens verwerkt attribuut wordt gebaseerd?

Aangezien berekende kenmerken worden gemaakt met de velden Experience Event en zich in een Profile-veld bevinden, is het niet mogelijk om een berekend kenmerk rechtstreeks te gebruiken om een ander berekend kenmerk te maken.

## Zijn er grenzen aan het aantal gegevens verwerkte attributen ik kan creëren?

Ja, er geldt een limiet voor het aantal berekende kenmerken dat u kunt maken. Raadpleeg de productbeschrijving of neem contact op met het accountteam van de Adobe voor meer informatie.

## Zijn er om het even welke stroomafwaartse implicaties voor het onbruikbaar maken van een gegevens verwerkt attribuut?

Alvorens uw gegevens verwerkte attributen onbruikbaar te maken, zou u **hen uit uw stroomafwaartse systemen (zoals segmentatie, reizen, of bestemmingen) moeten verwijderen, aangezien er complicaties kunnen zijn die zich voordoen als zij niet worden verwijderd.**

## Wat gebeurt wanneer ik een gegevens verwerkt attribuut onbruikbaar maak? {#inactive-status}

Wanneer een berekend kenmerk is uitgeschakeld of inactief wordt gemaakt, wordt het niet meer bijgewerkt. Dientengevolge, kan dit gegevens verwerkte attribuut **niet** in profielraadpleging of andere downstreamtoepassingen worden gebruikt.

## Hoe kunnen berekende kenmerken de betrokkenheid stimuleren?

Met berekende kenmerken wordt de profielverrijking bevorderd door de gebeurteniskenmerken samen te voegen op het niveau van het samengevoegde profiel. U kunt bijvoorbeeld marketingberichten personaliseren met het meest recente weergegeven product.

## Hoe vaak worden berekende kenmerken geëvalueerd? Heeft dit betrekking op het beoordelingsschema voor de doelgroep?

De gegevens verwerkte attributen worden geëvalueerd in a **partij** frequentie die **** aan het programma van uw publiek, bestemming, en reisevaluatie onafhankelijk is. Dit betekent dat, ongeacht het segmentatietype (batchsegmentatie of streamingsegmentatie), het berekende kenmerk volgens zijn eigen schema (per uur, per dag, per week of per maand) wordt geëvalueerd.

De eerste tijdevaluatie van uw gegevens verwerkte attributen gebeurt binnen de 24 uren van zijn **verwezenlijking**. De daaropvolgende batchevaluaties vinden plaats op een uur-, dag-, week- of maandbasis, afhankelijk van de gedefinieerde terugzoekperiode.

Als bijvoorbeeld een eerste evaluatie plaatsvindt op 9 oktober om 12.00 uur UTC, vinden de volgende evaluaties plaats op de volgende tijdstippen:

- Volgende dag vernieuwen: 10 oktober om 12 uur UTC
- Volgende week vernieuwen: 15 oktober om 12 uur UTC
- Volgende maandelijkse vernieuwing: 12 uur UTC op 1 november

>[!IMPORTANT]
>
>Dit is slechts het geval als snel verfrist zich **niet** toegelaten. Om te leren hoe de raadplegingsperiode verandert wanneer snel verfrist wordt toegelaten, te lezen gelieve [ snel sectie ](./overview.md#fast-refresh) verfrist.

Zowel de **wekelijkse** en **maandelijkse** vernieuwingen vinden op het begin van de **kalenderweek** (de Zondag van de nieuwe week) of het begin van de **kalendermaand** (de eerste van de nieuwe maand), in tegenstelling tot precies één week of één maand na de eerste datum van de tijdevaluatie plaats.

>[!NOTE]
>
>De gegevens verwerkte attributenwaarde wordt **niet** onmiddellijk verfrist in profiel na elke evaluatie in werking gesteld. Om ervoor te zorgen dat de bijgewerkte waarde zich in uw profielen bevindt, moet u rekening houden met een buffer van een paar uur tussen de evaluatietijd en het berekende kenmerkgebruik. Het gegevens verwerkte attribuut verfrist programma zich **systeem-bepaald** en **kan niet** worden gewijzigd. Neem voor meer informatie contact op met de klantenservice van de Adobe.

## Hoe beïnvloeden de gegevens verwerkte attributen met publiek geëvalueerd gebruikend het stromen segmentatie?

Als een het stromen-segmenteren-geëvalueerd publiek een gegevens verwerkt attribuut gebruikt, zal het de **recentste waarde** van de gegevens verwerkte attributen nemen terwijl het publiek wordt geëvalueerd. Als het publiek bijvoorbeeld op zoek is naar aankoopgebeurtenissen, verwijst het publiek naar de laatst berekende waarde van het kenmerk wanneer de aankoopgebeurtenis plaatsvindt.

## Kan ik berekende kenmerken gebruiken op Edge?

Net als andere profielkenmerken zijn berekende kenmerken beschikbaar en kunnen deze worden gebruikt aan de randen. Gelieve te merken op dat de gegevens verwerkte attributen **niet** op rand worden verwerkt.

## Hoe worden labels voor gegevensgebruik toegepast op berekende kenmerken?

De gegevens verwerkte attributen leiden automatisch de etiketten van het gegevensgebruik van de brongebieden en datasets af die werden gebruikt om de gegevens verwerkte attributen te bepalen. Dit zorgt ervoor dat uw gedragsgegevens correct worden gebruikt.

## Hoe gebruik ik berekende kenmerken met Adobe Journey Optimizer?

Als u berekende kenmerken wilt gebruiken tijdens reizen, moet u de veldgroep `SystemComputedAttributes` toevoegen aan de gegevensbron van het Experience Platform. Voor meer informatie bij het vormen van de gegevensbron van het Experience Platform, te lezen gelieve de [ gegevensbrongids van Adobe Experience Platform ](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/configure-journeys/data-source-journeys/adobe-experience-platform-data-source.html).
