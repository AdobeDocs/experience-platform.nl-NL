---
title: Aanvullende informatie van september 2024 voor Adobe Experience Platform
description: Aanvullende informatie voor de versie van september 2024 voor Adobe Experience Platform.
source-git-commit: eac613434f631cab567ab3fa6e30d33acac79d2f
workflow-type: tm+mt
source-wordcount: '2196'
ht-degree: 100%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: 24 september 2024**

Updates van bestaande functies en documentatie in Adobe Experience Platform:

- [Waarschuwingen](#alerts)
- [Dashboards](#dashboards)
- [Gegevensvoorbereiding](#data-prep)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Query-service](#query-service)
- [Segmentatieservice](#segmentation-service)
- [Bronnen](#sources)

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich aanmelden voor gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich aanmelden op verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van het platform, en u kunt ervoor kiezen waarschuwingsmeldingen te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor ontwikkelingssandbox | U kunt zich nu [abonneren op waarschuwingen](../../observability/alerts/ui.md) in zowel productie- als ontwikkelingssandboxen, waardoor naadloze bewaking in alle omgevingen mogelijk wordt. |
| E-mailsjablonen | [E-mailwaarschuwingen](../../observability/alerts/ui.md) omvatten nu gedetailleerde informatie over assets, zodat u alle belangrijke gegevens binnen handbereik hebt. |
| Verbeterde aanpassing | U kunt nu [waarschuwingsdrempels](../../observability/alerts/ui.md#alert-threshold) configureren, waardoor u meer flexibiliteit hebt om waarschuwingen af te stemmen op uw specifieke behoeften voor de volgende waarschuwingstypen:<br><ul><li>Vertraging segmenttaak</li><li>Vertraging bij exporteren segment</li><li>Vertraging bij uitvoering bestemmingsworkflow</li><li>Vertraging bij uitvoering identiteitsserviceworkflow</li><li>Vertraging bij uitvoering van profielworkflow</li><li>Vertraging bij uitvoering van workflow voor bronnen</li><li>Vertraging bij het uitvoeren van query&#39;s</li><li>Activeringssnelheid overschreden</li><li>Foutpercentage van opname van bronnen overschreden</ul> |
| Uitgebreide waarschuwingen | Informatiewaarschuwingen over controlegebeurtenissen zijn nu beschikbaar voor lidmaatschappen voor de volgende [waarschuwingsregels](../../observability/alerts/rules.md):<br><ul><li>Doelgroep maken</li><li>Doelgroep bijwerken</li><li>Doelgroep verwijderen</li><li>Dataset maken</li><li>Dataset bijwerken</li><li>Dataset verwijderen</li><li>Schema maken</li><li>Schema bijwerken</li><li>Schema verwijderen. |

{style="table-layout:auto"}

Raadpleeg het [[!DNL Observability Insights] overzicht](../../observability/home.md) voor meer informatie over meldingen.

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten krijgt in de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnames.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Tabel voor licentiegebruik van invoegtoepassingen | Zorg voor granulaire zichtbaarheid van het licentiegebruik en beheer uw platformresources met specifieke tabellen voor kernproducten en invoegtoepassingen. Volg en analyseer de kernmetrics van elk kernproduct, met uitgevouwen weergaven op sandboxniveau. Metrics van invoegtoepassingen integreren naadloos met metrics van kernproducten, waardoor u een uitgebreide weergave van het gebruik krijgt. Dankzij de verbeterde zichtbaarheid kunt u het licentiebeheer optimaliseren en de resources afstemmen op de behoeften van de organisatie. Raadpleeg de [[!UICONTROL License Usage]handleiding van het dashboard](../../dashboards/guides/license-usage.md#overview-tab) voor meer informatie. |
| Query Pro-modus - Algemene filterupgrades | Verbeter analyse met de nieuwe datumfilter van de Query Pro-modus. Verfijn inzichten met dynamische datumparameters in uw SQL-query&#39;s en filter gegevens op specifieke tijdsbestekken. Kies vooraf ingestelde of aangepaste datumbereiken met een intuïtieve gebruikersinterface, zodat de dashboards voor alle gebruikers relevant blijven. Vereenvoudig workflows, houd precisie in stand en maak tijdig beslissingen. Raadpleeg de [handleiding over het maken van datumfilters](../../dashboards/sql-insights-query-pro-mode/filters/global-filter.md) voor meer informatie. |
| Query Pro-modi - Drill Throughs | Krijg diepere inzichten met de Drill Through-functie van de Query Pro-modus en navigeer naadloos van algemene grafieken naar gedetailleerde dashboards. Met deze functie kunt u moeiteloos van samenvattingen naar diepgaande analyses gaan en trends, klantgedrag en KPI&#39;s verkennen. Automatische pass-throughs voor filters en drill-throughs op meerdere niveaus zorgen voor consistente gegevens, zodat de verkenning soepel verloopt. Vereenvoudig workflows, behoud de context en versnel beslissingen. Raadpleeg de [stapsgewijze handleiding voor het maken van drill-throughs](../../dashboards/sql-insights-query-pro-mode/drill-through.md) voor meer informatie. |
| Query Pro-modus - Geavanceerde tabelkenmerken | Gebruik de geavanceerde tabelkenmerken van de Query Pro-modus om de gegevensvisualisatie te stroomlijnen, de efficiëntie van de workflow en de duidelijkheid van de gegevens te verbeteren. Voeg automatisch sorteren, formaat wijzigen en paginering toe aan uw tabellen, rechtstreeks vanuit aangepaste dashboards. Sorteer kolommen om prioriteit te geven aan belangrijke gegevens, wijzig de grootte voor optimale leesbaarheid en navigeer naadloos door grote datasets zonder SQL-query&#39;s te wijzigen. Raadpleeg de handleiding [Meer weergeven](../../dashboards/sql-insights-query-pro-mode/view-more.md) voor meer informatie over hoe u deze functies kunt integreren en uw gegevensinzichten kunt verbeteren. |
| Totaal gegevensvolume | De metric &quot;Gemiddelde profielomvang&quot; is vervangen door de metric &quot;Totaal gegevensvolume&quot;. Het totale gegevensvolume betreft de totale hoeveelheid beschikbare gegevens die kan worden gebruikt met het realtimeklantenprofiel voor workflows van betrokkenheid en personalisatie. Meer details over deze wijziging vindt u in de [handleiding over het totale gegevensvolume](../../landing/license-usage-and-guardrails/total-data-volume.md). |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Gegevensvoorbereiding {#data-prep}

Gebruik gegevensvoorbereiding om gegevens toe te wijzen, te transformeren en te valideren van en naar Experience-datamodel (XDM).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} Nieuwe functies voor gegevensvoorbereiding voor gebruik in bestemmingen | U kunt nu de volgende arrayfuncties gebruiken voor gebruiksscenario&#39;s voor bestemmingen:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Voor meer informatie, raadpleegt u de [handleiding voor functies voor gegevensvoorbereiding](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Voor meer informatie over gegevensvoorbereiding, raadpleegt u het [overzicht van gegevensvoorbereiding](../../data-prep/home.md).

## Bestemmingen {#destinations}

**Bijgewerkt: 30 september 2024**

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [Amazon Ads](/help/destinations/catalog/advertising/amazon-ads.md) | De release van september 2024 voegt de toewijzingsoptie toe om de parameter `countryCode` te exporteren naar Amazon Ads. Gebruik `countryCode` in de [toewijzingsstap](/help/destinations/catalog/advertising/amazon-ads.md#map) om uw afstemmingspercentages voor identiteiten met Amazon te verbeteren. |
| [[!BADGE B2B]{type=Informative} Demandbase](/help/destinations/catalog/advertising/demandbase.md) | Gebruik dit doel om uw accountdoelgroepen te activeren voor gebruiksscenario&#39;s van Account-Based Marketing (ABM). Adverteer aan relevante personen en rollen in uw doelaccounts via het B2B Demand Side Platform (DSP) van DemandBase. Doelaccounts kunnen ook worden verrijkt met gegevens van derden van Demandbase, voor andere downstreamgebruiksscenario&#39;s in marketing en verkoop. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen voor [exporteren van datasets](/help/destinations/ui/export-datasets.md) | De release van Experience Platform van september 2024 bevat diverse verbeteringen aan de mogelijkheden van de dataset-exportfunctie, om verschillende gebruiksscenario&#39;s voor gegevensuitvoer beter te ondersteunen. Deze functieverbeteringen zijn onder meer: <ul><li>Nieuwe configureerbaarheidsopties voor gegevensmappen, waaronder de optie voor het toevoegen en verwijderen van submappen.</li><li>Nieuwe exportopties, inclusief volledige bestandsuitvoer (eenmaal) en de mogelijkheid om einddatums op te geven</li><li>Opmerking: Adobe introduceert ook een standaardeinddatum van 1 mei 2025 voor alle dataset-exportgegevensstromen die vóór de release van september zijn gemaakt. Voor al deze gegevensstromen moeten klanten de einddatum in de gegevensstroom vóór de einddatum handmatig bijwerken, anders stopt de export op deze datum.</li></ul> <br> ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Planning bewerken gemarkeerd in de planningsstap.](../2024/assets/september/edit-schedule-folders.png "De optie Planning en mappen bewerken in de planningsstap."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen aan de Schema-editor | Neem de controle over uw schemaverhoudingen met een bijgewerkte verhoudingsworkflow in de Schema-editor. U kunt eenvoudig bestaande verhoudingen rechtstreeks bijwerken of verwijderen vanuit de interface van het Experience Platform, waardoor het schemabeheer vloeiender en intuïtiever wordt. Pas verwijzingsschema&#39;s aan en hernoem verhoudingen met vertrouwen, zodat naadloze gegevensintegriteit wordt gegarandeerd bij segmentatie en andere belangrijke processen. Voor meer informatie over het efficiënt beheren van uw schemaverhoudingen raadpleegt u de handleidingen over [het definiëren van verhoudingsvelden in de gebruikersinterface](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) en voor [B2B-verhoudingen](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Voor meer informatie over XDM, raadpleegt u het [systeemoverzicht van XDM](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Met Identity Service van Adobe Experience Platform krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real-time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Beperkte beschikbaarheid van koppelingsregels voor identiteitsgrafieken | Koppelingsregels voor identiteitsgrafieken is een reeks tools in Identity Service die u kunt gebruiken om nauwkeurige personalisatie voor uw gebruikers te garanderen. <ul><li>U kunt nu het [algoritme voor identiteitsoptimalisatie](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) gebruiken om te zorgen dat een identiteitsgrafiek representatief is voor één persoon, en daardoor de ongewenste samenvoeging van identiteiten op het realtimeklantenprofiel verhindert.</li><li>Configureer [naamruimteprioriteiten](../../identity-service/identity-graph-linking-rules/namespace-priority.md) om het belang van uw betreffende naamruimten te definiëren en te beïnvloeden hoe uw profielen worden gevormd en gesegmenteerd.</li><li>Gebruik de [grafieksimulatietool in de gebruikersinterface](../../identity-service/identity-graph-linking-rules/graph-simulation.md) om identiteitsgrafieken met verschillende configuraties te simuleren.</li><li>Gebruik de [interface van de identiteitsinstellingen](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) om uw unieke naamruimte aan te wijzen en prioriteiten voor alle naamruimten in uw organisatie vast te leggen.</li><li>Verwijs naar het [identiteitsdashboard](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) voor metrics en tendensen van uw grafiekgegevens.</li></ul> Neem contact op met uw Adobe-accountteam voor toegang tot ontwikkelingssandboxes om koppelingsregels voor identiteitsgrafieken uit te proberen. |

**Bijgewerkte documentatie**

| Functie | Beschrijving |
| --- | --- |
| Handleiding voor het oplossen van problemen met koppelingsregels voor identiteitsgrafieken | Raadpleeg de nieuwe [handleiding voor het oplossen van problemen met koppelingsregels voor identiteitsgrafieken](../../identity-service/identity-graph-linking-rules/troubleshooting.md) voor benaderingen en oplossingen voor foutopsporing die u kunt gebruiken om veelvoorkomende problemen op te lossen die u kunt tegenkomen bij het werken met koppelingsregels voor identiteitsgrafieken. |
| Veelgestelde vragen over koppelingsregels voor identiteitsgrafieken | Raadpleeg de nieuwe [veelgestelde vragen over koppelingsregels voor identiteitsgrafieken](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) voor een lijst met antwoorden op veelgestelde vragen over de prioriteit van de naamruimte, het algoritme voor identiteitsoptimalisatie en andere facetten van de koppelingsregels voor identiteitsgrafieken. |

{style="table-layout:auto"}

Voor meer informatie over Identity Service, raadpleegt u het [overzicht van Identity Service](../../identity-service/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL data lake]. U kunt alle datasets uit Data Lake samenvoegen en de queryresultaten vastleggen als een nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Data Distiller-doelgroepen | Maak, beheer en activeer eenvoudig doelgroepen met de SQL-doelgroepextensie in Data Distiller van Experience Platform. Bepaal doelgroepsegmenten met SQL-opdrachten rechtstreeks vanuit uw data lake, waardoor u de behoefte aan onbewerkte gegevens in profielen omzeilt. Verfijn doelgerichte strategieën en synchroniseer doelgroepen automatisch met op bestanden gebaseerde bestemmingen met deze flexibele, datagestuurde aanpak. Stroomlijn workflows, optimaliseer het beheer van doelgroepen en ontgrendel het volledige potentieel van de gegevens. Raadpleeg de [handleiding over het gebruik van de SQL-doelgroepextensie](../../query-service/data-distiller-audiences/overview.md) om uw doelgroepstrategieën naar een hoger niveau te tillen. |
| Statistieken van Data Distiller - Hypercubes | Optimaliseer big data-analyse met Hypercubes. Verwerk complexe berekeningen, zoals verschillende tellingen en multidimensionale analyse, zonder historische gegevens opnieuw te verwerken. Gegevens stapsgewijs bijwerken, workflows stroomlijnen en verwerkingstijd verkorten terwijl de nauwkeurigheid en efficiëntie behouden blijven. Krijg snellere, schaalbare en kosteneffectieve inzichten die uw besluitvorming transformeren. Bekijk de [handleiding over het gebruik van Hypercubes](../../query-service/hypercubes/overview.md) voor geavanceerde analyse. |
| Query-editor Objectbrowser | Verhoog de efficiëntie van query&#39;s met de nieuwe Objectbrowser in de Query-editor. Zoek, filter en open snel datasets om query&#39;s sneller te schrijven en te verfijnen. Dankzij real-time schema-updates en directe tabelmetadata kunt u workflows stroomlijnen, de navigatietijd verkorten en uw query-ervaring verbeteren. Ontgrendel het potentieel van uw gegevens en optimaliseer de analyse. Raadpleeg de [handleiding over het gebruik van de objectbrowser](../../query-service/ui/user-guide.md#object-browser) voor meer informatie. |
| Looptijd | Krijg controle over het resourcegebruik met de nieuw zichtbare rekenurenstatistiek voor geplande query&#39;s. Bekijk de looptijd op het uitvoeringsniveau van query&#39;s om het resourcegebruik voor CTAS/ITAS-batchquery&#39;s te controleren en te optimaliseren. Houd de starttijden, voltooiingsstatus en looptijd bij voor elke query-uitvoering. Prestaties nauwkeurig afstellen en kosten moeiteloos verlagen. Raadpleeg de [handleiding over Looptijd](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) voor informatie over hoe u de efficiëntie van uw query&#39;s kunt maximaliseren. |

{style="table-layout:auto"}

Voor meer informatie over Query Service raadpleegt u het [overzicht van Query Service](../../query-service/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Criteria voor segmentatie van streaming bijwerken | Vanaf de release van september 2024 zijn de criteria voor uw doelgroepen om in aanmerking te komen voor segmentatie van streaming bijgewerkt. Meer informatie over deze wijzigingen vindt u in de [update van de criteria voor het bepalen van de geschiktheid voor segmentatie van streaming](../../segmentation/eligibility-criteria-update.md). |
| Implementatie van Unified Search | Zoekgedrag binnen Segment Builder maakt nu gebruik van Unified Search. Dit zorgt voor een robuustere ervaring bij het beheren en zoeken naar doelgroepen die u opnieuw kunt gebruiken voor segmentlidmaatschap. Voor meer informatie over deze verandering, raadpleegt u de [handleiding voor Segment Builder](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service] raadpleegt u het [segmentatieoverzicht](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} Ondersteuning voor gecodeerde gegevensopname in de gebruikersinterface | U kunt nu gecodeerde gegevens uit een batchbron voor cloudopslag invoeren met de werkruimte Bronnen in de gebruikersinterface van het Experience Platform. Raadpleeg de tutorial over [het opnemen van gecodeerde gegevens in de gebruikersinterface](../../sources/tutorials/ui/encryped-ingestion.md) voor meer informatie. |
| Algemene beschikbaarheid van de [!DNL Snowflake Streaming]-bron | De [!DNL Snowflake Streaming]-bron bevindt zich nu in GA. Gebruik deze bron om gegevens van uw [!DNL Snowflake]-account naar Experience Platform te streamen. Raadpleeg het [[!DNL Snowflake Streaming] overzicht](../../sources/connectors/databases/snowflake-streaming.md) voor meer informatie. |
| Ondersteuning voor verificatie van serviceaccounts in [!DNL Google BigQuery] | U kunt nu uw [!DNL Google BigQuery]-account aan Experience Platform koppelen met behulp van serviceaccountverificatie. Raadpleeg het [[!DNL Google BigQuery] overzicht](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) voor meer informatie. <br> ![Afbeelding van de gebruikersinterface van Experience Platform met de optie Planning bewerken gemarkeerd in de planningsstap.](../2024/assets/september/service_auth.png "Serviceverificatie voor Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Ondersteuning voor het overslaan van de voorvertoning van voorbeeldgegevens | U kunt er nu voor kiezen om de voorvertoning van gegevens over te slaan wanneer u een bronverbinding maakt met de volgende bronnen: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> U kunt gegevensvoorvertoning overslaan om een time-out te omzeilen die kan optreden bij het invoeren van grote batches van gegevens. Als u dit doet, voorkomt u mogelijk de automatische validatie van uw berekende en vereiste velden. Als u ervoor kiest om de gegevensvoorvertoning over te slaan, moet u de berekende en vereiste velden mogelijk handmatig valideren tijdens de toewijzing. |
| Ondersteuning voor het uitschakelen van chunking in [!DNL SFTP] | U kunt nu een instelling configureren waarmee u chunking in de [!DNL SFTP]-bron kunt uitschakelen. Lees het [[!DNL SFTP] overzicht](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).
