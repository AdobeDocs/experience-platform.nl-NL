---
title: Real-Time overzicht van klantprofiel
description: In real-time klantprofiel worden gegevens uit verschillende bronnen samengevoegd en krijgt toegang tot die gegevens in de vorm van individuele klantprofielen en gerelateerde tijdreeksgebeurtenissen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden.
exl-id: c93d8d78-b215-4559-a806-f019c602c4d2
source-git-commit: dde38e230a6bcb10cd38a12f644f2dd03f0cebaf
workflow-type: tm+mt
source-wordcount: '1821'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile]-overzicht

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-Time Customer Profile], kunt u een holistische mening van elke individuele klant zien door gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derde te combineren. [!DNL Profile] staat u toe om uw klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt. Dit overzicht helpt u de rol en het gebruik van [!DNL Real-Time Customer Profile] in [!DNL Experience Platform].

## [!DNL Profile] in Experience Platform

De verhouding tussen het Profiel van de Klant in real time en andere diensten binnen Experience Platform wordt benadrukt in het volgende diagram:

![De relatie tussen het Real-Time Klantprofiel en andere services in Adobe Experience Platform. In dit diagram ziet u dat Profiel een van de kerncomponenten van Adobe Experience Platform is.](images/profile-overview/profile-in-platform.png)

## Werken met profielen

[!DNL Real-Time Customer Profile] voegt gegevens van verschillende bedrijfssystemen samen en verleent dan toegang tot die gegevens in de vorm van klantenprofielen met verwante gebeurtenissen van de tijdreeksen. Met deze functie kunnen marketers op meerdere kanalen hun publiek gecoördineerde, consistente en relevante ervaringen bieden. De volgende secties benadrukken enkele kernconcepten die u moet begrijpen om profielen binnen Platform effectief te bouwen en te handhaven.

### Samenstelling van profielentiteit

Een Real-Time Klantprofiel bestaat uit een hoofdentiteit, de **primaire entiteit** en diverse ondersteunende entiteiten. In de context van Experience Platform is de primaire entiteit doorgaans een **profielentiteit**, die bestaat uit eigenschappen, gedrag en publieksleden van een individuele persoon. Andere entiteiten staan de segmenteringsmotor toe om gegevens buiten de primaire entiteit van het profiel te gebruiken, en omvatten het volgende:

- **Maateenheid**: De entiteit die wordt gebruikt om het modelleringsproces voor gegevens te vereenvoudigen die over gebeurtenissen of profielverslagen worden gedeeld. Dit wordt ook wel de opgezochte entiteit of classificatieentiteit genoemd.
- **B2B-entiteit**: Entiteiten die de relatie van het profiel met business-to-business accounts en mogelijkheden beschrijven.

![Een diagram waarin de samenstelling van de profielentiteit wordt toegelicht.](./images/profile-overview/profile-entity-composition.png)

>[!IMPORTANT]
>
>Aangezien dimensionale en B2B-entiteiten alleen buiten de primaire entiteit bestaan, worden deze alleen gebruikt voor batchsegmentatie.

Maateenheden en B2B-entiteiten zijn via **schema-relaties**. Raadpleeg de volgende documentatie voor meer informatie:

- [Creeer een één-op-één schemaverhouding voor raadplegingsentiteiten](../xdm/tutorials/relationship-ui.md)
- [Creeer een vele-aan-één schemaverhouding voor B2B-entiteiten](../xdm/tutorials/relationship-b2b.md)

### Profielgegevensopslag

Hoewel [!DNL Real-Time Customer Profile] verwerkt ingesloten gegevens en gebruikt Adobe Experience Platform [!DNL Identity Service] om gerelateerde gegevens samen te voegen via identiteitstoewijzing, worden er eigen gegevens bijgehouden in de [!DNL Profile] gegevensopslag. De [!DNL Profile] store is gescheiden van catalogusgegevens in het datumpeer en [!DNL Identity Service] gegevens in de identiteitsgrafiek.

De profielopslag gebruikt een Microsoft Azure Cosmos DB-infrastructuur en het Platform Data Lake gebruikt Microsoft Azure Data Lake-opslag.

### Profielhulplijnen

Experience Platform biedt een aantal hulplijnen om te voorkomen dat u [XDM-schema&#39;s (Experience Data Model)](../xdm/home.md) die in real time profiel van de Klant niet kan steunen. Dit omvat zachte grenzen die in prestatiesdegradatie zullen resulteren, evenals harde grenzen die in fouten en systeembreuken zullen resulteren. Lees voor meer informatie, zoals een lijst met richtlijnen en voorbeelden van gebruiksgevallen de [Profielhulplijnen](guardrails.md) documentatie.

### Profieldashboard {#profile-dashboard}

De interface van het Experience Platform biedt een dashboard waardoor u belangrijke informatie over uw gegevens van het Profiel van de Klant in real time kunt bekijken, zoals die tijdens een dagelijkse momentopname wordt gevangen. Leren hoe u toegang krijgt tot en werkt met de [!DNL Profile] het dashboard in UI, en gedetailleerde informatie over de metriek die in het dashboard wordt getoond, verwijs naar [UI-gids voor profieldashboard](ui/profile-dashboard.md).

### Profielfragmenten versus samengevoegde profielen {#profile-fragments-vs-merged-profiles}

Elk individueel klantprofiel bestaat uit meerdere profielfragmenten die zijn samengevoegd tot één weergave van die klant. Bijvoorbeeld, als een klant met uw merk over verscheidene kanalen in wisselwerking staat, zal uw organisatie veelvoudige profielfragmenten met betrekking tot die enige klant hebben die in veelvoudige datasets verschijnen. Wanneer deze fragmenten in Platform worden opgenomen, worden ze samengevoegd om één profiel voor die klant te maken.

Met andere woorden, profielfragmenten vertegenwoordigen een unieke primaire identiteit en de bijbehorende [opnemen](#record-data) of [event](#time-series-events) gegevens voor die ID binnen een bepaalde dataset.

Wanneer de gegevens van veelvoudige datasets in conflict zijn (bijvoorbeeld één fragment maakt een lijst van de klant &quot;enig&quot;terwijl andere de klant als &quot;gehuwd&quot;maakt) [samenvoegingsbeleid](#merge-policies) Hiermee bepaalt u welke informatie u als prioriteit wilt instellen en in het profiel voor het individu wilt opnemen. Daarom is het totale aantal profielfragmenten binnen Platform waarschijnlijk altijd hoger dan het totale aantal samengevoegde profielen, aangezien elk profiel typisch uit veelvoudige fragmenten van veelvoudige datasets bestaat.

### Gegevens opnemen {#record-data}

Een profiel is een weergave van een onderwerp, een organisatie of een individu, dat uit vele kenmerken bestaat (ook wel recordgegevens genoemd). Het profiel van een product kan bijvoorbeeld een SKU en een beschrijving bevatten, terwijl het profiel van een persoon informatie bevat zoals voornaam, achternaam en e-mailadres. Gebruiken [!DNL Experience Platform], kunt u profielen aanpassen om specifieke gegevens te gebruiken relevant voor uw zaken. De norm [!DNL Experience Data Model] (XDM)-klasse, [!DNL XDM Individual Profile], is de aangewezen klasse waarop om een schema te bouwen wanneer het beschrijven van de gegevens van het klantenverslag, en levert de gegevensintegraal aan vele interactie tussen de diensten van het Platform. Voor meer informatie over het werken met schema&#39;s in [!DNL Experience Platform], te beginnen met het lezen van [XDM System, overzicht](../xdm/home.md).

### Gebeurtenissen van tijdreeksen {#time-series-events}

De gegevens van de tijdreeksen verstrekken een momentopname van het systeem op het tijdstip dat een actie of direct of indirect door een onderwerp werd genomen, evenals gegevens detailleert de gebeurtenis zelf. Deze tijdreeksgegevens worden vertegenwoordigd door de XDM ExperienceEvent-standaardschemaklasse en kunnen gebeurtenissen beschrijven, zoals items die aan een winkelwagentje worden toegevoegd, koppelingen waarop wordt geklikt en weergegeven video&#39;s. Gegevens uit tijdreeksen kunnen worden gebruikt om segmentatieregels te baseren op, en gebeurtenissen kunnen individueel worden benaderd in de context van een profiel.

### Identiteiten

Elk bedrijf wil met zijn klanten op een manier communiceren die zich persoonlijk voelt. Een van de uitdagingen bij het aanbieden van relevante digitale ervaringen aan klanten is echter het begrijpen van hoe ze hun losgekoppelde gegevens aan elkaar kunnen koppelen. Deze gegevens worden vaak verspreid over verschillende digitale kanalen, zoals tablets, mobiele telefoons en laptops. [!DNL Identity Service] kunt u het volledige beeld van uw klant samenvoegen door identiteiten van veelvoudige kanalen te verbinden en een identiteitsgrafiek voor elke klant te creëren. Ga naar [Overzicht van identiteitsservice](../identity-service/home.md) voor meer informatie .

### Beleid samenvoegen

Wanneer het brengen van gegevensfragmenten uit veelvoudige bronnen en het combineren van hen om een volledige mening van elk van uw individuele klanten te zien, zijn het fusieprincipe de regels die [!DNL Platform] gebruikt om te bepalen hoe de gegevens voorrang krijgen en welke gegevens worden gebruikt om het klantprofiel te maken.

Wanneer er conflicterende gegevens van veelvoudige datasets zijn, bepaalt het fusiebeleid hoe die gegevens moeten worden behandeld en welke waarde zou moeten worden gebruikt. Via RESTful APIs of de gebruikersinterface, kunt u nieuw samenvoegbeleid tot stand brengen, bestaand beleid beheren, en een standaardsamenvoegbeleid voor uw organisatie plaatsen.

Als u meer wilt weten over samenvoegingsbeleid en hun rol in het Experience Platform, leest u eerst de [overzicht van samenvoegbeleid](merge-policies/overview.md).

### Unieregelingen {#profile-fragments-and-union-schemas}

Een van de belangrijkste kenmerken van [!DNL Real-Time Customer Profile] is de mogelijkheid om multikanaalsgegevens te verenigen. Wanneer [!DNL Real-Time Customer Profile] wordt gebruikt om tot een entiteit toegang te hebben, kan het u van een samengevoegde mening van alle profielfragmenten voor die entiteit over datasets voorzien, die als &quot;verenigingsmening&quot;wordt bedoeld en door wat als verenigingsschema wordt genoemd mogelijk gemaakt.

Ga voor meer informatie over vakbondsschema&#39;s, waaronder hoe u vakbondsschema&#39;s kunt openen in de gebruikersinterface naar de [UI-hulplijn verenigingsschema](ui/union-schema.md).

<!-- ### (Alpha) Computed attributes

>[!IMPORTANT]
>
>Computed attribute functionality is in alpha. The documentation and functionality are subject to change.

Computed attributes are functions used to aggregate event-level data into profile-level attributes. These functions are automatically computed so that they can be used across segmentation, activation, and personalization. These computations help you to easily answer questions related to things like lifetime purchase value, time between purchases, or number of application opens, without requiring you to manually perform complex calculations each time the information is needed. For more information on computed attributes, including understanding the role computed attributes play within Adobe Experience Platform, please begin by reading the [computed attributes overview](computed-attributes/overview.md). -->

## Profielen en doelgroepen

Adobe Experience Platform [!DNL Segmentation Service] produceert het publiek nodig om ervaringen voor uw individuele klanten van energie te voorzien. Wanneer een publiek wordt gecreeerd, wordt identiteitskaart van dat publiek toegevoegd aan de lijst van publiekslidmaatschappen voor alle kwalificerende profielen. Segmentregels worden gemaakt en toegepast op [!DNL Real-Time Customer Profile] gegevens die RESTful APIs en het gebruikersinterface van de Bouwer van het Segment gebruiken. Om meer over segmentatie te leren, gelieve te beginnen door te lezen [Overzicht van segmentatieservice](../segmentation/home.md).

### Streaming opname en streamingsegmentatie

Invoer in realtime wordt mogelijk gemaakt via een proces dat streaming opname wordt genoemd. Wanneer gegevens uit profiel- en tijdreeksen worden opgenomen, [!DNL Real-Time Customer Profile] besluit automatisch om die gegevens van het publiek op te nemen of uit te sluiten door middel van een doorlopend proces dat streaming segmentatie wordt genoemd, alvorens het met bestaande gegevens samen te voegen en de mening van de unie bij te werken. Dientengevolge, kunt u onmiddellijk berekeningen uitvoeren en besluiten nemen om verbeterde, geïndividualiseerde ervaringen aan klanten te leveren aangezien zij met uw merk in wisselwerking staan. Terwijl het worden opgenomen, ondergaat de gegevens ook bevestiging om ervoor te zorgen het behoorlijk wordt opgenomen en conform het schema is waarop de dataset gebaseerd is. Voor meer informatie over welke validatie tijdens inname wordt uitgevoerd, leest u eerst de [kwaliteitsoverzicht van gegevensinvoer](../ingestion/quality/overview.md).

## Gegevens invoegen in [!DNL Profile]

[!DNL Platform] kan worden gevormd om verslag en tijdreeksgegevens naar te verzenden [!DNL Profile], die streaming opname in realtime en batch-opname ondersteunen. Zie de zelfstudie waarin wordt uitgelegd hoe u [gegevens toevoegen aan realtime klantprofiel](tutorials/add-profile-data.md).

>[!NOTE]
>
>Gegevens verzameld via Adobe-oplossingen, waaronder [!DNL Analytics Cloud], [!DNL Marketing Cloud], en [!DNL Advertising Cloud], stromen naar [!DNL Experience Platform] en wordt opgenomen in [!DNL Profile].

### Metrische gegevens voor het opnemen van profielen

Met waarnemingsinformatie kunt u belangrijke metriek in Adobe Experience Platform onthullen. Naast [!DNL Experience Platform] gebruiksstatistieken en prestatie-indicatoren voor diverse [!DNL Platform] functionaliteit, zijn er specifieke op profiel betrekking hebbende metriek die u toestaan om inzicht in inkomende verzoektarieven, succesvolle innametarieven, ingebedde verslaggrootte, en meer te krijgen. Om meer te leren, begin door te lezen [Overzicht van de API voor waarnemingsinformatie](../observability/api/overview.md)en voor een volledige lijst van de metriek van het Profiel van de Klant in real time, zie de documentatie over [beschikbare cijfers](../observability/api/metrics.md#available-metrics).

## Profielopslaggegevens bijwerken

Soms kan het nodig zijn gegevens bij te werken in de profielopslag van uw organisatie. U moet bijvoorbeeld records corrigeren of een kenmerkwaarde wijzigen. Dit kan door partijopname worden gedaan en vereist een profiel-Toegelaten dataset die met een upsert markering wordt gevormd. Voor meer informatie over hoe te om een dataset voor attributenupdates te vormen, gelieve te verwijzen naar het leerprogramma voor [het toelaten van een dataset voor Profiel en upsert](../catalog/datasets/enable-upsert.md).

## Beheer van gegevens en [!DNL Privacy]

Gegevensbeheer is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van verordeningen, beperkingen, en beleid te verzekeren die op gegevensgebruik van toepassing zijn.

Aangezien gegevensbeheer betrekking heeft op de toegang tot gegevens, speelt het binnen [!DNL Experience Platform] op verschillende niveaus:

- Labels voor gegevensgebruik
- Beleid voor gegevenstoegang
- Toegangscontrole van gegevens voor marketingacties

Gegevensbeheer wordt op verschillende punten beheerd. Dit zijn onder andere het bepalen van welke gegevens worden ingevoerd [!DNL Platform] en welke gegevens toegankelijk zijn na inname voor een bepaalde marketingactie. Voor meer informatie, begin door te lezen [gegevensbeheer - overzicht](../data-governance/home.md).

### Verzoeken om opt-out en privacy van gegevens afhandelen

[!DNL Experience Platform] biedt uw klanten de mogelijkheid om aanvragen voor een opt-out te verzenden met betrekking tot het gebruik en de opslag van hun gegevens binnen [!DNL Real-Time Customer Profile]. Raadpleeg de documentatie over voor meer informatie over de manier waarop aanvragen voor een opt-out worden afgehandeld [naleven van opt-out-verzoeken](../segmentation/consents.md).

## Volgende stappen en extra bronnen

Als u meer wilt weten over het werken met realtime gegevens van het klantprofiel met de interface van het Experience Platform of de profiel-API, leest u eerst de [Handleiding voor profielgebruikersinterface](ui/user-guide.md) of [Handleiding voor API-ontwikkelaars](api/overview.md), respectievelijk.
