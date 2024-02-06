---
title: Opmerkingen bij de release van Adobe Experience Platform januari 2024
description: Opmerkingen bij de release van januari 2024 voor Adobe Experience Platform.
source-git-commit: c6d471d7bb8cb9d5e376cc49c9c89c39e663d7f9
workflow-type: tm+mt
source-wordcount: '1646'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 30 januari 2024**

Nieuwe functies in Adobe Experience Platform:

- [Hoofdletters gebruiken](#use-case-playbooks)

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

## Hoofdletters gebruiken {#use-case-playbooks}

De [!UICONTROL Use Case Playbooks] Deze functionaliteit is nu algemeen beschikbaar voor alle Real-Time CDP- en Adobe Journey Optimizer-klanten. [!UICONTROL Use Case Playbooks] zijn ontworpen om gebruikers te helpen bij het overwinnen van uitdagingen wanneer ze met Real-time Customer Data Platform of Adobe Journey Optimizer beginnen. Als u niet zeker weet waar u moet beginnen of hoe u de juiste middelen voor uw gewenste gebruiksscenario&#39;s kunt maken, kunt u met Afspeelboeken voor hoofdletters en kleine letters inspiratie bieden en verschillende middelen maken die u kunt testen en importeren in productieomgevingen wanneer u klaar bent.

Aan de slag met [!UICONTROL Use Case Playbooks], lees de volgende documentatiepagina&#39;s:

- Lees de [overzichtspagina](/help/use-case-playbooks/playbooks/overview.md) om het doel, de beschikbaarheidsinformatie te begrijpen, en een demonstratie van begin tot eind te krijgen van hoe playbooks werken van ontdekking tot het creëren van instanties, aan het invoeren van geproduceerde activa in andere zandbakmilieu&#39;s.
- Een lijst met alles ophalen [beschikbare playbooks](/help/use-case-playbooks/playbooks/playbooks-list.md), gegroepeerd op product (Real-Time CDP of Journey Optimizer)
- Informatie ophalen over alle [vereiste machtigingen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) om playbooks en de activa te gebruiken die door playbooks worden geproduceerd.
- Begrijp het [functionaliteit voor gegevensbewustzijn](/help/use-case-playbooks/playbooks/data-awareness.md) waarmee u gegenereerde elementen naar andere sandboxomgevingen kunt kopiëren
- Get [tips voor problemen](/help/use-case-playbooks/playbooks/troubleshooting.md) als u fouten of problemen ondervindt bij het gebruik van hoofdletters en kleine letters.

## Toegangsbeheer op basis van kenmerken {#abac}

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform die privacybewuste merken meer flexibiliteit biedt om gebruikerstoegang te beheren. Afzonderlijke objecten zoals schemavelden en segmenten kunnen worden toegewezen aan gebruikersrollen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot, gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en ander aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijwerken | Beschrijving |
| --- | --- |
| Nieuwe API eindpunten gedocumenteerd voor op attributen-gebaseerd toegangsbeheer | De [Referentiedocumentatie van Access Control API](https://developer.adobe.com/experience-platform-apis/references/access-control/) omvat nu op attribuut-gebaseerde API rollen, beleid, en producteindpunten van toegangsbeheer. Deze eindpunten kunnen worden gebruikt om relevante rollen, beleid, en producten voor een gebruiker op bepaalde middelen in een gespecificeerde zandbak terug te winnen. |

{style="table-layout:auto"}

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie [op attributen-gebaseerd toegangsbeheeroverzicht](../../access-control/abac/overview.md). Voor een uitvoerige gids over het op attributen-gebaseerde toegangsbeheerwerkschema, lees [attribuut-based toegangsbeheergids van begin tot eind](../../access-control/abac/end-to-end-guide.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe mapfuncties | <ul><li>`object_to_map`: Gebruik de `object_to_map` functie om kaartgegevenstypen te maken. Deze functie ondersteunt verschillende syntaxis. Lees voor meer informatie de handleiding op [functies voor hiërarchieën - objecten](../../data-prep/functions.md#objects). </li><li>`to_map`: Gebruik de `to_map` gebruiken om een kaart met bepaalde veldnaam en waardeparen te maken met behulp van objecten. Lees voor meer informatie de handleiding op [functies voor hiërarchieën - kaarten](../../data-prep/functions.md#map). </li><li>`array_to_map`: Gebruik de `array_to_map` functie voor het maken van een kaart met opgegeven veldnaam- en waardeparen met behulp van objectarrays. Lees voor meer informatie de handleiding op [functies voor hiërarchieën - kaarten](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Voor meer informatie over de Prep van Gegevens, lees [Overzicht van Data Prep](../../data-prep/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| SQL weergeven | U kunt SQL nu achter uw Profielen, Soorten publiek, Doelen, en aangepaste inzichten met de knevel van SQL van de Mening bekijken SQL, dan de vraag op bestelling door de Redacteur van de Vraag uitvoeren. Als u toegang krijgt tot de SQL die uw Real-time Customer Data Platform-inzichten kracht geeft, kunt u beter begrijpen wat de logica achter de analyse van uw gegevensmodel is. Deze transparantie maakt uw Adobe in real time CDP gegevens toegankelijker, begrijpelijker, en beïnvloedend voor besluitvorming.<br>inspiratie halen uit de SQL van meer dan 40 bestaande inzichten om nieuwe vragen tot stand te brengen die unieke inzichten uit de gegevens van het Platform voortbrengen die op uw bedrijfsbehoeften worden gebaseerd. SQL is ook beschikbaar voor uw [Profielen](../../dashboards/insights/profiles.md), [Soorten publiek](../../dashboards/insights/audiences.md), en [Doelen](../../dashboards/insights/destinations.md) inzichten in de documentatie van het Experience League. Deze documenten benadrukken de zaken van het bedrijfsgebruik die met de standaardinzichten kunnen worden beantwoord. Lees voor meer informatie de handleiding op [inzicht weergeven in SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [Publicatieverbinding](../../destinations/catalog/advertising/pubmatic.md) | Gebruik deze bestemming om publieksgegevens naar te verzenden [!DNL PubMatic Connect] platform. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuw **overgenomen rol** verificatietype voor Amazon S3-doelen | Gebruik het nieuwe veronderstelde type van rolauthentificatie wanneer het verbinden van Experience Platform met uw emmers van Amazon S3 als u geen rekeningssleutels en geheime sleutels met Experience Platform wilt delen. Lees meer over de nieuwe authentificatiemethode in [verificatiesectie](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) van de Amazon S3 documentatie. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijwerken | Beschrijving |
| --- | --- |
| Herstructurering van documenten | De documentatie van de identiteitsdienst is geherstructureerd om de presentatie en duidelijkheid van concepten binnen de identiteitsdienst te verbeteren:<ul><li>Ga naar [Overzicht van identiteitsservice-pagina](../../identity-service/home.md) voor een uitgebreide terminologiegids, een gebruiksgeval voorbeeld die een typische klantenreis, een specificatie van hoe de Dienst van de Identiteit identificeert samen verbindt, en een samenvatting van de rol die de Dienst van de Identiteit binnen het ecosysteem van de Experience Platform plaatst.</li><li>Lees de handleiding op [inzicht krijgen in de relatie tussen Identiteitsservice en Real-Time Klantprofiel](../../identity-service/identity-and-profile.md) voor een gedetailleerd overzicht van de manier waarop de twee diensten samenwerken en de verschillen tussen hun doelstellingen, processen, input, en output.</li><li>Zie de [Logica-handleiding voor identiteitsservice-koppeling](../../identity-service/features/identity-linking-logic.md) voor uitleg en visualisatie van het gedrag van de identiteitsgrafiek worden verschillende scenario&#39;s en tijdstempels gegeven.</li></ul> |

{style="table-layout:auto"}

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Gebouwd op Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen met intelligente besluitvorming door de klantenreis te activeren. [!DNL Real-Time CDP] combineert veelvoudige bronnen van ondernemingsgegevens om klantenprofielen in real time tot stand te brengen. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates van de [Homepage van Real-Time CDP](https://experience.adobe.com) | <ul><li>**Profielwidget**: U kunt nu de widget Profielen gebruiken om naar de overzichtspagina Profielen te navigeren en om profielgegevens voor uw organisatie weer te geven.</li><li>**Metrische kaart van profiel**: De metriekkaart van het Profiel in het dashboard van de homepage toont nu het totale aantal profielen in uw organisatie, afhankelijk van uw respectieve samenvoegingsbeleid.</li><li>**Schemaswidget**: U kunt nu de widget schema&#39;s gebruiken om naar de workflow voor het maken van schema&#39;s in de gebruikersinterface te navigeren.</li></ul> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijwerken | Beschrijving |
| --- | --- |
| Nieuwe Real-Time CDP-documentatiewebsite | Ga naar [nieuwe Real-Time CDP-documentatiehomepage](/help/rtcdp/home.md) voor informatie over hoe u in één oogopslag aan de slag kunt gaan met het product, de guardrails, de draagtas van het monstergebruik en nog veel meer. |
| Voorbeeld Real-Time CDP-gebruiksscenario&#39;s - overzicht | Ga naar [nieuwe voorbeeldpagina met voorbeelden bekijken](/help/rtcdp/use-case-guides/overview.md) voor een verzameling voorbeelden van gebruiksgevallen die uw organisatie met Real-Time CDP kan bereiken. |

{style="table-layout:auto"}

Voor meer informatie over Real-Time CDP leest u de [Real-Time CDP-overzicht](../../rtcdp/overview.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen voor het lokaliseren van de standaarddashboardkaarten van de profielviewer | De standaardprofielkaarten hebben nu dynamisch gelokaliseerde namen. Aangepaste profielkaarten kunnen aangepaste namen blijven bevatten die kunnen worden bewerkt. |

{style="table-layout:auto"}

Lees voor meer informatie over Real-Time Customer Profile de [Profieloverzicht](../../profile/home.md)

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Extern gegenereerde publieksupload | Het maximumaantal kolommen is verhoogd tot **25**. |
| Schatting opbouwen | Schattingen en gekwalificeerde profielen worden nu weergegeven in de sectie met publiekseigenschappen. Voor meer informatie over deze wijziging raadpleegt u de [Handleiding voor de gebruikersinterface van Segment Builder](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] bronnen | Gebruik de [!DNL Oracle NetSuite] integratie in de broncatalogus om gegevens van uw [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) en [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) rekeningen bij het Experience Platform. |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] bron | Gebruik de [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) integratie in de broncatalogus om gegevens van uw [!DNL Braze] aan Experience Platform. |
| Ondersteuning voor sleutelpaarverificatie voor [!DNL Snowflake] batchbron | U kunt zeer belangrijk-paarauthentificatie nu gebruiken wanneer het creëren van een nieuw [!DNL Snowflake] account voor batchgegevens. Lees voor meer informatie de handleiding op [een [!DNL Snowflake] account die de API gebruikt](../../sources/tutorials/api/create/databases/snowflake.md) of de handleiding [een [!DNL Snowflake] account die de gebruikersinterface gebruikt](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).