---
title: Aanvullende informatie van april 2023 voor Adobe Experience Platform
description: Aanvullende informatie van april 2023 voor Adobe Experience Platform.
exl-id: 7b501467-99a7-4aee-ae86-66c851250ecf
source-git-commit: 2e41a1716e057cd33e4635c11ba9c3cfc185418a
workflow-type: tm+mt
source-wordcount: '1983'
ht-degree: 30%

---

# Aanvullende informatie voor Adobe Experience Platform

>[!IMPORTANT]
>
>Vanaf 15 mei 2023 wordt de status `Existing` afgekeurd van de segmentlidmaatschapskaart om redundantie in de levenscyclus van het segmentlidmaatschap te verwijderen. Na deze wijziging worden profielen die in een segment zijn gekwalificeerd, weergegeven als `Realized` en worden profielen die zijn gediskwalificeerd, weergegeven als `Exited` . Voor meer details op deze verandering, gelieve de [ sectie van de Dienst van de Segmentatie ](#segmentation) te lezen.

**Releasedatum: donderdag 26 april 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensvoorbereiding](#data-prep)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Experience-datamodel](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [Realtime-klantenprofiel](#profile)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies** {#dashboards-new-updated-features}

| Functie | Beschrijving |
| --- | --- |
| Door gebruiker gedefinieerde dashboards | U kunt **historische gegevens** van uw widgetinzichten nu filtreren, en of recente gegevens of een periode van de douaneanalyse gebruiken. Zie de [ user-defined dashboards gids ](../../dashboards/standard-dashboards.md#filter-historical-data) voor meer informatie.<br> u kunt **uw bestaande widgets** nu ook dupliceren. Door een duplicaat aan te passen en de kenmerken ervan te bewerken, kunt u voorkomen dat u bij het maken van een nieuwe, unieke widget opnieuw begint. Lees de [ gids van de widgetduplicatie ](../../dashboards/standard-dashboards.md#duplicate-a-widget) om meer te leren. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe u toegangsrechten verleent en aangepaste widgets maakt, raadpleegt u eerst het [overzicht van dashboards](../../dashboards/home.md).

## Gegevensvoorbereiding {#data-prep}

Met gegevensvoorbereiding kunnen gegevenstechnici gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience-datamodel).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates van de back-upperiode voor Adobe Analytics in niet-productiesandboxen | De periode voor het terugvullen van Adobe Analytics in niet voor de productie bestemde sandboxen is teruggebracht tot drie maanden. De back-up van productiesandboxen blijft na 13 maanden ongewijzigd. Deze wijziging geldt alleen voor nieuwe stromen en heeft geen invloed op bestaande stromen. Voor meer informatie, lees het [ overzicht van Adobe Analytics ](../../sources/connectors/adobe-applications/analytics.md). |
| Nieuwe mapfunctie om FPID-tekenreeksen om te zetten in ECID | Gebruik de functie `fpid_to_ecid` om FPID-tekenreeksen om te zetten in ECID voor gebruik in Experience Platform- en Experience Cloud-toepassingen. Voor meer informatie, lees de [ Prep functies van Gegevens gids ](../../data-prep/functions.md). |

{style="table-layout:auto"}

Voor meer informatie over Prep van Gegevens, gelieve het [ overzicht van de Prep van Gegevens ](../../data-prep/home.md) te lezen.

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| IP adresverwarring voor gegevensstromen | U kunt gedeeltelijke of volledige datastream-vlakke IP verduisteringsopties in de [ configuratie UI van de datastream ](../../datastreams/configure.md) nu bepalen. <br><br> de datastream-vlakke IP verwarring het plaatsen neemt belangrijkheid over om het even welke IP die obfuscatie in Adobe Target en Audience Manager wordt gevormd. <br><br> gegevens die naar Adobe Analytics worden verzonden worden niet beïnvloed door het datastream-niveau [!UICONTROL IP Obfuscation] plaatsen. Adobe Analytics ontvangt momenteel onopvallende IP-adressen. Voor Analytics om verduisterde IP adressen te ontvangen, moet u IP verduistering afzonderlijk vormen, in Adobe Analytics. Dit gedrag wordt in toekomstige versies bijgewerkt.<br><br> voor meer details over IP verwarring en instructies op hoe te om het te vormen, zie de [ documentatie van de gegevensstroomconfiguratie ](../../datastreams/configure.md#advanced-options). |
| [ de configuratietreedt van DataStream ](../../datastreams/overrides.md) | U kunt extra configuratieopties voor gegevensstromen nu bepalen, die u kunt gebruiken om specifieke montages met voeten te treden, zoals gebeurtenisdatasets, de bezitstokens van het Doel, de containers van de synchronisatie van identiteitskaart, en de rapportreeksen van Analytics. <br><br> met voeten treedt de configuraties van de gegevensstroom is een proces in twee stappen: <ol><li>Eerst, moet u uw configuratie van de gegevensstroom met voeten treden in de [ gegevenstream configuratiepagina ](../../datastreams/configure.md).</li><li>Dan, moet u de met voeten treden naar Edge Network of via een bevel van SDK van het Web, of door de de markeringsuitbreiding van SDK van het Web te gebruiken [&#128279;](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT Secret | [ OAuth JWT Geheim ](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html) staat klanten toe om de tokens van de Dienst van Adobe en van Google te gebruiken om server-aan-server interactie in Gebeurtenis te steunen die door:sturen. |
| [!DNL Pinterest Conversions API] extensie | Met de [[!DNL Pinterest Conversions API] ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) -extensie voor het doorsturen van gebeurtenissen kunt u gegevens die zijn vastgelegd in Adobe Experience Platform Edge Network, gebruiken en naar [!DNL Pinterest] verzenden in de vorm van gebeurtenissen aan de serverzijde met behulp van [!DNL Pinterest Conversions API] . |

{style="table-layout:auto"}

## Bestemmingen {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] verbinding](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | Gebruik de Salesforce Marketing Cloud Account Engagement (voorheen Pardot genoemd)-bestemming om leads vast te leggen, bij te houden, te scoren, te scoren en te beoordelen. Gebruik deze bestemming voor B2B gebruiksgevallen waarbij meerdere afdelingen en besluitvormers betrokken zijn en die langere verkoop- en beslissingscycli vereisen. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| Dataflow-controle voor [!DNL Custom Personalization] - en [!DNL Adobe Commerce] -doelen | <p> U kunt activeringsmetriek voor [ Adobe Commerce ](/help/destinations/catalog/personalization/adobe-commerce.md), [ Douane Personalization ](../../destinations/catalog/personalization/custom-personalization.md) en [ Douane Personalization met Attributen ](../../destinations/catalog/personalization/custom-personalization.md) verbindingen nu zien. </p> <p>![ het beeld van Adobe Commerce {de metriek van 1} Adobe Commerce "){width="100" zoomable="yes"}] (/help/destinations/assets/common/adobe-commerce-metrics.png "</p>  Zie [ dataflows van de Monitor in de werkruimte van Doelen ](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) voor meer details. |
| Nieuw veld **[!UICONTROL Append segment ID to segment name]** voor de doelen [!DNL Google Ad Manager] en [!DNL Google Ad Manager 360] | <p>U kunt nu de segmentnaam opnemen in [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) en [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) de segment-id van Experience Platform, zoals in het volgende voorbeeld: `Segment Name (Segment ID)` .</p><p>![ voeg segmentidentiteitskaart beeld ](/help/destinations/assets/common/append-segment-id-to-segment-name.png " Nieuw toe toevoegt segmentidentiteitskaart aan segmentnaamgebied "){width="100" zoomable="yes"}</p> |
| Geplande terugvullingen voor publiek | <p>Voor de [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) bestemming, is de activering van publieksbackfills aan de bestemming gepland om 24 tot 48 uur voor te komen nadat een segment eerst aan een bestemmingsverbinding in kaart wordt gebracht. Deze update is een reactie op het Google-beleid om 24 uur te wachten tot er gegevens zijn ingevoerd. De overeenkomst tussen Real-Time CDP en [!DNL Google Display & Video 360] wordt hierdoor verbeterd.</p> <p>Merk op dat dit een achtergrondconfiguratie is die op deze bestemming slechts van toepassing is en die niet met om het even welke klant-configureerbare het plannen opties in UI verwant is.</p> |

{style="table-layout:auto"}

**Bevestigingen en verhogingen** {#destinations-fixes-and-enhancements}

- Wij hebben een kwestie in de **Uitgesloten Identiteiten** rapporteringsmetriek voor op dossier-gebaseerde bestemmingsuitvoer opgelost. Klanten ontvingen alle geëxporteerde id&#39;s van de geactiveerde exportbewerking zoals verwacht. Nochtans, de **Uitgesloten Identiteiten** rapporterend metrisch in UI tonen verkeerd hoge aantallen uitgesloten identiteiten toe te schrijven aan verkeerd tellende identiteiten die nooit werden verondersteld om te worden uitgevoerd. (PLAT-149774)
- Wij hebben een kwestie in de **Plannende** stap van het activeringswerkschema opgelost. Voor bestemmingen die een afbeeldingID vereisen, konden de klanten geen afbeeldingidentiteitskaart voor segmenten toevoegen die aan bestaande bestemmingsverbindingen worden toegevoegd. (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Schakelen tussen weergavenamen | De Schema-editor biedt nu een schakeloptie tussen de oorspronkelijke veldnamen en de meer leesbare weergavenamen.<br>![ de Redacteur van het Schema met de benadrukte knevel van de vertoningsnaam."){width="100" zoomable="yes"}<br> van de de vertoningsnaam van de Redacteur van het 0&rbrace; Schema knevel &lbrace;Deze flexibiliteit staat voor betere gebiedsontdekkingsbekwaamheid en het uitgeven van uw schema&#39;s toe. ] (../../xdm/images/ui/resources/schemas/display-name-toggle.png " De weergavenamen voor standaardveldgroepen worden gegenereerd door het systeem, maar kunnen indien nodig ook via de gebruikersinterface worden aangepast. Gelieve te lezen de [ documentatie van de knevel van de vertoningsnaam ](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) om meer te leren. |

{style="table-layout:auto"}

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Schema | [[!UICONTROL Adobe Target Classification Fields]](https://github.com/adobe/xdm/pull/1719/files) | Een nieuw XDM-schema voor de datasets van de Classificatie van het Doel die een reeks meta-gegevens gebieden bevatten om de activiteiten en de ervaringen van het Doel te classificeren. |

{style="table-layout:auto"}

**Bijgewerkte XDM-onderdelen**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL Adobe Unified Profile Service Account Union Extension]](https://github.com/adobe/xdm/pull/1696/files) | Er is een accountextensieveldgroep toegevoegd voor Real-Time Klantprofiel waarmee gebruikers segmentlidmaatschap kunnen toevoegen aan de Account union. |
| Schema | [[!UICONTROL Computed Attributes System Schema]](https://github.com/adobe/xdm/pull/1696/files) | De de gebiedsgroep van de Attributen die door het Profiel van de Klant in real time wordt gebruikt is bijgewerkt aan een systeem read-only globaal schema. |
| Veldgroep | Meerdere | Diverse gebeurtenissen toegevoegd als velden voor [[!UICONTROL Time-series Schema] ](https://github.com/adobe/xdm/pull/1718/files) . |
| Veldgroep | Profiellogo | [ Vaste de titel ](https://github.com/adobe/xdm/pull/1717/files) voor `xdm:upgradeDate` van &quot;Naam van het Programma&quot;aan &quot;Datum van de Verbetering&quot;. |
| Veldgroep | Meerdere | Verschillende velden uit [[!UICONTROL Decision Item] ](https://github.com/adobe/xdm/pull/1714/files) zijn bijgewerkt om de dubbele geneste hiërarchie te verwijderen. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Experience Platform, lees het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Real-Time Customer Data Platform

Real-Time Customer Data Platform ([!DNL Real-Time CDP]) is gebaseerd op Experience Platform en helpt bedrijven bekende en onbekende gegevens samen te brengen om klantprofielen te activeren met behulp van intelligente besluitvorming gedurende de hele klanttraject. [!DNL Real-Time CDP] combineert meerdere bedrijfsgegevensbronnen om klantprofielen in real-time te maken. Segmenten die op basis van deze profielen zijn samengesteld, kunnen vervolgens naar downstreambestemmingen worden verzonden om gepersonaliseerde één-op-één klantervaringen te bieden via alle kanalen en apparaten.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Verbeterde Real-Time CDP-startpagina | De [ homepage van Real-Time CDP ](https://experience.adobe.com) is verbeterd met een verfrist blik en betere prestaties. De homepage is nu toestemmingsbewust en zal widgets relevant voor de eigenschappen voorstellen die u toegang tot hebt. Voor meer informatie, lees het [ overzicht van het de homepage van Real-Time CDP dashboard ](../../rtcdp/home-page-dashboards.md). |
| Zelfidentificatie-onderzoek | De zelfidentificatiecode-enquête is een korte vragenlijst die wordt weergegeven op de homepage van de gebruikersinterface van Adobe Experience Platform. Met de zelfidentificatiecode-enquête kunt u uw Experience Platform-profiel samenstellen en op maat gemaakte richtlijnen ontvangen op basis van uw selecties. Voor meer informatie, leest het [ zelfidentificatieoverzicht ](../../landing/self-identification.md). |

Voor meer informatie over [!DNL Real-Time CDP], zie het [[!DNL Real-Time CDP]  overzicht ](../../rtcdp/overview.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Vervaldatum van pseudoniem profielgegevens | De vervaldatum van pseudoniem profielgegevens is nu over het algemeen beschikbaar. Deze release verwijdert ononderbroken pseudoniem-profielen uit uw Experience Platform-exemplaar als deze zijn ingeschakeld. Raadpleeg de [gids over de vervaldatum voor gegevens van pseudonieme profielen](../../profile/pseudonymous-profiles.md) om meer te weten te komen over deze functie en pseudonieme profielen. |

{style="table-layout:auto"}

## Segmentatieservice {#segmentation}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Segmentlidmaatschapstoewijzing | Als vervolg op de vorige aankondiging in februari, op 15 mei 2023, zal de `Existing` status van de kaart van het segmentlidmaatschap worden afgekeurd om overtolligheid in de cyclus van het segmentlidmaatschap te verwijderen. Na deze wijziging worden profielen die in een segment zijn gekwalificeerd, weergegeven als `Realized` en worden profielen die zijn gediskwalificeerd, weergegeven als `Exited` .<br/><br/> Deze verandering zou u kunnen beïnvloeden als, u [ ondernemingsbestemmingen ](../../destinations/destination-types.md#advanced-enterprise-destinations) (Amazon Kinesis, de Hubs van de Gebeurtenis van de Azure, HTTP API) gebruikt, en zou stroomafwaartse processen kunnen geautomatiseerd hebben die op de `Existing` status worden gebaseerd. Als dit voor u het geval is, gelieve uw downstreamintegratie te herzien. Als u pas gekwalificeerde profielen wilt identificeren na een bepaalde tijd, kunt u overwegen een combinatie van de status `Realized` en de status `lastQualificationTime` in uw overzicht van segmentlidmaatschap te gebruiken. Neem voor meer informatie contact op met uw Adobe-vertegenwoordiger. |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| API-ondersteuning voor het filteren van gegevens op rijniveau voor Salesforce CRM-bron. | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de Salesforce CRM-bron. Lees de gids over [ het filtreren gegevens voor een bron gebruikend API ](../../sources/tutorials/api/filter.md) voor meer informatie. |
| Beta-beschikbaarheid van Shopify Streaming | [ Shopify Streaming bron ](../../sources/connectors/ecommerce/shopify-streaming.md) is nu beschikbaar in bèta. Gebruik de Shopify Streaming-bron om gegevens van uw Shopify-partneraccount naar Experience Platform te streamen. |
| Algemene beschikbaarheid van OneTrust Integration | De [ bron van de Integratie OneTrust ](../../sources/connectors/consent-and-preferences/onetrust.md) is nu GA. Gebruik de OneTrust Integration-bron om toestemmings- en voorkeursgegevens van uw OneTrust Integration-account naar Experience Platform te verzenden. |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u het [overzicht van bronnen](../../sources/home.md).
