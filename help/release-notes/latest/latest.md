---
title: Aanvullende informatie over Adobe Experience Platform
description: In de releaseopmerkingen van april 2023 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: e3fc587d924b2183806918f91e5ae3aa3fee52f3
workflow-type: tm+mt
source-wordcount: '2067'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

>[!IMPORTANT]
>
>Vanaf 15 mei 2023 `Existing` status zal van de kaart van het segmentlidmaatschap worden verouderd om overtolligheid in de levenscyclus van het segmentlidmaatschap te verwijderen. Na deze wijziging worden profielen die in een segment zijn gekwalificeerd, weergegeven als `Realized` en de gediskwalificeerde profielen blijven worden weergegeven als `Exited`. Lees voor meer informatie over deze wijziging de [Sectie Segmenteringsservice](#segmentation).

**Releasedatum: 26 april 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensvoorbereiding](#data-prep)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Experience Data Model](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Klantprofiel in realtime](#profile)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies** {#dashboards-new-updated-features}

| Functie | Beschrijving |
| --- | --- |
| Door gebruiker gedefinieerde dashboards | U kunt nu **historische gegevens filteren** vanuit uw widgetinzichten en gebruik recente gegevens of een aangepaste analyseperiode. Zie de [door de gebruiker gedefinieerde handleiding voor dashboards](../../dashboards/user-defined-dashboards.md#filter-historical-data) voor meer informatie .<br>U kunt nu ook **bestaande widgets dupliceren**. Door een duplicaat aan te passen en de kenmerken ervan te bewerken, kunt u voorkomen dat u bij het maken van een nieuwe, unieke widget opnieuw begint. Lees de [widget duplicatiegids](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) voor meer informatie. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates van de back-upperiode voor Adobe Analytics in niet-productiesandboxen | De periode voor het terugvullen van Adobe Analytics in niet voor de productie bestemde sandboxen is teruggebracht tot drie maanden. De back-up van productiesandboxen blijft na 13 maanden ongewijzigd. Deze wijziging geldt alleen voor nieuwe stromen en heeft geen invloed op bestaande stromen. Lees voor meer informatie de [Adobe Analytics-overzicht](../../sources/connectors/adobe-applications/analytics.md). |
| Nieuwe mapfunctie om FPID-tekenreeksen om te zetten in ECID | Gebruik de `fpid_to_ecid` FPID-tekenreeksen converteren naar ECID voor gebruik in Experience Platform- en Experience Cloud-toepassingen. Lees voor meer informatie de [Handleiding voor functies Data Prep](../../data-prep/functions.md). |

{style="table-layout:auto"}

Voor meer informatie over Data Prep, gelieve te lezen [Overzicht van Data Prep](../../data-prep/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| IP adresverwarring voor gegevensstromen | U kunt gedeeltelijke of volledige datastream-vlakke IP verduisteringsopties in nu bepalen [interface voor gegevensstroomconfiguratie](../../edge/datastreams/configure.md). <br><br>De gegevensstroom-vlakke IP het obfusceren plaatsen neemt belangrijkheid over om het even welke IP die obfuscatie in Adobe Target en Audience Manager wordt gevormd. <br><br>De gegevens die naar Adobe Analytics worden verzonden, worden niet beïnvloed door de gegevensstroom op niveau [!UICONTROL IP Obfuscation] instellen. Adobe Analytics ontvangt momenteel onopvallende IP-adressen. Voor Analytics om verduisterde IP adressen te ontvangen, moet u IP verduistering afzonderlijk vormen, in Adobe Analytics. Dit gedrag wordt in toekomstige versies bijgewerkt.<br><br> Voor meer details over IP verwarring en instructies op hoe te om het te vormen, zie [configuratiedocumentatie voor gegevensstroom](../../edge/datastreams/configure.md#advanced-options). |
| [DataStream-configuratieoverschrijvingen](../../edge/datastreams/overrides.md) | U kunt extra configuratieopties voor gegevensstromen nu bepalen, die u kunt gebruiken om specifieke montages met voeten te treden, zoals gebeurtenisdatasets, de bezitstokens van het Doel, de containers van de synchronisatie van identiteitskaart, en de rapportreeksen van Analytics. <br><br>Het overschrijven van gegevensstroomconfiguraties is een proces in twee stappen: <ol><li>Eerst moet u de configuratie van uw gegevensstroom overschrijven in het dialoogvenster [databaseconfiguratiepagina](../../edge/datastreams/configure.md).</li><li>Dan, moet u de met voeten treedt naar het Netwerk van de Rand of via het bevel van SDK van het Web of door SDK van het Web te gebruiken verzenden [tagextensie](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT Secret | De [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) Hiermee kunnen klanten Adobe- en Google Service-tokens gebruiken ter ondersteuning van server-naar-server interacties bij het doorsturen van gebeurtenissen. |
| [!DNL Pinterest Conversions API] extension | De [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) Met de extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in Adobe Experience Platform Edge Network, benutten en verzenden naar [!DNL Pinterest] in de vorm van server-side-gebeurtenissen die de [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] verbinding](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Gebruik de Salesforce-bestemming (voorheen Pardot genoemd) voor Marketing Cloud-accounts om leads vast te leggen, bij te houden, te behalen en te behalen. Gebruik deze bestemming voor B2B gebruiksgevallen waarbij meerdere afdelingen en besluitvormers betrokken zijn en die langere verkoop- en beslissingscycli vereisen. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Dataflow-controle voor [!DNL Custom Personalization] en [!DNL Adobe Commerce] bestemmingen | <p> U ziet nu activeringsmaatstaven voor de [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [Aangepaste aanpassing](../../destinations/catalog/personalization/custom-personalization.md) en de [Aangepaste aanpassing met kenmerken](../../destinations/catalog/personalization/custom-personalization.md) verbindingen. </p> <p>![Adobe Commerce-afbeelding](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce-meetgegevens"){width="100" zoomable="yes"}</p>  Zie [Gegevens controleren in de werkruimte Doelen](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) voor meer informatie . |
| Nieuw **[!UICONTROL Append segment ID to segment name]** veld voor de [!DNL Google Ad Manager] en [!DNL Google Ad Manager 360] bestemmingen | <p>U kunt nu de segmentnaam hebben in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) en [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) omvat segmentidentiteitskaart van Experience Platform, als dit: `Segment Name (Segment ID)`.</p><p>![Segment-id-afbeelding toevoegen](/help/destinations/assets/common/append-segment-id-to-segment-name.png "Nieuw segment-id toevoegen aan segmentnaamveld "){width="100" zoomable="yes"}</p> |
| Geplande terugvullingen voor publiek | <p>Voor de [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) doel, is de activering van publieksbackfills aan de bestemming gepland om 24 tot 48 uur voor te komen nadat een segment eerst aan een bestemmingsverbinding in kaart wordt gebracht. Deze update is in reactie op het beleid van Google om 24 uur te wachten tot het opnemen van gegevens en zal gelijke tarieven tussen Real-time CDP en verbeteren [!DNL Google Display & Video 360].</p> <p>Merk op dat dit een achtergrondconfiguratie is die op deze bestemming slechts van toepassing is en die niet met om het even welke klant-configureerbare het plannen opties in UI verwant is.</p> |

{style="table-layout:auto"}

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

- We hebben een probleem opgelost in het **Uitgesloten identiteiten** rapporteringsmetriek voor op dossier-gebaseerde bestemmingsuitvoer. Klanten ontvingen alle geëxporteerde id&#39;s van de geactiveerde exportbewerking zoals verwacht. De **Uitgesloten identiteiten** Bij de rapportage van metrische gegevens in de gebruikersinterface werden ten onrechte grote aantallen uitgesloten identiteiten weergegeven als gevolg van onjuist tellende identiteiten die nooit werden geacht te zijn geëxporteerd. (PLAT-149774)
- We hebben een probleem opgelost in het **Planning** stap van de activeringsworkflow. Voor bestemmingen die een afbeeldingID vereisen, konden de klanten geen afbeeldingidentiteitskaart voor segmenten toevoegen die aan bestaande bestemmingsverbindingen worden toegevoegd. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Schakelen tussen weergavenamen | De Schema-editor biedt nu een schakeloptie tussen de oorspronkelijke veldnamen en de meer leesbare weergavenamen.<br>![De Schema-editor met de schakeloptie voor weergavenaam gemarkeerd.](../../xdm/images/ui/resources/schemas/display-name-toggle.png "Schakelen tussen weergavenamen van schema-editor"){width="100" zoomable="yes"}<br>Dankzij deze flexibiliteit is het mogelijk uw schema&#39;s beter te detecteren en te bewerken. De weergavenamen voor standaardveldgroepen worden gegenereerd door het systeem, maar kunnen indien nodig ook via de gebruikersinterface worden aangepast. Lees de [documentatie over naamschakelen](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) voor meer informatie. |

{style="table-layout:auto"}

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Schema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1719/files) | Een nieuw XDM-schema voor de datasets van de Classificatie van het Doel die een reeks meta-gegevens gebieden bevatten om de activiteiten en de ervaringen van het Doel te classificeren. |

{style="table-layout:auto"}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL Adobe Unified Profile Service Account Union Extension]](https://github.com/adobe/xdm/pull/1696/files) | Er is een accountextensieveldgroep toegevoegd voor Real-Time Klantprofiel waarmee gebruikers segmentlidmaatschap kunnen toevoegen aan de Account union. |
| Schema | [[!UICONTROL Computed Attributes System Schema]](https://github.com/adobe/xdm/pull/1696/files) | De de gebiedsgroep van de Attributen die door het Profiel van de Klant in real time wordt gebruikt is bijgewerkt aan een systeem read-only globaal schema. |
| Veldgroep | Meerdere | Verschillende gebeurtenissen zijn toegevoegd als velden voor [[!UICONTROL Time-series Schema]](https://github.com/adobe/xdm/pull/1718/files). |
| Veldgroep | Profiellogo | [De titel is gecorrigeerd](https://github.com/adobe/xdm/pull/1717/files) for `xdm:upgradeDate` van &quot;Programmanaam&quot; naar &quot;Datum van upgrade&quot;. |
| Veldgroep | Meerdere | Verschillende velden van [[!UICONTROL Decision Item]](https://github.com/adobe/xdm/pull/1714/files) zijn bijgewerkt om de dubbele geneste hiërarchie te verwijderen. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, lees [XDM System, overzicht](../../xdm/home.md).

## Real-Time Customer Data Platform

Gebouwd op Experience Platform, Real-time Customer Data Platform ([!DNL Real-Time CDP]) helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen met intelligente besluitvorming door de klantenreis te activeren. [!DNL Real-Time CDP] combineert veelvoudige bronnen van ondernemingsgegevens om klantenprofielen in real time tot stand te brengen. De segmenten die van deze profielen worden gebouwd kunnen dan naar stroomafwaartse bestemmingen worden verzonden om één-aan-één gepersonaliseerde klantenervaringen over alle kanalen en apparaten te verstrekken.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde Real-Time CDP-startpagina | De [Homepage van Real-Time CDP](https://experience.adobe.com) is verbeterd dankzij een vernieuwde vormgeving en verbeterde prestaties. De homepage is nu toestemmingsbewust en zal widgets relevant voor de eigenschappen voorstellen die u toegang tot hebt. Lees voor meer informatie de [Overzicht van het dashboard voor Real-Time CDP-homepage](../../rtcdp/home-page-dashboards.md). |
| Zelfidentificatie-onderzoek | De zelfidentificatiecode-enquête is een korte vragenlijst die wordt weergegeven op de homepage van de gebruikersinterface van Adobe Experience Platform. Gebruik de zelfidentificatiecode-enquête om uw persoonlijke profiel voor het Experience Platform te maken en op maat gemaakte richtlijnen te ontvangen op basis van uw selecties. Lees voor meer informatie de [overzicht van de zelfidentificatie-enquête](../../landing/self-identification.md). |

Voor meer informatie over [!DNL Real-Time CDP], zie de [[!DNL Real-Time CDP] overzicht](../../rtcdp/overview.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Vervaldatum van pseudoniem profielgegevens | De vervaldatum van pseudoniem profielgegevens is nu over het algemeen beschikbaar. Deze release verwijdert ononderbroken pseudoniem-profielen uit uw Experience Platform-exemplaar als deze zijn ingeschakeld. Lees voor meer informatie over deze functie en Pseudoniem-profielen de [Handleiding voor het verlopen van Pseudoniem-profielgegevens](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Segmentlidmaatschapstoewijzing | Als vervolg op de vorige aankondiging in februari, op 15 mei 2023, `Existing` status zal van de kaart van het segmentlidmaatschap worden verouderd om overtolligheid in de levenscyclus van het segmentlidmaatschap te verwijderen. Na deze wijziging worden profielen die in een segment zijn gekwalificeerd, weergegeven als `Realized` en de gediskwalificeerde profielen blijven worden weergegeven als `Exited`.<br/><br/> Deze wijziging kan van invloed zijn op [ondernemingsbestemmingen](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis, Azure Event Hubs, HTTP API) en hebben mogelijk stroomafwaartse processen op hun plaats geautomatiseerd op basis van de `Existing` status. Als dit voor u het geval is, gelieve uw downstreamintegratie te herzien. Als u pas na een bepaalde tijd gekwalificeerde profielen wilt identificeren, kunt u een combinatie van de `Realized` en de `lastQualificationTime` in uw overzicht van het segmentlidmaatschap. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger. |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| API steun voor het filtreren van rij-vlakke gegevens voor de Dynamica van Microsoft, Salesforce CRM, en Marketing Cloud Salesforce | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de bronnen van de Marketing Cloud Microsoft Dynamics, Salesforce CRM en Salesforce. Lees de handleiding op [gegevens filteren voor een bron met behulp van de API](../../sources/tutorials/api/filter.md) voor meer informatie . |
| Beta beschikbaarheid van Shopify Streaming | De [Streaming bron optimaliseren](../../sources/connectors/ecommerce/shopify-streaming.md) is nu beschikbaar in bèta. Gebruik de Shopify Streaming bron om gegevens van uw Shopify partnerrekening aan Experience Platform te stromen. |
| Algemene beschikbaarheid van OneTrust Integration | De [OneTrust Integration-bron](../../sources/connectors/consent-and-preferences/onetrust.md) is nu GA. Gebruik de OneTrust Integration-bron om toestemmings- en voorkeursgegevens van uw OneTrust Integration-account naar Experience Platform te verzenden. |
| Algemene beschikbaarheid van Oracle Service Cloud | De [Cloud-bron voor oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md) is nu GA. Gebruik de Cloud-bron van de service Oracle om uw Oracle Service Cloud-gegevens naar het Experience Platform te brengen. |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).