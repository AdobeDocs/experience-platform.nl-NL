---
title: Opmerkingen bij de release Adobe Experience Platform
description: Opmerkingen bij de release Experience Platform van 18 november 2019
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Opmerkingen bij de release Adobe Experience Platform

## Releasedatum: 18 november 2019

Nieuwe releases:
* [Gegevensplatform voor realtime klanten](#real-time-customer-data-platform)
* [Doelen](#destinations)
* [Bronnen](#sources)

Updates voor bestaande functies:
* [Werkruimte voor gegevenswetenschap](#data-science-workspace)
* [XDM-systeem (Experience Data Model)](#experience-data-model-xdm-system)
* [Klantprofiel in realtime](#real-time-customer-profile)
* [Segmenteringsservice](#segmentation-service)

## Gegevensplatform voor realtime klanten

Dankzij het Adobe Real-Time Customer Data Platform (CDP in realtime), dat is gebaseerd op het Adobe Experience Platform, kunnen bedrijven bekende en onbekende gegevens samenbrengen om klantprofielen te activeren en tijdens de reis van de klant intelligent te beslissen. CDP in real time combineert veelvoudige bronnen van ondernemingsgegevens om verenigde profielen in real time tot stand te brengen die kunnen worden gebruikt om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

Het platform van de Gegevens van de Klant in real time omvat hulpmiddelen voor gegevensbeheer, identiteitsbeheer, geavanceerde segmentatie, en gegevenswetenschap zodat u profielen kunt bouwen en publiek bepalen, evenals rijke inzichten af te leiden terwijl het kunnen strikte beleid van het gegevensbeheer afdwingen.

Adobe maakt verbinding met een groot ecosysteem van partners, om nog maar te zwijgen van native integratie met Adobe Experience Cloud, zodat u dit publiek naadloos kunt activeren en klanten overal een geweldige ervaring kunt bieden, van on-site of in-app personalisatie tot e-mail, betaalde media, callcenters, verbonden apparaten en nog veel meer.

Met CDP in real time, kunt u:

* Zorg voor één weergave van uw klant met een stroomsgewijze verzameling van klantgegevens in de hele onderneming.
* Beheer profielen op verantwoordelijke wijze met vertrouwde governance en privacycontroles voor bekende en onbekende id&#39;s.
* Genereer activeerbare inzichten en schaal publiek met AI en machine leren aangedreven door Adobe Sensei en gebouwd voor marketers.
* Lever gepersonaliseerde ervaringen in real time over alle kanalen en bestemmingen.

Raadpleeg de documentatie [van het](../../rtcdp/overview.md)Adobe Real-Time Customer Data Platform voor meer informatie.

### Belangrijkste kenmerken

| Functie | Beschrijving |
|---|---|
| Doelen | Vooraf gebouwde integratie met doelplatforms die worden ondersteund door het realtime klantgegevensplatform van Adobe dat gegevens naadloos aan die partners activeert. Zie [Doelen](#destinations) hieronder voor meer informatie. |
| Metrisch dashboard voor startpagina | De homepage van het Platform van de Gegevens van de Klant van Adobe In real time (CDP in real time) omvat een metriek dashboard dat informatie over profielen en segmenten toont. De homepage bevat ook koppelingen naar leermaterialen. Zie de sectie over de [gegevens](#real-time-customer-data-platform-metrics) van het platform van de Gegevens van de Klant in real time hieronder. |
| Bronnen | U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe Solutions, cloudopslag, software van derden en uw CRM. Zie de sectie [Bronnen](#sources) hieronder voor meer informatie. |

### Metrische gegevens van het platform van de Gegevens van de Klant in real time

De homepage van het Platform van de Gegevens van de Klant van Adobe In real time (CDP in real time), die een metriek dashboard omvat, verschijnt wanneer u login aan CDP in real time.

De homepage is slechts een van de plaatsen waar metrische kaarten verschijnen. CDP in real time verstrekt metrische kaarten door uw ervaring. Deze metriek informeren u over de gegevens, het profiel, en het segmentpubliek in het systeem.

Als er geen gegevens in het systeem zijn wanneer u login aan CDP in real time, verschijnt het dashboard op de homepage niet. In dit geval biedt de startpagina leermateriaal voor een eerste gebruikerservaring. Terwijl gegevens worden verzameld, wordt het dashboard automatisch bijgewerkt om informatie over die gegevens weer te geven.

Voor meer informatie, zie het de metriek van het Platform van Gegevens van de [Klant in real time](../../rtcdp/home-page-dashboards.md)

## Doelen

Doelen zijn vooraf gebouwde integraties met doelplatforms die worden ondersteund door het realtime klantgegevensplatform van Adobe en die gegevens naadloos aan die partners activeren. Lees het overzichtsartikel [](../../rtcdp/destinations/destinations-overview.md) Doelen voor meer informatie.

### Beschikbare bestemmingen

Met de release van november ondersteunt het Real-time Customer Data Platform van Adobe de volgende doelen:

* Reclame: Google
* E-mailmarketing: Adobe Campagne, Salesforce Marketing Cloud, Oracle Responsys, Oracle Eloqua

Zie de [bestemmingscatalogus](../../rtcdp/destinations/destinations-catalog.md) voor informatie over elk van de bestemmingen.

### Bekende beperkingen

* Het besturingselement voor aangepaste activeringsschema&#39;s in de [activeringsstroom](../../rtcdp/destinations/activate-destinations.md#activate-data) (stap Planning) is niet beschikbaar bij de eerste release.
* Er is momenteel geen manier om een bestemmingsconfiguratie uit te geven of te schrappen. Als u deze beperking wilt omzeilen, kunt u het doel in de rechterbovenhoek van de pagina [met](../../rtcdp/destinations/destination-details-page.md)doeldetails in- of uitschakelen.
* Er is momenteel geen validatie voor accountdetails, paden of referenties wanneer verbinding wordt gemaakt met uw doel- of opslagaccount. Controleer of u de juiste referenties invoert en dubbelklik op spelfouten of typefouten.
* Er zijn geen referentie-verlengingen beschikbaar bij de eerste release. Als een account is verlopen of moet worden vernieuwd, moet u een nieuwe doelverbinding maken en de eerder toegewezen segmenten opnieuw toewijzen.

## Bronnen

Met het Adobe Experience Platform kunt u gegevens uit externe bronnen ophalen en tegelijk die gegevens structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens invoeren uit verschillende bronnen, zoals Adobe Solutions, cloudopslag, software van derden en uw CRM-systeem.

Het Platform van de ervaring verstrekt RESTful API en een interactieve UI die u bronverbindingen voor diverse gegevensleveranciers met gemak laat opzetten. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

### Belangrijkste kenmerken

| Functie | Beschrijving |
| ---------- | ------------ |
| Broninterface | Nieuwe gebruikersinterface voor het maken, weergeven en beheren van bronverbindingen. |
| Herziene workflows voor CRM-connectors | Nieuwe intuïtieve UI-workflow voor het maken en beheren van Microsoft Dynamics en Salesforce-connectors. |
| Connectorondersteuning voor op cloud gebaseerde opslagsystemen | Connectors hebben nu toegang tot op de cloud gebaseerde opslagsystemen. Nieuwe bronnen zijn onder andere Amazon S3-, Azure Blob- en FTP-/SFTP-servers. |

### Bekende problemen

* Bronconnectors voor op cloud gebaseerde opslagsystemen ondersteunen het opnemen van gecomprimeerde bestanden niet.

Voor meer informatie over bronnen, zie [Bronoverzicht](../../sources/home.md).

## Werkruimte voor gegevenswetenschap

De Werkruimte van de Wetenschap van de Gegevens van het Platform van Adobe laat gegevenswetenschappers toe om inzichten van gegevens en inhoud over de toepassingen en derdesystemen van Adobe foutloos te produceren door de Modellen van het Leren van de Machine te bouwen en te exploiteren. De Werkruimte van de Wetenschap van Gegevens is strak geïntegreerd met Platform en machtigt de levenscyclus van de gegevenswetenschap van begin tot eind, met inbegrip van exploratie en voorbereiding van XDM gegevens, die door de ontwikkeling en de verrichting van Modellen wordt gevolgd om het Profiel van de Klant in real time met de Inzichten van het Leren van de Machine automatisch te verrijken.

### Nieuwe functies

| Functie | Beschrijving |
| -----------| ---------- |
| Gegevenstoegang met Platform SDK | De vooraf gebouwde Ontvangers en lanceerlaptops in Python gebruiken nu Platform SDK voor de toegang tot van gegevens. |
| Ondersteuning voor sandboxen | Ondersteuning voor aanstaande sandboxfunctionaliteit (momenteel in bèta), waaronder de mogelijkheid om laptops en recept te isoleren in ontwikkelings- of productiesandboxen. Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie. |

Voor meer informatie, zie het Overzicht [van de Werkruimte van de Wetenschap van](../../data-science-workspace/home.md)Gegevens.

## XDM-systeem (Experience Data Model)

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter het ervaringsplatform. Experience Data Model (XDM), aangestuurd door Adobe, is een poging om gegevens over klantervaring te standaardiseren en schema&#39;s voor het beheer van klantervaring te definiëren.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Deze biedt algemene structuren en definities waarmee toepassingen kunnen communiceren met services op het Adobe Experience Platform. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

### Nieuwe functies

| Functie | Beschrijving |
| ---------- | ------------ |
| Meldingsschema | Nieuw schema dat berichtgegevens vertegenwoordigt die tijdens het proces van gegevensopname worden verzonden. |
| Adobe AdCloud DSP-schema&#39;s | Er zijn vijf nieuwe schema&#39;s toegevoegd voor de weergave van DSP-metagegevens (Adobe Advertising Cloud demand-side platform): Plaatsing, campagne, pakket, adverteerder, account. |
| De vermenging van de Details van de Implementatie van de ExperienceEvent | Nieuwe ExperienceEvent-mixfunctie waarmee een standaardveld wordt toegevoegd waarin informatie wordt opgeslagen over de software die wordt gebruikt om de gebeurtenis te verzamelen. |
| Profielprivacy-mix | Nieuwe profielmix waarmee velden worden toegevoegd voor het accepteren van algemene out- en uitverkoop-/deelsignalen voor het profiel van de klant in realtime. |
| Opmaakbeperkingen voor `xdm:alternateDisplayInfo` | De velden Titel en Beschrijving `xdm:alternateDisplayInfo` moeten tekenreeksen zijn om validatie door te geven. |
| Naam wijzigen: Afzonderlijk XDM-profiel | De titel van de klasse &quot;XDM Profile&quot; is bijgewerkt naar &quot;XDM Individual Profile&quot;. De formele indeling `$id` van de klasse is niet gewijzigd. |

### Bekende problemen

* Geen.

Meer informatie over het werken met XDM gebruikend de Registratie API van het Schema en gebruikersinterface van de Redacteur van het Schema, gelieve de documentatie [van het](../../xdm/home.md)Systeem XDM te lezen.

## Klantprofiel in realtime

Met het Adobe Experience Platform kunt u een gecoördineerde, consistente en relevante ervaring voor uw klanten ontwikkelen, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen voor profielopzoekopdracht | Gebruikers kunnen nu profielen opzoeken met behulp van referentiebeschrijvingen en verwante entiteiten. |
| Gegevens voor een bepaalde gegevensset opschonen | De gebruikers kunnen gegevens voor een bepaalde dataset of een partij nu schrappen gebruikend de Banen API van het Systeem van het Profiel. |
| Verbeteringen voor Edge Profile-query | Toepassingen kunnen nu een query uitvoeren op Edge Profile door een van de identiteiten van een bepaald profiel. |
| Samenvoegbeleid per projectie configureren | Toepassingen kunnen nu samenvoegingsbeleid per projectie configureren om een weergave van de gegevens te genereren zoals deze wordt bepaald door een specifiek samenvoegingsbeleid. |
| Berekende kenmerken | Berekende kenmerken berekenen automatisch de waarde van velden op basis van andere waarden, berekeningen en expressies. Op profielniveau worden de berekende kenmerken gebruikt om waarden zoals &quot;totale aankoop&quot;, &quot;levenslange waarde&quot; of &quot;treinstatus&quot; samen te voegen op basis van een binnenkomende gebeurtenis, een binnenkomende gebeurtenis en profielgegevens of een binnenkomende gebeurtenis, profielgegevens en historische gebeurtenissen. |

### Bugfixes

* Vereenvoudigde lijst met beschikbare strategieën voor het stikken van id&#39;s in de workflow voor het maken van beleid voor samenvoegen.

### Bekende problemen

* Geen.

Lees voor meer informatie over het realtime profiel van de klant, zoals zelfstudies en aanbevolen procedures voor het werken met profielgegevens, het overzicht [van het](../../profile/home.md)realtime profiel van de klant.

## Segmenteringsservice

De Dienst van de Segmentatie van het Platform van de Ervaring van Adobe verstrekt een gebruikersinterface en RESTful API die u toestaat om segmenten te bouwen en publiek van uw gegevens van het Profiel van de Klant in real time te produceren. Deze segmenten worden centraal geconfigureerd en onderhouden op Platform, waardoor ze gemakkelijk toegankelijk zijn voor elke Adobe-toepassing.

De Dienst van de segmentatie bepaalt een bepaalde ondergroep van profielen door de criteria te beschrijven die een verhandelbare groep mensen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

| Functie | Beschrijving |
| -----------| ---------- |
| Geplande segmentatie | De gebruikers kunnen geplande segmentevaluatie voor alle segmenten via UI en API nu toelaten. Zodra toegelaten, zullen alle segmenten eenmaal per dag worden geëvalueerd. Dit heeft geen invloed op de segmenteringsmogelijkheden op aanvraag die nog steeds werken zoals voorheen.<br/><br/>Opmerking: De geplande segmentatiefunctie kan niet worden gebruikt in sandboxen met meer dan vijf samenvoegbeleidsregels voor XDM Individual Profile. |
| Streaming segmentering | De steun voor ononderbroken evaluatie van segmenten (het stromen segmentatie) laat de meeste segmentregels toe om worden geëvalueerd aangezien de gegevens in Platform overgaan. Deze eigenschap betekent dat het segmentlidmaatschap bijgewerkt zal zijn zonder de behoefte om geplande segmentatietaken in werking te stellen. Sommige uitzonderingen zijn van toepassing, zoals segmenten die relaties met meerdere entiteiten gebruiken of met verrijkte nuttige lasten. |
| Segmenten als bouwstenen | Wanneer het creëren van segmenten gebruikend de Bouwer UI van het Segment, kunnen de gebruikers eerder-bepaalde segmenten als bouwstenen voor extra segmenten nu gebruiken. <ul><li>Huidig publiekslidmaatschap van referentie: updates wanneer mensen zich binnen en buiten het publiek bewegen.</li><li>Logica kopiëren: Neem de geselecteerde segmentdefinitie en dupliceer het in het nieuwe segment.</li></ul> |
| Segmentlidmaatschap weergeven op naamruimte ID | Segmentlidmaatschap kan nu worden weergegeven door naamruimte ID (e-mail, ECID en totale telling). |
| RBAC-ondersteuning | De Bouwer van het segment verleent nu steun voor basisop rol-gebaseerde toegangscontroles en toestemmingen. |
| Verbeterde ondersteuning voor het delen van externe doelgroepen tussen Platform- en Adobe-oplossingen | Gebruikers kunnen nu metagegevens voor externe doelgroepen (niet-Experience Platform) gebruiken in scenario&#39;s waarbij het aantal doelgroepen a priori groot of onbekend is. Deze versie omvat toegang tot de meta-gegevens van de Manager van de Publiek voor klanten die de oplossingsschakelaar hebben geleverd. Deze publieksmeta-gegevens kunnen binnen de Bouwer van het Segment worden gebruikt om nieuwe segmenten van het Platform van de Ervaring tot stand te brengen. <br/><br/> Bovendien zijn segmenten die zijn gemaakt in het Experience Platform nu beschikbaar voor gebruik in geïntegreerde Adobe-oplossingen, zoals Audience Manager, Target en Ad Cloud. |

### Bugfixes

* Probleem verholpen waarbij profielen van meerdere entiteiten werden geretourneerd als geneste relaties werden gebruikt.
* Probleem opgelost waarbij de uitsluitingslogica tot misleidende resultaten leidde.
* Verbeterde leesbaarheid voor mappen met meerdere entiteiten. Ze tonen nu de vriendelijke naam van de klasse XDM.
* Probleem verholpen waarbij meerdere kopieën van dezelfde XDM-map werden weergegeven.
* Het bericht wordt nu geproduceerd om een gebruiker te informeren als de segmentramingen voor het geselecteerde fusiebeleid niet beschikbaar zijn.

### Bekende problemen

* Geen.

Meer over de Dienst van de Segmentatie leren, gelieve het overzicht [van de Dienst van de](../../segmentation/home.md)Segmentatie te lezen.