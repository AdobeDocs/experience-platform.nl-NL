---
keywords: Experience Platform;home;popular topics;XDM;XDM system;XDM individual profile;XDM ExperienceEvent;XDM Experience Event;experienceEvent;experience event;Mixins;mixins;mixin;Mixin;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;schema library;Schema Library;schema;record data;time series;time-series
solution: Experience Platform
title: XDM System, overzicht
topic: overview
description: 'Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. Het Model van Gegevens van de ervaring (XDM), die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema''s voor het beheer van de klantenervaring te bepalen. '
translation-type: tm+mt
source-git-commit: b0b2f0c5aa91a5aeb5836d9795a580ccc69e3e17
workflow-type: tm+mt
source-wordcount: '1581'
ht-degree: 0%

---


# XDM System, overzicht

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de [!DNL Platform] diensten te gebruiken te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier kan leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden uitdrukken.

XDM is het grondkader dat Adobe Experience Cloud, aangedreven door [!DNL Experience Platform], toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op het juiste moment te leveren. De methodologie waarop [!DNL Experience Platform] wordt gebouwd, het Systeem XDM, exploiteert [!DNL Experience Data Model] schema&#39;s voor gebruik door de [!DNL Platform] diensten.

Dit document biedt een overzicht van de rol van XDM System in [!DNL Experience Platform].

## XDM-schema&#39;s

[!DNL Experience Platform] gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens kunnen worden opgenomen in [!DNL Platform], moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. Schema&#39;s bestaan uit een basisklasse en nul of meer mixen.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie de [grondbeginselen van schemacompositie](schema/composition.md).

### [!DNL Schema Registry] en [!DNL Schema Library]

Het **[!DNL Schema Registry]** biedt een gebruikersinterface en RESTful-API waarmee u alle schemagerelateerde bronnen in de Adobe Experience Platform kunt weergeven en beheren **[!DNL Schema Library]**. Het [!DNL Schema Library] bevat industrie-standaardmiddelen die aan u door Adobe worden ter beschikking gesteld, evenals middelen van [!DNL Experience Platform] partners en verkopers de waarvan toepassingen u gebruikt. De gebruikersinterface en API van het schemaregister kunnen ook worden gebruikt om nieuwe schema&#39;s en middelen tot stand te brengen en te beheren die aan uw organisatie uniek zijn.

Voor een uitvoerige gids voor de belangrijkste verrichtingen beschikbaar in [!DNL Schema Registry], zie de de ontwikkelaarsgids [van de Registratie van het](api/getting-started.md)Schema.

## Gegevensgedrag in XDM-systeem {#data-behaviors}

Gegevens die bestemd zijn voor gebruik in [!DNL Experience Platform] worden gegroepeerd in twee gedragstypen:

* **Opnamegegevens**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **Gegevens** tijdreeks: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen.

Hoewel u uw eigen klassen binnen de klasse kunt bepalen, [!DNL Schema Registry]adviseert men dat u de aangewezen klassen **[!DNL XDM Individual Profile]** en **[!DNL XDM ExperienceEvent]** voor verslag en tijdreeksgegevens, respectievelijk gebruikt. Deze klassen worden hieronder gedetailleerder beschreven.

### [!DNL XDM Individual Profile] {#xdm-individual-profile}

[!DNL XDM Individual Profile] is een op records gebaseerde klasse die een unieke representatie vormt van de kenmerken van zowel geïdentificeerde als gedeeltelijk geïdentificeerde onderwerpen. De profielen die hoogst geïdentificeerd zijn kunnen voor persoonlijke mededelingen of gerichte overeenkomsten worden gebruikt, en kunnen gedetailleerde persoonlijke informatie zoals naam, geslacht, geboortedatum, plaats, en contactinformatie met inbegrip van telefoonaantallen en e-mailadressen bevatten.

Minder geïdentificeerde profielen kunnen alleen uit anonieme gedragssignalen bestaan, zoals browsercookies. In dit geval worden de gegevens van het verspreide profiel gebruikt om een informatiebasis te bouwen waarin de belangen en voorkeuren van het anonieme profiel worden gesorteerd en opgeslagen. Deze id&#39;s kunnen in de loop der tijd gedetailleerder worden naarmate het onderwerp zich aanmeldt voor meldingen, abonnementen, aankopen, enzovoort. Deze toename van profielkenmerken kan uiteindelijk resulteren in een bepaald onderwerp en een hogere mate van gerichte betrokkenheid mogelijk maken.

Naarmate een consumentenprofiel blijft groeien, wordt het een robuuste opslagplaats voor persoonlijke informatie, identificatiegegevens, contactgegevens en communicatievoorkeuren.

### [!DNL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent is een op tijdreeksen gebaseerde klasse die wordt gebruikt om de status van het systeem vast te leggen wanneer een gebeurtenis (of set gebeurtenissen) heeft plaatsgevonden, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn feitenverslagen van wat voorkwam, zodat zijn zij onveranderlijk en vertegenwoordigen wat gebeurde zonder samenvoeging of interpretatie. Zij zijn kritiek voor tijd-domein analyses aangezien zij kunnen worden gebruikt om veranderingen te analyseren die in een bepaald venster van tijd voorkomen, en tussen veelvoudige vensters van tijd te vergelijken om trends te volgen.

De Gebeurtenissen van de ervaring kunnen of expliciet of impliciet zijn. Expliciete gebeurtenissen zijn direct waarneembare menselijke acties die plaatsvinden tijdens een punt op een reis. Impliciete gebeurtenissen zijn gebeurtenissen die worden opgeworpen zonder directe menselijke actie, maar die nog steeds betrekking hebben op een individu. Voorbeelden van impliciete gebeurtenissen zijn onder meer het geplande verzenden van e-mailnieuwsbrieven of batterijspanning die een bepaalde drempelwaarde bereiken.

Hoewel niet alle gebeurtenissen gemakkelijk over alle gegevensbronnen worden gecategoriseerd, is het uiterst waardevol om gelijkaardige gebeurtenissen in gelijkaardige types te harmoniseren waar mogelijk voor verwerking.

![ExperienceEvent Klantenreis](images/overview/experience-event-journey.png)

## XDM-schema&#39;s en - [!DNL Experience Platform] services

[!DNL Experience Platform] is schema-agnostisch, betekenend dat om het even welk schema dat aan de norm voldoet XDM voor gebruik door de [!DNL Platform] diensten beschikbaar is. De manieren waarop de verschillende [!DNL Platform] diensten schema&#39;s gebruiken worden hieronder meer in detail beschreven.

### [!DNL Catalog Service], [!DNL Data Ingestion] &amp; [!DNL Data Lake]

[!DNL Catalog Service] is het systeem van registratie voor [!DNL Experience Platform] activa en de bijbehorende schema&#39;s. [!DNL Catalog] Dit zijn niet de feitelijke bestanden of mappen met gegevens, maar de metagegevens en beschrijvingen van deze bestanden en mappen.

[!DNL Catalog] gegevens worden opgeslagen in de [!DNL Data Lake], een zeer granulaire gegevensopslag die alle gegevens bevat die door worden beheerd, [!DNL Platform]ongeacht de oorsprong of bestandsindeling.

Om te beginnen met het opnemen van gegevens in [!DNL Experience Platform], wordt een dataset gecreeerd gebruikend [!DNL Catalog Service]. De dataset verwijst naar een XDM-schema dat de structuur van de gegevens beschrijft die moeten worden opgenomen. Als een dataset zonder een schema wordt gecreeerd, zal een &quot;waargenomen schema&quot;afleiden door het type en de inhoud van ingebedde gegevensgebieden te inspecteren. [!DNL Experience Platform] Datasets worden vervolgens bijgehouden in [!DNL Catalog] en opgeslagen in de [!DNL Data Lake] parallel aan de schema&#39;s en geobserveerde schema&#39;s waarop ze zijn gebaseerd.

Voor meer informatie over [!DNL Catalog], zie het overzicht [van de Dienst van de](../catalog/home.md)Catalogus. Voor meer informatie over de Ingestie van Gegevens van Adobe Experience Platform, zie het Overzicht [van de](../ingestion/home.md)Ingestie van Gegevens.

### [!DNL Query Service]

Met Adobe Experience Platform [!DNL Query Service] kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op [!DNL Experience Platform] gegevens die vele verschillende gebruiksgevallen ondersteunen.

Nadat een schema is samengesteld en een dataset is gecreeerd die verwijzingen dat schema, worden de gegevens dan opgenomen en in [!DNL Data Lake]opgeslagen. Gebruikend [!DNL Query Service], kunt u zich bij om het even welke datasets in aansluiten [!DNL Data Lake] en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, machine het leren, of voor opname in [!DNL Real-time Customer Profile].

Voor meer over [!DNL Query Service], te zien gelieve de inleiding [van de Dienst van de](../query-service/home.md)Vraag.

### [!DNL Real-time Customer Profile]

Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen waarmee u werkt [!DNL Experience Platform].

[!DNL Real-time Customer Profile] verbruikt schema-geformatteerde gegevens die op de [!DNL XDM Individual Profile] of [!DNL XDM ExperienceEvent] klassen worden gebaseerd, en antwoordt aan vragen die op die gegevens worden gebaseerd. [!DNL Profile] biedt geen ondersteuning voor het gebruik van schema&#39;s die op andere klassen zijn gebaseerd.

[!DNL Profile] onderhoudt een geval van elk klantenprofiel, samen samenvoegend gegevens om een &quot;enige bron van waarheid&quot;voor het individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsmening&quot;wordt bekend is. Een verenigingsmening voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel schema uitvoeren.  Wanneer het samenstellen van een schema gebruikend UI of API, kunt u het schema voor gebruik met toelaten [!DNL Real-time Customer Profile] en het etiketteren voor opneming in de verenigingsmening. Het gelabelde schema neemt dan deel aan de schemadefinitie die wordt doorgegeven aan [!DNL Profile].

Aangezien [!DNL XDM Individual Profile] en de [!DNL XDM ExperienceEvent] gegevens door worden opgenomen en worden beheerd, brengt het [!DNL Catalog][!DNL Real-time Customer Profile] in werking beginnen het opnemen gegevens die voor zijn gebruik zijn toegelaten. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

[!DNL XDM Individual Profile] gegevens helpen acties over om het even welk kanaal of Adobe oplossingsintegratie te informeren en macht, en wanneer in combinatie met een rijke geschiedenis van gedrags en interactiegegevens, worden deze gegevens gebruikt om machine het leren te aandrijven. De [!DNL Real-time Customer Profile] API kan ook worden gebruikt om de functionaliteit van derdeoplossingen, CRMs, en merkgebonden oplossingen te verrijken.

Zie het overzicht [van het profiel van de Klant in](../profile/home.md) real time voor meer informatie.

### [!DNL Data Science Workspace]

Adobe Experience Platform [!DNL Data Science Workspace] maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te krijgen van gegevens die in het systeem zijn opgeslagen [!DNL Experience Platform]. [!DNL Data Science Workspace] staat gegevenswetenschappers toe om recepten te bouwen die op Individuele XDM [!DNL Profile] [!DNL XDM ExperienceEvent] en gegevens over klanten en hun activiteiten worden gebaseerd, die voorspellingen zoals het kopen van neiging en geadviseerde aanbiedingen vergemakkelijken dat het individu waarschijnlijk zal waarderen en gebruiken.

Met [!DNL Data Science Workspace]behulp van computerleren kunnen gegevenswetenschappers eenvoudig intelligente services-API&#39;s maken. Deze services werken samen met andere Adobe-oplossingen, zoals Adobe Target en Adobe Analytics Cloud, om u te helpen persoonlijke, doelgerichte digitale ervaringen te automatiseren.

Voor meer informatie bij het gebruiken van [!DNL Experience Platform] gegevens aan machtsinzichten, zie het Overzicht [van de Werkruimte van de Wetenschap van](../data-science-workspace/home.md)Gegevens.

## Volgende stappen en extra bronnen

Nu u beter de rol van schema&#39;s door heel [!DNL Experience Platform]kunt begrijpen, bent u bereid om uw te beginnen samenstellen. Als u uw leerproces wilt voortzetten, begint u met het lezen van de voorgestelde documentatie en bekijkt u de onderstaande video.

Om ontwerpprincipes en beste praktijken voor het samenstellen van schema&#39;s te leren die met moeten worden gebruikt [!DNL Experience Platform], begin door de [grondbeginselen van schemacompositie](schema/composition.md)te lezen. Voor geleidelijke instructies op hoe te om een schema tot stand te brengen, zie de leerprogramma&#39;s bij het creëren van een schema [gebruikend API](tutorials/create-schema-api.md) of [gebruikend het gebruikersinterface](tutorials/create-schema-ui.md).

Bekijk de volgende video om uw begrip van [!DNL XDM System] in [!DNL Experience Platform]te versterken:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)

