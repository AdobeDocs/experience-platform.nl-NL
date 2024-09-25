---
title: Aanvullende informatie van januari 2024 voor Adobe Experience Platform
description: Aanvullende informatie van januari 2024 voor Adobe Experience Platform.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: ht
source-wordcount: '1650'
ht-degree: 100%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: 30 januari 2024**

Nieuwe functies in Adobe Experience Platform:

- [Playbooks voor gebruiksscenario&#39;s](#use-case-playbooks)

Updates van bestaande functies in Experience Platform:

- [Toegangsbeheer op basis van kenmerken](#abac)
- [Gegevensvoorbereiding](#data-prep)
- [Dashboards](#dashboards)
- [Bestemmingen](#destinations)
- [Identiteitsservice](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Realtime-klantenprofiel](#profile)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Playbooks voor gebruiksscenario&#39;s {#use-case-playbooks}

De [!UICONTROL Use Case Playbooks]-functionaliteit is nu algemeen beschikbaar voor alle Real-Time CDP- en Adobe Journey Optimizer-klanten. [!UICONTROL Use Case Playbooks] zijn ontworpen om gebruikers te helpen uitdagingen te overwinnen, wanneer ze met Real-time Customer Data Platform of Adobe Journey Optimizer beginnen. Als u niet zeker weet waar u moet beginnen of hoe u de juiste assets voor uw gewenste gebruiksscenario&#39;s kunt maken, biedt Playbooks voor gebruiksscenario&#39;s inspiratie en maakt verschillende assets die u kunt testen en in productieomgevingen importeren, zodra ze klaar zijn.

Raadpleeg de volgende documentatiepagina&#39;s om met [!UICONTROL Use Case Playbooks] aan de slag te gaan:

- Raadpleeg de [overzichtspagina](/help/use-case-playbooks/playbooks/overview.md) om te begrijpen wat de doelen van playbooks zijn en voor informatie over de beschikbaarheid. Bekijk een complete demonstratie van de werking van playbooks en leer hoe u ernaar zoekt, hoe u instanties maakt en hoe u gegenereerde assets in andere sandbox-omgevingen importeert.
- Krijg een lijst van alle [beschikbare playbooks](/help/use-case-playbooks/playbooks/playbooks-list.md), gegroepeerd naar product (Real-Time CDP of Journey Optimizer)
- Krijg informatie over alle [vereiste machtigingen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) om playbooks en de assets te gebruiken die door playbooks worden gegenereerd.
- Inzicht in de [functie gegevensbewustzijn](/help/use-case-playbooks/playbooks/data-awareness.md) waarmee u gegenereerde assets naar andere sandbox-omgevingen kunt kopiëren
- Krijg [tips voor het oplossen van problemen](/help/use-case-playbooks/playbooks/troubleshooting.md) als u bij het gebruik van playbooks voor gebruiksscenario&#39;s op fouten of moeilijkheden stuit.

## Toegangsbeheer op basis van kenmerken {#abac}

Toegangsbeheer op basis van kenmerken is een functionaliteit van Adobe Experience Platform waarmee merken die aandacht hebben voor privacy, meer flexibiliteit krijgen bij toegangsbeheer voor gebruikers. Individuele objecten, zoals schemavelden en segmenten, kunnen aan gebruikersrollen worden toegewezen. Met deze functie kunt u toegang tot individuele objecten verlenen of intrekken voor specifieke platformgebruikers in uw organisatie.

Met toegangsbeheer op basis van kenmerken kunnen beheerders van uw organisatie de toegang van gebruikers tot gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en andere aangepaste typen gegevens in alle platformworkflows en -bronnen beheren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die bij die velden horen.

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijgewerkt | Beschrijving |
| --- | --- |
| Nieuwe API-eindpunten gedocumenteerd voor toegangsbeheer op basis van kenmerken | Het [referentiedocument voor de toegangsbeheer-API](https://developer.adobe.com/experience-platform-apis/references/access-control/) omvat nu ook rollen, beleidsregels en producteindpunten voor toegangsbeheer op basis van kenmerken. Deze eindpunten kunnen worden gebruikt om relevante rollen, beleidsregels en producten op te halen voor een gebruiker van bepaalde bronnen in een gespecificeerde sandbox. |

{style="table-layout:auto"}

Zie het [overzicht van toegangsbeheer op basis van kenmerken](../../access-control/abac/overview.md) voor meer informatie over toegangsbeheer op basis van kenmerken. Voor een uitgebreide handleiding over de workflow voor toegangsbeheer op basis van kenmerken raadpleegt u de [end-to-end handleiding voor toegangsbeheer op basis van kenmerken](../../access-control/abac/end-to-end-guide.md).

## Gegevensvoorbereiding {#data-prep}

Met gegevensvoorbereiding kunnen gegevenstechnici gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience-datamodel).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe toewijzingsfuncties | <ul><li>`object_to_map`: gebruik de functie `object_to_map` om gegevenstypen voor toewijzing te maken. Deze functie ondersteunt verschillende syntaxis. Voor meer informatie, raadpleegt u de handleiding voor [functies voor hiërarchieën - objecten](../../data-prep/functions.md#objects). </li><li>`to_map`: gebruik de functie `to_map` om een toewijzing met bepaalde veldnaam en waardeparen te maken met behulp van objecten. Voor meer informatie, raadpleegt de handleiding voor [functies voor hiërarchieën - toewijzingen](../../data-prep/functions.md#map). </li><li>`array_to_map`: gebruik de functie `array_to_map` om een toewijzing met bepaalde veldnaam en waardeparen te maken met behulp van objectarrays. Voor meer informatie, raadpleegt u de handleiding voor [functies voor hiërarchieën - toewijzingen](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Voor meer informatie over gegevensvoorbereiding, raadpleegt u het [overzicht van gegevensvoorbereiding](../../data-prep/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| SQL weergeven | U kunt de SQL nu achter uw profielen, doelgroepen, bestemmingen, en aangepaste inzichten bekijken met de schakelaar SQL weergeven en vervolgens de query op aanvraag uitvoeren via de Query-editor. Door toegang te krijgen tot de SQL die uw Real-time Customer Data Platform-inzichten aanstuurt, krijgt u inzicht in de logica achter de analyse van uw datamodel. Deze transparantie maakt uw Adobe Real-time CDP-gegevens toegankelijker, gemakkelijker te begrijpen en impactvoller voor de besluitvorming.<br>Laat u inspireren door de SQL van meer dan 40 bestaande inzichten om nieuwe query&#39;s te maken die unieke inzichten uit platformgegevens afleiden op basis van uw zakelijke behoeften. De SQL is ook beschikbaar voor uw inzichten in [Profielen](../../dashboards/insights/profiles.md), [Doelgroepen](../../dashboards/insights/audiences.md) en [Bestemmingen](../../dashboards/insights/destinations.md) in de documentatie van de Experience League. In deze documenten worden de zakelijke gebruiksscenario&#39;s belicht die met de standaardinzichten kunnen worden beantwoord. Voor meer informatie, raadpleegt u de handleiding voor [het weergeven van SQL-inzichten](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Bestemmingen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met bestemmingsplatforms die een naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [Pubmatic-verbinding](../../destinations/catalog/advertising/pubmatic.md) | Gebruik deze bestemming om doelgroepgegevens naar het [!DNL PubMatic Connect]-platform te verzenden. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Nieuw verificatietype **Veronderstelde rol** voor Amazon S3-bestemmingen | Gebruik het nieuwe verificatietype Veronderstelde rol wanneer u Experience Platform verbindt met uw Amazon S3-buckets als u geen accountsleutels en geheime sleutels wilt delen met Experience Platform. Lees meer over de nieuwe verificatiemethode in de [sectie Verificatie](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) van de documentatie van Amazon S3. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Identiteitsservice {#identity-service}

Met Adobe Experience Platform Identity Service krijgt u een compleet beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen. Zo kunt u in real-time impactvolle, persoonlijke digitale ervaringen bieden.

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijgewerkt | Beschrijving |
| --- | --- |
| Herstructurering van documentatie | De documentatie van de Identity Service is opnieuw gestructureerd om de presentatie en duidelijkheid van concepten binnen de Identity Service te verbeteren:<ul><li>Bezoek de [overzichtspagina van Identity Service](../../identity-service/home.md) voor een uitgebreide terminologiegids, een gebruiksvoorbeeld waarin een typisch klanttraject wordt beschreven, een overzicht van hoe Identity Service identiteiten aan elkaar koppelt en een samenvatting van de rol die Identity Service daarin speelt binnen het Experience Platform-ecosysteem.</li><li>Raadpleeg de handleiding voor [inzicht in de verhouding tussen Identity Service en Real-Time Customer Profile](../../identity-service/identity-and-profile.md) voor een gedetailleerd overzicht van hoe de twee services samenwerken en de verschillen tussen hun doelen, processen, invoer en uitvoer.</li><li>Raadpleeg de [handleiding voor koppelingslogica van Identity Service](../../identity-service/features/identity-linking-logic.md) voor uitleg en visualisaties van hoe de identiteitsgrafiek zich gedraagt in verschillende scenario&#39;s en tijdstempels.</li></ul> |

{style="table-layout:auto"}

Voor meer informatie over Identity Service, raadpleegt u het [overzicht van Identity Service](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Real-Time Customer Data Platform ([!DNL Real-Time CDP]) is gebaseerd op Experience Platform en helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen te activeren met behulp van intelligente besluitvorming gedurende de hele klanttraject. [!DNL Real-Time CDP] combineert meerdere bedrijfsgegevensbronnen om klantprofielen in real-time te maken. Segmenten die op basis van deze profielen zijn samengesteld, kunnen vervolgens naar downstreambestemmingen worden verzonden om gepersonaliseerde één-op-één klantervaringen te bieden via alle kanalen en apparaten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates voor de [startpagina van Real-Time CDP](https://experience.adobe.com) | <ul><li>**Widget voor profielen**: u kunt nu de widget voor profielen gebruiken om naar de overzichtspagina van Profielen te gaan en profielstatistieken voor uw organisatie te bekijken.</li><li>**Kaart Profielstatistieken**: De kaart Profielstatistieken op het dashboard van de startpagina geeft nu het totale aantal profielen in uw organisatie weer, afhankelijk van uw respectievelijke samenvoegingsbeleid.</li><li>**Widget voor schema&#39;s**: u kunt nu de widget voor schema&#39;s gebruiken om naar de workflow voor het maken van schema&#39;s in de gebruikersinterface te gaan.</li></ul> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Documentatie bijgewerkt | Beschrijving |
| --- | --- |
| Nieuwe startpagina voor Real-Time CDP-documentatie | Bezoek de [nieuwe startpagina voor Real-Time CDP-documentatie](/help/rtcdp/home.md) om snel informatie te verkrijgen over hoe u aan de slag kunt gaan met het product, richtlijnen, voorbeeldgebruiksscenario&#39;s en nog veel meer. |
| Voorbeeldoverzicht van Real-Time CDP-gebruiksscenario&#39;s | Bezoek de [nieuwe overzichtspagina met voorbeeldgebruiksscenario&#39;s](/help/rtcdp/use-case-guides/overview.md) voor een verzameling voorbeeldgebruiksscenario&#39;s die uw organisatie met Real-Time CDP kan bereiken. |

{style="table-layout:auto"}

Voor meer informatie over Real-Time CDP kunt u het [Real-Time CDP-overzicht](../../rtcdp/overview.md) raadplegen.

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in het lokaliseren van de standaard dashboardkaarten van de profielkijker | De standaardprofielkaarten hebben nu dynamisch gelokaliseerde namen. Aangepaste profielkaarten kunnen nog steeds aangepaste namen bevatten die kunnen worden bewerkt. |

{style="table-layout:auto"}

Voor meer informatie over Real-Time Customer Profile, raadpleegt u het [overzicht van profielen](../../profile/home.md)

## Segmentatieservice {#segmentation}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Extern gegenereerde doelgroepupload | Het maximale aantal kolommen is verhoogd naar **25**. |
| Schattingen van Segment Builder | Schattingen en gekwalificeerde profielen worden nu weergegeven in de sectie met doelgroepeigenschappen. Voor meer informatie over deze verandering, raadpleegt u de [gebruikershandleiding voor de Segment Builder-gebruikersinterface](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] bronnen | Gebruik de [!DNL Oracle NetSuite]-integraties in de broncatalogus om gegevens van uw [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)- en [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md)-accounts naar Experience Platform over te zetten. |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents]-bron | U kunt de [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md)-integratie in de broncatalogus gebruiken om gegevens van uw [!DNL Braze]-account naar Experience Platform over te zetten. |
| Ondersteuning voor sleutelpaarverificatie voor [!DNL Snowflake]-batchbron | U kunt nu sleutelpaarverificatie gebruiken bij het maken van een nieuw [!DNL Snowflake]-account voor batchgegevens. Voor meer informatie leest u de handleiding voor [het maken van een  [!DNL Snowflake] -account met behulp van de API](../../sources/tutorials/api/create/databases/snowflake.md) of de handleiding voor het [het maken van een  [!DNL Snowflake] -account met behulp van de gebruikersinterface](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u het [overzicht van bronnen](../../sources/home.md).
