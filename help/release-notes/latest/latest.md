---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van september 2023 staat Adobe Experience Platform vermeld.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 30e927ec78a953aae8ac90829ec8b3b0475c5db4
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 september 2023**

Nieuwe functies in Adobe Experience Platform:

- [Berekende kenmerken](#computed-attributes)

Updates voor bestaande functies in Experience Platform:

- [Waarschuwingen](#alerts)
- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Gegevensbeheer](#data-governance)
- [Gegevenshygiëne](#hygiene)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Query-service](#query-service)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Berekende kenmerken {#computed-attributes}

Met behulp van berekende kenmerken kunt u gebeurtenisgegevens eenvoudig samenvatten in profielkenmerken via een intuïtieve gebruikersinterface voor verbeterde op gedrag gebaseerde segmentatie, personalisatie en activering. Met deze functie kunt u berekende kenmerken maken op een manier die zichzelf aanbiedt, deze beheren en ze in segmentatie, Real-Time CDP-doelen of Adobe Journey Optimizer gebruiken. Bovendien vereenvoudigen de berekende kenmerken de segmentatie en de workflows voor reizen, zodat u probleemloos relevante ervaringen kunt opdoen. Voor meer informatie over berekende kenmerken leest u de [overzicht van berekende kenmerken](../../profile/computed-attributes/overview.md).

## Waarschuwingen {#alerts}

Met Experience Platform kunt u zich abonneren op gebeurtenisgebaseerde waarschuwingen voor verschillende platformactiviteiten. U kunt zich abonneren op verschillende waarschuwingsregels via de [!UICONTROL Alerts] in de gebruikersinterface van het Platform en kan ervoor kiezen waarschuwingsberichten te ontvangen binnen de gebruikersinterface zelf of via e-mailmeldingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Tabblad Waarschuwingsgeschiedenis | De waarschuwingen [!UICONTROL History] tab bevat nu alle gebeurtenissen zoals vertragingen , het starten , het voltooien en mislukken . Lees de [UI-documentatie met waarschuwingen](../../observability/alerts/ui.md) voor meer informatie over het geschiedenislusje. |

{style="table-layout:auto"}

Lees voor meer informatie over waarschuwingen de [[!DNL Observability Insights] overzicht](../../observability/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waardoor u belangrijke informatie over de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen wordt gevangen.

| Functie | Beschrijving |
| --- | --- |
| [Verbetering van het gebruiksdashboard voor licenties](../../dashboards/guides/license-usage.md) | Houd controle over uw licentieovereenkomsten met verbeterde rapportering en belangrijke metrische visualisaties met betrekking tot het gebruik van uw licentie. Deze verbeteringen bieden een hoge mate van granulariteit ten opzichte van de maatstaven voor het licentiegebruik voor alle producten van het Experience Platform die u hebt aangeschaft. |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over het dashboard voor licentiegebruik de [Overzicht van het licentiegebruiksdashboard](../../dashboards/guides/destinations.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Gegevensstromen | Ondersteuning voor opzoeken van apparaten | Wanneer het vormen van een gegevensstroom, kunt u het niveau van apparaat raadplegingsinformatie nu selecteren die moet worden verzameld. De opzoekinformatie van het apparaat omvat gegevens over het apparaat, de hardware, het besturingssysteem en de browser die worden gebruikt om met uw pagina te communiceren. <br>  Opzoekgegevens van het apparaat kunnen niet samen met de gebruikersagent en de clienthints worden verzameld. Als u ervoor kiest apparaatinformatie te verzamelen, wordt de verzameling van gebruikersagent- en clienthints uitgeschakeld en andersom. Alle gegevens van de apparatenraadpleging worden opgeslagen in `xdm:device` veldgroep. Meer informatie vindt u in de documentatie op [configureren, gegevensstromen](../../datastreams/configure.md#geolocation-device-lookup). |
| Extensies | [!DNL TikTok] API-extensie voor webgebeurtenissen | De [[!DNL TikTok] Web Events API](https://exchange.adobe.com/apps/ec/109834/tiktok-web-events-api) kunt u gegevens die zijn vastgelegd in het Adobe Experience Platform Edge Network gebruiken en verzenden naar [!DNL TikTok] in de vorm van server-side-gebeurtenissen die de [!DNL TikTok] Web Events API. |

{style="table-layout:auto"}

Voor meer informatie over gegevensverzameling leest u de [overzicht van gegevensverzameling](../../tags/home.md).

## Gegevensbeheer {#data-governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| De nieuwe etiketten van het Ecosysteem van de Partner voor derdegegevens | Er zijn nieuwe labels voor gegevensgebruik beschikbaar voor verrijking en prospectie door derden. Zie de [documentatie over Partner Ecosystem-labels](../../data-governance/labels/reference.md#partner) voor meer informatie . |

{style="table-layout:auto"}

Lees voor meer informatie over gegevensbeheer de [gegevensbeheer - overzicht](../../data-governance/home.md).

## Gegevenshygiëne {#hygiene}

Experience Platform biedt een reeks mogelijkheden voor gegevenshygiëne waarmee u uw opgeslagen gegevens kunt beheren via programmatische verwijderingen van consumentengegevens en gegevenssets. Het gebruiken van één van beide [!UICONTROL Data Lifecycle] De werkruimte in UI of door vraag aan de Hygiene API van Gegevens, kunt u uw gegevensopslag effectief beheren. Gebruik deze mogelijkheden om ervoor te zorgen dat de informatie zoals verwacht wordt gebruikt, wordt bijgewerkt wanneer onjuiste gegevens het bevestigen vereisen, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} | Beheer uw levenscyclus van gegevens in alle gegevensopslagruimten om te voldoen aan de verplichtingen van de klant en licentieovereenkomsten met de geavanceerde functies voor levenscyclusbeheer van gegevens in Adobe Experience Platform: automatische gegevenssetvervaldatum en verwijdering van records.<br>Met geautomatiseerde datasetafloop, kunt u volledige datasets schrappen en een datum en een tijd voor de dataset plaatsen om worden geschrapt.<br>Met Record verwijderen kunt u afzonderlijke consumentenprofielen verwijderen door zich te richten op hun primaire identiteit. U kunt de primaire identiteiten individueel door UI of via CSV/JSON- dossierupload verstrekken. Zie de [Documentatie verwijderen opnemen](../../hygiene/ui/record-delete.md) voor meer informatie |
| Verlopen gegevensset | Beperk uw gegevens tot een minimum en houd de controle over uw licentieovereenkomsten met de automatische gegevenssetvervaldatum. Verminder gegevensvolumes door volledige datasets te schrappen en plaats een datum en een tijd voor de dataset om worden geschrapt. Zie de [documentatie betreffende de vervaldatum van gegevenssets](../../hygiene/ui/dataset-expiration.md) voor meer informatie . |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over de mogelijkheden van Platform op het gebied van gegevenshygiëne de [overzicht van de gegevenshygiëne](../../hygiene/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte doelen** {#new-updated-destinations}

| Bestemming | Nieuw of Bijgewerkt | Beschrijving |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) | Nieuw | Soorten publiek activeren die eerder zijn opgenomen in [!DNL LiveRamp] voor hoogwaardige uitgevers op mobiele media, het web, het beeldscherm en de aangesloten tv-media. <br> Nadat u een publiek aan boord hebt genomen [!DNL LiveRamp] via de [LiveRamp - Onboarding](../../destinations/catalog/advertising/liveramp-onboarding.md) verbinding, gebruik de nieuwe [[!DNL LiveRamp - Distribution]](../../destinations/catalog/advertising/liveramp-distribution.md) verbinding om het publiek naar downstreambestemmingen te activeren. |
| [[!DNL HubSpot]](../../destinations/catalog/crm/hubspot.md) | Nieuw | [[!DNL HubSpot]](https://www.hubspot.com) is een platform van CRM met alle software, integratie, en middelen u marketing, verkoop, inhoudsbeheer, en de klantendienst moet verbinden. Het staat u toe om uw gegevens, teams, en klanten op één platform van CRM te verbinden. |
| [[!DNL Microsoft Dynamics 365]](../../destinations/catalog/crm/microsoft-dynamics-365.md) | Bijgewerkt | Extra ondersteuning voor [!DNL Dynamics 365] aangepaste veldvoorvoegsels voor aangepaste velden die niet zijn gemaakt binnen de standaardoplossing in [!DNL Dynamics 365]. Een nieuw invoerveld, **[!UICONTROL Customization Prefix]**, is toegevoegd aan de [Doelgegevens invullen](#destination-details) stap. |
| [[!DNL Experience Cloud Audiences]](../../destinations/catalog/adobe/experience-cloud-audiences.md) | Bijgewerkt | De bestemming van het publiek van het Experience Cloud is nu over het algemeen beschikbaar. Gebruik deze bestemming om publiek van Real-Time CDP aan Audience Manager en Adobe Analytics te activeren. U hebt een licentie voor Audience Managers nodig om een publiek naar Adobe Analytics te sturen. |

{style="table-layout:auto"}

<!-- 


Add these to release notes as they go out

| [[!DNL Qualtrics]] | New | Use the aggregation of multiple sources of operational data in Adobe Experience Platform as an input in Qualtrics Experience ID to better understand your customers and enable targeted outreach to close the gap when it comes to understanding intent, emotion and experience drivers. | 

-->

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Uitvoer van gegevens in Real-Time CDP | De [gegevensset exporteren](../../destinations/ui/export-datasets.md) functionaliteit is nu algemeen beschikbaar. Zie [welke gegevenssets u kunt exporteren op basis van de app Experience Platform](../../destinations/ui/export-datasets.md#datasets-to-export) u hebt aangeschaft en de [instructies voor de uitvoer van gegevenssets](/help/destinations/guardrails.md#dataset-exports). |
| (bèta) Ondersteuning voor het exporteren van arraytype-objecten | Exporteer arrays met primitieve waarden (tekenreeks, int of booleaanse waarden) als platte schemabestanden naar de opslagdoelen van de cloud. Meer informatie over de functionaliteit in het dialoogvenster [documentatie](../../destinations/ui/export-arrays-calculated-fields.md). |
| Dynamische dropdown-kiezers in Destination SDK | Wanneer u een doel maakt met Destination SDK, kunt u nu [dynamische vervolgkeuzekiezers](../../destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#dynamic-dropdown-selectors) om de velden van een vervolgkeuzekiezer te vullen met waarden die zijn opgehaald uit een API. |

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

- Gebruik van [transparantie controleren](../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-streaming-destinations) nu beschikbaar voor ondernemingsdoelen ([HTTP-API](../../destinations/catalog/streaming/http-destination.md), [Amazon Kinesis](../../destinations/catalog/cloud-storage/amazon-kinesis.md) en [Azure Event Hubs](../../destinations/catalog/cloud-storage/azure-event-hubs.md)) op het niveau van de dataflow-run om de activeringscijfers en de status in de [gegevensstroomweergave](../../dataflows/ui/monitor-destinations.md#dataflow-run-details-page), met aanvullende informatie via foutcodes en berichten voor probleemoplossing.
- Wanneer u de naam van het publiek bijwerkt die aan [Google Ad Manager](../../destinations/catalog/advertising/google-ad-manager.md), [Google Display &amp; Video 360](../../destinations/catalog/advertising/google-dv360.md)en andere bestemmingen [update-sjablonen voor publiek](../../destinations/destination-sdk/metadata-api/update-audience-template.md)Deze naamwijzigingen worden nu verderop in de bestemming weergegeven.

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Snelle acties toegevoegd aan de Schema-editor | Er zijn nieuwe snelle acties toegevoegd aan het canvas van de Schema-editor. U kunt nu de JSON-structuur kopiëren of het schema rechtstreeks uit de editor verwijderen.<br>![De snelle acties in de Redacteur van het Schema.](../2023/assets/schema-editor-copy-json.png "De Schemas Editor met Meer en Kopiëren naar JSON gemarkeerd."){width="100" zoomable="yes"} |
| XDM-bronnen filteren op basis van aangepaste of standaardmaker | De lijsten met beschikbare schema&#39;s, veldgroepen, gegevenstypen en klassen worden nu vooraf gefilterd op basis van de methode waarmee ze zijn gemaakt. Op deze manier kunt u bronnen filteren op basis van het feit of ze op maat zijn gemaakt of door Adobe zijn gemaakt.<br>![De filters Standaard en Aangepast in de werkruimte Schema.](../2023/assets/standard-and-custom-classes.png "De werkruimte Schema&#39;s met de filters Standaard en Aangepast gemarkeerd."){width="100" zoomable="yes"} <br> Zie de [documentatie met bronnen maken en bewerken](../../xdm/ui/resources/classes.md#filter.md) voor meer informatie . |

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte workflow voor het maken van schema&#39;s | Er is een nieuwe workflow voor het maken van schema&#39;s geïmplementeerd om het proces te stroomlijnen. <br> ![De nieuwe interface voor het maken van het schema.](../2023/assets/schema-class-options.png "Selector voor nieuwe schemadetails gemarkeerd."){width="100" zoomable="yes"} <br> Zie de [documentatie over het maken van schema](../../xdm/ui/resources/schemas.md#create) voor meer informatie . |

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gegevenstype | [[!UICONTROL Return]](https://github.com/adobe/xdm/pull/1773/files) | De afgegeven RMA (Return Merchandise Authorization). |
| Gegevenstype | [[!UICONTROL Return Item]](https://github.com/adobe/xdm/pull/1773/files) | De teruggekeerde informatie van het punt binnen RMA (de Vergunning van de Goederen van de Terugkeer). |

{style="table-layout:auto"}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving bijwerken |
| --- | --- | --- |
| Extensie | [!UICONTROL AJO Entity Fields] | De [[!UICONTROL flag for multi-variant]](https://github.com/adobe/xdm/pull/1774/files) is toegevoegd aan [!UICONTROL AJO Entity Fields] om na te gaan of de variant al dan niet een meervoudige variant is. |
| Gegevenstype | [!UICONTROL Product list item] | [[!UICONTROL Return Item]](https://github.com/adobe/xdm/pull/1773/files) is toegevoegd om de gegevens van de Autorisatie retourgoederen op te nemen. |
| Gegevenstype | Volgorde | [[!UICONTROL Return Info]](https://github.com/adobe/xdm/pull/1773/files) is toegevoegd om de uitgegeven RMA (Return Merchandise Authorization) op te nemen. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md)

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verbeteringen in de gebruikersinterface van Identity Service | Gebruik het verbeterde gereedschap voor het maken van aangepaste naamruimten in de gebruikersinterface van het Experience Platform om uw aangepaste naamruimten en de bijbehorende identiteitstypen beter te beheren. De verbeterde interface van de Identiteitsdienst voorziet u van: <ul><li>Contextuele Ervaring: Visuele aanwijzingen, helderheid, en context aan wat een identiteitsnamespace is en identiteitstypes zijn.</li><li>Nauwkeurigheid: betere foutafhandeling, zonder dubbele identiteitsnamen.</li><li>Detectie: toegang tot documentatie vanuit een productdialoogvenster.</li></ul> Lees voor meer informatie de handleiding op [aangepaste naamruimten maken](../../identity-service/namespaces.md#create-namespaces). |
| Wijzigingen in limieten van identiteitsgrafieken | De limiet voor identiteitsgrafieken is gewijzigd van 150 identiteiten in 50 identiteiten. Wanneer een nieuwe identiteit wordt opgenomen in een volledige grafiek, wordt de oudste identiteit op basis van de tijdstempel en het identiteitstype van de inname verwijderd. Identiteitstypen van cookies krijgen prioriteit voor verwijdering. Neem contact op met het accountteam van de Adobe om een wijziging in het type identiteit aan te vragen als uw productiessandbox het volgende bevat: <ul><li>een aangepaste naamruimte waarin de personen-id&#39;s (zoals CRM-id&#39;s) zijn geconfigureerd als cookie-/apparaatidentiteitstype.</li><li>een aangepaste naamruimte waarin cookie-/apparaat-id&#39;s zijn geconfigureerd als identiteitstype voor verschillende apparaten.</li></ul> Deze aanvragen worden handmatig verwerkt door Adobe-engineering. Lees voor meer informatie de [handleidingen voor identiteitsservicegegevens](../../identity-service/guardrails.md) en handleiding [best practices op het gebied van licentierechten voor gegevensbeheer](../../landing/license-usage-and-guardrails/data-management-best-practices.md). |

{style="table-layout:auto"}

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om gegevens in Adobe Experience Platform op te vragen [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| UI-updates voor het filteren van logbestanden | Het betere filtreren van het vraaglogboek verbetert zicht voor user-generated logboeken voor controle, het beheer, en het oplossen van problemen. U kunt de lijst met querylogbestanden filteren op basis van verschillende instellingen. <br> ![De filterinstellingen van het querylogboek.](../2023/assets/log-filter-settings.png "De nieuwe filters van het vraaglogboek worden benadrukt."){width="100" zoomable="yes"}  <br> Zie de [documentatie met querylogbestanden](../../query-service/ui/query-logs.md#filter-logs) voor meer informatie . |
| UI-updates van Multiple Query Editor | U kunt veelvoudige opeenvolgende vragen in de Redacteur van de Vraag nu uitvoeren of meer dan één vraag schrijven en alle vragen op een opeenvolgende manier uitvoeren. Om meer flexibiliteit aan uw vraaguitvoering toe te voegen, kunt u uw gekozen vraag benadrukken en die specifieke vraag selecteren om onafhankelijk van anderen te lopen. Zie de [Handleiding voor de Query Editor](../../query-service/ui/user-guide.md#execute-multiple-sequential-queries) voor meer informatie . |

{style="table-layout:auto"}

Raadpleeg voor meer informatie over Query Services de [Overzicht van Query Service](../../query-service/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Aanpasbare kolommen | U kunt de lay-out van het Portaal van de Publiek met re-sizable kolommen nu aanpassen. Lees voor meer informatie over deze functie de [segmenteringsUI-hulplijn](../../segmentation/ui/overview.md#customize). |
| Uitsplitsing naar frequentie bijwerken | U kunt nu een verdeling van de updatefrequenties van het publiek in uw organisatie bekijken. Lees voor meer informatie over deze functie de [segmenteringsUI-hulplijn](../../segmentation/ui/overview.md#browse). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).

Voor meer informatie over Segmentatieservice leest u de [Overzicht van segmentatieservice](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Nieuwe parameters voor `offset` paginering in Self-Serve Sources (Batch SDK) | U kunt nu een `endConditionName` en `endConditionValue` voor uw bron wanneer u `offset` paginering. Met deze parameters kunt u de voorwaarde aangeven die de pagineringslus in de volgende HTTP-aanvraag beëindigt. Lees voor meer informatie de [pagination guide for Self-Serve Sources (Batch SDK)](../../sources/sources-sdk/config/sourcespec.md#pagination). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
