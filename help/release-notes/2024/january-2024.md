---
title: Opmerkingen bij de release van Adobe Experience Platform januari 2024
description: Aanvullende informatie van januari 2024 voor Adobe Experience Platform.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 30 januari 2024**

Nieuwe functies in Adobe Experience Platform:

- [Playbooks voor gebruiksscenario](#use-case-playbooks)

Updates voor bestaande functies in Experience Platform:

- [Toegangsbeheer op basis van kenmerken](#abac)
- [Gegevensvoorbereiding](#data-prep)
- [Dashboards](#dashboards)
- [Doelen](#destinations)
- [Identiteitsservice](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Playbooks voor gebruiksscenario {#use-case-playbooks}

De [!UICONTROL Use Case Playbooks] -functionaliteit is nu algemeen beschikbaar voor alle Real-Time CDP- en Adobe Journey Optimizer-klanten. [!UICONTROL Use Case Playbooks] zijn ontworpen om gebruikers te helpen bij het overwinnen van uitdagingen wanneer ze met Real-time Customer Data Platform of Adobe Journey Optimizer beginnen. Als u niet zeker weet waar u moet beginnen of hoe u de juiste middelen voor uw gewenste gebruiksscenario&#39;s kunt maken, kunt u met Afspeelboeken voor hoofdletters en kleine letters inspiratie bieden en verschillende middelen maken die u kunt testen en importeren in productieomgevingen wanneer u klaar bent.

Lees de volgende documentatiepagina&#39;s om aan de slag te gaan met [!UICONTROL Use Case Playbooks] :

- Lees de [ overzichtspagina ](/help/use-case-playbooks/playbooks/overview.md) om het doel, beschikbaarheidsinformatie te begrijpen, en een demonstratie van begin tot eind te krijgen van hoe playbooks van ontdekking tot het creëren van instanties werken, aan het invoeren van geproduceerde activa in andere zandbakmilieu&#39;s.
- Krijg een lijst van alle [ beschikbare playbooks ](/help/use-case-playbooks/playbooks/playbooks-list.md), gegroepeerd door product (Real-Time CDP of Journey Optimizer)
- Krijg informatie over alle [ vereiste toestemmingen ](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) om playbooks en de activa te gebruiken die door playbooks worden geproduceerd.
- Begrijp de [ functionaliteit van het gegevensbewustzijn ](/help/use-case-playbooks/playbooks/data-awareness.md) die u toestaat om geproduceerde activa aan andere zandbakmilieu&#39;s te kopiëren
- Krijg [ het oplossen van problemenuiteinden ](/help/use-case-playbooks/playbooks/troubleshooting.md) als u in fouten of moeilijkheden gebruikend de Hoofdletters van het Gebruik loopt.

## Toegangsbeheer op basis van kenmerken {#abac}

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform die privacybewuste merken meer flexibiliteit biedt om gebruikerstoegang te beheren. Afzonderlijke objecten zoals schemavelden en segmenten kunnen worden toegewezen aan gebruikersrollen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot, gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en ander aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijwerken | Beschrijving |
| --- | --- |
| Nieuwe API eindpunten gedocumenteerd voor op attributen-gebaseerd toegangsbeheer | De [ API van het Toegangsbeheer verwijzingsdocumentatie ](https://developer.adobe.com/experience-platform-apis/references/access-control/) omvat nu op attribuut-gebaseerde API rollen, beleid, en producteindpunten van toegangsbeheer. Deze eindpunten kunnen worden gebruikt om relevante rollen, beleid, en producten voor een gebruiker op bepaalde middelen in een gespecificeerde zandbak terug te winnen. |

{style="table-layout:auto"}

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie het [ op attributen-gebaseerde toegangsbeheeroverzicht ](../../access-control/abac/overview.md). Voor een uitvoerige gids over het op attribuut-gebaseerde toegangsbeheerwerkschema, lees de [ op attribuut-gebaseerde gids van begin tot eind van de toegangscontrole ](../../access-control/abac/end-to-end-guide.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe mapfuncties | <ul><li>`object_to_map`: gebruik de functie `object_to_map` om gegevenstypen met hyperlinks te maken. Deze functie ondersteunt verschillende syntaxis. Voor meer informatie, lees de gids op [ functies voor hiërarchieën - voorwerpen ](../../data-prep/functions.md#objects). </li><li>`to_map`: gebruik de functie `to_map` om een kaart met bepaalde veldnaam en waardeparen te maken met behulp van objecten. Voor meer informatie, lees de gids op [ functies voor hiërarchieën - kaarten ](../../data-prep/functions.md#map). </li><li>`array_to_map`: gebruik de functie `array_to_map` om een kaart met bepaalde veldnaam en waardeparen te maken met behulp van objectarrays. Voor meer informatie, lees de gids op [ functies voor hiërarchieën - kaarten ](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Voor meer informatie over de Prep van Gegevens, lees het [ Overzicht van de Prep van Gegevens ](../../data-prep/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| SQL weergeven | U kunt SQL nu achter uw Profielen, Soorten publiek, Doelen, en aangepaste inzichten met de knevel van SQL van de Mening bekijken SQL, dan de vraag op bestelling door de Redacteur van de Vraag uitvoeren. Als u toegang krijgt tot de SQL die uw Real-time Customer Data Platform-inzichten kracht geeft, kunt u beter begrijpen wat de logica achter de analyse van uw gegevensmodel is. Deze transparantie maakt uw Adobe in real time CDP gegevens toegankelijker, begrijpelijker, en beïnvloedend voor besluitvorming.<br> neem inspiratie van SQL van meer dan 40 bestaande inzichten om nieuwe vragen tot stand te brengen die unieke inzichten uit de gegevens van het Platform voortbrengen die op uw bedrijfsbehoeften worden gebaseerd. SQL is ook beschikbaar voor uw [ Profielen ](../../dashboards/insights/profiles.md), [ Soorten publiek ](../../dashboards/insights/audiences.md), en [ Doelen ](../../dashboards/insights/destinations.md) inzichten in de documentatie van het Experience League. Deze documenten benadrukken de zaken van het bedrijfsgebruik die met de standaardinzichten kunnen worden beantwoord. Voor meer informatie, lees de gids bij [ het bekijken van inzicht SQL ](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanegidgets tot stand te brengen, begin door het [ overzicht van dashboards ](../../dashboards/home.md) te lezen.

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [ Pubmatic verbinding ](../../destinations/catalog/advertising/pubmatic.md) | Gebruik deze bestemming om publieksgegevens naar het [!DNL PubMatic Connect] -platform te verzenden. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuw **veronderstelde rol** authentificatietype voor Amazon S3 bestemmingen | Gebruik het nieuwe veronderstelde type van rolauthentificatie wanneer het verbinden van Experience Platform met uw emmers van Amazon S3 als u geen rekeningssleutels en geheime sleutels met Experience Platform wilt delen. Lees meer over de nieuwe authentificatiemethode in de [ authentificatiesectie ](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) van de documentatie van Amazon S3. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijwerken | Beschrijving |
| --- | --- |
| Herstructurering van documenten | De documentatie van de identiteitsdienst is geherstructureerd om de presentatie en duidelijkheid van concepten binnen de identiteitsdienst te verbeteren:<ul><li>Bezoek de [ pagina van het overzicht van de Dienst van de Identiteit ](../../identity-service/home.md) voor een uitgebreide terminologiegids, een gebruik-geval voorbeeld die een typische klantenreis, een verdeling van hoe de Identiteitsdienst identiteiten samen, en een samenvatting van de rol detailhandelt die de Dienst binnen het ecosysteem van het Experience Platform plaatst.</li><li>Lees de gids op [ het begrip van het verband tussen de Dienst van de Identiteit en het Profiel van de Klant in real time ](../../identity-service/identity-and-profile.md) voor een gedetailleerde samenvatting van hoe de twee diensten samenwerken en de verschillen tussen hun doeleinden, processen, input, en output.</li><li>Verwijs naar de [ Dienst van de Identiteit die logische gids ](../../identity-service/features/identity-linking-logic.md) met elkaar verbindt voor verklaringen en visualisaties van hoe de identiteitsgrafiek zich gedraagt verschillende scenario&#39;s en timestamps.</li></ul> |

{style="table-layout:auto"}

Om meer over de Dienst van de Identiteit te leren, te lezen gelieve het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Real-time Customer Data Platform ([!DNL Real-Time CDP]) is gebaseerd op Experience Platform en helpt bedrijven bekende en onbekende gegevens bijeen te brengen om klantprofielen te activeren door middel van intelligente beslissingen tijdens de reis van de klant. [!DNL Real-Time CDP] combineert meerdere bedrijfsgegevensbronnen om klantprofielen in real-time te maken. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Updates aan de [ homepage van Real-Time CDP ](https://experience.adobe.com) | <ul><li>**widget van Profielen**: U kunt nu de widget van Profielen gebruiken om aan de het overzichtspagina van Profielen te navigeren en de metriek van het Profiel voor uw organisatie te bekijken.</li><li>**de metriekkaart van het Profiel**: De kaart van de Metriek van het Profiel in het dashboard van de homepage toont nu de totale telling van profielen in uw organisatie, afhankelijk van uw respectieve samenvoegingsbeleid.</li><li>**widget van Schema&#39;s**: U kunt de schema&#39;s nu gebruiken widget om aan het werkschema van de schemaverwezenlijking in UI te navigeren.</li></ul> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijwerken | Beschrijving |
| --- | --- |
| Nieuwe Real-Time CDP-documentatiewebsite | Bezoek de [ nieuwe de documentatiehomepage van Real-Time CDP ](/help/rtcdp/home.md) voor in-a-blik informatie over hoe te om met het product, guardrails, de geval van het steekproefgebruik, en veel meer te beginnen. |
| Voorbeeld Real-Time CDP-gebruiksscenario&#39;s - overzicht | Bezoek de [ nieuwe pagina van de de gevaloverzicht van het steekproefgebruik ](/help/rtcdp/use-case-guides/overview.md) voor een inzameling van de gevallen van het steekproefgebruik die uw organisatie met Real-Time CDP kan bereiken. |

{style="table-layout:auto"}

Meer over Real-Time CDP leren, lees het [ overzicht van Real-Time CDP ](../../rtcdp/overview.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen voor het lokaliseren van de standaarddashboardkaarten van de profielviewer | De standaardprofielkaarten hebben nu dynamisch gelokaliseerde namen. Aangepaste profielkaarten kunnen aangepaste namen blijven bevatten die kunnen worden bewerkt. |

{style="table-layout:auto"}

Meer over het Profiel van de Klant in real time leren, lees het [ overzicht van het Profiel ](../../profile/home.md)

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Extern gegenereerde publieksupload | Het maximumaantal kolommen is verhoogd tot **25**. |
| Schatting opbouwen | Schattingen en gekwalificeerde profielen worden nu weergegeven in de sectie met publiekseigenschappen. Voor meer informatie over deze verandering, lees de [ gids UI van de Bouwer van het Segment ](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], gelieve te zien het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Beta ] {type=Informative} [!DNL Oracle NetSuite] bronnen | Gebruik de [!DNL Oracle NetSuite] -integratie in de broncatalogus om gegevens van uw [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) - en [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) -accounts naar het Experience Platform te halen. |
| [!BADGE  Beta ] {type=Informative} [!DNL Braze Currents] bron | Gebruik de [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) -integratie in de broncatalogus om gegevens van uw [!DNL Braze] -account over te brengen naar het Experience Platform. |
| Ondersteuning voor sleutelpaarverificatie voor [!DNL Snowflake] batchbron | U kunt nu sleutelparverificatie gebruiken bij het maken van een nieuw [!DNL Snowflake] -account voor batchgegevens. Voor meer informatie, lees de gids op [ creërend a  [!DNL Snowflake]  rekening gebruikend API ](../../sources/tutorials/api/create/databases/snowflake.md) of de gids op [ creërend a  [!DNL Snowflake]  rekening gebruikend UI ](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Meer over bronnen leren, lees het [ overzicht van bronnen ](../../sources/home.md).
