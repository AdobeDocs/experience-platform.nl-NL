---
title: Real-Time overzicht van klantprofiel
description: In real-time klantprofiel worden gegevens uit verschillende bronnen samengevoegd en krijgt toegang tot die gegevens in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: fc53d1b32eb3fc0251f307d5b2f076b1153a2931
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile]-overzicht

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met [!DNL Real-Time Customer Profile], kunt u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. Met [!DNL Profile] kunt u uw klantgegevens consolideren in een uniforme weergave die een actief, tijdstempelaccount voor elke interactie van de klant biedt. Dit overzicht geeft inzicht in de rol en het gebruik van [!DNL Real-Time Customer Profile] in [!DNL Experience Platform] .

## [!DNL Profile] in Experience Platform

Het verband tussen het Real-Time Profiel van de Klant en andere diensten binnen Experience Platform wordt benadrukt in het volgende diagram:

![ het verband tussen het Profiel van de Klant in real time en andere diensten in Adobe Experience Platform. Dit diagram toont aan dat het Profiel één van de kerncomponenten van Adobe Experience Platform is.](images/profile-overview/profile-in-platform.png)

## Werken met profielen

[!DNL Real-Time Customer Profile] voegt gegevens van diverse bedrijfssystemen samen en biedt vervolgens toegang tot die gegevens in de vorm van klantprofielen met gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden. De volgende secties benadrukken enkele kernconcepten die u moet begrijpen om profielen binnen Platform effectief te bouwen en te handhaven.

### Samenstelling van profielentiteit

Een profiel van de Klant in real time is samengesteld uit een belangrijkste entiteit, genoemd de **primaire entiteit**, en diverse ondersteunende entiteiten. In de context van Experience Platform, is de primaire entiteit typisch a **profielentiteit**, die uit eigenschappen, gedrag, en publiekslidmaatschappen van een individuele persoon bestaat. Andere entiteiten staan de segmenteringsmotor toe om gegevens buiten de primaire entiteit van het profiel te gebruiken, en omvatten het volgende:

- **Dimensionele entiteit**: De entiteit die wordt gebruikt om het gegevens modelleringsproces voor informatie te vereenvoudigen die over gebeurtenissen of profielverslagen wordt gedeeld. Dit wordt ook wel de opgezochte entiteit of classificatieentiteit genoemd.
- **B2B entiteit**: Entiteiten die de verhouding van het profiel met zaken-aan-zaken rekeningen en kansen beschrijven.

![ een diagram dat de samenstelling van de profielentiteit verklaart.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Aangezien dimensionale en B2B-entiteiten alleen buiten de primaire entiteit bestaan, worden deze alleen gebruikt voor batchsegmentatie.

De entiteiten van de dimensie en B2B zijn verbonden aan de primaire entiteit door **schemaverhoudingen**. Raadpleeg de volgende documentatie voor meer informatie:

- [Creeer een één-op-één schemaverhouding voor raadplegingsentiteiten](../xdm/tutorials/relationship-ui.md)
- [Creeer een vele-aan-één schemaverhouding voor B2B-entiteiten](../xdm/tutorials/relationship-b2b.md)

### Profielgegevensopslag

Hoewel [!DNL Real-Time Customer Profile] ingesloten gegevens verwerkt en Adobe Experience Platform [!DNL Identity Service] gebruikt om verwante gegevens samen te voegen via identiteitstoewijzing, blijven de eigen gegevens behouden in de gegevensopslag van [!DNL Profile] . De opslag van [!DNL Profile] is gescheiden van catalogusgegevens in het datumpomeer en [!DNL Identity Service] -gegevens in het identiteitsdiagram.

De profielopslag gebruikt een Microsoft Azure Cosmos DB-infrastructuur en het Platform Data Lake gebruikt Microsoft Azure Data Lake-opslag.

### Profielhulplijnen

Experience Platform verstrekt een reeks gidsen om u te helpen vermijden creërend [ schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) ](../xdm/home.md) die het Profiel van de Klant in real time niet kan steunen. Dit omvat zachte grenzen die in prestatiesvermindering zullen resulteren, evenals harde grenzen die in fouten en systeembreuken zullen resulteren. Voor meer informatie, met inbegrip van een lijst van richtlijnen en de gevallen van het voorbeeldgebruik, gelieve te lezen de [ guardrails van het Profiel ](guardrails.md) documentatie.

### Profieldashboard {#profile-dashboard}

De gebruikersinterface van Experience Platform biedt een dashboard waarmee u belangrijke informatie over uw gegevens van het profiel van de Klant in real time kunt bekijken, zoals vastgelegd tijdens een dagelijkse momentopname. Leren hoe te om met het [!DNL Profile] dashboard in UI toegang te hebben en te werken, en gedetailleerde informatie betreffende de metriek die in het dashboard wordt getoond, verwijs naar de [ gids UI van het dashboard van het Profiel ](ui/profile-dashboard.md).

### Profielfragmenten versus samengevoegde profielen {#profile-fragments-vs-merged-profiles}

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Met andere woorden, vertegenwoordigen de profielfragmenten een unieke primaire identiteit en het overeenkomstige [ verslag ](#record-data) of [ gebeurtenis ](#time-series-events) gegevens voor die identiteitskaart binnen een bepaalde dataset.

Wanneer de gegevens van veelvoudige datasets conflicten (bijvoorbeeld één fragment maakt een lijst van de klant als &quot;enig&quot;terwijl andere van de klant als &quot;gehuwd&quot;een lijst maakt) bepaalt het [ fusiebeleid ](#merge-policies) welke informatie om in het profiel voor het individu voorrang te geven en te omvatten. Daarom is het totale aantal profielfragmenten binnen Platform waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel typisch uit veelvoudige fragmenten van veelvoudige datasets bestaat.

### Gegevens opnemen {#record-data}

Een profiel is een weergave van een onderwerp, een organisatie of een individu, dat uit vele kenmerken bestaat (ook wel recordgegevens genoemd). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. Met [!DNL Experience Platform] kunt u profielen aanpassen voor het gebruik van specifieke gegevens die relevant zijn voor uw bedrijf. De standaard [!DNL Experience Data Model] (XDM) klasse, [!DNL XDM Individual Profile], is de aangewezen klasse waarop om een schema te bouwen wanneer het beschrijven van de gegevens van het klantenverslag, en levert de gegevensintegraal aan vele interactie tussen de diensten van het Platform. Voor meer informatie bij het werken met schema&#39;s in [!DNL Experience Platform], gelieve te beginnen door het [ XDM overzicht van het Systeem te lezen ](../xdm/home.md).

### Gebeurtenissen van tijdreeksen {#time-series-events}

De gegevens van de tijdreeksen verstrekken een momentopname van het systeem op het tijdstip dat een actie of direct of indirect door een onderwerp werd genomen, evenals gegevens detailleert de gebeurtenis zelf. Deze tijdreeksgegevens worden vertegenwoordigd door de XDM ExperienceEvent-standaardschemaklasse en kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. Gegevens uit tijdreeksen kunnen worden gebruikt om segmentatieregels te baseren op, en gebeurtenissen kunnen individueel worden benaderd in de context van een profiel.

### Identiteiten

Elk bedrijf wil met zijn klanten op een manier communiceren die zich persoonlijk voelt. Een van de uitdagingen bij het aanbieden van relevante digitale ervaringen aan klanten is echter het begrijpen van hoe ze hun losgekoppelde gegevens aan elkaar kunnen koppelen. Deze gegevens worden vaak verspreid over verschillende digitale kanalen, zoals tablets, mobiele telefoons en laptops. Met [!DNL Identity Service] kunt u het volledige beeld van uw klant samenvoegen door identiteiten van meerdere kanalen te koppelen en een identiteitsgrafiek voor elke klant te maken. Bezoek het [ overzicht van de Dienst van de Identiteit ](../identity-service/home.md) voor meer informatie.

### Beleid samenvoegen

Wanneer het brengen van gegevensfragmenten uit veelvoudige bronnen en het combineren van hen om een volledige mening van elk van uw individuele klanten te zien, zijn het fusiebeleid de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens aan voorrang zullen worden gegeven en welke gegevens zullen worden gebruikt om het klantenprofiel tot stand te brengen.

Wanneer er conflicterende gegevens van veelvoudige datasets zijn, bepaalt het fusiebeleid hoe die gegevens moeten worden behandeld en welke waarde zou moeten worden gebruikt. Via RESTful APIs of de gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen.

Om meer over fusiebeleid en hun rol binnen Experience Platform te leren, gelieve te beginnen door het [ overzicht van het fusiebeleid ](merge-policies/overview.md) te lezen.

### Unieregelingen {#profile-fragments-and-union-schemas}

Een van de belangrijkste functies van [!DNL Real-Time Customer Profile] is de mogelijkheid om multikanaalgegevens te verenigen. Wanneer [!DNL Real-Time Customer Profile] wordt gebruikt om tot een entiteit toegang te hebben, kan het u van een samengevoegde mening van alle profielfragmenten voor die entiteit over datasets voorzien, die als &quot;verenigingsmening&quot;wordt bedoeld en mogelijk gemaakt door wat als verenigingsschema wordt bekend.

Meer over verenigingsschema&#39;s leren, met inbegrip van hoe te om tot verenigingsschema&#39;s in UI toegang te hebben, bezoek de [ gids UI van het unieschema ](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profielen en doelgroepen

Adobe Experience Platform [!DNL Segmentation Service] geeft het publiek dat nodig is om uw individuele klanten van energie te voorzien. Wanneer een publiek wordt gecreeerd, wordt identiteitskaart van dat publiek toegevoegd aan de lijst van publiekslidmaatschappen voor alle kwalificerende profielen. De regels van het segment worden gebouwd en toegepast op [!DNL Real-Time Customer Profile] gegevens gebruikend RESTful APIs en de gebruikersinterface van de Bouwer van het Segment. Meer over segmentatie leren, gelieve te beginnen door het [ overzicht van de Dienst van de Segmentatie ](../segmentation/home.md) te lezen.

### Streaming opname en streamingsegmentatie

Invoer in realtime wordt mogelijk gemaakt via een proces dat streaming opname wordt genoemd. Wanneer gegevens uit profiel- en tijdreeksen worden ingesloten, besluit [!DNL Real-Time Customer Profile] automatisch om die gegevens van het publiek op te nemen of uit te sluiten via een doorlopend proces dat streaming segmentatie wordt genoemd, voordat het wordt samengevoegd met bestaande gegevens en de weergave Vereniging wordt bijgewerkt. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan. Terwijl het worden opgenomen, ondergaat de gegevens ook bevestiging om ervoor te zorgen het behoorlijk wordt opgenomen en conform het schema is waarop de dataset gebaseerd is. Voor meer informatie over welke bevestiging tijdens opname wordt gedaan, gelieve te beginnen door het [ overzicht van de gegevensopname van kwaliteit ](../ingestion/quality/overview.md) te lezen.

## Gegevens invoegen in [!DNL Profile]

[!DNL Platform] kan worden geconfigureerd om record- en tijdreeksgegevens naar [!DNL Profile] te verzenden, ter ondersteuning van streaming opname in realtime en batch-opname. Voor meer informatie, zie het leerprogramma schetterend hoe te [ gegevens aan het Profiel van de Klant in real time ](tutorials/add-profile-data.md) toevoegen.

>[!NOTE]
>
>Gegevens die met Adobe-oplossingen zijn verzameld, zoals [!DNL Analytics Cloud] , [!DNL Marketing Cloud] en [!DNL Advertising Cloud] , lopen door in [!DNL Experience Platform] en worden opgenomen in [!DNL Profile] .

### Metrische gegevens voor het opnemen van profielen

Met waarnemingsinformatie kunt u belangrijke metriek in Adobe Experience Platform onthullen. Naast [!DNL Experience Platform] gebruiksstatistieken en prestatie-indicatoren voor diverse [!DNL Platform] functies, zijn er specifieke aan profielen gerelateerde metriek waarmee u inzicht kunt krijgen in inkomende aanvraagfrequenties, geslaagde inname, ingesloten recordgrootten en meer. Om meer te leren, begin door het [ overzicht van de Inzichten API van de Waarneming ](../observability/api/overview.md) te lezen, en voor een volledige lijst van metriek van het Profiel van de Klant in real time, zie de documentatie over [ beschikbare metriek ](../observability/api/metrics.md#available-metrics).

## Gegevens in profielarchief bijwerken

Soms kan het nodig zijn gegevens bij te werken in het profielarchief van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Dit kan door partijopname worden gedaan en vereist een profiel-Toegelaten dataset die met een upsert markering wordt gevormd. Voor meer informatie over hoe te om een dataset voor attributenupdates te vormen, gelieve te verwijzen naar het leerprogramma voor [ toelatend een dataset voor Profiel en op te nemen ](../catalog/datasets/enable-upsert.md).

## Gegevensbeheer en [!DNL Privacy]

Gegevensbeheer is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren die op gegevensgebruik van toepassing zijn.

Met betrekking tot de toegang tot gegevens speelt gegevensbeheer een sleutelrol binnen [!DNL Experience Platform] op verschillende niveaus:

- Labels voor gegevensgebruik
- Beleid voor gegevenstoegang
- Toegangscontrole van gegevens voor marketingacties

Gegevensbeheer wordt op verschillende punten beheerd. Deze omvatten het bepalen van welke gegevens in [!DNL Platform] worden opgenomen en welke gegevens toegankelijk zijn na inname voor een bepaalde marketingactie. Voor meer informatie, begin door het [ overzicht van het gegevensbeheer ](../data-governance/home.md) te lezen.

### Verzoeken om opt-out en privacy van gegevens afhandelen

Met [!DNL Experience Platform] kunnen uw klanten aanvragen voor een opt-out verzenden voor het gebruik en de opslag van hun gegevens binnen [!DNL Real-Time Customer Profile] . Voor meer informatie over hoe opt-out verzoeken worden behandeld, gelieve de documentatie over [ het behandelen van opt-out verzoeken ](../segmentation/tutorials/consents.md).

## Volgende stappen en extra bronnen

Om meer over het werken met de gegevens van het Profiel van de Klant in real time te leren gebruikend Experience Platform UI of het Profiel API, gelieve te beginnen door de [ gids van het Profiel UI ](ui/user-guide.md) of [ API ontwikkelaarsgids ](api/overview.md) te lezen, respectievelijk.
