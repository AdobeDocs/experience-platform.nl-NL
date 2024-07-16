---
title: Adobe Experience Platform Release Notes April 2022
description: Aanvullende informatie van april 2022 voor Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '2547'
ht-degree: 4%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 27 april 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [Gegevensstromen](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B Edition](#B2B)
- [Bronnen](#sources)

## [!DNL Dashboards] {#dashboards}

Platform biedt meerdere dashboards waardoor u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen wordt vastgelegd.

De dashboards verstrekken pre-gevormde rapporteringsopties voor de gegevens van uw organisatie en zijn direct in de markeringenwerkschema binnen Platform gebouwd. Deze dashboards zijn beschikbaar zonder de behoefte aan extra steun van IT of de tijd en de inspanning het anders zou vergen om gegevens met extra het opslagontwerp en implementatie van gegevens uit te voeren en te verwerken.

De volgende widgets zijn beschikbaar via de widgetbibliotheek op hun respectieve dashboards. Zie de documentatie voor meer informatie over [ hoe te om widgets door de bibliotheek van Widget toe te voegen ](../../dashboards/customize/widget-library.md).

**Nieuwe widgets**

| Widget | Dashboard | Beschrijving |
| ------ | --------- | ----------- |
| [!UICONTROL Profiles added trend] | Profielen | Deze widget gebruikt een lijngrafiek om het totale aantal samengevoegde profielen te illustreren die de afgelopen 30 dagen, 90 dagen, of 12 maanden dagelijks aan de opslag van het Profiel zijn toegevoegd. |
| [!UICONTROL Audiences mapped to destination status] | Profielen | Deze widget geeft het totale aantal in kaart gebrachte en niet-toegewezen doelgroepen in één meting weer en gebruikt een donutdiagram om het proportionele verschil tussen de totalen aan te geven. |
| [!UICONTROL Audiences size] | Profielen | Deze widget biedt een tabel met twee kolommen met maximaal 20 segmenten en het totale aantal soorten publiek in elk segment. De lijst is afhankelijk van het toegepaste samenvoegingsbeleid en wordt van hoog tot laag geordend volgens het totale aantal doelgroepen. |
| [!UICONTROL Profile count trend] | Profielen | Deze widget gebruikt een lijngrafiek om de trend in het totale aantal profielen in het systeem in tijd te illustreren. De gegevens kunnen gedurende perioden van 30 dagen, 90 dagen en 12 maanden worden weergegeven. |
| [!UICONTROL Single identity profiles by identity] | Profielen | Deze widget gebruikt een staafdiagram om het totale aantal profielen te illustreren dat met slechts één unieke id wordt geïdentificeerd. De widget ondersteunt maximaal vijf van de meest voorkomende identiteiten. |
| [!UICONTROL Destination status] | Doelen | Deze widget geeft het totale aantal ingeschakelde bestemmingen als één enkele metrische waarde weer en gebruikt een doughnut grafiek om het proportionele verschil tussen toegelaten en gehandicapte bestemmingen te illustreren. |
| [!UICONTROL Active destinations by destination platform] | Doelen | Deze widget gebruikt een twee-kolom lijst om een lijst van actieve bestemmingsplatforms en het totale aantal actieve bestemmingen voor elk bestemmingsplatform te tonen. |
| [!UICONTROL Activated audiences across all destinations] | Doelen | Deze widget biedt het totale aantal soorten publiek dat op alle doelen in één meting is geactiveerd. |
| [!UICONTROL Audience activation order] | Segmenten | Deze widget biedt een tabel met drie kolommen met de doelnaam, het platform en de activeringsdatum van het publiek. |
| [!UICONTROL Audience size trend] | Segmenten | Deze widget biedt een illustratie van de lijngrafiek voor het totale aantal profielen dat gedurende 30 dagen, 90 dagen en perioden van 12 maanden aan de criteria van om het even welke segmentdefinitie voldoet. |
| [!UICONTROL Audience size change trend] | Segmenten | Deze widget geeft een lijngrafiekillustratie van het verschil in het totale aantal profielen dat voor een bepaald segment in aanmerking kwam tussen de meest recente dagelijkse momentopnamen. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. |
| [!UICONTROL Audience size trend by identity] | Segmenten | Deze widget illustreert de trend van de publieksgrootte voor een bepaald segment dat op een geselecteerd identiteitstype wordt gebaseerd. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. |

**Nieuwe eigenschappen** {#new-features}

| Functie | Dashboard | Beschrijving |
| ------- | --------- | ----------- |
| Opschonen van segment met weesprofiel | Profielen en licentiegebruik | De Dienst van het profiel verwijdert nu achtergebleven segmentleden op een dagelijkse basis om een nauwkeurigere vertegenwoordiging van uw profielen in uw systeem te geven. Deze opschoning vindt plaats nadat alle profielfragmenten voor een bepaald profiel zijn verwijderd. Dit kan een daling in &quot;Adressable publiek&quot;metrisch in het dashboard van het vergunningsgebruik tonen en kan een daling in &quot;Aantal van het Profiel&quot;metrisch in het dashboard van het Profiel tonen, aangezien deze metriek overgebleven segmentfragmenten voorafgaand aan deze versie omvatte. |

{style="table-layout:auto"}

Zie de documentatie voor meer informatie over [[!DNL Profiles]](../../dashboards/guides/profiles.md) -, [[!DNL Destinations]](../../dashboards/guides/destinations.md) - en [[!DNL Segments]](../../dashboards/guides/audiences.md) dashboards.

## Gegevensstromen {#dataflows}

In Platform, worden de gegevens opgenomen van vele verschillende bronnen, binnen het systeem geanalyseerd, en geactiveerd aan een brede verscheidenheid van bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Dataflows zijn een weergave van taken die gegevens over het hele platform verplaatsen. Deze dataflows worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door de Dienst van de Identiteit en het Profiel van de Klant in real time alvorens uiteindelijk aan bestemmingen wordt geactiveerd wordt gebruikt.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Segmentdashboard | U kunt het controledashboard nu gebruiken om de gegevensstromen voor segmenten te controleren. Om meer te leren, te lezen gelieve de gids op [ controlesegmenten in UI ](../../dataflows/ui/monitor-audiences.md) |

Voor meer algemene informatie over dataflows, verwijs naar het [ dataflows overzicht ](../../dataflows/home.md). Meer over segmentatie leren, verwijs naar het [ segmentatieoverzicht ](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor Adobe Analytics-bron | De Adobe Analytics-bron biedt nu ondersteuning voor functies voor het voorvertonen van gegevens, zodat u uw gegevens uit de Analytics-rapportenreeks kunt toewijzen aan een doel-XDM-schema wanneer u een gegevensstroom maakt. Zie het leerprogramma op [ creërend een Analytics bronverbinding ](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie. |
| Ondersteuning voor het importeren van bestaande toewijzingsregels | U kunt nu toewijzingsregels importeren uit een bestaande gegevensstroom om uw databaseconfiguraties te versnellen en fouten te beperken. Zie het leerprogramma bij [ het invoeren van bestaande toewijzingsregels ](../../data-prep/ui/mapping.md) voor meer informatie. |

Voor meer informatie over [!DNL Data Prep], gelieve te zien het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ----------- | ----------- |
| Geavanceerde Enterprise-doelconnectors | Drie bedrijfsdoelconnectors zijn nu over het algemeen beschikbaar: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md) , [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md) en [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md) . <br> De algemene beschikbaarheid van bedrijfsdoelconnectors omvat alle mogelijkheden die eerder in de Beta-fase werden aangeboden, en meer: <ul><li>De nieuwe authentificatiemogelijkheden, met inbegrip van [ Gedeelde Ondertekening van de Toegang in de Hubs van de Gebeurtenis van de Gebeurtenis van de Gebeurtenis ](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) en meer [ authentificatietypen ](../../destinations/catalog/streaming/http-destination.md#authentication-information) (tokens aan tokens, OAuth 2) in de bestemming van HTTP API;</li><li>[ het Steunen van historische profielgegevens ](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (verzendend historische profielen die voor het segment worden gekwalificeerd wanneer eerst geactiveerd);</li><li>Dataflow loopmetriek wordt nu gesteund voor deze bestemmingen;</li><li>[ extra segmentmeta-gegevens ](../../destinations/catalog/streaming/http-destination.md#destination-details) inbegrepen in de gegevensuitkering, met inbegrip van segmentnamen en segmenttimestamps;</li><li>Steun voor [ statische IP adressen ](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor klanten die Experience Platform moeten lijsten van gewenste personen.</li></ul> |
| In-context alarm voor bestemmingsdataflows | U kunt [ nu aan alarm ](../../destinations/ui/alerts.md) intekenen wanneer het creëren van een bestemmingsdataflow, om waakzame berichten betreffende de status, het succes, of de mislukking van uw dataflow looppas te ontvangen. U kunt ervoor kiezen waarschuwingen te ontvangen in de gebruikersinterface van het Experience Platform of via e-mail. |

### Geen proces voor geavanceerde bedrijfsdoelconnectors {#release-process-enterprise-destinations}

Voor Amazon Kinesis, Azure Event Hubs, en HTTP API bestemmingen, tijdens het versieproces (die 27 april begint), zult u zowel de vroegere Beta bestemmingskaart, evenals de nieuwe algemeen beschikbare (GA) bestemmingskaart in de bestemmingscatalogus zien. Om het even welke gegevensstromen die door klanten worden gevormd die de bètabestemmingen gebruiken zullen in de volgende dagen aan de GA versie van de zelfde bestemming worden gemigreerd. Deze migratie zou uiteindelijk moeten zijn voltooid tegen het einde van dag vrijdag 29 april. De bestemmingen van Beta zullen tijdens dit korte tijd-venster zichtbaar blijven en geëtiketteerd als **Vervangen**.

Als u deze bestemmingen in de fase van Beta hebt gebruikt, gelieve te merken op het volgende:

- Als u al eerder in Beta met een van de drie doelen bent geweest, is er geen actie nodig. Alle gegevensstromen die als onderdeel van Beta worden ingesteld, blijven functioneel en worden gemigreerd naar de GA-versie.
- Als u deze bestemmingen vanaf 27 april wilt instellen, gelieve dit te doen met de nieuwe GA-versie van de bestemmingen.
- De als afgekeurd gemarkeerde bètakaarten worden verwijderd zodra de releasebewerking is voltooid, naar schatting tegen het einde van dag 29 april. Het technische team van het Experience Platform volgt nauwlettend voor een succesvolle versieverrichting.

**Nieuwe bestemmingen**

| Doel | Beschrijving |
| ----------- | ----------- |
| [!DNL Criteo] | Maak verbinding met en activeer gegevens naar het [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) advertentieplatform. |
| [!DNL Sendgrid] | Verbind en activeer gegevens aan het [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) platform voor transactie en marketing e-mail. |

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Afzonderlijke standaardvelden voor een schema toevoegen of verwijderen | De Redacteur UI van het Schema staat u nu toe om gedeelten standaardgebiedsgroepen aan uw schema&#39;s toe te voegen, die meer flexibiliteit voor de gebieden verstrekken u verkiest te omvatten zonder het moeten douanemiddelen van kras bouwen.<br><br> u kunt nu ad hoc douanegebieden direct binnen de schemastructuur ook bepalen en hen toewijzen aan een nieuwe of bestaande groep van het douaneveld zonder het moeten tot stand brengen of de gebiedsgroep van tevoren uitgeven.<br><br> zie de gids op [ creërend en het uitgeven schema&#39;s in UI ](../../xdm/ui/resources/schemas.md) voor meer informatie over deze nieuwe werkschema&#39;s. |

{style="table-layout:auto"}

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Hiermee legt u de details vast van een verzoek om gegevens te wissen om records in een opgegeven gegevensset of sandbox te verwijderen of te wijzigen. |
| Descriptor | [[!UICONTROL Time-series Granularity Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Geeft de granulariteit van tijdreeksen en samenvattingsgegevens aan. Wanneer het op een schema wordt toegepast, is het `timestamp` gebied van het schema eerste timestamp in een periode van deze granulariteit. |
| Klasse | [[!UICONTROL XDM Summary Metrics]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Verstrekt vooraf samengevatte metriek met groeperingsdimensies, zoals de resultaten van SQL UITGEZOCHT met GROUP DOOR. |
| Veldgroep | [[!UICONTROL Consent policies evaluation results map]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | Vangt het resultaat van de beoordeling van het toestemmingsbeleid voor een individu. |
| Veldgroep | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Vangt plaats-onderzoek verwante informatie zoals onderzoeksvraag, het filtreren, en het opdracht geven tot. |
| Veldgroep | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Hiermee legt u de details vast van een gebeurtenis waarbij twee of meer leads worden samengevoegd. |
| Veldgroep | [[!UICONTROL Email Sent]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Hiermee legt u de details vast van een gebeurtenis waarbij een e-mailbericht naar een ontvanger wordt verzonden. |
| Veldgroep | [[!UICONTROL Stitching Fields]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Hiermee legt u waarden vast die zijn berekend via het identiteitsstitching-proces voor een gebeurtenis. |
| Veldgroep | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Een Adobe Journey Optimizer gebiedsgroep die een secundair ontvangend detail voor een controle vangt. |
| Veldgroep | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hiermee worden gegevens vastgelegd die betrekking hebben op een relatie tussen een rekeningpersoon. |
| Veldgroep | [[!UICONTROL Account Person Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hiermee worden gegevens vastgelegd die betrekking hebben op een relatie tussen een rekeningpersoon. |
| Gegevenstype | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Leg informatie vast over een winkelwagentje voor e-handel. |
| Gegevenstype | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Vangt verzendgegevens voor een of meer producten. |
| Gegevenstype | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | Hiermee legt u gegevens vast over zoekactiviteiten ter plaatse. |
| Extensie (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Hiermee legt u details vast met betrekking tot een operationele taak. |
| Extensie (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Hiermee legt u gegevens vast die betrekking hebben op een werkportfolio. |
| Extensie (Workfront) | [[!UICONTROL Work Program Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Hiermee legt u de details van een werkprogramma vast. |
| Extensie (Workfront) | [[!UICONTROL Work Project Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Hiermee legt u details vast met betrekking tot een werkproject. |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nieuwe opsommingswaarden voor `destinationCategory` . |
| Descriptor | [[!UICONTROL Friendly Name Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Extra ondersteuning voor het verwijderen van voorgestelde waarden (`meta:enum`) die niet nodig zijn in standaardvelden. |
| Veldgroep | [[!UICONTROL User Login Process]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` veld toegevoegd. |
| Gegevenstype | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Er zijn verschillende tekstvelden toegevoegd die betrekking hebben op winkelwagentjes. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nieuwe velden toegevoegd voor geselecteerde opties en kortingsbedrag. |
| Extensie (intelligente diensten) | [[!UICONTROL Intelligent Services JourneyAI Send Time Optimization]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimaliseer opslagindeling voor scores tijdens het verzenden. |
| Extensie (Workfront) | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Verschillende velden die zijn vervangen door een `workfront:customData` -veld voor aangepaste formuliervelden. |
| Extensie (Workfront) | [[!UICONTROL Work Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Verschillende velden toegevoegd. |
| Extensie (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nieuwe velden voor het bovenliggende objecttype en aangepaste formuliervelden. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

Met AI/ML-services kunnen marketinganalisten en praktijkmensen gebruikmaken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen voor de klant. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Attribution AI

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor meerdere gegevenssets | De Multi eigenschap van de Dataset van de Dataset steunt nu alle datasets van de Gebeurtenis van de Ervaring evenals de selectie van de Kaart van de Identiteit als identiteit. De klanten kunnen de Kaart van de Identiteit en om het even welke bijbehorende IDs selecteren zolang er een gemeenschappelijke identiteitsnaamruimte over datasets is. Attribution AI ondersteunt de volgende schema&#39;s: Adobe Analytics, Experience Event, Consumer Experience Event. Voor meer informatie over MultiDataset steun in Attribution AI, verwijs naar de [ gebruikersgids van de Attribution AI ](../../intelligent-services/attribution-ai/user-guide.md). |

Voor meer informatie over [!DNL Intelligent Services], gelieve te zien het [[!DNL Intelligent Services]  overzicht ](../../intelligent-services/home.md).

### Customer AI

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren. Dit wordt bereikt zonder de bedrijfsbehoeften te hoeven omzetten in een machine learning-probleem, een algoritme te kiezen, te trainen of te implementeren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor meerdere gegevenssets | De Multi eigenschap van de Dataset van de Dataset steunt nu alle datasets van de Gebeurtenis van de Ervaring evenals de selectie van de Kaart van de Identiteit als identiteit. De klanten kunnen de Kaart van de Identiteit en om het even welke bijbehorende IDs selecteren zolang er een gemeenschappelijke identiteitsnaamruimte over datasets is. AI van de klant ondersteunt de volgende schema&#39;s: Adobe Analytics, Experience Event, Consumer Experience Event en het Adobe Audience Manager-schema. Voor meer informatie over de MultiSteun van de Dataset in Klant AI, verwijs naar de [ gebruikersgids van de Klant AI ](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nieuwe maatstaven voor modelevaluatie in Customer AI | Met nieuwe winstkaarten in AI-kaarten van klanten kunnen marketers de groepsgrootte bepalen op basis van hun budget- en ROI-doelstellingen. Met nieuwe diagrammen kunt u de kwaliteit van het model meten, zodat u een betere zichtbaarheid krijgt in de lift die ze boven willekeurige doelen kunnen plaatsen. Voor meer informatie, zie [ inzichten met het document van AI van de Klant ](../../intelligent-services/customer-ai/user-guide/discover-insights.md) ontdekken. |

Voor meer informatie over [!DNL Intelligent Services], gelieve te zien het [[!DNL Intelligent Services]  overzicht ](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B Edition {#B2B}

Real-Time CDP B2B Edition is gebaseerd op Real-time Customer Data Platform (Real-Time CDP) en is speciaal ontworpen voor marketers die werken in een servicemodel voor bedrijven. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen in dienst te nemen.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor `isDeleted` -functionaliteit | Alle [!DNL Marketo] datasets behalve `Activities` ondersteunen nu de `isDeleted` -toewijzing. De nieuwe toewijzing wordt automatisch toegevoegd aan uw bestaande B2B dataflows. Met de toewijzing `isDeleted` kunt u records filteren die zijn verwijderd, zodat de gegevens in [!DNL Data Lake] consistent zijn met de brongegevens. Zie de [[!DNL Marketo]  gids van kaartgebieden ](../../sources/connectors/adobe-applications/mapping/marketo.md) voor meer informatie over `isDeleted`. |

Meer over de Uitgave van Real-time Customer Data Platform B2B leren, zie het [ B2B overzicht ](../../rtcdp/b2b-overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor [!DNL OneTrust Integration] | U kunt nu de [!DNL OneTrust Integration] -bron gebruiken om toestemmings- en voorkeursgegevens in te voeren van uw [!DNL OneTrust] -account naar Platform. Zie de documentatie bij [ het creëren van a  [!DNL OneTrust Integration]  bronverbinding ](../../sources/connectors/consent-and-preferences/onetrust.md) voor meer informatie. |
| Ondersteuning voor [!DNL Square] | U kunt nu de [!DNL Square] -bron gebruiken om betalingsgegevens van uw [!DNL Square] -account in te voeren naar Platform. |
| Ondersteuning voor het verwijderen van klantkenmerkgegevensstromen | U kunt nu dataflows verwijderen die zijn gemaakt met de bronconnector Klantkenmerken. |

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
