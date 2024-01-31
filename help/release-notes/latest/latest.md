---
title: Aanvullende informatie over Adobe Experience Platform
description: Opmerkingen bij de release van januari 2024 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6ee30e00bceb392b775d15ca2cad95b746698dc4
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 30 januari 2024**

Nieuwe functies in Adobe Experience Platform:

- [Hoofdletters gebruiken](#use-case-playbooks)

Updates voor bestaande functies in Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensvoorbereiding](#data-prep)
- [Doelen](#destinations)
- [Real-Time Customer Data Platform](#rtcdp)
- [Klantprofiel in realtime](#profile)
- [Bronnen](#sources)

## Hoofdletters gebruiken {#use-case-playbooks}

De [!UICONTROL Use Case Playbooks] Deze functionaliteit is nu algemeen beschikbaar voor alle Real-Time CDP- en Adobe Journey Optimizer-klanten. [!UICONTROL Use Case Playbooks] zijn ontworpen om gebruikers te helpen bij het overwinnen van uitdagingen wanneer ze met Real-time Customer Data Platform of Adobe Journey Optimizer beginnen. Als u niet zeker weet waar u moet beginnen of hoe u de juiste middelen voor uw gewenste gebruiksscenario&#39;s kunt maken, kunt u met Afspeelboeken voor hoofdletters en kleine letters inspiratie bieden en verschillende middelen maken die u kunt testen en importeren in productieomgevingen wanneer u klaar bent.

Aan de slag met [!UICONTROL Use Case Playbooks], lees de volgende documentatiepagina&#39;s:

- Lees de [overzichtspagina](/help/use-case-playbooks/playbooks/overview.md) om het doel, de beschikbaarheidsinformatie te begrijpen, en een demonstratie van begin tot eind te krijgen van hoe playbooks werken van ontdekking tot het creëren van instanties, aan het invoeren van geproduceerde activa in andere zandbakmilieu&#39;s.
- Een lijst met alles ophalen [beschikbare playbooks](/help/use-case-playbooks/playbooks/playbooks-list.md), gegroepeerd op product (Real-Time CDP of Journey Optimizer)
- Informatie ophalen over alle [vereiste machtigingen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) om playbooks en de activa te gebruiken die door playbooks worden geproduceerd.
- Begrijp het [functionaliteit voor gegevensbewustzijn](/help/use-case-playbooks/playbooks/data-awareness.md) waarmee u gegenereerde elementen naar andere sandboxomgevingen kunt kopiëren
- Get [tips voor problemen](/help/use-case-playbooks/playbooks/troubleshooting.md) als u fouten of problemen ondervindt bij het gebruik van hoofdletters en kleine letters.

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe mapfuncties | <ul><li>`object_to_map`: Gebruik de `object_to_map` functie om kaartgegevenstypen te maken. Deze functie ondersteunt verschillende syntaxis. Lees voor meer informatie de handleiding op [functies voor hiërarchieën - objecten](../../data-prep/functions.md#objects). </li><li>`to_map`: Gebruik de `to_map` gebruiken om een kaart met bepaalde veldnaam en waardeparen te maken met behulp van objecten. Lees voor meer informatie de handleiding op [functies voor hiërarchieën - kaarten](../../data-prep/functions.md#objects). </li><li>`array_to_map`: Gebruik de `array_to_map` functie voor het maken van een kaart met opgegeven veldnaam- en waardeparen met behulp van objectarrays. Lees voor meer informatie de handleiding op [functies voor hiërarchieën - kaarten](../../data-prep/functions.md#objects). |

{style="table-layout:auto"}

Voor meer informatie over de Prep van Gegevens, lees [Overzicht van Data Prep](../../data-prep/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| SQL weergeven | U kunt SQL nu achter uw Profielen, Soorten publiek, Doelen, en aangepaste inzichten bekijken en dan de vraag op bestelling door de Redacteur van de Vraag uitvoeren. inspiratie halen uit de SQL van meer dan 40 bestaande inzichten om nieuwe vragen tot stand te brengen die unieke inzichten uit de gegevens van het Platform voortbrengen die op uw bedrijfsbehoeften worden gebaseerd. Lees voor meer informatie de handleiding op [inzicht weergeven in SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Doel | Beschrijving |
| ----------- | ----------- |
| [Publicatieverbinding](../../destinations/catalog/advertising/pubmatic.md) | Gebruik deze bestemming om publieksgegevens naar te verzenden [!DNL PubMatic Connect] platform. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Gebouwd op Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen met intelligente besluitvorming door de klantenreis te activeren. [!DNL Real-Time CDP] combineert veelvoudige bronnen van ondernemingsgegevens om klantenprofielen in real time tot stand te brengen. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates van de [Homepage van Real-Time CDP](https://experience.adobe.com) | <ul><li>**Profielwidget**: U kunt nu de widget Profielen gebruiken om naar de overzichtspagina Profielen te navigeren en om profielgegevens voor uw organisatie weer te geven.</li><li>**Metrische kaart van profiel**: De metriekkaart van het Profiel in het dashboard van de homepage toont nu het totale aantal profielen in uw organisatie, afhankelijk van uw respectieve samenvoegingsbeleid.</li><li>**Schemaswidget**: U kunt nu de widget schema&#39;s gebruiken om naar de workflow voor het maken van schema&#39;s in de gebruikersinterface te navigeren.</li></ul> |

Lees voor meer informatie over Real-Time CDP de [Real-Time CDP-overzicht](../../rtcdp/overview.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen voor het lokaliseren van de standaarddashboardkaarten van de profielviewer | De standaardprofielkaarten hebben nu dynamisch gelokaliseerde namen. Aangepaste profielkaarten kunnen aangepaste namen blijven bevatten die kunnen worden bewerkt. |

{style="table-layout:auto"}

Lees voor meer informatie over Real-Time Customer Profile de [Profieloverzicht](../../profile/home.md)

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