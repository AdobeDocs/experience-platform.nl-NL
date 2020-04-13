---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Overzicht van het realtime klantprofiel
topic: guide
translation-type: tm+mt
source-git-commit: d349ffab7c0de72d38b5195585c14a4a8f80e37c

---


# Overzicht van het realtime klantprofiel

Met het Adobe Experience Platform kunt u een gecoördineerde, consistente en relevante ervaring voor uw klanten ontwikkelen, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt. Dit overzicht zal u helpen de rol en het gebruik van het Profiel van de Klant in real time in het Platform van de Ervaring begrijpen.

## Klantprofiel in realtime

Klantprofiel in real-time is een algemene opzoekeenheid die gegevens uit verschillende bedrijfsgegevenselementen samenvoegt en vervolgens toegang tot die gegevens biedt in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden.

### Profielgegevensopslag

Hoewel in real time het Profiel van de Klant ingebedde gegevens verwerkt en de Dienst van de Identiteit van het Platform van de Ervaring van Adobe gebruikt om verwante gegevens door identiteitstoewijzing samen te voegen, handhaaft het zijn eigen gegevens in de opslag van het Profiel. Met andere woorden, de opslag van het Profiel is gescheiden van de gegevens van de Catalogus (Gegevens meer) en van de Dienst van de Identiteit (identiteitsgrafiek).

### Profiel- en platformservices

De verhouding tussen het Profiel van de Klant in real time en andere diensten binnen het Platform van de Ervaring wordt benadrukt in het volgende diagram:

![De relatie tussen Profiel en andere diensten van het Platform van de Ervaring.](images/profile-overview/profile-in-platform.png)

### Profielen en gegevens opnemen

Een profiel is een weergave van een onderwerp, een organisatie of een individu, ook wel recordgegevens genoemd. Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. Met het Experience Platform kunt u profielen aanpassen voor het gebruik van gegevenstypen die relevant zijn voor uw bedrijf. De standaard klasse van het Profiel van de Gegevens van de Ervaring Model (XDM) Individuele is de aangewezen klasse waarop om een schema te bouwen wanneer het beschrijven van gegevens van het klantenverslag, en verstrekt de gegevensintegraal aan vele interactie tussen de diensten van het Platform. Voor meer informatie over het werken met schema&#39;s in het Platform van de Ervaring, gelieve te beginnen door het [XDM systeemoverzicht](../xdm/home.md)te lezen.

### Gebeurtenissen van tijdreeksen

De gegevens van de tijdreeksen verstrekken een momentopname van het systeem op het tijdstip dat een actie of direct of indirect door een onderwerp werd genomen, evenals gegevens detailleert de gebeurtenis zelf. Deze tijdreeksgegevens worden vertegenwoordigd door de XDM ExperienceEvent-standaardschemaklasse en kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. Gegevens uit tijdreeksen kunnen worden gebruikt om segmentatieregels te baseren op, en gebeurtenissen kunnen individueel worden benaderd in de context van een profiel.

### Identiteiten

Elk bedrijf wil met zijn klanten op een manier communiceren die zich persoonlijk voelt. Een van de uitdagingen bij het aanbieden van relevante digitale ervaringen aan klanten is echter het begrijpen van hoe ze hun losgekoppelde gegevens aan elkaar kunnen koppelen. Deze gegevens worden vaak verspreid over verschillende digitale kanalen, zoals tablets, mobiele telefoons en laptops. Met de identiteitsservice kunt u het volledige beeld van uw klant samenvoegen door identiteiten van meerdere kanalen te koppelen, een identiteitsgrafiek voor elke klant te maken, zodat u deze beter kunt begrijpen. Ga naar het overzicht [van de](../identity-service/home.md) identiteitsservice voor meer informatie.

### Segmentering

De Adobe Experience Platform Segmentation Service geeft het publiek dat nodig is om ervaringen voor uw individuele klanten in te schakelen. Wanneer een publiekssegment wordt gecreeerd, wordt identiteitskaart van dat segment toegevoegd aan de lijst van segmentlidmaatschap voor alle kwalificerende profielen. De regels van het segment worden gebouwd en toegepast op de gegevens van het Profiel van de Klant in real time gebruikend RESTful APIs en de gebruikersinterface van de Bouwer van het Segment. Om meer over segmentatie te leren, gelieve te beginnen door het overzicht [van de Dienst van de](../segmentation/home.md)Segmentatie te lezen.

### Profielfragmenten en samenvoegingsschema&#39;s {#profile-fragments-and-union-schemas}

Een van de belangrijkste kenmerken van Real-Time Customer Profile is de mogelijkheid om gegevens met meerdere kanalen te verenigen. Wanneer het Profiel van de Klant in real time wordt gebruikt om tot een entiteit toegang te hebben, kan het u van een samengevoegde mening van alle profielfragmenten voor die entiteit over datasets voorzien, die als verenigingsmening wordt bedoeld en die door wat als verenigingsschema wordt genoemd mogelijk gemaakt. In real time gegevens van het Profiel van de Klant worden samengevoegd over bronnen wanneer een entiteit of een profiel door zijn identiteitskaart wordt betreden of als segment wordt uitgevoerd. Meer informatie over de toegang tot van profielen en verenigingsmeningen, bezoek de in real time de ontwikkelaar van het Profiel van de Klant API subgids op [Entiteiten, die ook als &quot;Toegang van het Profiel&quot;](api/entities.md)wordt bekend.

### Beleid samenvoegen

Wanneer het samenbrengen van gegevens uit veelvoudige bronnen en het combineren om een volledige mening van elk van uw individuele klanten te zien, is het fusiebeleid de regels die het Platform gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gecombineerd om die verenigde mening tot stand te brengen. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Voor meer informatie bij het werken met samenvoegbeleid gebruikend APIs, te zien gelieve de in real time [fusie beleidsondergids](api/merge-policies.md) van het Profiel van de Klant of de gebruikersgids [van het](ui/merge-policies.md) fusiebeleid voor hoe te met fusiebeleid gebruikend de UI van het Platform werken.

## (Alfa) Berekende kenmerken configureren

>[!IMPORTANT]
>De berekende kenmerkfunctionaliteit die in dit document wordt beschreven is in alpha. De documentatie en de functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen. Elk berekend kenmerk bevat een expressie, of &#39;regel&#39;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Zie de [subhandleiding Real-time Customer Profile API over berekende kenmerken](api/computed-attributes.md)voor meer informatie over berekende kenmerken en stapsgewijze instructies voor het werken met deze kenmerken. Deze handleiding geeft u een beter inzicht in de rol die berekende kenmerken spelen in het Adobe Experience Platform en bevat voorbeelden van API-aanroepen voor het uitvoeren van standaard CRUD-bewerkingen met behulp van de Real-time Customer Profile API.

## Realtime componenten

Deze sectie introduceert de componenten die het Profiel van de Klant in real time toestaan om verslag en tijdreeksgegevens in real time bij te werken en te controleren.

### Streaming opname en streamingsegmentatie

Invoer in realtime wordt mogelijk gemaakt via een proces dat streaming opname wordt genoemd. Aangezien profiel en tijdreeksgegevens worden opgenomen, beslist het Profiel van de Klant in real time automatisch om die gegevens van segmenten door een aan de gang zijnde proces te omvatten of uit te sluiten die het stromen segmentatie wordt genoemd, alvorens het met bestaande gegevens samen te voegen en de verenigingsmening bij te werken. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan. Terwijl het worden opgenomen, ondergaat de gegevens ook bevestiging om ervoor te zorgen het behoorlijk wordt opgenomen en conform het schema is waarop de dataset gebaseerd is. Voor meer informatie over welke bevestiging tijdens opname wordt gedaan, gelieve te beginnen door het kwaliteitsoverzicht [van](../ingestion/quality/overview.md)gegevensinvoer te lezen.

### Edge-prognoses

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Met het Adobe Experience Platform hebt u in real-time toegang tot gegevens via zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. Adobe-toepassingen zoals Adobe Target en Adobe Campaign maken bijvoorbeeld gebruik van randen om klanten in real-time persoonlijke ervaringen te bieden. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Raadpleeg de subhandleiding voor [Edge Projections in real-time profiel-API van de klant voor Edge-projecties voor meer informatie en om te gaan werken met randen en projecties](api/edge-projections.md).

## Gegevens toevoegen aan realtime klantprofiel

Het platform kan worden gevormd om uw verslag en tijdreeksgegevens naar Profiel te verzenden, ondersteunend het stromen in real time en partij ingestie. Voor meer informatie, zie de zelfstudie die schetst hoe te om gegevens aan het Profiel [van de Klant in real time](tutorials/add-profile-data.md)toe te voegen.

>[!Nofferte]
>De gegevens die via Adobe-oplossingen zijn verzameld, waaronder Analytics Cloud, Marketing Cloud en Advertising Cloud, lopen over op het Experience Platform en worden opgenomen in Profile.

### Metrische gegevens voor het streamen van profielen

Met Observability Insights kunt u belangrijke metriek in het Adobe Experience Platform beschikbaar maken. Naast het gebruiksstatistieken van het Platform en prestatiesindicatoren voor diverse functies van het Platform, zijn er specifieke op Profiel betrekking hebbende metriek die u toestaan om inzicht in inkomende verzoektarieven, succesvolle innametarieven, ingebedde verslaggrootte, en meer te krijgen. Meer leren, begin door het overzicht [van de Inzichten van de](../observability/home.md)Waarnemelijkheid te lezen, en voor een volledige lijst van de metriek van het Profiel, zie de documentatie over [beschikbare metriek](../observability/metrics.md).

## Beheer van gegevens en privacy

Het beheer van gegevens is een reeks strategieën en technologieën die worden gebruikt om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren van toepassing op gegevensgebruik.

Met betrekking tot de toegang tot gegevens speelt gegevensbeheer een sleutelrol binnen het ervaringsplatform op verschillende niveaus:
* Labels voor gegevensgebruik
* Beleid voor gegevenstoegang
* Toegangscontrole van gegevens voor marketingacties

Het gegevensbeheer wordt op verschillende punten beheerd. Deze omvatten het bepalen van welke gegevens in Platform worden opgenomen en welke gegevens na inname voor een bepaalde marketingactie toegankelijk zijn. Voor meer informatie, begin door het overzicht [van het](../data-governance/home.md)gegevensbeheer te lezen.

### Verzoeken om opt-out en privacy van gegevens verwerken

Met het Experience Platform kunnen uw klanten weigeren-aanvragen met betrekking tot het gebruik en de opslag van hun gegevens verzenden binnen het Real-time Klantprofiel. Raadpleeg de documentatie over het [naleven van opt-out-verzoeken](../segmentation/honoring-opt-outs.md)voor meer informatie over de manier waarop aanvragen vooropt-out worden afgehandeld.

## Volgende stappen en extra bronnen

Als u meer wilt weten over Real-time klantprofiel, blijft u de documentatie lezen die in deze handleiding wordt geleverd en kunt u uw kennis aanvullen met de onderstaande video of andere videozelfstudies [van het](https://docs.adobe.com/content/help/en/platform-learn/tutorials/overview.html)Experience Platform bekijken.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)