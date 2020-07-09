---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: XDM-systeem (Experience Data Model)
topic: overview
translation-type: tm+mt
source-git-commit: 8ea3b09f86fe11ce7043f22c56ff9756b909e716
workflow-type: tm+mt
source-wordcount: '1777'
ht-degree: 0%

---


# XDM System, overzicht

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het Adobe Experience Platform. Experience Data Model (XDM), aangestuurd door Adobe, is een poging om gegevens over klantervaring te standaardiseren en schema&#39;s voor het beheer van klantervaring te definiëren.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten van het Platform te gebruiken te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier kan leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden uitdrukken.

XDM is het basisraamwerk dat Adobe Experience Cloud, aangedreven door Experience Platform, in staat stelt de juiste boodschap af te geven aan de juiste persoon, op het juiste kanaal, op het juiste moment. De methodologie waarop het Experience Platform wordt gebouwd, **XDM Systeem**, stelt de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van het Platform in werking.

Dit document biedt een overzicht van de rol van XDM System in Experience Platform.

## XDM-schema&#39;s

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het gemakkelijker om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basisklasse en nul of meer mixen.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie de [grondbeginselen van schemacompositie](schema/composition.md).

### Schema-register en Schema-bibliotheek

De **Registratie** van het Schema verstrekt een gebruikersinterface en RESTful API waarvan u alle schema-verwante middelen in de Bibliotheek **van het** Schema van het Adobe Experience Platform kunt bekijken en beheren. De Schemabibliotheek bevat industriestandaard bronnen die beschikbaar worden gesteld door Adobe, evenals bronnen van partners en leveranciers van Experience Platforms van wie u de toepassingen gebruikt. De gebruikersinterface en API van het schemaregister kunnen ook worden gebruikt om nieuwe schema&#39;s en middelen tot stand te brengen en te beheren die aan uw organisatie uniek zijn.

Voor een uitvoerige gids voor de belangrijkste verrichtingen beschikbaar in de Registratie van het Schema, zie de de ontwikkelaarsgids [van de Registratie van het](api/getting-started.md)Schema.

## Gegevensgedrag in XDM-systeem {#data-behaviors}

Gegevens die bestemd zijn voor gebruik in Experience Platform worden gegroepeerd in twee gedragstypen:

* **Opnamegegevens**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **Gegevens** tijdreeks: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de **klasse** van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen.

Hoewel u uw eigen klassen binnen de Registratie van het Schema kunt bepalen, adviseert men dat u de aangewezen klassen **XDM Individueel Profiel** en **XDM ExperienceEvent** voor verslag en tijdreeksgegevens, respectievelijk gebruikt. Deze klassen worden hieronder gedetailleerder beschreven.

### Afzonderlijk XDM-profiel

Het Individuele Profiel van XDM is een op verslag-gebaseerde klasse die een enige vertegenwoordiging van de attributen van zowel geïdentificeerde als gedeeltelijk-geïdentificeerde onderwerpen vormt. De profielen die hoogst geïdentificeerd zijn kunnen voor persoonlijke mededelingen of gerichte overeenkomsten worden gebruikt, en kunnen gedetailleerde persoonlijke informatie zoals naam, geslacht, geboortedatum, plaats, en contactinformatie met inbegrip van telefoonaantallen en e-mailadressen bevatten.

Minder geïdentificeerde profielen kunnen alleen uit anonieme gedragssignalen bestaan, zoals browsercookies. In dit geval worden de gegevens van het verspreide profiel gebruikt om een informatiebasis te bouwen waarin de belangen en voorkeuren van het anonieme profiel worden gesorteerd en opgeslagen. Deze id&#39;s kunnen in de loop der tijd gedetailleerder worden naarmate het onderwerp zich aanmeldt voor meldingen, abonnementen, aankopen, enzovoort. Deze toename van profielkenmerken kan uiteindelijk resulteren in een bepaald onderwerp en een hogere mate van gerichte betrokkenheid mogelijk maken.

Naarmate een consumentenprofiel blijft groeien, wordt het een robuuste opslagplaats voor persoonlijke informatie, identificatiegegevens, contactgegevens en communicatievoorkeuren.

### XDM ExperienceEvent

XDM ExperienceEvent is een op tijdreeksen gebaseerde klasse die wordt gebruikt om de status van het systeem vast te leggen wanneer een gebeurtenis (of set gebeurtenissen) heeft plaatsgevonden, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn feitenverslagen van wat voorkwam, zodat zijn zij onveranderlijk en vertegenwoordigen wat gebeurde zonder samenvoeging of interpretatie. Zij zijn kritiek voor tijd-domein analyses aangezien zij kunnen worden gebruikt om veranderingen te analyseren die in een bepaald venster van tijd voorkomen, en tussen veelvoudige vensters van tijd te vergelijken om trends te volgen.

De Gebeurtenissen van de ervaring kunnen of expliciet of impliciet zijn. Expliciete gebeurtenissen zijn direct waarneembare menselijke acties die plaatsvinden tijdens een punt op een reis. Impliciete gebeurtenissen zijn gebeurtenissen die worden opgeworpen zonder directe menselijke actie, maar die nog steeds betrekking hebben op een individu. Voorbeelden van impliciete gebeurtenissen zijn onder meer het geplande verzenden van e-mailnieuwsbrieven of batterijspanning die een bepaalde drempelwaarde bereiken.

Hoewel niet alle gebeurtenissen gemakkelijk over alle gegevensbronnen worden gecategoriseerd, is het uiterst waardevol om gelijkaardige gebeurtenissen in gelijkaardige types te harmoniseren waar mogelijk voor verwerking.

![ExperienceEvent Klantenreis](images/overview/experience-event-journey.png)

## XDM-schema&#39;s en Experience Platforms

Experience Platform is schema-agnostisch, betekenend dat om het even welk schema dat aan de norm XDM voldoet voor gebruik door de diensten van het Platform beschikbaar is. De manieren waarop de verschillende diensten van de Platform schema&#39;s gebruiken worden hieronder meer in detail beschreven.

### Catalogusservice, gegevensinsluiting en datameer

De Catalogusdienst is het systeem van verslag voor de activa van het Experience Platform en hun verwante schema&#39;s. Catalogus is niet de daadwerkelijke dossiers of folders die gegevens bevatten, maar het houdt eerder de meta-gegevens en de beschrijvingen van die dossiers en folders.

De gegevens van de catalogus worden opgeslagen in het meer van Gegevens, een hoogst korrelige gegevensopslag die alle gegevens bevat die door Platform, ongeacht oorsprong of dossierformaat worden beheerd.

Beginnen opnemend gegevens in Experience Platform, wordt een dataset gecreeerd gebruikend de Dienst van de Catalogus. De dataset verwijst naar een XDM-schema dat de structuur van de gegevens beschrijft die moeten worden opgenomen. Als een dataset zonder een schema wordt gecreeerd, zal het Experience Platform een &quot;waargenomen schema&quot;afleiden door het type en de inhoud van ingebedde gegevensgebieden te inspecteren. Datasets worden vervolgens bijgehouden in Catalog en opgeslagen in het Data Lake naast de schema&#39;s en geobserveerde schema&#39;s waarop ze zijn gebaseerd.

Voor meer informatie over Catalog, zie het overzicht [van de Dienst van de](../catalog/home.md)Catalogus. Voor meer informatie over de Ingestie van de Gegevens van het Adobe Experience Platform, zie het Overzicht [van de Ingestie van](../ingestion/home.md)Gegevens.

### Query-service

De Dienst van de Vraag van het Adobe Experience Platform staat u toe om standaardSQL aan vraaggegevens van het Experience Platform te gebruiken om vele verschillende gebruiksgevallen te steunen.

Nadat een schema is samengesteld en een dataset is gecreeerd die verwijzingen dat schema, wordt het gegeven dan opgenomen en opgeslagen in het meer van Gegevens. Gebruikend de Dienst van de Vraag, kunt u zich bij om het even welke datasets in het meer van Gegevens aansluiten en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, machine het leren, of voor opname in het Profiel van de Klant in real time.

Om meer over de Dienst van de Vraag te leren, te zien gelieve de inleiding [van de Dienst van de](../query-service/home.md)Vraag.

### Klantprofiel in realtime

Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen die u met Experience Platform gebruikt.

Klantprofiel in realtime verbruikt schema-opgemaakte gegevens op basis van de klassen Individueel XDM Profile of XDM ExperienceEvent en reageert op query&#39;s die op die gegevens zijn gebaseerd. Profiel ondersteunt het gebruik van schema&#39;s die op andere klassen zijn gebaseerd niet.

Het profiel handhaaft een geval van elk klantenprofiel, die gegevens samenvoegen om een &quot;enige bron van waarheid&quot;voor het individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel schema uitvoeren.  Wanneer het samenstellen van een schema gebruikend UI of API, kunt u het schema voor gebruik met het Profiel van de Klant in real time toelaten en het etiketteren voor opneming in de verenigingsmening. Het gelabelde schema neemt dan deel aan de schemadefinitie die aan Profiel wordt doorgegeven.

Aangezien het Individuele Profiel XDM en de gegevens XDM ExperienceEvent door Catalogus worden opgenomen en beheerd, brengt het het Profiel van de Klant in real time in werking beginnen innemend gegevens die voor zijn gebruik zijn toegelaten. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

De gegevens van het Individuele Profiel XDM helpen en acties over om het even welk kanaal of de oplossingsintegratie van Adobe informeren en macht, en wanneer samengevoegd met een rijke geschiedenis van gedrags en interactiegegevens, worden deze gegevens gebruikt om machine het leren te aandrijven. De Real-time API van het Profiel van de Klant kan ook worden gebruikt om de functionaliteit van derdeoplossingen, CRMs, en merkgebonden oplossingen te verrijken.

Zie het overzicht [van het profiel van de Klant in](../profile/home.md) real time voor meer informatie.

### Werkruimte voor gegevenswetenschap

De Werkruimte van de Wetenschap van Gegevens van het Adobe Experience Platform gebruikt machine het leren en kunstmatige intelligentie om inzichten van gegevens te verkrijgen die binnen Experience Platform worden opgeslagen. De Werkruimte van de Wetenschap van gegevens staat gegevenswetenschappers toe om recepten te bouwen die op het Individuele Profiel van XDM en gegevens XDM ExperienceEvent over klanten en hun activiteiten worden gebaseerd, die voorspellingen zoals het kopen van neiging en geadviseerde aanbiedingen vergemakkelijken dat het individu waarschijnlijk zal waarderen en gebruiken.

Met de Werkruimte van de Wetenschap van Gegevens, kunnen de gegevenswetenschappers intelligente diensten APIs gemakkelijk tot stand brengen die door machine het leren worden aangedreven. Deze services werken met andere Adobe-oplossingen, waaronder Adobe Target en Adobe Analytics Cloud, om u te helpen persoonlijke, doelgerichte digitale ervaringen te automatiseren.

Voor meer informatie bij het gebruiken van de gegevens van het Experience Platform aan machtsinzichten, zie het Overzicht [van de Werkruimte van de Wetenschap van](../data-science-workspace/home.md)Gegevens.

### Beslissingsservice

De beslissingsdienst verstrekt het vermogen om gepersonaliseerde aanbiedingsbeslissing in Platform-geïntegreerde toepassingen te vormen. Aanbiedingen zouden productaanbevelingen, inhoudcomponenten voor een Webervaring, gespreksmanuscripten, en te nemen acties kunnen zijn.

De Beslissende Dienst hefboomwerkingen de gegevens van het Profiel van de Klant in real time, en is daarom slechts compatibel met datasets die op schema&#39;s worden gebaseerd die het Individuele Profiel XDM of de klasse XDM ExperienceEvent uitvoeren.

Zie het overzicht [van de Dienst van het](../decisioning-service/home.md) Beslissen voor meer informatie.

## Volgende stappen en extra bronnen

Nu u beter de rol van schema&#39;s door Experience Platform begrijpt, bent u bereid om uw te beginnen samenstellen. Als u uw leerproces wilt voortzetten, begint u met het lezen van de voorgestelde documentatie en bekijkt u de onderstaande video.

Om ontwerpprincipes en beste praktijken voor het samenstellen van schema&#39;s te leren die met Experience Platform moeten worden gebruikt, begin door de [grondbeginselen van schemacompositie](schema/composition.md)te lezen. Voor geleidelijke instructies op hoe te om een schema tot stand te brengen, zie de leerprogramma&#39;s bij het creëren van een schema [gebruikend API](tutorials/create-schema-api.md) of [gebruikend het gebruikersinterface](tutorials/create-schema-ui.md).

Bekijk de volgende video om uw inzicht in XDM System in Experience Platform te versterken:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

