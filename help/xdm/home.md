---
keywords: Experience Platform;home;populaire onderwerpen;XDM;XDM-systeem;XDM individueel profiel;XDM ExperienceEvent;XDM Experience Event;ExperienceEvent;ExperienceEvent;Field-groepen;field-groep;Field-groep;ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;experienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;XDM ExperienceEvent;ExperienceDataModel;DataModel;DataModel;Schema-register;schema-bibliotheek;Schema-bibliotheek;schema;recordgegevens;tijdreeks;tijdreeks
solution: Experience Platform
title: XDM-systeemoverzicht
description: Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. Het Model van Gegevens van de ervaring (XDM), dat door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema's voor het beheer van de klantenervaring te bepalen.
exl-id: 294d5f02-850f-47ea-9333-8b94a0bb291e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2095'
ht-degree: 0%

---

# XDM System, overzicht

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter Adobe Experience Platform. Het Model van Gegevens van de ervaring (XDM), dat door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities die om het even welke toepassing toestaan om met de diensten van Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier kan leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden uitdrukken.

XDM is het basiskader dat Adobe Experience Cloud, aangedreven door Experience Platform, toestaat om het juiste bericht aan de juiste persoon, op het juiste kanaal, op het juiste moment te leveren. De methodologie waarop Experience Platform, het Systeem van XDM, wordt gebouwd exploiteert de Modelschema&#39;s van de Gegevens van de Ervaring voor gebruik door de diensten van Experience Platform.

Meer informatie over de rol van XDM System in Experience Platform.

## XDM-schema&#39;s {#xdm-schemas}

Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en zo waarde te verkrijgen van gegevens.

Voordat gegevens in Experience Platform kunnen worden ingevoerd, moet een schema zijn samengesteld om de gegevensstructuur te beschrijven en om beperkingen te bieden aan het type gegevens dat binnen elk veld kan worden opgenomen. De schema&#39;s bestaan uit een basisklasse en nul of meer groepen van het schemagebied.

Voor meer informatie over het model van de schemacompositie, met inbegrip van ontwerpprincipes, en beste praktijken, zie de [ grondbeginselen van schemacompositie ](schema/composition.md).

### Standaard XDM-componenten {#Standard-xdm-components}

XDM verstrekt een robuuste inzameling van standaardgebiedsgroepen en gegevenstypes, die bedoeld zijn om gemeenschappelijke concepten en gebruiksgevallen over verschillende industrieën te vangen. Met Experience Platform kunt u deze componenten filteren op branche, zodat u snel en op een betrouwbare manier schema&#39;s kunt maken die het beste uw specifieke bedrijfsbehoeften ondersteunen.

Wanneer het construeren van schema&#39;s in Experience Platform UI, worden de vermelde gebiedsgroepen getoond met populariteit metrisch. Deze maatstaf wordt bepaald door hoe vaak andere Experience Platform-gebruikers de veldgroep in hun schema&#39;s gebruiken. Hoe hoger het getal, hoe populairder de veldgroep. Standaard worden de resultaten weergegeven van populairste tot minst populaire gegevens, zodat u op de hoogte blijft van trends in de modellering van gegevens in uw branche.

![ de populariteitskolom van de [!UICONTROL Add field group] dialoog.](./images/overview/popularity.png)

### [!DNL Schema Library] {#schema-library}

Experience Platform biedt een gebruikersinterface en RESTful-API waarmee u alle schemagerelateerde bronnen in de Experience Platform **[!DNL Schema Library]** kunt weergeven en beheren. [!DNL Schema Library] bevat standaard XDM componenten die door Adobe aan u ter beschikking worden gesteld, evenals middelen van de partners van Experience Platform en verkopers van wie toepassingen u gebruikt.

U kunt ook nieuwe schema&#39;s en bronnen maken en beheren die uniek zijn voor uw organisatie met de [!DNL Schema Registry API] - of [!UICONTROL Schemas] -werkruimte in de gebruikersinterface van Experience Platform.

Raadpleeg de volgende documentatie voor meer informatie over het beheren van en werken met schema&#39;s in Experience Platform:

* [XDM UI-hulplijn](./ui/overview.md)
* [Handleiding Schema Registry API](./api/overview.md)

## Gegevensgedrag in XDM-systeem {#data-behaviors}

>[!CONTEXTUALHELP]
>id="platform_schemas_behavior"
>title="Gedrag van gegevens"
>abstract="Gegevens die bestemd zijn voor gebruik in Experience Platform, worden gegroepeerd in drie gedragstypen: record, tijdreeks en ad hoc. De schema&#39;s van het verslag verstrekken informatie over de attributen van een onderwerp, terwijl de tijdreeksregelingen een momentopname van het systeem vangen op het tijdstip een actie werd genomen. Ad hoc schema&#39;s vangen gebieden die namespaced voor gebruik slechts door één enkele dataset zijn. Zie de documentatie voor meer informatie over gegevensgedrag in Experience Platform."

Gegevens die bestemd zijn voor gebruik in Experience Platform worden gegroepeerd in drie gedragstypen:

* **Verslag**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **tijd-reeks**: Verstrekt een momentopname van het systeem in de tijd dat een actie of direct of indirect door een verslagonderwerp werd genomen.
* **ad hoc**: Vangt gebieden die voor gebruik slechts door één enkele dataset worden genoemd. Ad-hocschema&#39;s worden gebruikt in verschillende gegevensinsluitingsworkflows voor Experience Platform, waaronder het innemen van CSV-bestanden en het maken van bepaalde soorten bronverbindingen.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. De klassen XDM beschrijven het kleinste aantal eigenschappen een schema moet bevatten om een bepaald gegevensgedrag te vertegenwoordigen.

Hoewel u uw eigen klassen binnen [!DNL Schema Registry] kunt definiëren, wordt u aangeraden de standaardklassen **[!UICONTROL XDM Individual Profile]** en **[!UICONTROL XDM ExperienceEvent]** te gebruiken voor record- en tijdreeksgegevens. Deze klassen worden hieronder gedetailleerder beschreven.

>[!NOTE]
>
>Er zijn geen standaardklassen op basis van het ad-hocgedrag. Ad-hoc schema&#39;s worden automatisch geproduceerd door de processen van Experience Platform die hen gebruiken, maar zij kunnen ook [ manueel worden gecreeerd gebruikend de Registratie API van het Schema ](./tutorials/ad-hoc.md).

### [!UICONTROL XDM Individual Profile] {#xdm-individual-profile}

[!UICONTROL XDM Individual Profile] is een op records gebaseerde klasse die een unieke weergave vormt van de kenmerken van zowel geïdentificeerde als gedeeltelijk geïdentificeerde onderwerpen. De profielen die hoogst worden geïdentificeerd kunnen voor persoonlijke mededelingen of gerichte overeenkomsten worden gebruikt. Hooggeïdentificeerde profielen kunnen gedetailleerde persoonlijke gegevens bevatten zoals naam, geslacht, geboortedatum, locatie en contactgegevens, zoals telefoonnummers en e-mailadressen.

Minder geïdentificeerde profielen kunnen alleen uit anonieme gedragssignalen bestaan, zoals browsercookies. In dit geval worden de gegevens van het verspreide profiel gebruikt om een informatiebasis te bouwen waarin de belangen en voorkeuren van het anonieme profiel worden gesorteerd en opgeslagen. Deze id&#39;s kunnen in de loop der tijd gedetailleerder worden naarmate het onderwerp zich aanmeldt voor meldingen, abonnementen, aankopen, enzovoort. Deze toename van profielkenmerken kan uiteindelijk resulteren in een bepaald onderwerp en een hogere mate van gerichte betrokkenheid mogelijk maken.

Naarmate een profiel blijft groeien, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identificatiegegevens, contactgegevens en communicatievoorkeuren van een individu.

Zie de [[!UICONTROL XDM Individual Profile] verwijzingsgids ](./classes/individual-profile.md) voor meer informatie over de structuur en het gebruik-geval van de gebieden die door de klasse worden verstrekt.

### [!UICONTROL XDM ExperienceEvent] {#xdm-experience-event}

XDM ExperienceEvent is een op tijdreeksen gebaseerde klasse die wordt gebruikt om de status van het systeem vast te leggen wanneer een gebeurtenis (of set gebeurtenissen) heeft plaatsgevonden, inclusief het tijdstip en de identiteit van het betreffende onderwerp. De gebeurtenissen van de ervaring zijn onveranderlijk, feitelijke verslagen van wat op dat ogenblik voorkwam, die wat vormden zonder samenvoeging of interpretatie. Zij zijn kritiek voor tijd-domein analyses aangezien zij kunnen worden gebruikt om veranderingen te analyseren die in een bepaald venster van tijd voorkomen, en tussen veelvoudige vensters van tijd te vergelijken om trends te volgen.

De Gebeurtenissen van de ervaring kunnen of expliciet of impliciet zijn. Expliciete gebeurtenissen zijn direct waarneembare menselijke acties die plaatsvinden tijdens een punt op een reis. Impliciete gebeurtenissen zijn gebeurtenissen die worden opgeworpen zonder directe menselijke actie, maar die nog steeds betrekking hebben op een individu. Voorbeelden van impliciete gebeurtenissen zijn onder meer het geplande verzenden van e-mailnieuwsbrieven of batterijspanning die een bepaalde drempelwaarde bereiken.

Hoewel niet alle gebeurtenissen gemakkelijk over alle gegevensbronnen worden gecategoriseerd, is het uiterst waardevol om gelijkaardige gebeurtenissen in gelijkaardige types te harmoniseren waar mogelijk voor verwerking.

![ Infographic van de Reis van de Klant die met ervaringsgebeurtenissen in tijd wordt visualiseerd.](images/overview/experience-event-journey.png)

Zie de [[!UICONTROL XDM ExperienceEvent] verwijzingsgids ](./classes/experienceevent.md) voor meer informatie over de structuur en het gebruik-geval van de gebieden die door de klasse worden verstrekt.

## XDM-schema&#39;s en Experience Platform-services {#schemas-and-platform-services}

Experience Platform is schema-agnostisch, betekenend dat om het even welk schema dat aan de norm voldoet XDM ter beschikking wordt gesteld aan de diensten van Experience Platform. De manieren waarop verschillende Experience Platform-services schema&#39;s gebruiken, worden hieronder nader beschreven.

### Catalogusservice, gegevensinsluiting en datumpeer {#ingestion-catalog-and-storage}

Catalogusservice is het systeem van registratie voor Experience Platform-middelen en de bijbehorende schema&#39;s. Catalog bevat niet de feitelijke gegevensbestanden of directory&#39;s, maar wel de metagegevens en beschrijvingen van die bestanden en mappen.

Catalogusgegevens worden opgeslagen in het datumpigment, een zeer granulaire gegevensopslag die alle gegevens bevat die door Experience Platform worden beheerd, ongeacht de oorsprong of bestandsindeling.

Om met het opnemen van gegevens in Experience Platform te beginnen, kunt u de Dienst van de Catalogus gebruiken om een dataset tot stand te brengen. De dataset verwijst naar een XDM-schema dat de structuur van de gegevens beschrijft die moeten worden opgenomen. Als een dataset zonder een schema wordt gecreeerd, leidt Experience Platform een &quot;waargenomen schema&quot;af door het type en de inhoud van opgenomen gegevensgebieden te inspecteren. Datasets worden vervolgens bijgehouden in de Catalogusservice en opgeslagen in het datumpomeer naast de schema&#39;s en waargenomen schema&#39;s waarop ze zijn gebaseerd.

Zie het [ overzicht van de Dienst van de Catalogus ](../catalog/home.md) voor meer informatie. Zie het [ overzicht van de Ingestie van Gegevens ](../ingestion/home.md) voor meer informatie over de Ingestie van Gegevens van Adobe Experience Platform.

### Query-service {#query-service}

U kunt standaard SQL gebruiken om Experience Platform-gegevens te vragen ter ondersteuning van vele verschillende gebruiksgevallen met Adobe Experience Platform Query Service.

Nadat een schema is samengesteld en een dataset is gecreeerd die verwijzingen dat schema, wordt het gegeven dan ingebed en opgeslagen in het gegevensmeer. U kunt de Dienst van de Vraag dan gebruiken om zich bij om het even welke datasets in het gegevensmeer aan te sluiten en de vraagresultaten als nieuwe dataset voor gebruik in rapportering, machine het leren, of opname in het Profiel van de Klant in real time te vangen.

Verwijs naar het [ overzicht van de Dienst van de Vraag ](../query-service/home.md) voor meer informatie over de dienst.

### Realtime-klantenprofiel {#real-time-customer-profile}

Het profiel van de Klant in real time verstrekt een gecentraliseerd consumentenprofiel voor gericht en gepersonaliseerd ervaringsbeheer. Elk profiel bevat gegevens die op alle systemen zijn geaggregeerd en actioneerbare tijdstempelaccounts bevatten van gebeurtenissen die het onderwerp van het profiel betreffen. Deze gebeurtenissen kunnen hebben plaatsgevonden in elk systeem dat u gebruikt met Experience Platform.

In real time het Profiel van de Klant verbruikt schema-geformatteerde gegevens die op de [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent] klassen worden gebaseerd, en antwoordt aan vragen die op die gegevens worden gebaseerd.

Het systeem onderhoudt een geval van elk klantenprofiel, die gegevens samenvoegen om een &quot;enige bron van waarheid&quot;voor het individu te vormen. Deze verenigde gegevens worden vertegenwoordigd gebruikend wat als &quot;verenigingsschema&quot;wordt bekend (die soms als &quot;verenigingsmening wordt bedoeld). Een verenigingsschema voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkel schema uitvoeren. Wanneer het samenstellen van een schema gebruikend UI of API, kunt u het schema voor gebruik met het Profiel van de Klant in real time toelaten en het etiketteren voor opneming in de unie. Het gelabelde schema neemt dan deel aan de schemadefinitie die aan Profiel wordt doorgegeven.

Aangezien [!UICONTROL XDM Individual Profile] en [!UICONTROL XDM ExperienceEvent] gegevens in het gegevensmeer worden opgenomen, neemt het Profiel van de Klant in real time om het even welke gegevens op die voor zijn gebruik zijn toegelaten. Hoe meer interacties en details worden opgenomen, hoe robuuster de afzonderlijke profielen worden.

Met [!UICONTROL XDM Individual Profile] -gegevens kunt u acties via elk kanaal of via Adobe-productintegratie informeren en inschakelen. Als deze gegevens worden gecombineerd met een rijke geschiedenis van gedrags- en interactiegegevens, kunnen ze worden gebruikt om het leren van machines te stimuleren. De real-time API van het Profiel van de Klant kan ook worden gebruikt om de functionaliteit van derdeoplossingen, CRMs, en merkgebonden oplossingen te verrijken.

Zie het [ overzicht van het Profiel van de Klant in real time ](../profile/home.md) voor meer informatie.

### Data Science-werkruimte {#data-science-workspace}

>[!NOTE]
>
>Data Science Workspace kan niet meer worden aangeschaft. Deze documentatie is bedoeld voor bestaande klanten met eerdere rechten op Data Science Workspace.

Adobe Experience Platform Data Science Workspace maakt gebruik van machinaal leren en kunstmatige intelligentie om inzichten te verkrijgen uit gegevens die in Experience Platform zijn opgeslagen. Data Science Workspace stelt wetenschappers in staat recepten te bouwen op basis van [!UICONTROL XDM Individual Profile] - en [!UICONTROL XDM ExperienceEvent] -gegevens over klanten en hun activiteiten. Deze recepten maken voorspellingen mogelijk, zoals het kopen van neiging en aanbevolen aanbiedingen die de betrokkene waarschijnlijk zal waarderen en gebruiken.

Met Data Science Workspace kunnen gegevenswetenschappers eenvoudig intelligente service-API&#39;s maken die aangedreven worden door machinaal leren. Deze services werken samen met andere Adobe-oplossingen, waaronder Adobe Target en Adobe Analytics Cloud, om u te helpen persoonlijke, doelgerichte digitale ervaringen te automatiseren.

Voor meer informatie bij het gebruiken van de gegevens van Experience Platform aan machtsinzichten, zie het [ overzicht van Workspace van de Wetenschap van Gegevens ](../data-science-workspace/home.md).

## Volgende stappen en extra bronnen

Nu je de rol van schema&#39;s in Experience Platform beter begrijpt, ben je klaar om je eigen schema&#39;s samen te stellen.

Om ontwerpprincipes en beste praktijken voor het samenstellen van schema&#39;s te leren die met Experience Platform moeten worden gebruikt, begin door de [ grondbeginselen van schemacompositie ](schema/composition.md) te lezen. Voor geleidelijke instructies op hoe te om een schema tot stand te brengen, zie de leerprogramma&#39;s bij het creëren van een schema [ gebruikend API ](tutorials/create-schema-api.md) of [ gebruikend het gebruikersinterface ](tutorials/create-schema-ui.md).

Bekijk de volgende video om uw begrip van [!DNL XDM System] in Experience Platform te versterken:

>[!VIDEO](https://video.tv.adobe.com/v/27105?quality=12&learn=on)
