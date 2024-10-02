---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2024
description: In de release van september 2024 staat een opmerking voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 33d1305aef7c763e7b0bd8c6db6a1a9417cc2a9d
workflow-type: tm+mt
source-wordcount: '2196'
ht-degree: 23%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: woensdag 24 september 2024**

Updates voor bestaande functies en documentatie in Adobe Experience Platform:

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
| Ondersteuning van ontwikkelingssandboxen | U kunt [ nu aan alarm ](../../observability/alerts/ui.md) in zowel productie als ontwikkelingszandbakken intekenen, toelatend naadloze controle over alle milieu&#39;s. |
| E-mailsjablonen | [ E-mailalarm ](../../observability/alerts/ui.md) omvat nu gedetailleerde activa informatie, die u verzekeren alle zeer belangrijke details bij uw vingertoppen hebt. |
| Verbeterde aanpassing | U kunt [ waakzame drempels ](../../observability/alerts/ui.md#alert-threshold) nu vormen die grotere flexibiliteit aanbieden om alarm aan uw specifieke behoeften voor de volgende waakzame types aan te passen:<br><ul><li>Vertraging segmenttaak</li><li>Vertraging bij exporteren segment</li><li>Uitvoervertraging bestemming</li><li>Vertraging bij uitvoering identiteitsservicestroom</li><li>Vertraging bij uitvoering van profielstroom</li><li>Bronnen: Vertraging bij uitvoering</li><li>Vertraging bij het uitvoeren van query&#39;s</li><li>Activeringssnelheid overschreden</li><li>Bronopinievormingsfoutfrequentie overschreden</ul> |
| Uitgebreide waarschuwingen | Het alarm van de gebeurtenisinformatie van de controle is nu beschikbaar voor abonnement op de volgende [ waakzame regels ](../../observability/alerts/rules.md):<br><ul><li>Auditie maken</li><li>Publiek bijwerken</li><li>Publiek verwijderen</li><li>Gegevensset maken</li><li>Dataset bijwerken</li><li>Gegevensset verwijderen</li><li>Schema maken</li><li>Schema-update</li><li>Schema verwijderen. |

{style="table-layout:auto"}

Voor meer informatie over alarm, lees het [[!DNL Observability Insights]  overzicht ](../../observability/home.md).

## Dashboards {#dashboards}

Experience Platform biedt meerdere dashboards waardoor u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Toevoegingstabel voor licentiegebruik | Verbeter granulair zicht in vergunningsgebruik en beheer uw middelen van het Platform met specifieke lijsten voor kernproducten en toe:voegen-ons. De belangrijkste metriek van het spoor en analyseert voor elk kernproduct met boor-door meningen op het zandbakniveau. De metriek van de toe:voegen-op integreren naadloos met kernproductmetriek, die een uitvoerige mening van gebruik aanbieden. Dankzij de verbeterde zichtbaarheid kunt u het licentiebeheer optimaliseren en bronnen afstemmen op de behoeften van de organisatie. Zie de [[!UICONTROL License Usage] dashboardgids ](../../dashboards/guides/license-usage.md#overview-tab) voor meer informatie. |
| Query Pro-modus - Algemene filterupgrades | Verbeter analyse met de nieuwe datumfilter van de Wijze van de Vraag Pro. Verfijn inzichten met dynamische datumparameters in uw SQL vragen en filtergegevens door specifieke tijdkaders. Kies vooraf ingestelde of aangepaste datumbereiken met een intuïtieve gebruikersinterface, zodat de dashboards voor alle gebruikers relevant blijven. Vereenvoudig workflows, houd precisie in stand en maak tijdig beslissingen. Lees de [ gids bij het creëren van datumfilters ](../../dashboards/data-distiller/query-pro-mode/filters/global-filter.md) voor meer informatie. |
| Query Pro-modi - Boordoorloop | Ontgrendel diepere inzichten met de Boorfunctie van de Wijze van de Vraag Pro en navigeer naadloos van grafieken op hoog niveau aan gedetailleerde dashboards. Gebruik deze functie om moeiteloos over te stappen van overzichten naar diepgaande analyse en trends, klantgedrag en KPI&#39;s te verkennen. Automatische doorvoeropties voor filters en boor op meerdere niveaus zorgen voor consistente gegevens, zodat de exploratie soepel verloopt. Vereenvoudig workflows, houd context en versnelde beslissingen. Lees de [ geleidelijke gids bij het creëren van boor-door ](../../dashboards/data-distiller/query-pro-mode/drill-through.md) voor meer informatie. |
| Modus Query Pro - Geavanceerde tabelkenmerken | Gebruik de geavanceerde tabelkenmerken van Query Pro-modus om de gegevensvisualisatie te stroomlijnen, de efficiëntie van de workflow te verbeteren en de gegevens helderder te maken. U kunt automatisch sorteren, vergroten of verkleinen en pagineren rechtstreeks vanuit aangepaste dashboards aan tabellen toevoegen. Sorteer kolommen om aan zeer belangrijke gegevens voorrang te geven, resize voor optimale leesbaarheid, en navigeer naadloos grote datasets zonder SQL vragen te wijzigen. Lees meer ](../../dashboards/data-distiller/query-pro-mode/view-more.md) gids &#39;[ Mening {om te leren hoe te om deze eigenschappen te integreren en uw gegevensinzichten op te heffen. |
| Totale gegevensvolume | De maatstaf &quot;Gemiddelde rijvaardigheid van profiel&quot; is vervangen door de maatstaf &quot;Totaal gegevensvolume&quot;. Het totale gegevensvolume heeft betrekking op de totale hoeveelheid beschikbare gegevens die kan worden gebruikt met het realtime profiel van de klant voor service- en personalisatieworkflows. Meer details over deze verandering kunnen in de [ Totale gids van het Volume van Gegevens ](../../landing/license-usage-and-guardrails/total-data-volume.md) worden gevonden. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Gegevensvoorbereiding {#data-prep}

Gebruik gegevensvoorbereiding om gegevens toe te wijzen, te transformeren en te valideren van en naar Experience-datamodel (XDM).

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Beta ] {type=Informative} Nieuwe functies van Prep van Gegevens voor gebruik in Doelen | U kunt nu de volgende arrayfuncties gebruiken voor het gebruik van Doelen:<ul><li>`array_to_string`</li><li>`filterArray`</li><li>`transformArray`</li><li>`flattenArray`</li></ul> Voor meer informatie, raadpleegt u de [handleiding voor functies voor gegevensvoorbereiding](../../data-prep/functions.md#arrays). |

{style="table-layout:auto"}

Voor meer informatie over gegevensvoorbereiding, raadpleegt u het [overzicht van gegevensvoorbereiding](../../data-prep/home.md).

## Bestemmingen {#destinations}

**Bijgewerkt: 30 september, 2024**

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Bestemming | Beschrijving |
| --- | --- |
| [ Advertentie Amazon ](/help/destinations/catalog/advertising/amazon-ads.md) | De release van september 2024 voegt de toewijzingsoptie toe om de parameter `countryCode` te exporteren naar Amazon Ads. Gebruik `countryCode` in de [ kaartstap ](/help/destinations/catalog/advertising/amazon-ads.md#map) om uw tarieven van de identiteitsgelijke met Amazon te verbeteren. |
| [ [!BADGE  B2B] {type=Informative} Demandbase ](/help/destinations/catalog/advertising/demandbase.md) | Gebruik deze bestemming om gebruikers van je account te activeren voor gebruik van Account-Based Marketing (ABM). Adverteer aan relevante personen en rollen in uw doelrekeningen via het B2B-Demand Side Platform (DSP) van DemandBase. Doelaccounts kunnen ook worden verrijkt met gegevens van derden over demandbase, voor andere downstreamtoepassingen bij marketing en verkoop. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functie | Beschrijving |
| --- | --- |
| ](/help/destinations/ui/export-datasets.md) verhogingen van de uitvoer van 0} Dataset {[ | De versie van september 2024 van Experience Platform omvat verscheidene verhogingen van de de eigenschapmogelijkheden van de datasetuitvoer, om diverse gevallen van het gegevensegress beter te steunen. Deze functieverbeteringen zijn onder meer: <ul><li>Nieuwe configureerbaarheidsopties voor gegevensmappen, waaronder de optie voor het toevoegen en verwijderen van submappen.</li><li>Nieuwe exportopties, inclusief volledige bestandsuitvoer (eenmaal) en de mogelijkheid om einddatums op te geven</li><li>Opmerking: Adobe introduceert ook een standaardeinddatum van 1 mei 2025 voor alle gegevensset exportgegevens die vóór de release van september zijn gemaakt. Voor om het even welk van deze gegevensstromen, zullen de klanten de einddatum in dataflow manueel vóór de einddatum moeten bijwerken, anders zal de uitvoer op deze datum ophouden.</li></ul> <br> ![ Beeld van het gebruikersinterface van het Experience Platform die de Edit planning en omslagoptie in de het plannen stap benadrukt.](../2024/assets/september/edit-schedule-folders.png " geef programma en omslagoptie in het plannen stap uit."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Voor meer informatie raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen aan de Schema-editor | Neem controle van uw schemaverhoudingen met een bijgewerkt relatiewerkschema in de Redacteur van het Schema. U kunt eenvoudig bestaande relaties rechtstreeks bijwerken of verwijderen vanuit de interface van het Experience Platform, waardoor het schemabeheer vloeiender en intuïtiever wordt. Pas verwijzingsschema&#39;s aan en verander verhoudingen met vertrouwen, die naadloze gegevensintegriteit over segmentatie en andere zeer belangrijke processen verzekeren. Meer leren over efficiënt het beheren van uw schemaverhoudingen, zie de gidsen op [ bepalend relatiegebieden in UI ](../../xdm/tutorials/relationship-ui.md#create-a-relationship-field-group) en voor [ B2B verhoudingen ](../../xdm/tutorials/relationship-b2b.md#edit-a-b2b-schema-relationship). |

{style="table-layout:auto"}

Voor meer informatie over XDM, lees het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Met Identity Service van Adobe Experience Platform krijgt u een uitgebreid beeld van uw klanten en hun gedrag door identiteiten op verschillende apparaten en systemen te koppelen, zodat u in real-time een impactvolle, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| Beperkte beschikbaarheid van regels voor identiteitsgrafieken | Identiteitsgrafiek die regels verbindt is een reeks hulpmiddelen in de Dienst van de Identiteit die u kunt gebruiken om nauwkeurige verpersoonlijking voor uw gebruikers te verzekeren. <ul><li>U kunt gebruik van het [ algoritme van de identiteitsoptimalisering ](../../identity-service/identity-graph-linking-rules/identity-optimization-algorithm.md) nu maken om ervoor te zorgen dat een identiteitsgrafiek van één enkele persoon representatief is, en daarom, de ongewenste samenvoeging van identiteiten op het Profiel van de Klant in real time verhindert.</li><li>Vorm [ namespace prioriteiten ](../../identity-service/identity-graph-linking-rules/namespace-priority.md) om het belang van uw respectieve namespaces te bepalen en te beïnvloeden hoe uw profielen worden gevormd en gesegmenteerd.</li><li>Gebruik het [ hulpmiddel van de grafieksimulatie in UI ](../../identity-service/identity-graph-linking-rules/graph-simulation.md) om identiteitsgrafieken met variërende configuraties te simuleren.</li><li>Gebruik de [ interface van identiteitsmontages ](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md) om uw unieke namespace aan te wijzen en prioriteiten voor alle namespaces in uw organisatie te vestigen.</li><li>Verwijs naar het [ identiteitsdashboard ](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs) voor metriek en tendensen betreffende uw grafiekgegevens.</li></ul> Om identiteitsgrafiek uit te proberen verbindend regels, contacteer uw Team van de Rekening van de Adobe voor toegang tot ontwikkelingszandbakken. |

**Bijgewerkte documentatie**

| Functie | Beschrijving |
| --- | --- |
| De gids van het oplossen van problemen voor identiteitsgrafiek die regels verbindt | Lees de nieuwe [ het oplossen van problemengids voor identiteitsgrafiek die regels ](../../identity-service/identity-graph-linking-rules/troubleshooting.md) verbindt voor benaderingen en het zuiveren oplossingen die u kunt verbinden om gemeenschappelijke kwesties op te lossen die u zou kunnen ontmoeten wanneer het werken met identiteitsgrafiek die regels verbindt. |
| Veelgestelde vragen over koppelingsregels voor identiteitsgrafieken | Lees de nieuwe [ identiteitsgrafiek die regels verbindt FAQ ](../../identity-service/identity-graph-linking-rules/troubleshooting.md#frequently-asked-questions) voor een lijst van antwoorden aan vaak gestelde vragen betreffende namespaceprioriteit, het algoritme van de identiteitsoptimalisering, en andere facetten van identiteitsgrafiek die regels verbinden. |

{style="table-layout:auto"}

Voor meer informatie over Identity Service, raadpleegt u het [overzicht van Identity Service](../../identity-service/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL data lake]. U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Distiller-publiek gegevens | Maak, beheer en activeer eenvoudig soorten publiek met de SQL-publieksextensie in Data Distiller van Experience Platform. Bepaal publiekssegmenten met SQL bevelen direct van uw gegevens meer, die de behoefte aan ruwe gegevens in profielen omzeilen. Verfijn het richten strategieën en synchroniseer automatisch publiek aan op dossier-gebaseerde bestemmingen met deze flexibele, gegeven-gedreven benadering. Stroomlijn workflows, optimaliseer het beheer van het publiek en ontgrendel het volledige potentieel van gegevens. Lees de [ gids bij het gebruiken van de SQL publieksuitbreiding ](../../query-service/data-distiller-audiences/overview.md) om uw publieksstrategieën op te heffen. |
| Distiller-statistieken gegevens - Hyperkubussen | Optimaliseer de analyse van grote gegevens met Hyperkubussen. Verwerk complexe berekeningen, zoals verschillende tellingen en multidimensionale analyse, zonder historische gegevens opnieuw te verwerken. Gegevens stapsgewijs bijwerken, workflows stroomlijnen en verwerkingstijd verkorten terwijl de nauwkeurigheid en efficiëntie behouden blijven. Krijg snellere, scalable, en rendabele inzichten die besluitvorming transformeren. Onderzoek de [ gids bij het gebruiken van Hyperkubussen ](../../query-service/hypercubes/overview.md) om geavanceerde analyse te ontgrendelen. |
| Query Editor Object-browser | De vraagefficiency van de verhoging met nieuwe Browser van Objecten in de Redacteur van de Vraag. Snel onderzoek, filter, en toegangsdatasets om vragen sneller te schrijven en te raffineren. Met schema-updates in real time en onmiddellijke lijstmeta-gegevens, kunt u werkschema&#39;s stroomlijnen, navigatietijd verminderen, en uw vraagervaring verbeteren. Ontgrendel het potentieel van uw gegevens en optimaliseer de analyse. Lees de [ gids bij het gebruiken van Browser van Objecten ](../../query-service/ui/user-guide.md#object-browser) voor meer informatie. |
| Rekenuren | De controle van de winst over middelgebruik met onlangs zichtbare Compute metrische Uren voor geplande vragen. De Uren van de Output van de mening op het niveau van de vraaguitvoering om middelgebruik voor CTAS/ITAS partijvragen te controleren en te optimaliseren. De begintijden van het spoor, voltooiingsstatus, en gegevens tijd voor elke vraaglooppas gegevens. Prestaties nauwkeurig afstellen en kosten moeiteloos verlagen. Lees de [ gids op Compute Uren ](../../query-service/ui/query-schedules.md#compute-hours-at-job-level) voor informatie over hoe te om uw vraagefficiency te maximaliseren. |

{style="table-layout:auto"}

Meer over de Dienst van de Vraag leren, lees het [ overzicht van de Dienst van de Vraag ](../../query-service/home.md).

## Segmentatieservice {#segmentation-service}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Streaming segmenteringscriteria bijwerken | Vanaf de release van september 2024 zijn de criteria voor uw publiek om in aanmerking te komen voor streamingsegmentatie bijgewerkt. Meer informatie over deze veranderingen kan in [ worden gevonden die de aanpassing van de segmenteringsgeschiktheidscriteria ](../../segmentation/eligibility-criteria-update.md) stromen. |
| Unified Search-implementatie | Het gedrag van het onderzoek binnen de Bouwer van het Segment zal nu Verenigde Onderzoek gebruiken. Dit maakt een robuustere ervaring mogelijk bij het beheren van en het zoeken naar publiek voor segmentlidmaatschap. Voor meer informatie over deze verandering, raadpleegt u de [handleiding voor Segment Builder](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], lees het [ overzicht van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

Gebruik bronnen in Experience Platform om gegevens vanuit een Adobe-applicatie of een databron van derden toe te voegen.

**Bijgewerkte functie**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Beta ] {type=Informative} Steun voor gecodeerde gegevensopname in UI | U kunt nu gecodeerde gegevens uit een batchbron voor cloudopslag invoeren met de werkruimte Bronnen in de gebruikersinterface van het Experience Platform. Lees het leerprogramma op [ het opnemen van gecodeerde gegevens in UI ](../../sources/tutorials/ui/encryped-ingestion.md) voor meer informatie. |
| Algemene beschikbaarheid van [!DNL Snowflake Streaming] bron | De [!DNL Snowflake Streaming] -bron bevindt zich nu in GA. Gebruik deze bron om gegevens van uw [!DNL Snowflake] -account naar het Experience Platform te streamen. Lees het [[!DNL Snowflake Streaming]  overzicht ](../../sources/connectors/databases/snowflake-streaming.md) voor meer informatie. |
| Ondersteuning voor verificatie van serviceaccounts in [!DNL Google BigQuery] | U kunt uw [!DNL Google BigQuery] -account nu met Experience Platform verbinden via verificatie van serviceaccount. Lees het [[!DNL Google BigQuery]  overzicht ](../../sources/connectors/databases/bigquery.md#generate-your-google-bigquery-credentials) voor meer informatie. <br> ![ Beeld van het gebruikersinterface van het Experience Platform die de Edit planning en omslagoptie in de het plannen stap benadrukt.](../2024/assets/september/service_auth.png " de authentificatie van de Dienst voor Google BigQuery."){width="250" align="center" zoomable="yes"} |
| Ondersteuning voor het overslaan van voorbeeldgegevensvoorvertoning | U kunt nu de optie inschakelen om de voorvertoning van gegevens over te slaan wanneer u een bronverbinding maakt met de volgende bronnen: <ul><li>[[!DNL Google BigQuery]](../../sources/tutorials/ui/create/databases/bigquery.md#skip-preview-of-sample-data)</li><li>[[!DNL Salesforce]](../../sources/tutorials/ui/create/crm/salesforce.md#skip-preview-of-sample-data)</li><li>[[!DNL Snowflake]](../../sources/tutorials/ui/create/databases/snowflake.md#skip-preview-of-sample-data)</li></ul> U kunt gegevensvoorvertoning overslaan om een time-out te omzeilen die kan optreden bij het invoeren van grote batchgegevens. Als u dit doet, voorkomt u mogelijk de automatische validatie van uw berekende en vereiste velden. Als u ervoor kiest om de gegevensvoorvertoning over te slaan, moet u de berekende en vereiste velden mogelijk handmatig valideren tijdens de toewijzing. |
| Ondersteuning voor het uitschakelen van chunking in [!DNL SFTP] | U kunt nu een instelling configureren waarmee u het afknippen in de [!DNL SFTP] -bron kunt uitschakelen. Lees het [[!DNL SFTP] overzicht](../../sources/connectors/cloud-storage/sftp.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie, raadpleegt u het [overzicht van bronnen](../../sources/home.md).
