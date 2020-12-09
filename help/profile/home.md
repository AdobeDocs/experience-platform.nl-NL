---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API;unified profile;Unified Profile;unified;Profile;rtcp;XDM graphs
title: Overzicht van het realtime klantprofiel
topic: guide
description: Klantprofiel in real-time is een algemene opzoekeenheid die gegevens uit verschillende bedrijfsgegevenselementen samenvoegt en vervolgens toegang tot die gegevens biedt in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden.
translation-type: tm+mt
source-git-commit: b8d6bd5caf6c6f4d1da218b6ca12cec154d64412
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] - overzicht

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-time Customer Profile], kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt. Dit overzicht zal u helpen de rol en het gebruik van [!DNL Real-time Customer Profile] in begrijpen [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

De verhouding tussen het Profiel van de Klant in real time en andere diensten binnen Experience Platform wordt benadrukt in het volgende diagram:

![Adobe Experience Platform-services.](images/profile-overview/profile-in-platform.png)

### Profielgegevensopslag

Hoewel [!DNL Real-time Customer Profile] ingesloten gegevens verwerkt en Adobe Experience Platform gebruikt [!DNL Identity Service] om verwante gegevens samen te voegen via identiteitstoewijzing, blijven de gegevens in de [!DNL Profile] opslag behouden. De [!DNL Profile] opslagruimte is gescheiden van de [!DNL Catalog] gegevens in de identiteitsgrafiek [!DNL Data Lake] en de [!DNL Identity Service] gegevens in de identiteitsgrafiek.

De profielopslag gebruikt een Microsoft Azure Cosmos DB-infrastructuur en het Platform Data Lake gebruikt de opslag van Microsoft Azure Data Lake.

### Profielhulplijnen

Experience Platform biedt een reeks instructies om u te helpen het maken van XDM-schema&#39;s ( [Experience Data Model) te voorkomen](../xdm/home.md) die niet kunnen worden ondersteund door het Real-Time Customer Profile. Dit omvat zachte grenzen die in prestatiesdegradatie zullen resulteren, evenals harde grenzen die in fouten en systeembreuken zullen resulteren. Lees voor meer informatie, zoals een lijst met richtlijnen en voorbeelden van gevallen van gebruik, de documentatie bij [Profielhulplijnen](guardrails.md) .

## Werken met profielen

[!DNL Real-time Customer Profile] voegt gegevens van verschillende bedrijfssystemen samen en verleent dan toegang tot die gegevens in de vorm van klantenprofielen met verwante gebeurtenissen van de tijdreeksen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden. In de volgende secties worden enkele kernconcepten beschreven die u moet begrijpen om profielen op effectieve wijze te kunnen maken en onderhouden binnen het Platform.

### Profielfragmenten versus samengevoegde profielen {#profile-fragments-vs-merged-profiles}

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Wanneer de gegevens uit veelvoudige bronnen conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl andere de klant als &quot;gehuwd&quot;opsomt) bepaalt het [fusiebeleid](#merge-policies) welke informatie om aan voorrang te geven en in het profiel voor het individu te omvatten. Daarom is het totale aantal profielfragmenten in Platform waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel uit meerdere fragmenten bestaat.

### Gegevens opnemen

Een profiel is een weergave van een onderwerp, een organisatie of een individu, dat uit vele kenmerken bestaat (ook wel recordgegevens genoemd). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. Met behulp [!DNL Experience Platform]van profielen kunt u profielen aanpassen voor het gebruik van specifieke gegevens die relevant zijn voor uw bedrijf. De standaard [!DNL Experience Data Model] (XDM) klasse, [!DNL XDM Individual Profile], is de aangewezen klasse waarop om een schema te bouwen wanneer het beschrijven van de gegevens van het klantenverslag, en levert de gegevensintegraal aan vele interactie tussen de diensten van het Platform. Voor meer informatie over het werken met schema&#39;s in [!DNL Experience Platform], gelieve te beginnen door het [XDM systeemoverzicht](../xdm/home.md)te lezen.

### Gebeurtenissen van tijdreeksen

De gegevens van de tijdreeksen verstrekken een momentopname van het systeem op het tijdstip dat een actie of direct of indirect door een onderwerp werd genomen, evenals gegevens detailleert de gebeurtenis zelf. Deze tijdreeksgegevens worden vertegenwoordigd door de XDM ExperienceEvent-standaardschemaklasse en kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. Gegevens uit tijdreeksen kunnen worden gebruikt om segmentatieregels te baseren op, en gebeurtenissen kunnen individueel worden benaderd in de context van een profiel.

### Identiteiten

Elk bedrijf wil met zijn klanten op een manier communiceren die zich persoonlijk voelt. Een van de uitdagingen bij het aanbieden van relevante digitale ervaringen aan klanten is echter het begrijpen van hoe ze hun losgekoppelde gegevens aan elkaar kunnen koppelen. Deze gegevens worden vaak verspreid over verschillende digitale kanalen, zoals tablets, mobiele telefoons en laptops. [!DNL Identity Service] kunt u het volledige beeld van uw klant samenvoegen door identiteiten van veelvoudige kanalen te verbinden en een identiteitsgrafiek voor elke klant te creëren. Ga naar het overzicht [van de](../identity-service/home.md) identiteitsservice voor meer informatie.

### Beleid samenvoegen

Wanneer het brengen van gegevensfragmenten uit veelvoudige bronnen en het combineren van hen om een volledige mening van elk van uw individuele klanten te zien, zijn het fusieprincipe de regels die [!DNL Platform] gebruiken om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gebruikt om het klantenprofiel tot stand te brengen. Wanneer er conflicterende gegevens van veelvoudige datasets zijn, zal het fusiebeleid bepalen hoe die gegevens moeten worden behandeld en welke waarde zou moeten worden gebruikt. Gebruikend RESTful APIs of het gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen. Voor meer informatie bij het werken met fusiebeleid gebruikend [!DNL Real-time Customer Profile] API, te zien gelieve de het eindpuntgids [van het](api/merge-policies.md)fusiebeleid. Om met samenvoegbeleid te werken gebruikend [!DNL Experience Platform] UI, verwijs naar de de gebruikersgids [van het](ui/merge-policies.md)fusiebeleid.

### Unieregelingen {#profile-fragments-and-union-schemas}

Een van de belangrijkste kenmerken van [!DNL Real-time Customer Profile] deze gegevens is de mogelijkheid om gegevens met meerdere kanalen te verenigen. Wanneer [!DNL Real-time Customer Profile] wordt gebruikt om tot een entiteit toegang te hebben, kan het u van een samengevoegde mening van alle profielfragmenten voor die entiteit over datasets voorzien, die als verenigingsmening wordt bedoeld en door wat als verenigingsschema wordt bekend mogelijk gemaakt. [!DNL Real-time Customer Profile] gegevens worden samengevoegd tussen verschillende bronnen wanneer een entiteit of profiel wordt benaderd door de id of als segment wordt geëxporteerd. Ga voor meer informatie over het benaderen van profielen en samenvoegweergaven met de [!DNL Real-time Customer Profile] API naar de [eindgebruikershandleiding](api/entities.md)voor entiteiten.

### Segmentatie

Adobe Experience Platform [!DNL Segmentation Service] produceert het publiek dat nodig is om uw individuele klanten van energie te voorzien. Wanneer een publiekssegment wordt gecreeerd, wordt identiteitskaart van dat segment toegevoegd aan de lijst van segmentlidmaatschap voor alle kwalificerende profielen. De regels van het segment worden gebouwd en toegepast op [!DNL Real-time Customer Profile] gegevens gebruikend RESTful APIs en het gebruikersinterface van de Bouwer van het Segment. Om meer over segmentatie te leren, gelieve te beginnen door het overzicht [van de Dienst van de](../segmentation/home.md)Segmentatie te lezen.

### (Alfa) Berekende kenmerken configureren

>[!IMPORTANT]
>
>De berekende kenmerkfunctionaliteit staat in alpha. De documentatie en de functionaliteit kunnen worden gewijzigd.

Met de berekende kenmerken kunt u automatisch de waarde van velden berekenen op basis van andere waarden, berekeningen en expressies. De berekende attributen werken op het profielniveau, betekenend kunt u waarden over alle verslagen en gebeurtenissen bijeenvoegen. Elk berekend kenmerk bevat een expressie, of &#39;regel&#39;, die binnenkomende gegevens evalueert en de resulterende waarde opslaat in een profielkenmerk of in een gebeurtenis. Met deze berekeningen kunt u eenvoudig vragen beantwoorden die betrekking hebben op de waarde van levenslange aankopen, de tijd tussen aankopen of het aantal geopende toepassingen, zonder dat u telkens wanneer de informatie nodig is, handmatig complexe berekeningen hoeft uit te voeren. Voor meer informatie over gegevens verwerkte attributen, en geleidelijke instructies voor het werken met hen die API gebruiken, gelieve de [!DNL Real-time Customer Profile] gegevens verwerkte gids [](api/computed-attributes.md)van het attributeneindpunt te zien. Deze handleiding geeft u een beter inzicht in de rol die berekende kenmerken spelen in Adobe Experience Platform en bevat voorbeelden van API-aanroepen voor het uitvoeren van standaard CRUD-bewerkingen.

## Realtime componenten

Deze sectie introduceert de componenten die toestaan [!DNL Real-time Customer Profile] om verslag en tijdreeksgegevens in real time bij te werken en te controleren.

### Streaming opname en streamingsegmentatie

Invoer in realtime wordt mogelijk gemaakt via een proces dat streaming opname wordt genoemd. Aangezien profiel en tijdreeksgegevens worden opgenomen, besluit [!DNL Real-time Customer Profile] automatisch om die gegevens van segmenten door een aan de gang zijnde proces te omvatten of uit te sluiten genoemd het stromen segmentatie, alvorens het met bestaande gegevens samen te voegen en de verenigingsmening bij te werken. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan. Terwijl het worden opgenomen, ondergaat de gegevens ook bevestiging om ervoor te zorgen het behoorlijk wordt opgenomen en conform het schema is waarop de dataset gebaseerd is. Voor meer informatie over welke bevestiging tijdens opname wordt gedaan, gelieve te beginnen door het kwaliteitsoverzicht [van](../ingestion/quality/overview.md)gegevensinvoer te lezen.

### Edge-projectieconfiguraties en -doelen

Om gecoördineerde, verenigbare, en gepersonaliseerde ervaringen voor uw klanten over veelvoudige kanalen in real time te drijven, moeten de juiste gegevens gemakkelijk beschikbaar en onophoudelijk bijgewerkt zijn aangezien de veranderingen gebeuren. Adobe Experience Platform biedt realtime toegang tot gegevens via het gebruik van zogenaamde randen. Een rand is een geografisch geplaatste server die gegevens opslaat en deze gemakkelijk toegankelijk maakt voor toepassingen. Bijvoorbeeld, gebruiken de toepassingen van de Adobe zoals Adobe Target en Adobe Campaign randen om gepersonaliseerde klantenervaringen in real time te verstrekken. De gegevens worden verpletterd aan een rand door een projectie, met een projectiebestemming die de rand bepaalt waarnaar de gegevens zullen worden verzonden, en een projectieconfiguratie die de specifieke informatie bepaalt die op de rand beschikbaar zal worden gemaakt. Raadpleeg de handleiding voor de eindpunten van de [!DNL Real-time Customer Profile] randprojectie voor meer informatie en voor meer informatie over het werken met projecties met de [](api/edge-projections.md)API.

## Gegevens verzamelen in [!DNL Profile]

[!DNL Platform] kan worden gevormd om verslag en tijdreeksgegevens naar te verzenden [!DNL Profile], ondersteunend het stromen in real time en partijingestie. Voor meer informatie, zie de zelfstudie die schetst hoe te om gegevens aan het Profiel [van de Klant in real time](tutorials/add-profile-data.md)toe te voegen.

>[!NOTE]
>
>Gegevens die worden verzameld via Adobe-oplossingen, waaronder [!DNL Analytics Cloud], [!DNL Marketing Cloud]en [!DNL Advertising Cloud], stromen naar [!DNL Experience Platform] en worden opgenomen in [!DNL Profile].

### [!DNL Profile] metriek

Met observability Insights kunt u belangrijke metriek in Adobe Experience Platform onthullen. Naast [!DNL Platform] gebruiksstatistieken en prestatie-indicatoren voor diverse [!DNL Platform] functies, zijn er specifieke [!DNL Profile]verwante metriek die u toestaan om inzicht in inkomende verzoektarieven, succesvolle innamepercentages, ingebedde verslaggrootte, en meer te krijgen. Voor meer informatie, begin door het overzicht [van](../observability/api/overview.md)Observability Insights API te lezen, en voor een volledige lijst van [!DNL Profile] metriek, zie de documentatie over [beschikbare metriek](../observability/api/metrics.md#available-metrics).

## [!DNL Data governance] en [!DNL Privacy]

[!DNL Data governance] is een reeks strategieën en technologieën die worden gebruikt om klantengegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren van toepassing op gegevensgebruik.

Met betrekking tot de toegang tot gegevens speelt gegevensbeheer een sleutelrol binnen [!DNL Experience Platform] verschillende niveaus:
* Labels voor gegevensgebruik
* Beleid voor gegevenstoegang
* Toegangscontrole van gegevens voor marketingacties

[!DNL Data governance] wordt op verschillende punten beheerd. Deze omvatten het bepalen van welke gegevens worden opgenomen in [!DNL Platform] en welke gegevens toegankelijk zijn na inname voor een bepaalde marketingactie. Voor meer informatie, begin door het overzicht [van het](../data-governance/home.md)gegevensbeheer te lezen.

### Verzoeken om opt-out en privacy van gegevens verwerken

[!DNL Experience Platform] biedt uw klanten de mogelijkheid om weigeren-aanvragen te verzenden met betrekking tot het gebruik en de opslag van hun gegevens binnen [!DNL Real-time Customer Profile]. Raadpleeg de documentatie over het [naleven van opt-out-verzoeken](../segmentation/honoring-opt-outs.md)voor meer informatie over de manier waarop aanvragen vooropt-out worden afgehandeld.

## Volgende stappen en extra bronnen

Lees voor meer informatie over het werken met [!DNL Real-time Customer Profile]de handleiding voor [de gebruikersinterface van het](ui/user-guide.md) profiel of de handleiding voor [API-ontwikkelaars](api/overview.md).

>[!WARNING]
>
>De gebruikersinterface van het Experience Platform wordt vaak bijgewerkt en kan sinds de opname van deze video zijn veranderd. Raadpleeg de gebruikershandleiding [van het profiel van de](ui/user-guide.md) real-time klant voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/27251?quality=12)