---
keywords: Experience Platform;home;populaire onderwerpen;XDM;XDM-systeem;XDM individueel profiel;XDM ExperienceEvent;XDM Experience Event;ExperienceEvent;ExperienceEvent;Field-groepen;field-groep;Field-groep;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceDataModel;ExperienceDataModel;DataModel;DataModel register;Schema-register;schema-bibliotheek;Schema-bibliotheek;schema;recordgegevens;tijdreeks;tijdreeks
solution: Experience Platform
title: XDM-systeemoverzicht
topic-legacy: overview
description: Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. Het Model van Gegevens van de ervaring (XDM), die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema's voor het beheer van de klantenervaring te bepalen.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: 196147e7691010707953561c110a3934fec8ba1b
workflow-type: tm+mt
source-wordcount: '1910'
ht-degree: 0%

---

# XDM System, overzicht

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities die om het even welke toepassing toestaan om met de diensten van het Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier kan leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden uitdrukken.

XDM is het grondkader dat Adobe Experience Cloud, aangedreven door Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op precies het juiste moment te leveren. De methodologie waarop Experience Platform wordt gebouwd, het Systeem van XDM, operationeel [!DNL Experience Data Model] schema&#39;s voor gebruik door Platforms.

Dit document biedt een overzicht van de rol van XDM System in Experience Platform.

## XDM-schema&#39;s

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens in Platform kunnen worden opgenomen, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. De schema&#39;s bestaan uit een basisklasse en nul of meer groepen van het schemagebied.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes en beste praktijken, zie [grondbeginselen van de schemacompositie](schema/composition.md).

### Standaard XDM-componenten

XDM verstrekt een robuuste inzameling van standaardgebiedsgroepen en gegevenstypes, die bedoeld zijn om gemeenschappelijke concepten en gebruiksgevallen over verschillende industrieën te vangen. Experience Platform staat u toe om deze componenten door industrie te filtreren, toelatend u om schema&#39;s snel en vol vertrouwen te construeren die het best uw bijzondere bedrijfsbehoeften steunen.

Wanneer het construeren van schema&#39;s in Experience Platform UI, worden de vermelde gebiedsgroepen getoond met metrische populariteit. Deze metrische waarde wordt bepaald door hoe vaak andere gebruikers van het Platform de gebiedsgroep in hun schema&#39;s in dienst nemen. Hoe hoger het getal, hoe populairder de veldgroep. Standaard worden de resultaten weergegeven van populairste tot minst populaire gegevens, zodat u op de hoogte blijft van trends in de modellering van gegevens in uw branche.

![Veldgroeppopulariteit](./images/overview/popularity.png)

### [!DNL Schema Library]

Experience Platform verstrekt een gebruikersinterface en RESTful API waarvan u alle op schema betrekking hebbende middelen in het Experience Platform kunt bekijken en beheren **[!DNL Schema Library]**. De [!DNL Schema Library] bevat standaardXDM componenten die aan u door Adobe, evenals middelen van de partners en verkopers van het Experience Platform beschikbaar worden gemaakt van wie toepassingen u gebruikt.

Met de [!DNL Schema Registry API] of de [!UICONTROL Schemas] in de gebruikersinterface van het Platform kunt u ook nieuwe schema&#39;s en bronnen maken en beheren die uniek zijn voor uw organisatie.

Raadpleeg de volgende documentatie voor meer informatie over het beheren van en werken met schema&#39;s in Platform:

* [XDM UI-hulplijn](./ui/overview.md)
* [Handleiding Schema Registry API](./api/overview.md)

## Gegevensgedrag in XDM-systeem {#data-behaviors}

Gegevens die bestemd zijn voor gebruik in Experience Platform worden gegroepeerd in twee gedragstypen:

* **Gegevens opnemen**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **Gegevens uit tijdreeksen**: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen.

Hoewel u uw eigen klassen kunt definiëren in het dialoogvenster [!DNL Schema Registry], wordt u aangeraden de voorkeursklassen te gebruiken **[!UICONTROL XDM Individual Profile]** en **[!UICONTROL XDM ExperienceEvent]** voor gegevens uit respectievelijk record- en tijdreeksen. Deze klassen worden hieronder gedetailleerder beschreven.

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] is een op records gebaseerde klasse die een unieke representatie vormt van de kenmerken van zowel geïdentificeerde als gedeeltelijk geïdentificeerde onderwerpen. De profielen die hoogst geïdentificeerd zijn kunnen voor persoonlijke mededelingen of gerichte overeenkomsten worden gebruikt, en kunnen gedetailleerde persoonlijke informatie zoals naam, geslacht, geboortedatum, plaats, en contactinformatie met inbegrip van telefoonaantallen en e-mailadressen bevatten.

Minder geïdentificeerde profielen kunnen alleen uit anonieme gedragssignalen bestaan, zoals browsercookies. In dit geval worden de gegevens van het verspreide profiel gebruikt om een informatiebasis te bouwen waarin de belangen en voorkeuren van het anonieme profiel worden gesorteerd en opgeslagen. Deze id&#39;s kunnen in de loop der tijd gedetailleerder worden naarmate het onderwerp zich aanmeldt voor meldingen, abonnementen, aankopen, enzovoort. Deze toename van profielkenmerken kan uiteindelijk resulteren in een bepaald onderwerp en een hogere mate van gerichte betrokkenheid mogelijk maken.

Naarmate een profiel blijft groeien, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identificatiegegevens, contactgegevens en communicatievoorkeuren van een individu.

Zie de [[!UICONTROL XDM Individual Profile] naslaggids](./classes/individual-profile.md) voor meer informatie over de structuur en het gebruiksgeval van de velden die door de klasse worden verschaft.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent is een op tijdreeksen gebaseerde klasse die wordt gebruikt om de status van het systeem vast te leggen wanneer een gebeurtenis (of set gebeurtenissen) heeft plaatsgevonden, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn onveranderlijk, feitelijke verslagen van wat op dat ogenblik voorkwam, die wat vormden zonder samenvoeging of interpretatie. Zij zijn kritiek voor tijd-domein analyses aangezien zij kunnen worden gebruikt om veranderingen te analyseren die in een bepaald venster van tijd voorkomen, en tussen veelvoudige vensters van tijd te vergelijken om trends te volgen.

De Gebeurtenissen van de ervaring kunnen of expliciet of impliciet zijn. Expliciete gebeurtenissen zijn direct waarneembare menselijke acties die plaatsvinden tijdens een punt op een reis. Impliciete gebeurtenissen zijn gebeurtenissen die worden opgeworpen zonder directe menselijke actie, maar die nog steeds betrekking hebben op een individu. Voorbeelden van impliciete gebeurtenissen zijn onder meer het geplande verzenden van e-mailnieuwsbrieven of batterijspanning die een bepaalde drempelwaarde bereiken.

Hoewel niet alle gebeurtenissen gemakkelijk over alle gegevensbronnen worden gecategoriseerd, is het uiterst waardevol om gelijkaardige gebeurtenissen in gelijkaardige types te harmoniseren waar mogelijk voor verwerking.

![ExperienceEvent Klantenreis](images/overview/experience-event-journey.png)

Zie de [[!UICONTROL XDM ExperienceEvent] naslaggids](./classes/experienceevent.md) voor meer informatie over de structuur en het gebruiksgeval van de velden die door de klasse worden verschaft.

## XDM-schema&#39;s en Experience Platforms

Experience Platform is schema-agnostisch, betekenend dat om het even welk schema dat aan de norm voldoet XDM ter beschikking wordt gesteld aan de diensten van het Platform. De manieren waarop de verschillende diensten van de Platform schema&#39;s gebruiken worden hieronder meer in detail beschreven.

### Catalogusservice, Gegevensinsluiting en Datameer

De Catalogusdienst is het systeem van verslag voor de activa van het Experience Platform en hun verwante schema&#39;s. Catalog bevat niet de feitelijke gegevensbestanden of directory&#39;s, maar wel de metagegevens en beschrijvingen van die bestanden en mappen.

De gegevens van de catalogus worden opgeslagen in het meer van Gegevens, een hoogst korrelige gegevensopslag die alle gegevens bevat die door Platform, ongeacht oorsprong of dossierformaat worden beheerd.

Om te beginnen met het opnemen van gegevens in Experience Platform, kunt u de Dienst van de Catalogus gebruiken om een dataset tot stand te brengen. De dataset verwijst naar een XDM-schema dat de structuur van de gegevens beschrijft die moeten worden opgenomen. Als een dataset zonder een schema wordt gecreeerd, leidt het Experience Platform een &quot;waargenomen schema&quot;af door het type en de inhoud van ingebedde gegevensgebieden te inspecteren. Datasets worden vervolgens bijgehouden in Catalog en opgeslagen in het Data Lake naast de schema&#39;s en geobserveerde schema&#39;s waarop ze zijn gebaseerd.

Voor meer informatie over Catalog, zie [Overzicht van Catalog Service](../catalog/home.md). Voor meer informatie over Adobe Experience Platform Data Ingestie raadpleegt u de [Overzicht van gegevensinname](../ingestion/home.md).

### Query-service

Met Adobe Experience Platform Query Service kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens van Experience Platforms ter ondersteuning van vele verschillende gebruiksgevallen.

Nadat een schema is samengesteld en een dataset is gecreeerd die verwijzingen dat schema, wordt het gegeven dan opgenomen en opgeslagen in het meer van Gegevens. Gebruikend de Dienst van de Vraag, kunt u zich bij om het even welke datasets in het meer van Gegevens aansluiten en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, machine het leren, of voor opname in het Profiel van de Klant in real time.

Zie de [Overzicht van Query Service](../query-service/home.md) voor meer informatie over de dienst.

### Klantprofiel in realtime

Klantprofiel in realtime biedt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd, en actioneerbare tijdstempelaccounts van gebeurtenissen waarbij de persoon is betrokken die hebben plaatsgevonden in een van de systemen die u met Experience Platform gebruikt.

In real time het Profiel van de Klant verbruikt schema-geformatteerde gegevens die op het [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent] en reageert op query&#39;s die op die gegevens zijn gebaseerd. Profiel ondersteunt het gebruik van schema&#39;s die op andere klassen zijn gebaseerd niet.

Het systeem onderhoudt een geval van elk klantenprofiel, die gegevens samenvoegen om een &quot;enige bron van waarheid&quot;voor het individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsschema&quot;wordt bekend (die soms als &quot;verenigingsmening wordt bedoeld). Een verenigingsschema voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel schema uitvoeren.  Wanneer het samenstellen van een schema gebruikend UI of API, kunt u het schema voor gebruik met het Profiel van de Klant in real time toelaten en het etiketteren voor opneming in de unie. Het gelabelde schema neemt dan deel aan de schemadefinitie die aan Profiel wordt doorgegeven.

Als [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent] gegevens worden opgenomen in het meer van Gegevens, het Real-time Profiel van de Klant neemt om het even welke gegevens in die voor zijn gebruik zijn toegelaten. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

[!UICONTROL XDM Individual Profile] gegevens helpen acties te informeren en in staat te stellen via elk kanaal of Adobe-productintegratie. Als deze gegevens worden gecombineerd met een rijke geschiedenis van gedrags- en interactiegegevens, kunnen ze worden gebruikt om het leren van machines te stimuleren. De Real-time API van het Profiel van de Klant kan ook worden gebruikt om de functionaliteit van derdeoplossingen, CRMs, en merkgebonden oplossingen te verrijken.

Zie de [Overzicht van het realtime klantprofiel](../profile/home.md) voor meer informatie .

### Werkruimte voor gegevenswetenschap

Adobe Experience Platform Data Science Workspace maakt gebruik van machinaal leren en kunstmatige intelligentie om inzicht te krijgen in gegevens die in Experience Platform zijn opgeslagen. De Werkruimte van de Wetenschap van gegevens staat gegevenswetenschappers toe om recepten te bouwen die op worden gebaseerd [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent] gegevens over klanten en hun activiteiten, die voorspellingen zoals het kopen van neiging vergemakkelijken en aanbevolen aanbiedingen die de betrokkene waarschijnlijk zal waarderen en gebruiken.

Met de Werkruimte van de Wetenschap van Gegevens, kunnen de gegevenswetenschappers intelligente dienst gemakkelijk creëren APIs aangedreven door machine het leren. Deze services werken samen met andere Adobe-oplossingen, zoals Adobe Target en Adobe Analytics Cloud, om u te helpen persoonlijke, doelgerichte digitale ervaringen te automatiseren.

Zie voor meer informatie over het gebruik van Experience Platform-gegevens voor energieinzichten de [Overzicht van de Data Science Workspace](../data-science-workspace/home.md).

## Volgende stappen en extra bronnen

Nu u beter de rol van schema&#39;s door Experience Platform begrijpt, bent u bereid om uw te beginnen samenstellen.

Om ontwerpprincipes en beste praktijken voor het samenstellen van schema&#39;s te leren die met Experience Platform moeten worden gebruikt, begin door te lezen [grondbeginselen van de schemacompositie](schema/composition.md). Voor geleidelijke instructies op hoe te om een schema tot stand te brengen, zie de leerprogramma&#39;s bij het creëren van een schema [API gebruiken](tutorials/create-schema-api.md) of [de gebruikersinterface gebruiken](tutorials/create-schema-ui.md).

Om uw inzicht in [!DNL XDM System] bekijk de volgende video in Experience Platform:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
