---
title: Adobe Experience Platform Release Notes November 2019
description: De release van november 2019 bevat notities voor Adobe Experience Platform.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '1887'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 18 november 2019**

Nieuwe functies in Adobe Experience Platform:
* [[!DNL Real-time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Updates voor bestaande functies:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-time Customer Data Platform] {#rtcdp}

De Real-time Customer Data Platform (Real-Time CDP) is gebaseerd op Adobe Experience Platform en helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen te activeren met intelligente beslissingen gedurende de hele reis van de klant. CDP in real time combineert veelvoudige bronnen van ondernemingsgegevens om verenigde profielen in real time tot stand te brengen die kunnen worden gebruikt om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

[!DNL Real-time Customer Data Platform] omvat hulpmiddelen voor gegevensbeheer, identiteitsbeheer, geavanceerde segmentatie en gegevenswetenschap zodat u profielen kunt maken en het publiek kunt definiëren, en rijke inzichten kunt afleiden terwijl u strikte beleidsregels voor gegevensbeheer kunt afdwingen.

Adobe maakt verbinding met een groot ecosysteem van partners, om nog maar te zwijgen van de native integratie met Adobe Experience Cloud, zodat u deze doelgroepen naadloos kunt activeren en klanten overal goede ervaringen kunt bieden, van on-site of in-app personalisatie tot e-mail, betaalde media, callcenters, aangesloten apparaten en nog veel meer.

Met CDP in real time, kunt u:

* Zorg voor één weergave van uw klant met een stroomsgewijze verzameling van klantgegevens in de hele onderneming.
* Profielen op verantwoordelijke wijze beheren met vertrouwde governance en privacyopties voor bekende en onbekende id&#39;s.
* Maak actionable inzichten en schaal publiek met AI en machine leren aangedreven door Adobe Sensei en gebouwd voor marketers.
* Lever gepersonaliseerde ervaringen in real time over alle kanalen en bestemmingen.

Zie voor meer informatie de [Real-time Customer Data Platform-documentatie](../../rtcdp/overview.md).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| Doelen | Vooraf gebouwde integratie met bestemmingsplatforms die door Adobe worden gesteund [!DNL Real-time Customer Data Platform] die gegevens op een naadloze manier aan die partners activeren. Zie [Doelen](#destinations) hieronder voor meer informatie . |
| Metrisch dashboard voor startpagina | De homepage van Real-time Customer Data Platform (Real-time CDP) omvat een metriek dashboard dat informatie over profielen en segmenten toont. De homepage bevat ook koppelingen naar leermaterialen. Zie de sectie over [Real-time Customer Data Platform-meetgegevens](#real-time-customer-data-platform-metrics) hieronder. |
| Bronnen | U kunt gegevens van een verscheidenheid van bronnen zoals de Oplossingen van Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw CRM opnemen. Zie de [Bronnen](#sources) hieronder voor meer informatie. |

**[!DNL Real-time Customer Data Platform]cijfers**

De Real-time Customer Data Platform-startpagina (Real-time CDP), die een metriek-dashboard bevat, wordt weergegeven wanneer u zich aanmeldt bij Real-time CDP.

De homepage is slechts een van de plaatsen waar metrische kaarten verschijnen. CDP in real time verstrekt metrische kaarten door uw ervaring. Deze metriek informeren u over de gegevens, het profiel, en het segmentpubliek in het systeem.

Als er geen gegevens in het systeem zijn wanneer u login aan CDP in real time, verschijnt het dashboard op de homepage niet. In dit geval biedt de startpagina leermateriaal voor een eerste gebruikerservaring. Terwijl gegevens worden verzameld, wordt het dashboard automatisch bijgewerkt om informatie over die gegevens weer te geven.

Zie voor meer informatie de [Overzicht van Real-time Customer Data Platform-meetgegevens](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die door Real-time Customer Data Platform van Adobe worden gesteund die gegevens aan die partners op een naadloze manier activeren. Lees voor meer informatie de [Overzicht van doelen](../../destinations/home.md) artikel.

**Beschikbare bestemmingen**

Met de versie van November, steunt Adobe Real-time Customer Data Platform de volgende bestemmingen:

* Reclame: [!DNL Google]
* E-mailmarketing: Adobe Campaign [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Zie de [doelcatalogus](../../destinations/catalog/overview.md) voor informatie over elk van de bestemmingen.

**Bekende beperkingen**

* Het besturingselement voor aangepaste activeringsschema&#39;s in de activeringsstroom (stap Planning) is niet beschikbaar bij de eerste release.
* Er is momenteel geen manier om een bestemmingsconfiguratie uit te geven of te schrappen. Als u deze beperking wilt omzeilen, kunt u het doel in de rechterbovenhoek van het dialoogvenster [pagina met doelgegevens](../../destinations/ui/destination-details-page.md).
* Er is momenteel geen validatie voor accountdetails, paden of referenties wanneer verbinding wordt gemaakt met uw doel- of opslagaccount. Controleer of u de juiste referenties invoert en dubbelklik op spelfouten of typefouten.
* Er zijn geen referentie-verlengingen beschikbaar bij de eerste release. Als een account is verlopen of moet worden vernieuwd, moet u een nieuwe doelverbinding maken en de eerder toegewezen segmenten opnieuw toewijzen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens van een verscheidenheid van bronnen zoals de Oplossingen van Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ---------- | ------------ |
| Broninterface | Nieuwe gebruikersinterface voor het maken, weergeven en beheren van bronverbindingen. |
| Herziene workflows voor CRM-connectors | Nieuwe intuïtieve UI-workflow voor het maken en beheren van [!DNL Microsoft Dynamics] en [!DNL Salesforce] connectors. |
| Connectorondersteuning voor op cloud gebaseerde opslagsystemen | Connectors hebben nu toegang tot op de cloud gebaseerde opslagsystemen. Nieuwe bronnen omvatten [!DNL Amazon S3], [!DNL Azure Blob]en FTP-/SFTP-servers. |

**Bekende problemen**

* Bronconnectors voor op cloud gebaseerde opslagsystemen ondersteunen het opnemen van gecomprimeerde bestanden niet.

Voor meer informatie over bronnen raadpleegt u [Overzicht van bronnen](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Adobe Experience Platform [!DNL Data Science Workspace] stelt gegevenswetenschappers in staat om naadloos inzichten van gegevens en inhoud over Adobe toepassingen en derdesystemen te produceren door de Modellen van het Leren van de Machine te bouwen en te exploiteren. [!DNL Data Science Workspace] is nauw geïntegreerd met [!DNL Platform] en maakt de levenscyclus van de end-to-end gegevenswetenschap mogelijk, inclusief de exploratie en voorbereiding van XDM-gegevens, gevolgd door de ontwikkeling en de operationele implementatie van Modellen om automatisch te verrijken [!DNL Real-time Customer Profile] met Inzichten van het leren van de machine.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Toegang tot gegevens met [!DNL Platform] SDK | De vooraf gebouwde Ontvangers en lanceerlaptops in [!DNL Python] nu gebruiken [!DNL Platform] SDK voor toegang tot gegevens. |
| Ondersteuning voor sandboxen | Ondersteuning voor aanstaande sandboxfunctionaliteit (momenteel in bèta), waaronder de mogelijkheid om laptops en recept te isoleren in ontwikkelings- of productiesandboxen. Zie de [sandboxen, overzicht](../../sandboxes/home.md) voor meer informatie . |

Zie voor meer informatie de [Overzicht van de Data Science Workspace](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| ---------- | ------------ |
| Meldingsschema | Nieuw schema dat berichtgegevens vertegenwoordigt die tijdens het proces van gegevensopname worden verzonden. |
| Adobe AdCloud-DSP | Er zijn vijf nieuwe schema&#39;s toegevoegd voor de metagegevens van Adobe Advertising Cloud-platforms (DSP) voor de vraagzijde: Plaatsing, campagne, pakket, adverteerder, account. |
| ExperienceEvent Implementatie - Detailschema, veldgroepen | Nieuwe ExperienceEvent-veldgroepen die een standaardveld toevoegen voor het opslaan van informatie over de software die wordt gebruikt om de gebeurtenis te verzamelen. |
| [!DNL Profile Privacy] veldgroepen | Nieuwe profielveldgroepen die velden toevoegen voor het accepteren van algemene out- en verkoop/delen-uitschakelsignalen voor [!DNL Real-time Customer Profile]. |
| Opmaakbeperkingen voor `xdm:alternateDisplayInfo` | De velden Titel en Beschrijving voor `xdm:alternateDisplayInfo` moeten beide tekenreeksen zijn om validatie door te geven. |
| Naam wijzigen: XDM [!DNL Individual Profile] | De &quot;titel&quot; van de &quot;XDM&quot; [!DNL Profile]De klasse &quot; is bijgewerkt naar &quot;XDM [!DNL Individual Profile]&quot;. De formele `$id` van de klasse is niet gewijzigd. |

**Bekende problemen**

* Geen.

Meer informatie over het werken met XDM [!DNL Schema Registry] API en [!DNL Schema Editor] gebruikersinterface, lees de [XDM System-documentatie](../../xdm/home.md).

## [!DNL Real-time Customer Profile] {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met [!DNL Real-time Customer Profile], kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. [!DNL Profile] staat u toe om uw ongelijke klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen voor [!DNL Profile] opzoeken | Gebruikers kunnen nu profielen opzoeken met behulp van referentiebeschrijvingen en verwante entiteiten. |
| Gegevens voor een bepaalde gegevensset opschonen | Gebruikers kunnen nu gegevens voor een bepaalde gegevensset of batch verwijderen met behulp van de [!DNL Profile] System Jobs API. |
| Rand [!DNL Profile] queryverbeteringen | Toepassingen kunnen nu zoeken naar Edge [!DNL Profile] door een van de identiteiten van een bepaald profiel. |
| Samenvoegbeleid per projectie configureren | Toepassingen kunnen nu samenvoegingsbeleid per projectie configureren om een weergave van de gegevens te genereren zoals deze wordt bepaald door een specifiek samenvoegingsbeleid. |
| Berekende kenmerken | Berekende kenmerken berekenen automatisch de waarde van velden op basis van andere waarden, berekeningen en expressies. Op profielniveau worden de berekende kenmerken gebruikt om waarden zoals &quot;totale aankoop&quot;, &quot;levenslange waarde&quot; of &quot;treinstatus&quot; samen te voegen op basis van een binnenkomende gebeurtenis, een binnenkomende gebeurtenis en profielgegevens of een binnenkomende gebeurtenis, profielgegevens en historische gebeurtenissen. |

**Bugfixes**

* Vereenvoudigde lijst met beschikbare strategieën voor het stikken van id&#39;s in de workflow voor het maken van beleid voor samenvoegen.

**Bekende problemen**

* Geen.

Voor meer informatie over [!DNL Real-time Customer Profile], met inbegrip van zelfstudies en aanbevolen procedures voor het werken met [!DNL Profile] gegevens, lees de [Overzicht van realtime-klantprofiel](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] verstrekt een gebruikersinterface en RESTful API die u toestaat om segmenten te bouwen en publiek van uw te produceren [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe-toepassing.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

| Functie | Beschrijving |
| -----------| ---------- |
| Geplande segmentatie | De gebruikers kunnen geplande segmentevaluatie voor alle segmenten via UI en API nu toelaten. Zodra toegelaten, zullen alle segmenten eenmaal per dag worden geëvalueerd. Dit heeft geen invloed op de segmenteringsmogelijkheden op aanvraag die nog steeds werken zoals voorheen.<br/><br/>Opmerking: De geplande segmentatiefunctie kan niet worden gebruikt in sandboxen met meer dan vijf samenvoegbeleidsregels voor [!DNL XDM Individual Profile]. |
| Streaming segmentering | De steun voor ononderbroken evaluatie van segmenten (het stromen segmentatie) laat de meeste segmentregels toe om worden geëvalueerd aangezien de gegevens overgaan in [!DNL Platform]. Deze eigenschap betekent dat het segmentlidmaatschap bijgewerkt zal zijn zonder de behoefte om geplande segmentatietaken in werking te stellen. Sommige uitzonderingen zijn van toepassing, zoals segmenten die relaties met meerdere entiteiten gebruiken of met verrijkte nuttige lasten. |
| Segmenten als bouwstenen | Wanneer het creëren van segmenten gebruikend de Bouwer UI van het Segment, kunnen de gebruikers eerder-bepaalde segmenten als bouwstenen voor extra segmenten nu gebruiken. <ul><li>Huidig publiekslidmaatschap van referentie: updates wanneer mensen zich binnen en buiten het publiek bewegen.</li><li>Logica kopiëren: Neem de geselecteerde segmentdefinitie en dupliceer het in het nieuwe segment.</li></ul> |
| Segmentlidmaatschap weergeven op naamruimte ID | Segmentlidmaatschap kan nu worden weergegeven door naamruimte ID (e-mail, ECID en totale telling). |
| RBAC-ondersteuning | De Bouwer van het segment verleent nu steun voor basisop rol-gebaseerde toegangscontroles en toestemmingen. |
| Verbeterde ondersteuning voor het delen van externe doelgroepen tussen [!DNL Platform] en Adobe-oplossingen | Gebruikers kunnen nu externe (niet-[!DNL Experience Platform]) metagegevens voor het publiek in scenario&#39;s waarin het aantal doelgroepen groot of niet a priori bekend is. Deze release omvat toegang tot [!DNL Audience Manager] meta-gegevens voor klanten die de oplossingsschakelaar hebben geleverd. Deze publieksmeta-gegevens kunnen binnen de Bouwer van het Segment worden gebruikt om nieuwe [!DNL Experience Platform] segmenten. <br/><br/> Daarnaast worden segmenten gemaakt in [!DNL Experience Platform] is nu beschikbaar voor gebruik in geïntegreerde Adobe-oplossingen, waaronder [!DNL Audience Manager], [!DNL Target], en [!DNL Ad Cloud]. |

**Bugfixes**

* Probleem verholpen waarbij profielen van meerdere entiteiten werden geretourneerd als geneste relaties werden gebruikt.
* Probleem opgelost waarbij de uitsluitingslogica tot misleidende resultaten leidde.
* Verbeterde leesbaarheid voor mappen met meerdere entiteiten. Ze tonen nu de vriendelijke naam van de klasse XDM.
* Probleem verholpen waarbij meerdere kopieën van dezelfde XDM-map werden weergegeven.
* Het bericht wordt nu geproduceerd om een gebruiker te informeren als de segmentramingen voor het geselecteerde fusiebeleid niet beschikbaar zijn.

**Bekende problemen**

* Geen.

Meer informatie over [!DNL Segmentation Service], lees de [Overzicht van segmentatieservice](../../segmentation/home.md).
