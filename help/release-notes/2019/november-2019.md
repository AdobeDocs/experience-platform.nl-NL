---
title: Aanvullende informatie voor Adobe Experience Platform, november 2019
description: Aanvullende informatie voor Adobe Experience platform, november 2019.
doc-type: release notes
last-update: November 18, 2019
author: crhoades, ens28527
exl-id: 2c417c56-cc61-4788-b248-d98ea6cf89f0
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1889'
ht-degree: 7%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: dinsdag 18 november 2019**

Nieuwe functies in Adobe Experience Platform:
* [[!DNL Real-Time Customer Data Platform]](#rtcdp)
* [[!DNL Destinations]](#destinations)
* [[!DNL Sources]](#sources)

Updates voor bestaande functies:
* [[!DNL Data Science Workspace]](#dsw)
* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Real-Time Customer Profile]](#profile)
* [[!DNL Segmentation Service]](#segmentation)

## [!DNL Real-Time Customer Data Platform] {#rtcdp}

De Real-Time Customer Data Platform (Real-Time CDP) is gebaseerd op Adobe Experience Platform en helpt bedrijven om bekende en onbekende gegevens samen te brengen om klantprofielen te activeren door middel van intelligente beslissingen gedurende de hele reis van de klant. Real-Time CDP combineert meerdere bedrijfsgegevensbronnen om uniforme profielen in real-time te maken die kunnen worden gebruikt om een-op-een gepersonaliseerde klantenervaring op alle kanalen en apparaten te bieden.

[!DNL Real-Time Customer Data Platform] bevat gereedschappen voor gegevensbeheer, identiteitsbeheer, geavanceerde segmentatie en gegevenswetenschap, zodat u profielen kunt maken en doelgroepen kunt definiëren, en rijke inzichten kunt afleiden en tegelijkertijd een strikt beleid voor gegevensbeheer kunt toepassen.

Adobe maakt verbinding met een groot ecosysteem van partners, om nog maar te zwijgen van de native integratie met Adobe Experience Cloud, zodat u dit publiek naadloos kunt activeren en geweldige klantervaringen kunt bieden op alle kanalen, van on-site of in-app personalisatie tot e-mail, betaalde media, callcenters, verbonden apparaten en nog veel meer.

Met Real-Time CDP kunt u:

* Zorg voor één weergave van uw klant met een stroomsgewijze verzameling van klantgegevens in de hele onderneming.
* Profielen op verantwoordelijke wijze beheren met vertrouwde governance en privacyopties voor bekende en onbekende id&#39;s.
* Maak actionable inzichten en schaal publiek met AI en machine leren aangedreven door Adobe Sensei en gebouwd voor marketers.
* Lever gepersonaliseerde ervaringen in real time over alle kanalen en bestemmingen.

Voor meer informatie, zie de [ documentatie van Real-Time Customer Data Platform ](../../rtcdp/overview.md).

**Belangrijkste kenmerken**

| Functie | Beschrijving |
|---|---|
| Bestemmingen | Vooraf gebouwde integratie met doelplatforms die worden ondersteund door Adobe [!DNL Real-Time Customer Data Platform] die gegevens naadloos voor deze partners activeren. Zie [ Doelen ](#destinations) hieronder voor meer informatie. |
| Metrisch dashboard voor startpagina | De startpagina van Real-Time Customer Data Platform (Real-Time CDP) bevat een dashboard voor meetgegevens met informatie over profielen en segmenten. De homepage bevat ook koppelingen naar leermaterialen. Zie de sectie op [ metriek van Real-Time Customer Data Platform ](#real-time-customer-data-platform-metrics) hieronder. |
| Bronnen | U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe Solutions, cloudopslag, software van derden en uw CRM. Zie de [ Bronnen ](#sources) hieronder sectie om meer te leren. |

**[!DNL Real-Time Customer Data Platform]metrics**

De startpagina van Real-Time Customer Data Platform (Real-Time CDP), die een dashboard voor cijfergegevens bevat, wordt weergegeven wanneer u zich aanmeldt bij Real-Time CDP.

De homepage is slechts een van de plaatsen waar metrische kaarten verschijnen. Real-Time CDP biedt metrische kaarten voor je hele ervaring. Deze metriek informeren u over de gegevens, het profiel, en het segmentpubliek in het systeem.

Als het systeem geen gegevens bevat wanneer u zich aanmeldt bij Real-Time CDP, wordt het dashboard op de startpagina niet weergegeven. In dit geval biedt de startpagina leermateriaal voor een eerste gebruikerservaring. Terwijl gegevens worden verzameld, wordt het dashboard automatisch bijgewerkt om informatie over die gegevens weer te geven.

Meer leren, zie het [ metriek van Real-Time Customer Data Platform overzicht ](../../rtcdp/home-page-dashboards.md)

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met doelplatforms die door Real-Time Customer Data Platform van Adobe worden ondersteund en die gegevens naadloos naar die partners activeren. Voor meer informatie, lees het [ overzicht van Doelen ](../../destinations/home.md) artikel.

**Beschikbare bestemmingen**

Met de versie van November, steunt Adobe Real-Time Customer Data Platform de volgende bestemmingen:

* Advertising: [!DNL Google]
* E-mailmarketing: Adobe Campaign, [!DNL Salesforce Marketing Cloud], [!DNL Responsys], [!DNL Oracle Eloqua]

Zie de [ bestemmingscatalogus ](../../destinations/catalog/overview.md) voor informatie over elk van de bestemmingen.

**Bekende beperkingen**

* Het besturingselement voor aangepaste activeringsschema&#39;s in de activeringsstroom (stap Planning) is niet beschikbaar bij de eerste release.
* Er is momenteel geen manier om een bestemmingsconfiguratie uit te geven of te schrappen. Om rond deze beperking te werken, kunt u de bestemming in de hoogste juiste hoek van de [ pagina van bestemmingsdetails ](../../destinations/ui/destination-details-page.md) toelaten of onbruikbaar maken.
* Er is momenteel geen validatie voor accountdetails, paden of referenties wanneer verbinding wordt gemaakt met uw doel- of opslagaccount. Controleer of u de juiste referenties invoert en dubbelklik op spelfouten of typefouten.
* Er zijn geen referentie-verlengingen beschikbaar bij de eerste release. Als een account is verlopen of moet worden vernieuwd, moet u een nieuwe doelverbinding maken en de eerder toegewezen segmenten opnieuw toewijzen.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Experience Platform] -services. U kunt gegevens opnemen van verschillende bronnen, zoals Adobe Solutions, cloudopslag, software van derden en uw CRM-systeem.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

**Belangrijkste kenmerken**

| Functie | Beschrijving |
| ---------- | ------------ |
| Broninterface | Nieuwe gebruikersinterface voor het maken, weergeven en beheren van bronverbindingen. |
| Herziene workflows voor CRM-connectors | Nieuwe intuïtieve UI-workflow voor het maken en beheren van [!DNL Microsoft Dynamics] - en [!DNL Salesforce] -connectors. |
| Connectorondersteuning voor op cloud gebaseerde opslagsystemen | Connectors hebben nu toegang tot op de cloud gebaseerde opslagsystemen. Nieuwe bronnen zijn onder andere [!DNL Amazon S3] -, [!DNL Azure Blob] - en FTP-/SFTP-servers. |

**Bekende kwesties**

* Source-connectors voor opslag in de cloud bieden geen ondersteuning voor het opnemen van gecomprimeerde bestanden.

Voor meer informatie over bronnen, zie [ Overzicht van Bronnen ](../../sources/home.md).

## [!DNL Data Science Workspace] {#dsw}

Met Adobe Experience Platform [!DNL Data Science Workspace] kunnen wetenschappers op gegevensgebied naadloos inzichten genereren op basis van gegevens en inhoud in Adobe-toepassingen en systemen van derden door Modellen voor machinaal leren te maken en te gebruiken. [!DNL Data Science Workspace] is nauw geïntegreerd met [!DNL Experience Platform] en maakt de levenscyclus van de end-to-end gegevenswetenschap mogelijk, inclusief de exploratie en voorbereiding van XDM-gegevens, gevolgd door de ontwikkeling en de exploitatie van Modellen om [!DNL Real-Time Customer Profile] automatisch te verrijken met Inzichten voor het leren van machines.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Gegevenstoegang met [!DNL Experience Platform] SDK | De vooraf gebouwde Ontvangers en lanceerlaptops in [!DNL Python] gebruiken nu [!DNL Experience Platform] SDK voor de toegang tot van gegevens. |
| Ondersteuning voor sandboxen | Ondersteuning voor aanstaande sandboxfunctionaliteit (momenteel in bèta), waaronder de mogelijkheid om laptops en recept te isoleren in ontwikkelings- of productiesandboxen. Zie het [sandboxoverzicht](../../sandboxes/home.md) voor meer informatie. |

Voor meer informatie, zie het [ overzicht van Workspace van de Wetenschap van Gegevens ](../../data-science-workspace/home.md).

## [!DNL Experience Data Model] (XDM)-systeem {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . [!DNL Experience Data Model] (XDM), aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| ---------- | ------------ |
| Meldingsschema | Nieuw schema dat berichtgegevens vertegenwoordigt die tijdens het proces van gegevensopname worden verzonden. |
| Adobe AdCloud DSP-schema&#39;s | Er zijn vijf nieuwe schema&#39;s toegevoegd voor de metagegevens van het Adobe Advertising Cloud demand-side platform (DSP): Placement, Campaign, Package, Advertiser, Account. |
| ExperienceEvent Implementatie - Detailschema, veldgroepen | Nieuwe ExperienceEvent-veldgroepen die een standaardveld toevoegen voor het opslaan van informatie over de software die wordt gebruikt om de gebeurtenis te verzamelen. |
| [!DNL Profile Privacy] veldgroepen | Nieuwe profielveldgroepen die velden toevoegen voor het accepteren van algemene out- en verkoop-/deelsignalen voor [!DNL Real-Time Customer Profile] . |
| Opmaakbeperkingen voor `xdm:alternateDisplayInfo` | De velden Titel en Beschrijving voor `xdm:alternateDisplayInfo` moeten beide tekenreeksen zijn om de validatie door te geven. |
| Naam wijzigen: XDM [!DNL Individual Profile] | De titel van de klasse &quot;XDM [!DNL Profile]&quot; is bijgewerkt naar &quot;XDM [!DNL Individual Profile]&quot;. De formele `$id` van de klasse is niet gewijzigd. |

**Bekende kwesties**

* Geen.

Om meer over het werken met XDM te leren gebruikend [!DNL Schema Registry] API en [!DNL Schema Editor] gebruikersinterface, te lezen gelieve de [ documentatie van het Systeem XDM ](../../xdm/home.md).

## [!DNL Real-Time Customer Profile] {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met [!DNL Real-Time Customer Profile] ziet u een holistische weergave van elke individuele klant die gegevens van meerdere kanalen combineert, waaronder online, offline, CRM en gegevens van derden. Met [!DNL Profile] kunt u uw verschillende klantgegevens consolideren in een uniforme weergave die een actionabel, tijdstempelaccount voor elke klantinteractie biedt.

| Functie | Beschrijving |
| -----------| ---------- |
| Verbeteringen voor [!DNL Profile] lookup | Gebruikers kunnen nu profielen opzoeken met behulp van referentiebeschrijvingen en verwante entiteiten. |
| Gegevens voor een bepaalde gegevensset opschonen | Gebruikers kunnen nu gegevens voor een bepaalde gegevensset of batch verwijderen met de API [!DNL Profile] System Jobs. |
| Verbeteringen in Edge [!DNL Profile] -query | Toepassingen kunnen nu een query uitvoeren op Edge [!DNL Profile] door een van de identiteiten van een bepaald profiel. |
| Samenvoegbeleid per projectie configureren | Toepassingen kunnen nu samenvoegingsbeleid per projectie configureren om een weergave van de gegevens te genereren zoals deze wordt bepaald door een specifiek samenvoegingsbeleid. |
| Berekende kenmerken | Berekende kenmerken berekenen automatisch de waarde van velden op basis van andere waarden, berekeningen en expressies. Op profielniveau worden de berekende kenmerken gebruikt om waarden zoals &quot;totale aankoop&quot;, &quot;levenslange waarde&quot; of &quot;treinstatus&quot; samen te voegen op basis van een binnenkomende gebeurtenis, een binnenkomende gebeurtenis en profielgegevens of een binnenkomende gebeurtenis, profielgegevens en historische gebeurtenissen. |

**Bugfixes**

* Vereenvoudigde lijst met beschikbare strategieën voor id-stitching in de workflow voor het maken van beleid voor samenvoegen.

**Bekende kwesties**

* Geen.

Voor meer informatie over [!DNL Real-Time Customer Profile], met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met [!DNL Profile] gegevens, te lezen gelieve het [ Real-Time Overzicht van het Profiel van de Klant ](../../profile/home.md).

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform [!DNL Segmentation Service] biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Experience Platform], zodat ze gemakkelijk toegankelijk zijn voor alle Adobe-toepassingen.

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

| Functie | Beschrijving |
| -----------| ---------- |
| Geplande segmentatie | De gebruikers kunnen geplande segmentevaluatie voor alle segmenten via UI en API nu toelaten. Zodra toegelaten, zullen alle segmenten eenmaal per dag worden geëvalueerd. Dit heeft geen invloed op de segmenteringsmogelijkheden op aanvraag die nog steeds werken zoals voorheen.<br/><br/> Nota: De geplande segmenteringseigenschap kan niet in zandbakken met meer dan vijf fusiebeleid voor [!DNL XDM Individual Profile] worden gebruikt. |
| Streaming segmentering | Dankzij ondersteuning voor doorlopende evaluatie van segmenten (streaming segmentation) kunnen de meeste segmentregels worden geëvalueerd terwijl de gegevens worden doorgegeven aan [!DNL Experience Platform] . Deze eigenschap betekent dat het segmentlidmaatschap bijgewerkt zal zijn zonder de behoefte om geplande segmentatietaken in werking te stellen. Sommige uitzonderingen zijn van toepassing, zoals segmenten die relaties met meerdere entiteiten gebruiken of met verrijkte nuttige lasten. |
| Segmenten als bouwstenen | Wanneer het creëren van segmenten gebruikend de Bouwer UI van het Segment, kunnen de gebruikers eerder-bepaalde segmenten als bouwstenen voor extra segmenten nu gebruiken. <ul><li>Verwijzing naar huidige publiekslidmaatschap: updates wanneer mensen zich binnen en buiten het publiek verplaatsen.</li><li>Logica kopiëren: neem de geselecteerde segmentdefinitie en dupliceer deze in het nieuwe segment.</li></ul> |
| Segmentlidmaatschap weergeven op naamruimte ID | Segmentlidmaatschap kan nu worden weergegeven door naamruimte ID (e-mail, ECID en totale telling). |
| RBAC-ondersteuning | De Bouwer van het segment verleent nu steun voor basisop rol-gebaseerde toegangscontroles en toestemmingen. |
| Verbeterde ondersteuning voor het delen van externe doelgroepen tussen [!DNL Experience Platform] en Adobe-oplossingen | Gebruikers kunnen nu externe (niet- [!DNL Experience Platform]) publieksmetagegevens opnemen in scenario&#39;s waarbij het aantal doelgroepen a priori groot of onbekend is. Deze release omvat toegang tot [!DNL Audience Manager] -metagegevens voor klanten die de aansluiting voor de oplossing hebben ingericht. Deze publieksmetagegevens kunnen in Segment Builder worden gebruikt om nieuwe [!DNL Experience Platform] -segmenten te maken. <br/><br/> Bovendien zijn in [!DNL Experience Platform] gemaakte segmenten nu beschikbaar voor gebruik in geïntegreerde Adobe-oplossingen, waaronder [!DNL Audience Manager] , [!DNL Target] en [!DNL Ad Cloud] . |

**Bugfixes**

* Probleem verholpen waarbij profielen van meerdere entiteiten werden geretourneerd als geneste relaties werden gebruikt.
* Probleem opgelost waarbij de uitsluitingslogica tot misleidende resultaten leidde.
* Verbeterde leesbaarheid voor mappen met meerdere entiteiten. Ze tonen nu de vriendelijke naam van de klasse XDM.
* Probleem verholpen waarbij meerdere kopieën van dezelfde XDM-map werden weergegeven.
* Het bericht wordt nu geproduceerd om een gebruiker te informeren als de segmentramingen voor het geselecteerde fusiebeleid niet beschikbaar zijn.

**Bekende kwesties**

* Geen.

Meer over [!DNL Segmentation Service] leren, te lezen gelieve het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md).
