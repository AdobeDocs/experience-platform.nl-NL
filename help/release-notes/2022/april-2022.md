---
title: Opmerkingen bij de release van Adobe Experience Platform, april 2022
description: In de release van april 2022 staat een opmerking voor Adobe Experience Platform.
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: d4a4baf330925d6696f515bf650d86740c18e97c
workflow-type: tm+mt
source-wordcount: '2585'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 27 april 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Dashboards]](#dashboards)
- [Gegevensstromen](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [Real-time Customer Data Platform B2B Edition](#B2B)
- [Bronnen](#sources)

## [!DNL Dashboards] {#dashboards}

Platform biedt meerdere dashboards waardoor u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

De dashboards verstrekken pre-gevormde rapporteringsopties voor de gegevens van uw organisatie en zijn direct ingebouwd in het markeringswerkschema binnen Platform. Deze dashboards zijn beschikbaar zonder de behoefte aan extra steun van IT of de tijd en de inspanning het anders zou vergen om gegevens met extra het opslagontwerp en implementatie van gegevens uit te voeren en te verwerken.

De volgende widgets zijn beschikbaar via de widgetbibliotheek op hun respectieve dashboards. Zie de documentatie voor meer informatie over [widgets toevoegen via de Widget-bibliotheek](../../dashboards/customize/widget-library.md).

| Functie | Dashboard | Beschrijving |
| --------------------------------------------------------- | ------------- | ----------- |
| [!UICONTROL Profiles added trend] | Profielen | Deze widget gebruikt een lijngrafiek om het totale aantal samengevoegde profielen te illustreren die de afgelopen 30 dagen, 90 dagen, of 12 maanden dagelijks aan de Opslag van het Profiel zijn toegevoegd. |
| [!UICONTROL Audiences mapped to destination status] | Profielen | Deze widget geeft het totale aantal in kaart gebrachte en niet-toegewezen doelgroepen in één meting weer en gebruikt een donutdiagram om het proportionele verschil tussen de totalen aan te geven. |
| [!UICONTROL Audiences size] | Profielen | Deze widget biedt een tabel met twee kolommen met maximaal 20 segmenten en het totale aantal soorten publiek in elk segment. De lijst is afhankelijk van het toegepaste samenvoegingsbeleid dat van hoog tot laag wordt bevolen volgens het totale aantal soorten publiek. |
| [!UICONTROL Profile count trend] | Profielen | Deze widget gebruikt een lijngrafiek om de trend in het totale aantal profielen in het systeem in tijd te illustreren. De gegevens kunnen gedurende perioden van 30 dagen, 90 dagen en 12 maanden worden weergegeven. |
| [!UICONTROL Single identity profiles by identity] | Profielen | Deze widget gebruikt een staafdiagram om het totale aantal profielen te illustreren dat met slechts één unieke id wordt geïdentificeerd. De widget ondersteunt maximaal vijf van de meest voorkomende identiteiten. |
| [!UICONTROL Destination status] | Doelen | Deze widget geeft het totale aantal ingeschakelde bestemmingen als één enkele metrische waarde weer en gebruikt een doughnut grafiek om het proportionele verschil tussen toegelaten en gehandicapte bestemmingen te illustreren. |
| [!UICONTROL Active destinations by destination platform] | Doelen | Deze widget gebruikt een twee-kolom lijst om een lijst van actieve bestemmingsplatforms en het totale aantal actieve bestemmingen voor elk bestemmingsplatform te tonen. |
| [!UICONTROL Activated audiences across all destinations] | Doelen | Deze widget biedt het totale aantal soorten publiek dat op alle doelen in één meting is geactiveerd. |
| [!UICONTROL Audience activation order] | Segmenten | Deze widget biedt een tabel met drie kolommen met de doelnaam, het platform en de activeringsdatum van het publiek. |
| [!UICONTROL Audience size trend] | Segmenten | Deze widget biedt een illustratie van de lijngrafiek voor het totale aantal profielen dat gedurende 30 dagen, 90 dagen en perioden van 12 maanden aan de criteria van om het even welke segmentdefinitie voldoet. |
| [!UICONTROL Audience size change trend] | Segmenten | Deze widget geeft een lijngrafiekillustratie van het verschil in het totale aantal profielen dat voor een bepaald segment in aanmerking kwam tussen de meest recente dagelijkse momentopnamen. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. |
| [!UICONTROL Audience size trend by identity] | Segmenten | Deze widget illustreert de trend van de publieksgrootte voor een bepaald segment dat op een geselecteerd identiteitstype wordt gebaseerd. De periode van trendanalyse kan over 30 dagen, 90 dagen, en periodes van 12 maanden worden visualiseerd. |

Zie de documentatie voor meer informatie over [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md), en [[!DNL Segments]](../../dashboards/guides/segments.md) dashboards.

## Gegevensstromen {#dataflows}

In Platform, worden de gegevens opgenomen van vele verschillende bronnen, binnen het systeem geanalyseerd, en geactiveerd aan een brede verscheidenheid van bestemmingen. Platform maakt het proces om deze potentieel niet-lineaire stroom van gegevens te volgen gemakkelijker door transparantie van gegevensstromen te verstrekken.

Gegevensstromen zijn een weergave van taken die gegevens over het Platform verplaatsen. Deze gegevensstromen worden gevormd over de verschillende diensten, die gegevens van bronschakelaars aan doeldatasets helpen bewegen, waar het dan door de Dienst van de Identiteit en het Profiel van de Klant in real time alvorens uiteindelijk aan bestemmingen wordt geactiveerd wordt gebruikt.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Segmentdashboard | U kunt het controledashboard nu gebruiken om de gegevensstromen voor segmenten te controleren. Lees de handleiding voor meer informatie op [het controleren van segmenten in UI](../../dataflows/ui/monitor-segments.md) |

Voor meer algemene informatie over gegevensstromen raadpleegt u de [gegevensstroomoverzicht](../../dataflows/home.md). Als u meer wilt weten over segmentatie, raadpleegt u de [segmentatieoverzicht](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor Adobe Analytics-bron | De Adobe Analytics-bron biedt nu ondersteuning voor functies voor het voorvertonen van gegevens, zodat u uw gegevens uit de Analytics-rapportenreeks kunt toewijzen aan een doel-XDM-schema wanneer u een gegevensstroom maakt. Zie de zelfstudie aan [een verbinding met een bron voor Analytics maken](../../sources/tutorials/ui/create/adobe-applications/analytics.md) voor meer informatie . |
| Ondersteuning voor het importeren van bestaande toewijzingsregels | U kunt nu toewijzingsregels importeren uit een bestaande gegevensstroom om uw databaseconfiguraties te versnellen en fouten te beperken. Zie de zelfstudie aan [bestaande toewijzingsregels importeren](../../data-prep/ui/mapping.md) voor meer informatie . |

Voor meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| Geavanceerde Enterprise-doelconnectors | Drie schakelaars van de ondernemingsbestemming zijn nu over het algemeen beschikbaar: [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md), en [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> De algemene beschikbaarheid van de schakelaars van de ondernemingsbestemming omvat alle mogelijkheden die eerder in de bètafase, en meer worden aangeboden: <ul><li>Nieuwe verificatiemogelijkheden, waaronder [Shared Access Signature in Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) en meer [verificatietypen](../../destinations/catalog/streaming/http-destination.md#authentication-information) (tokens aan toonder, OAuth 2) in de HTTP API-bestemming;</li><li>[Back-up maken van historische profielgegevens](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) (het verzenden van historische profielen die voor het segment in aanmerking komen wanneer zij voor het eerst worden geactiveerd);</li><li>Dataflow loopmetriek wordt nu gesteund voor deze bestemmingen;</li><li>[Aanvullende segmentmetagegevens](../../destinations/catalog/streaming/http-destination.md#destination-details) opgenomen in de gegevenslading, met inbegrip van segmentnamen en segmenttijdstempels;</li><li>Ondersteuning voor [statische IP-adressen](/help/destinations/catalog/streaming/ip-address-allow-list.md) voor klanten die Experience Platform moeten lijsten van gewenste personen.</li></ul> |
| In-context alarm voor bestemmingsdataflows | U kunt nu [signaleren](../../destinations/ui/alerts.md) wanneer het creëren van een bestemmingsgegevensstroom, om waakzame berichten betreffende de status, het succes, of het mislukken van uw dataflow looppas te ontvangen. U kunt ervoor kiezen waarschuwingen te ontvangen in de gebruikersinterface van het Experience Platform of via e-mail. |

### Geen proces voor geavanceerde bedrijfsdoelconnectors {#release-process-enterprise-destinations}

Voor Amazon Kinesis, Azure Event Hubs, en HTTP API bestemmingen, tijdens het versieproces (die 27 april begint), zult u zowel de vroegere Beta bestemmingskaart, evenals de nieuwe algemeen beschikbare (GA) bestemmingskaart in de bestemmingscatalogus zien. Om het even welke gegevensstromen die door klanten worden gevormd die de bètabestemmingen gebruiken zullen in de volgende dagen aan de GA versie van de zelfde bestemming worden gemigreerd. Deze migratie zou uiteindelijk moeten zijn voltooid tegen het einde van dag vrijdag 29 april. De bètadoelen blijven zichtbaar tijdens dit korte tijdvenster en worden gelabeld als **Vervangen**.

Als u deze bestemmingen in de fase van Bèta hebt gebruikt, gelieve nota te nemen van het volgende:

- Als eerder in Bèta met om het even welke 3 bestemmingen geweest zijn, is geen actie nodig. Alle gegevensstromen die als deel van Beta worden opgezet zullen functioneel blijven en aan de versie GA worden gemigreerd.
- Als u deze bestemmingen vanaf 27 april wilt instellen, gelieve dit te doen met de nieuwe GA-versie van de bestemmingen.
- De als afgekeurd gemarkeerde bètakaarten worden verwijderd zodra de releasebewerking is voltooid, naar schatting tegen het einde van dag 29 april. Het technische team van het Experience Platform volgt nauwlettend voor een succesvolle versieverrichting.

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [!DNL Criteo] | Gegevens verbinden met en activeren op de [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) reclameplatform. |
| [!DNL Sendgrid] | Gegevens verbinden met en activeren op de [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) platform voor e-mails over transacties en marketing. |

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Afzonderlijke standaardvelden voor een schema toevoegen of verwijderen | De Redacteur UI van het Schema staat u nu toe om gedeelten standaardgebiedsgroepen aan uw schema&#39;s toe te voegen, die meer flexibiliteit voor de gebieden verstrekken u verkiest te omvatten zonder het moeten douanemiddelen van kras bouwen.<br><br>U kunt aangepaste ad-hocvelden nu ook rechtstreeks definiëren in de schemastructuur en deze toewijzen aan een nieuwe of bestaande aangepaste veldgroep zonder dat u de veldgroep vooraf hoeft te maken of te bewerken.<br><br>Zie de handleiding op [schema&#39;s maken en bewerken in de gebruikersinterface](../../xdm/ui/resources/schemas.md) voor meer informatie over deze nieuwe workflows. |

{style=&quot;table-layout:auto&quot;}

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL Data Hygiene Operation Request]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | Hiermee legt u de details vast van een verzoek om gegevens te wissen om records in een opgegeven gegevensset of sandbox te verwijderen of te wijzigen. |
| Descriptor | [[!UICONTROL Time-series Granularity Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | Geeft de granulariteit van tijdreeksen en samenvattingsgegevens aan. Wanneer toegepast op een schema, de schema&#39;s `timestamp` field is de eerste tijdstempel in een periode van deze granulariteit. |
| Klasse | [[!UICONTROL XDM Summary Metrics]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | Verstrekt vooraf samengevatte metriek met groeperingsdimensies, zoals de resultaten van SQL UITGEZOCHT met GROUP DOOR. |
| Veldgroep | [[!UICONTROL Consent policies evaluation results map]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Vangt het resultaat van de beoordeling van het toestemmingsbeleid voor een individu. |
| Veldgroep | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Vangt plaats-onderzoek verwante informatie zoals onderzoeksvraag, het filtreren, en het opdracht geven tot. |
| Veldgroep | [[!UICONTROL Merge Leads]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | Hiermee legt u de details vast van een gebeurtenis waarbij twee of meer leads worden samengevoegd. |
| Veldgroep | [[!UICONTROL Email Sent]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | Hiermee legt u de details vast van een gebeurtenis waarbij een e-mailbericht naar een ontvanger wordt verzonden. |
| Veldgroep | [[!UICONTROL Stitching Fields]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | Hiermee legt u waarden vast die zijn berekend via het identiteitsstitching-proces voor een gebeurtenis. |
| Veldgroep | [[!UICONTROL Secondary Recipient Detail For Audit]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Een Adobe Journey Optimizer gebiedsgroep die een secundair ontvangend detail voor een controle vangt. |
| Veldgroep | [[!UICONTROL XDM Business Account Person Relation Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hiermee worden gegevens vastgelegd die betrekking hebben op een relatie tussen een rekeningpersoon. |
| Veldgroep | [[!UICONTROL Account Person Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | Hiermee worden gegevens vastgelegd die betrekking hebben op een relatie tussen een rekeningpersoon. |
| Gegevenstype | [[!UICONTROL Cart]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | Leg informatie vast over een winkelwagentje voor e-handel. |
| Gegevenstype | [[!UICONTROL Shipping]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | Vangt verzendgegevens voor een of meer producten. |
| Gegevenstype | [[!UICONTROL Site Search]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | Hiermee legt u gegevens vast over zoekactiviteiten ter plaatse. |
| Extensie (Workfront) | [[!UICONTROL Operational Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | Hiermee legt u gegevens vast over een operationele taak. |
| Extensie (Workfront) | [[!UICONTROL Work Portfolio Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | Hiermee legt u gegevens vast die betrekking hebben op een werkportfolio. |
| Extensie (Workfront) | [[!UICONTROL Work Program Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | Hiermee legt u de details van een werkprogramma vast. |
| Extensie (Workfront) | [[!UICONTROL Work Project Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | Hiermee legt u de details van een werkproject vast. |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Algemeen schema | [[!UICONTROL Destinations]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | Nieuwe opsommingswaarden voor `destinationCategory`. |
| Descriptor | [[!UICONTROL Friendly Name Descriptor]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | Extra ondersteuning voor het verwijderen van voorgestelde waarden (`meta:enum`) die niet nodig zijn vanuit standaardvelden. |
| Veldgroep | [[!UICONTROL User Login Process]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` toegevoegd. |
| Gegevenstype | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | Er zijn verschillende tekstvelden toegevoegd die betrekking hebben op winkelwagentjes. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Nieuwe velden toegevoegd voor geselecteerde opties en kortingsbedrag. |
| Extensie (intelligente diensten) | [[!UICONTROL Intelligent Services JourneyAI Send Time Optimization]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | Optimaliseer opslagindeling voor scores tijdens het verzenden. |
| Extensie (Workfront) | [[!UICONTROL Workfront Change Event]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | Verschillende velden vervangen door een `workfront:customData` veld voor aangepaste formuliervelden. |
| Extensie (Workfront) | [[!UICONTROL Work Task Attributes]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | Verschillende velden toegevoegd. |
| Extensie (Workfront) | [[!UICONTROL Work Object]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | Nieuwe velden voor het type bovenliggend object en aangepaste formuliervelden. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

Intelligente services stellen marketinganalisten en praktijkmensen in staat om gebruik te maken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen van de klantervaring. Dit staat voor marketing analisten toe om voorspellingen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

Met Attribution AI en Customer AI kunnen klanten geavanceerde AI/ML-modellen configureren voor marketingtoewijzing en klantgevoeligheid. De Multi eigenschap van de Dataset helpt klanten om veelvoudige datasets op het tijdstip van modelconfiguratie in te brengen zonder de behoefte om gegevens vooraf te verbinden en voor te bereiden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor meerdere gegevenssets | De Multi eigenschap van de Dataset van de Dataset steunt nu alle datasets van de Gebeurtenis van de Ervaring evenals de selectie van de Kaart van de Identiteit als identiteit. De klanten kunnen de Kaart van de Identiteit en om het even welke bijbehorende IDs selecteren zolang er een gemeenschappelijke identiteitsnaamruimte over datasets is. Attribution AI ondersteunt de volgende schema&#39;s: Adobe Analytics, Experience Event, Consumer Experience Event. De AI van de klant steunt al deze schema&#39;s plus het schema van Adobe Audience Manager. Raadpleeg voor meer informatie over ondersteuning voor meerdere gegevenssets in Attribution AI &amp; Customer AI de [Gebruikershandleiding voor Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) en [Handleiding voor AI-gebruikers van klant](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Nieuwe maatstaven voor modelevaluatie in AI van de Klant | Met nieuwe winstkaarten in AI-kaarten van klanten kunnen marketers de groepsgrootte bepalen op basis van hun budget- en ROI-doelstellingen. Met nieuwe diagrammen kunt u de kwaliteit van het model meten, zodat u een betere zichtbaarheid krijgt in de lift die ze boven willekeurige doelen kunnen plaatsen. Zie voor meer informatie de [inzichten met Customer AI ontdekken](../../intelligent-services/customer-ai/user-guide/discover-insights.md) document. |

Voor meer informatie over [!DNL Intelligent Services], zie de [[!DNL Intelligent Services] overzicht](../../intelligent-services/home.md).

## Real-time Customer Data Platform B2B Edition {#B2B}

Gebaseerd op Real-time Customer Data Platform (Real-Time CDP), is de Echte - tijdCDP B2B Uitgave speciaal-gebouwd voor marketers die in een zaken-aan-zaken de dienstmodel werken. Het verenigt gegevens uit veelvoudige bronnen en combineert het in één enkele mening van mensen en rekeningsprofielen. Deze verenigde gegevens staan marketers toe om specifiek publiek nauwkeurig te richten en dat publiek over alle beschikbare kanalen te betrekken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor `isDeleted` functionaliteit | Alles [!DNL Marketo] gegevenssets, behalve `Activities` nu de `isDeleted` toewijzing. De nieuwe toewijzing wordt automatisch toegevoegd aan uw bestaande B2B dataflows. U kunt de `isDeleted` toewijzen aan filtergegevens die zijn verwijderd, zodat de gegevens in de [!DNL Data Lake] is consistent met uw brongegevens. Zie de [[!DNL Marketo] hulplijn met toewijzingsvelden](../../sources/connectors/adobe-applications/mapping/marketo.md) voor meer informatie over `isDeleted`. |

Als u meer wilt weten over de Real-time Customer Data Platform B2B Edition, raadpleegt u de [B2B-overzicht](../../rtcdp/b2b-overview.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor [!DNL OneTrust Integration] | U kunt nu de opdracht [!DNL OneTrust Integration] bron voor het toevoegen van toestemmings- en voorkeursgegevens uit uw [!DNL OneTrust] aan Platform. Zie de documentatie op [een [!DNL OneTrust Integration] bronverbinding](../../sources/connectors/consent-and-preferences/onetrust.md) voor meer informatie . |
| Ondersteuning voor [!DNL Square] | U kunt nu de opdracht [!DNL Square] bron om betalingsgegevens van uw [!DNL Square] aan Platform. |
| Ondersteuning voor het verwijderen van klantkenmerkgegevensstromen | U kunt nu dataflows verwijderen die zijn gemaakt met de bronconnector Klantkenmerken. |

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
