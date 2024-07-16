---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van september 2023 staat Adobe Experience Platform vermeld.
exl-id: ff7fb0c1-6941-4339-8648-58f9b9e9a91f
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '2238'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: vrijdag 28 september 2023**

Nieuwe functies in Adobe Experience Platform:

- [Berekende kenmerken](#computed-attributes)

Updates voor bestaande functies in Experience Platform:

- [Waarschuwingen](#alerts)
- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Gegevensbeheer](#data-governance)
- [ hygiëne van Gegevens ](#hygiene)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Query-service](#query-service)
- [Segmenteringsservice](#segmentation)
- [ Bronnen ](#sources)

## Berekende kenmerken {#computed-attributes}

Met behulp van berekende kenmerken kunt u gebeurtenisgegevens eenvoudig samenvatten in profielkenmerken via een intuïtieve gebruikersinterface voor verbeterde op gedrag gebaseerde segmentatie, personalisatie en activering. Met deze functie kunt u berekende kenmerken maken op een manier die zichzelf aanbiedt, deze beheren en ze in segmentatie, Real-Time CDP-doelen of Adobe Journey Optimizer gebruiken. Bovendien vereenvoudigen de berekende kenmerken de segmentatie en de workflows voor reizen, zodat u probleemloos relevante ervaringen kunt opdoen. Om meer over gegevens verwerkte attributen te leren, te lezen gelieve [ gegevens verwerkt attributenoverzicht ](../../profile/computed-attributes/overview.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich abonneren op verschillende waarschuwingsregels via het tabblad [!UICONTROL Alerts] in de gebruikersinterface van het platform en u kunt ervoor kiezen waarschuwingsberichten te ontvangen in de gebruikersinterface zelf of via e-mailberichten.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Tabblad Waarschuwingsgeschiedenis | Het tabblad Waarschuwingen [!UICONTROL History] bevat nu alle gebeurtenissen, zoals vertragingen, het starten, het voltooien en mislukken. Lees het [ alarm UI documentatie ](../../observability/alerts/ui.md) voor meer informatie over het geschiedenislusje. |

{style="table-layout:auto"}

Om meer over alarm te leren, te lezen gelieve het [[!DNL Observability Insights]  overzicht ](../../observability/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waarmee u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen zijn vastgelegd.

| Functie | Beschrijving |
| --- | --- |
| [ de verbetering van het gebruiksdashboard van de Vergunning ](../../dashboards/guides/license-usage.md) | Houd controle over uw licentieovereenkomsten met verbeterde rapportering en belangrijke metrische visualisaties met betrekking tot het gebruik van uw licentie. Deze verbeteringen bieden een hoge mate van granulariteit ten opzichte van de maatstaven voor het licentiegebruik voor alle producten van het Experience Platform die u hebt aangeschaft. |

{style="table-layout:auto"}

Meer over het dashboard van het vergunningsgebruik leren, zie het [ overzicht van het het dashboard van het vergunningsgebruik ](../../dashboards/guides/destinations.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Gegevensstromen | Ondersteuning voor opzoeken van apparaten | Wanneer het vormen van een gegevensstroom, kunt u het niveau van apparaat raadplegingsinformatie nu selecteren die moet worden verzameld. De opzoekinformatie van het apparaat omvat gegevens over het apparaat, de hardware, het besturingssysteem en de browser die worden gebruikt om met uw pagina te communiceren. <br> Opzoekgegevens van apparaten kunnen niet worden verzameld samen met gebruikersagent- en clienthints. Als u ervoor kiest apparaatinformatie te verzamelen, wordt de verzameling van gebruikersagent- en clienthints uitgeschakeld en andersom. Alle opzoekgegevens van het apparaat worden opgeslagen in de veldgroep `xdm:device` . Leer meer van de documentatie bij [ het vormen gegevensstromen ](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensies | [!DNL TikTok] API-extensie voor webgebeurtenissen | De [[!DNL TikTok]  Gebeurtenissen API van het Web ](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) uitbreiding staat u aan hefboomwerkingsgegevens toe die in de Edge Network van Adobe Experience Platform worden gevangen en het verzenden naar [!DNL TikTok] in de vorm van server-zijgebeurtenissen gebruikend [!DNL TikTok] Gebeurtenissen API van het Web. |

{style="table-layout:auto"}

Om meer over gegevensinzameling te leren, te lezen gelieve het [ overzicht van de gegevensinzameling ](../../tags/home.md).

## Gegevensbeheer {#data-governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| De nieuwe etiketten van het Ecosysteem van de Partner voor derdegegevens | Er zijn nieuwe labels voor gegevensgebruik beschikbaar voor verrijking en prospectie door derden. Zie de [ documentatie over de etiketten van het Ecosysteem van de Partner ](../../data-governance/labels/reference.md#partner) voor meer informatie. |

{style="table-layout:auto"}

Meer over gegevensbeheer leren, lees het [ overzicht van het gegevensbeheer ](../../data-governance/home.md).

## Gegevenshygiëne {#hygiene}

Experience Platform biedt een reeks mogelijkheden voor gegevenshygiëne waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentengegevens en gegevenssets. Met behulp van de [!UICONTROL Data Lifecycle] -werkruimte in de UI of via aanroepen van de Data Hygiene API kunt u uw gegevensopslagruimten op effectieve wijze beheren. Gebruik deze mogelijkheden om ervoor te zorgen dat de informatie zoals verwacht wordt gebruikt, wordt bijgewerkt wanneer onjuiste gegevens het bevestigen vereisen, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE  Beta ] {type=Informative} Verslag schrap (beperkte versie) | Beheer uw levenscyclus van gegevens in alle gegevensopslagruimten om te voldoen aan de verplichtingen van de klant en licentieovereenkomsten met de geavanceerde functies voor levenscyclusbeheer van gegevens in Adobe Experience Platform: automatische gegevenssetvervaldatum en verwijdering van records.<br> met geautomatiseerde datasetafloop, kunt u volledige datasets schrappen en een datum en een tijd voor de dataset plaatsen om worden geschrapt.<br> Schrapping van het Verslag staat u toe om individuele consumentenprofielen te schrappen door hun primaire identiteiten te richten. U kunt de primaire identiteiten individueel door UI of via CSV/JSON- dossierupload verstrekken. Zie de [ documentatie van de Schrapping van het Verslag ](../../hygiene/ui/record-delete.md) voor meer informatie |
| Verlopen gegevensset | Beperk uw gegevens tot een minimum en houd de controle over uw licentieovereenkomsten met de automatische gegevenssetvervaldatum. Verminder gegevensvolumes door volledige datasets te schrappen en plaats een datum en een tijd voor de dataset om worden geschrapt. Zie de [ documentatie van de datasetvervaldatums ](../../hygiene/ui/dataset-expiration.md) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over de mogelijkheden van de gegevenshygiëne van het Platform, verwijs naar het [ overzicht van de gegevenshygiëne ](../../hygiene/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Doel | Nieuw of Bijgewerkt | Beschrijving |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Nieuw | Activeer het publiek dat voorheen aan [!DNL LiveRamp] was toegewezen voor topuitgevers op mobiele media, het web, displays en aangesloten tv-media. <br> Na onboarding publiek aan uw [!DNL LiveRamp] rekening door [ LiveRamp - on boarding ](../../destinations/catalog/advertising/liveramp-onboarding.md) verbinding, gebruik de nieuwe [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) verbinding om het publiek aan stroomafwaartse bestemmingen te activeren. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nieuw | [[!DNL HubSpot] ](https://www.hubspot.com) is een platform van CRM met alle software, integratie, en middelen u marketing, verkoop, inhoudsbeheer, en de klantendienst moet verbinden. Het staat u toe om uw gegevens, teams, en klanten op één platform van CRM te verbinden. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Bijgewerkt | Extra ondersteuning voor [!DNL Dynamics 365] aangepaste veldvoorvoegsels voor aangepaste velden die niet zijn gemaakt in de standaardoplossing van [!DNL Dynamics 365] . Een nieuw inputgebied, **[!UICONTROL Customization Prefix]**, is toegevoegd in [ Vul de stap van bestemmingsdetails ](#destination-details). |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Bijgewerkt | De bestemming van het publiek van het Experience Cloud is nu over het algemeen beschikbaar. Gebruik deze bestemming om publiek van Real-Time CDP aan Audience Manager en Adobe Analytics te activeren. U hebt een licentie voor Audience Managers nodig om een publiek naar Adobe Analytics te sturen. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Uitvoer van gegevens in Real-Time CDP | De [ uitvoer ](../../destinations/ui/export-datasets.md) functionaliteit van de dataset is nu over het algemeen beschikbaar. Zie [ welke datasets u kunt uitvoeren gebaseerd op Experience Platform app ](../../destinations/ui/export-datasets.md#datasets-to-export) u, kocht en de [ gidsen voor het uitvoeren van datasets ](/help/destinations/guardrails.md#dataset-exports) controleert. |
| (Beta) Ondersteuning voor het exporteren van arraytype-objecten | Exporteer arrays met primitieve waarden (tekenreeks, int of booleaanse waarden) als platte schemabestanden naar de opslagdoelen van de cloud. Lees meer over de functionaliteit in de [ documentatie ](../../destinations/ui/export-arrays-calculated-fields.md). |
| Dynamische dropdown-kiezers in Destination SDK | Wanneer het creëren van een bestemming door Destination SDK, kunt u [ dynamische dropdown selecteurs ](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) nu gebruiken om de gebieden van een dropdown selecteur met waarden te bevolken die van API worden teruggewonnen. |

**Correcties en verhogingen** {#destinations-fixes-and-enhancements}

- Maak gebruik van [ controletransparantie ](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) nu beschikbaar voor ondernemingsbestemmingen ([ HTTP API ](../../destinations/catalog/streaming/http-destination.md), [ Amazon Kinesis ](../../destinations/catalog/cloud-storage/amazon-kinesis.md) en [ Azure Event Hubs ](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) op het dataflow loopniveau om activeringsmetriek en status in de [ dataflow detailmening ](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), met extra informatie via foutencodes en berichten voor het oplossen van problemen te controleren.
- Wanneer u de naam van publiek bijwerkt dat aan [ wordt in kaart gebracht Google Ad Manager ](../../destinations/catalog/advertising/google-ad-manager.md), [ de Vertoning van Google &amp; Video 360 ](../../destinations/catalog/advertising/google-dv360.md), en andere bestemmingen die [ malplaatjes van de publieksupdate ](../../destinations/destination-sdk/metadata-api/update-audience-template.md) gebruiken, worden deze naamveranderingen nu weerspiegeld stroomafwaarts in de bestemming.

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Snelle acties toegevoegd aan de Schema-editor | Er zijn nieuwe snelle acties toegevoegd aan het canvas van de Schema-editor. U kunt nu de JSON-structuur kopiëren of het schema rechtstreeks uit de editor verwijderen.<br>![ de snelle acties in de Redacteur van het Schema.](../2023/assets/schema-editor-copy-json.png " de Redacteur van Schema met Meer en het Exemplaar aan benadrukt JSON."){width="100" zoomable="yes"} |
| XDM-bronnen filteren op basis van aangepaste of standaardmaker | De lijsten met beschikbare schema&#39;s, veldgroepen, gegevenstypen en klassen worden nu vooraf gefilterd op basis van de methode waarmee ze zijn gemaakt. Op deze manier kunt u bronnen filteren op basis van het feit of ze op maat zijn gemaakt of door Adobe zijn gemaakt.<br>![ de Standaard en filters van de Douane in de werkruimte van Schema&#39;s.](../2023/assets/standard-and-custom-classes.png " de werkruimte van Schema&#39;s met de Standaard en Gemarkeerde filters van de Douane."){width="100" zoomable="yes"} <br> zie [ creeer en geef middelendocumentatie ](../../xdm/ui/resources/classes.md#filter.md) voor meer informatie uit. |

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte workflow voor het maken van schema&#39;s | Er is een nieuwe workflow voor het maken van schema&#39;s geïmplementeerd om het proces te stroomlijnen. <br> ![ de nieuwe schemaverwezenlijking UI.](../2023/assets/schema-class-options.png " de Nieuwe benadrukte selecteur van schemadetails."){width="100" zoomable="yes"} <br> zie de [ documentatie van de schemaverwezenlijking ](../../xdm/ui/resources/schemas.md#create) voor meer informatie. |

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Return]](https://github.com/adobe/xdm/pull/1773/files) | De afgegeven RMA (Return Merchandise Authorization). |
| Gegevenstype | [[!UICONTROL Return Item]](https://github.com/adobe/xdm/pull/1773/files) | De teruggekeerde informatie van het punt binnen RMA (de Vergunning van de Goederen van de Terugkeer). |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Extensie | [!UICONTROL AJO Entity Fields] | [[!UICONTROL flag for multi-variant] ](https://github.com/adobe/xdm/pull/1774/files) werd toegevoegd aan [!UICONTROL AJO Entity Fields] om te identificeren als de variant al dan niet een multi-variant is. |
| Gegevenstype | [!UICONTROL Product list item] | [[!UICONTROL Return Item] ](https://github.com/adobe/xdm/pull/1773/files) werd toegevoegd om de informatie van de Autorisatie van de Goederen van de Terugkeer te omvatten. |
| Gegevenstype | Volgorde | [[!UICONTROL Return Info] ](https://github.com/adobe/xdm/pull/1773/files) werd toegevoegd om uitgegeven RMA (de Vergunning van de Terugkeer Merchandise) te omvatten. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md)

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van Identity Service | Gebruik het verbeterde gereedschap voor het maken van aangepaste naamruimten in de gebruikersinterface van het Experience Platform om uw aangepaste naamruimten en de bijbehorende identiteitstypen beter te beheren. De verbeterde interface van de Identiteitsdienst voorziet u van: <ul><li>Contextuele Ervaring: Visuele aanwijzingen, helderheid, en context aan wat een identiteitsnamespace is en identiteitstypes zijn.</li><li>Nauwkeurigheid: betere foutafhandeling, zonder dubbele identiteitsnamen.</li><li>Detectie: toegang tot documentatie vanuit een productdialoogvenster.</li></ul> Voor meer informatie, leest de gids bij [ het creëren van douane namespaces ](../../identity-service/features/namespaces.md#create-namespaces). |
| Wijzigingen in limieten van identiteitsgrafieken | De limiet voor identiteitsgrafieken is gewijzigd van 150 identiteiten in 50 identiteiten. Wanneer een nieuwe identiteit wordt opgenomen in een volledige grafiek, wordt de oudste identiteit op basis van de tijdstempel en het identiteitstype van de inname verwijderd. Identiteitstypen van cookies krijgen prioriteit voor verwijdering. Neem contact op met het accountteam van de Adobe om een wijziging in het type identiteit aan te vragen als uw productiessandbox het volgende bevat: <ul><li>een aangepaste naamruimte waarin de personen-id&#39;s (zoals CRM-id&#39;s) zijn geconfigureerd als cookie-/apparaatidentiteitstype.</li><li>een aangepaste naamruimte waarin cookie-/apparaat-id&#39;s zijn geconfigureerd als identiteitstype voor verschillende apparaten.</li></ul> Deze aanvragen worden handmatig verwerkt door Adobe-engineering. Voor meer informatie, lees de [ gidsen voor de gegevens van de Dienst van de Identiteit ](../../identity-service/guardrails.md) en gids over [ best practices van de de vergunningsrechten van het gegevensbeheer ](../../landing/license-usage-and-guardrails/data-management-best-practices.md). |

{style="table-layout:auto"}

Om meer over de Dienst van de Identiteit te leren, te lezen gelieve het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake] . U kunt zich bij om het even welke datasets van [!DNL Data Lake] aansluiten en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Wetenschap van Gegevens Workspace, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| UI-updates voor het filteren van logbestanden | Het betere filtreren van het vraaglogboek verbetert zicht voor user-generated logboeken voor controle, het beheer, en het oplossen van problemen. U kunt de lijst met querylogbestanden filteren op basis van verschillende instellingen. <br> ![ de de filtermontages van het vraaglogboek.](../2023/assets/log-filter-settings.png " de Nieuwe filters van het vraaglogboek worden benadrukt."){width="100" zoomable="yes"} <br> zie de [ documentatie van vraaglogboeken ](../../query-service/ui/query-logs.md#filter-logs) voor meer informatie. |
| UI-updates van Multiple Query Editor | U kunt veelvoudige opeenvolgende vragen in de Redacteur van de Vraag nu uitvoeren of meer dan één vraag schrijven en alle vragen op een opeenvolgende manier uitvoeren. Om meer flexibiliteit aan uw vraaguitvoering toe te voegen, kunt u uw gekozen vraag benadrukken en die specifieke vraag selecteren om onafhankelijk van anderen te lopen. Zie de [ gids UI van de Redacteur van de Vraag ](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over de Diensten van de Vraag, verwijs naar het [ overzicht van de Dienst van de Vraag ](../../query-service/home.md).

## Segmenteringsservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) segmenteren naar het publiek. U kunt een publiek maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn gemakkelijk toegankelijk voor elke Adobe.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| ------- | ----------- |
| Aanpasbare kolommen | U kunt de lay-out van het Portaal van de Publiek met re-sizable kolommen nu aanpassen. Voor meer informatie over deze eigenschap, te lezen gelieve het [ Poortoverzicht van het Poort van het Publiek ](../../segmentation/ui/audience-portal.md#customize). |
| Uitsplitsing naar frequentie bijwerken | U kunt nu een verdeling van de updatefrequenties van het publiek in uw organisatie bekijken. Voor meer informatie over deze eigenschap, te lezen gelieve de [ gids van de segmentatie UI ](../../segmentation/ui/overview.md#browse). |

Om meer over de Dienst van de Segmentatie te leren, te lezen gelieve het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe parameters voor `offset` paginering in Self-Serve Sources (Batch SDK) | U kunt nu een `endConditionName` en `endConditionValue` voor uw bron opgeven wanneer u `offset` paginering gebruikt. Met deze parameters kunt u de voorwaarde aangeven die de pagineringslus in de volgende HTTP-aanvraag beëindigt. Voor meer informatie, lees de [ pagineringsgids voor Zelfbediening Bronnen (Batch SDK) ](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Om meer over bronnen te leren, te lezen gelieve het [ overzicht van bronnen ](../../sources/home.md).
