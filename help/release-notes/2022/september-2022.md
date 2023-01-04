---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2022
description: In de release van september 2022 staat een opmerking voor Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2883'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 september 2022**

Nieuwe functies in Adobe Experience Platform:

- [Op kenmerken gebaseerd toegangsbeheer](#abac)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Controlelogboeken](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Query-service](#query-service)
- [Bronnen](#sources)

## Op kenmerken gebaseerd toegangsbeheer {#abac}

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangsbeheer zal met ingang van Oktober 2022 worden toegelaten. Neem contact op met uw Adobe-vertegenwoordiger als u een vroege adoptietechnicus wilt zijn.

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform die privacybewuste merken meer flexibiliteit biedt om gebruikerstoegang te beheren. Afzonderlijke objecten zoals schemavelden en segmenten kunnen worden toegewezen aan gebruikersrollen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke gebruikers van Platforms in uw organisatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot, gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en ander aangepast type van gegevens over alle werkschema&#39;s en middelen van het Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.

| Functie | Beschrijving |
| --- | --- |
| Op kenmerken gebaseerd toegangsbeheer | Op attribuut-gebaseerde toegangscontrole staat u toe om het schemagebieden en de segmenten van het Model van de Gegevens van de Ervaring (XDM) met etiketten te etiketteren die organisatorische of gegevensgebruikswerkingsgebied bepalen. Parallel hieraan kunnen beheerders de gebruiker en de interface van het rolbeleid gebruiken om toegangsbeleid te bepalen dat XDM schemagebieden en segmenten behandelt om de toegang beter te beheren die aan gebruikers of groepen gebruikers (interne, externe, of derdegebruikers) wordt gegeven. Zie voor meer informatie de [op attributen-gebaseerd toegangsbeheeroverzicht](../../access-control/abac/overview.md). |
| Toestemmingen | De toestemmingen zijn het gebied van Experience Cloud waar de beheerders gebruikersrollen en toegangsbeleid kunnen bepalen om toegangstoestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren. Door Toestemmingen, kunt u rollen tot stand brengen en beheren, de gewenste middeltoestemmingen voor deze rollen toewijzen, en beleid bouwen aan hefboomwerkingsetiketten en bepalen welke gebruikersrollen toegang tot specifieke middelen van het Platform hebben. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld. Zie voor meer informatie de [Handleiding voor machtigingen-UI](../../access-control/abac/ui/browse.md). |

Voor meer informatie over op attribuut-gebaseerde toegangsbeheer, zie [op attributen-gebaseerd toegangsbeheeroverzicht](../../access-control/abac/overview.md). Voor een uitvoerige gids over het op attributen-gebaseerde toegangsbeheerwerkschema, lees [attribuut-based toegangsbeheergids van begin tot eind](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Met AI/ML-services kunnen marketinganalisten en praktijkmensen gebruikmaken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen voor de klant. Dit staat voor marketing analisten toe om modellen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Attribution AI

Attribution AI wordt gebruikt om credits toe te wijzen aan aanraakpunten die leiden tot conversiegebeurtenissen. Dit kan door marketers worden gebruikt om het marketing effect van elk individueel marketing aanraakpunt over klantenreizen te kwantificeren.

| Functie | Beschrijving |
| --- | --- |
| Concept-instantie opslaan | Met deze nieuwe functie kunnen marketinganalisten een modelconfiguratie opslaan als een conceptversie en deze blijven bewerken totdat deze voltooid is voordat ze training en scoring volgen. Scenario&#39;s waar deze functie nuttig is, zijn onder andere wanneer een gebruiker meerdere velden heeft die in de workflow moeten worden gedefinieerd, maar die vanwege tijdbeperkingen niet kunnen worden voltooid. Een ander scenario is wanneer één of meerdere datasetstatistieken worden verwerkt en nog niet beschikbaar. Lees de [Gebruikershandleiding voor Attribution AI](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) voor meer informatie. |
| Beleid inzake governance | Nadat de gebruikers voorleggen om een geval door het configuratiewerkschema tot stand te brengen, controleert de nieuwe dienst van de beleidshandhaving of er om het even welke beleidsschendingen van gegevensgebruik zijn en toont de details in popover. Het zorgt ervoor dat de gegevensverrichtingen en de marketing acties met het beleid van het gegevensgebruik verenigbaar zijn dat op Adobe Experience Platform wordt gevormd. |

Voor meer informatie over Attribution AI, [Overzicht van Attribution AI](../../intelligent-services/attribution-ai/overview.md). Voor informatie over het beleid inzake gegevensbeheer, lees [beleidsoverzicht](../../data-governance/policies/overview.md).

### Customer AI

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren.

| Functie | Beschrijving |
| --- | --- |
| Concept-instantie opslaan | Met deze nieuwe functie kunnen marketinganalisten een modelconfiguratie opslaan als een conceptversie en deze blijven bewerken totdat deze voltooid is voordat ze training en scoring volgen. Scenario&#39;s waar deze functie nuttig is, zijn onder andere wanneer een gebruiker meerdere velden heeft die in de workflow moeten worden gedefinieerd, maar die vanwege tijdbeperkingen niet kunnen worden voltooid. Een ander scenario is wanneer één of meerdere datasetstatistieken worden verwerkt en nog niet beschikbaar. Lees de [Handleiding voor AI-gebruikers van klant](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) voor meer informatie. |
| Beleid inzake governance | Nadat de gebruikers voorleggen om een geval door het configuratiewerkschema tot stand te brengen, controleert de nieuwe dienst van de beleidshandhaving of er om het even welke beleidsschendingen van gegevensgebruik zijn en toont de details in popover. Het zorgt ervoor dat de gegevensverrichtingen en de marketing acties met het beleid van het gegevensgebruik verenigbaar zijn dat op Adobe Experience Platform wordt gevormd. |

Voor meer informatie over AI van de Klant, lees [AI-overzicht van klant](../../intelligent-services/customer-ai/overview.md). Voor informatie over het beleid inzake gegevensbeheer, lees [beleidsoverzicht](../../data-governance/policies/overview.md).

## Controlelogboeken {#audit-logs}

Experience Platform staat u toe om gebruikersactiviteit voor diverse diensten en mogelijkheden te controleren. De auditlogboeken bevatten informatie over wie wat heeft gedaan en wanneer.

**Bijgewerkte functies**

| Functie | Naam | Beschrijving |
| --- | --- | --- |
| Toegevoegde bronnen | <ul><li>Attribution AI-instantie</li><li>AI-exemplaar van klant</li><li>DataStream</li></ul> | De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt. Als de eigenschap wordt toegelaten moet u niet manueel logboekinzameling toelaten. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over de verschillende middel-specifieke gebeurtenistypen die door controlelogboeken in Platform worden gevolgd, verwijs naar [overzicht van auditlogboeken](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

| Functie | Beschrijving |
| --- | --- |
| Label tijdens gebruik | Wanneer het label in de widgetbibliotheek wordt weergegeven, identificeert het in-use-label gemakkelijk de aanwezigheid van bestaande widgets in het dashboard. Hierdoor kunt u dubbel werk gemakkelijk voorkomen, maar u kunt nog steeds dezelfde widget meer dan één keer toevoegen als u wilt. |
| Door gebruiker gedefinieerde dashboards | Door de gebruiker gedefinieerde dashboards helpen u om inzichten te versnellen en visualisaties aan te passen door u in staat te stellen aangepaste dashboards te maken en te beheren. Met door de gebruiker gedefinieerde dashboards kunt u op maat gemaakte widgets maken, toevoegen en bewerken om belangrijke metriek die voor uw organisatie van belang is, zichtbaar te maken. Lees de [functiehandleiding](../../dashboards/user-defined-dashboards.md) voor meer informatie. |
| Gegevensmodel gegevens Platform klantgegevens | De eigenschap van het Model van Gegevens van de Gegevens van de Klant van het Platform van Gegevens (CDP) benadrukt de gegevensmodellen en SQL die de inzichten voor diverse profiel, bestemming, en segmentatiewidgets macht. U kunt deze SQL vraagmalplaatjes aanpassen om CDP- rapporten voor uw marketing en zeer belangrijke gebruiksgevallen van de prestatiesindicator tot stand te brengen. Deze inzichten kunnen dan als douanewidgets voor uw user-defined dashboards worden gebruikt. Lees de [Handleiding CDP-gegevensmodel voor ingesloten gegevens](../../dashboards/cdp-insights-data-model.md) voor meer informatie. |
| De widget Rapport voor publiek-overlap | Deze widget is beschikbaar voor beide [!UICONTROL Profiles] en [!UICONTROL Segments] dashboards. Het rapport bevat een geordende lijst met soorten publiek die worden gerangschikt op basis van de hoogste of laagste overlappende percentages voor het gekozen segment. Van de [!UICONTROL Profiles] het dashboard u kunt filteren en bekijken uw publieksoverlap door beleid van alle beschikbare segmenten samen te voegen. De [!UICONTROL Segments] Met dashboards kunt u de publieksoverlap filteren op een bepaald segment.<br>Gebruik deze analyse om nieuwe, krachtige segmenten te bouwen en te vermijden verzendend het zelfde publiek naar verschillende bestemmingen. Het verslag helpt ook verborgen inzichten te identificeren om segmentatie te verbeteren of unieke profielen te vinden om na te streven. Lees de respectievelijke [profielen](../../dashboards/guides/profiles.md#audience-overlap-report) en [segmenten](../../dashboards/guides/segments.md#audience-overlap-report) widgethulplijnen voor meer informatie. |

Voor meer informatie over [!DNL Dashboards], zie de [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Integratie van linkernavigatie in de gebruikersinterface van het Platform | Alle mogelijkheden die eerder exclusief waren aan de UI van de Inzameling van Gegevens (met inbegrip van markeringen, gebeurtenis door:sturen, en gegevensstromen) zijn nu ook beschikbaar door de linkernavigatie in Experience Platform, onder de categorie **[!UICONTROL Data Collection]**. Dit elimineert de behoefte om tussen UIs te schakelen wanneer het werken met de mogelijkheden van de gegevensinzameling in Platform. |
| Toewijzing door gebruiker in tags en gebeurtenis doorsturen | Als aanbieding beschikbaar is [!UICONTROL Properties] in markeringen en gebeurtenis door:sturen, toont elk vermeld bezit nu wanneer het het laatst werd bijgewerkt, en welke gebruiker de update maakte. |
| [[!DNL Snap Conversions API] extension](https://exchange.adobe.com/apps/ec/108550) voor gebeurtenis doorsturen | U kunt nu gegevens verzenden naar de [!DNL Snapchat Conversions API] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Voor meer informatie over het verifiëren en gebruiken van API, verwijs naar [[!DNL Snapchat Marketing API] documentatie](https://marketingapi.snapchat.com/docs/conversion.html). |
| [[!DNL User-Agent Client Hints] in Web SDK](../../edge/fundamentals/user-agent-client-hints.md) | De SDK van het Web ondersteunt nu [[!DNL User-Agent Client Hints]](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Met clienttips hebben websiteeigenaars toegang tot veel van de informatie die in het dialoogvenster [!DNL User-Agent] -tekenreeks, maar op een meer privacyvriendelijke manier. |
| [Web SDK pagina-voor-pagina migratie](../../edge/home.md#migrating-to-web-sdk) | U kunt nu bestaande wegeigenschappen migreren uit andere Experience Cloud-bibliotheken, zoals [!DNL at.js], naar Web SDK, één pagina tegelijk. Dit laat een gefaseerde benadering van de migratie van SDK van het Web toe, zonder de behoefte om al uw pagina&#39;s in één keer te migreren. |

{style=&quot;table-layout:auto&quot;}

<!-- | [[!DNL Adobe Journey Optimizer] support for datastreams](../../edge/datastreams/overview.md#aep)| The Adobe Experience Platform service for datastreams now supports [!DNL Adobe Journey Optimizer]. This option allows you to use web and app-based inbound channels in [!DNL Adobe Journey Optimizer].|
-->

Voor meer informatie over gegevensverzameling in Platform raadpleegt u de [overzicht van gegevensverzameling](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| Destination SDK | Destination SDK biedt nu volledige ondersteuning voor partners en klanten die in batch (of op bestand gebaseerd) gemaakte of persoonlijke doelen maken. Lees de volgende documentatiepagina&#39;s voor meer informatie: <ul><li>[Overzicht van Destination SDK](/help/destinations/destination-sdk/overview.md)</li><li>[Een op een bestand gebaseerde bestemming configureren](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Opties voor bestandsindeling configureren voor op bestanden gebaseerde doelen](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md)</li><li>[Test uw op een bestand gebaseerde doelen](/help/destinations/destination-sdk/file-based-destination-testing-overview.md)</li></ul> |

{style=&quot;table-layout:auto&quot;}

**Nieuwe of bijgewerkte doelen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services biedt een platform voor het ontwerpen van de ervaringen van klanten over meerdere kanalen en een omgeving voor visuele campagneorchestratie, real-time interactiebeheer en uitvoering via meerdere kanalen. [Aan de slag met campagne](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Deze integratie werkt met [Adobe Campaign versie 8.4 of hoger](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html?lang=en#release-8-4-1). |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | De [!DNL Salesforce CRM] de bestemming is bijgewerkt om zowel contacten en leidt updates, als prestatiesverbeteringen voor snellere updates te steunen. |

{style=&quot;table-layout:auto&quot;}

**Nieuwe of bijgewerkte documentatie**

| Documentatie | Beschrijving |
| ----------- | ----------- |
| API-documentatie voor Doelen Flow Service | De [Referentiedocumentatie voor doel-API](https://developer.adobe.com/experience-platform-apis/references/destinations/) werd bijgewerkt om begeleiding op te nemen over hoe te om verrichtingen op op dossier-gebaseerde bestemmingen uit te voeren. Bewerkingen voor streamingdoelen worden later toegevoegd. |

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| UI-ondersteuning voor opsommingen en voorgestelde waarden | Naast opsommingen die gegevensvalidatie mogelijk maken, kunt u nu [voorgestelde waarden toevoegen of verwijderen](../../xdm/ui/fields/enum.md) voor standaard of aangepaste tekenreeksvelden, zodat gebruikers van het Platform een lijst met waarden kunnen selecteren bij het maken van segmenten. |

**Nieuwe XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Eigenschappen van een specifiek element waarmee interactie heeft plaatsgevonden die ertoe heeft geleid dat de proposition-gebeurtenis werd geactiveerd. |
| Veldgroep | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Mediainteracties worden in de loop der tijd bijgehouden. |
| Veldgroep | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Hier vindt u informatie over mediagegevens. |
| Veldgroep | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beschrijft oppervlakken voor Experience Events in Adobe Journey Optimizer. |

{style=&quot;table-layout:auto&quot;}

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gedraging | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Toegevoegde waarden voor `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Verwijderde waarden voor `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Veldgroep | (Meerdere) | [Verschillende veldbeschrijvingen zijn bijgewerkt](https://github.com/adobe/xdm/pull/1628/files) over Journey Orchestration-componenten. |
| Veldgroep | (Meerdere) | [De titels voor verschillende Adobe Workfront-componenten zijn bijgewerkt](https://github.com/adobe/xdm/pull/1634/files) ter wille van de consistentie. |
| Veldgroep | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | De naamruimten van verschillende velden zijn bijgewerkt naar `xdm`. |
| Veldgroep | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Een nieuw veld toegevoegd, `isReadSegmentTriggerStartEvent`. |
| Veldgroep | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | De `xdm:uvIndex` veld aan een type geheel getal en de waarde `xdm` naamruimte maken voor verschillende velden waarin naamruimte ontbreekt. |
| Veldgroep | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` en `xdm:implementationDetails` zijn verwijderd uit de veldgroep. |
| Gegevenstype | (Meerdere) | [Verschillende namen van media-eigenschappen zijn bijgewerkt](https://github.com/adobe/xdm/pull/1626/files) voor diverse gegevenstypen, voor consistentie. |
| Gegevenstype | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Toegevoegde bekende namen voor flutter. |
| Gegevenstype | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Het gegevenstype kan nu een lijst met sleutelwaardeparen voor metagegevens accepteren die zijn gekoppeld aan het betreffende punt. |
| Gegevenstype | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | [!DNL AJO Classification Fields] is hernoemd naar [!UICONTROL Proposition Action]. |
| Gegevenstype | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | [!DNL AJO Classification Fields] is hernoemd naar [!UICONTROL Proposition Action]. |
| (Meerdere) | (Meerdere) | Experimentele eigenschappen zijn [gestabiliseerd over alle B2B-componenten](https://github.com/adobe/xdm/pull/1617/files). |
| (Meerdere) | (Meerdere) | Adobe Journey Optimizer-entiteiten zijn [gestabiliseerd](https://github.com/adobe/xdm/pull/1625/files). |
| (Meerdere) | (Meerdere) | De naamruimten van bepaalde velden in verschillende experimentele componenten zijn: [bijgewerkt voor consistentie](https://github.com/adobe/xdm/pull/1626/files). |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen gefragmenteerd zijn, die elke klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het verwijderen van gegevenssets | De Dienst van de identiteit steunt nu dataset schrapping wanneer het verzoeken door [Catalogusservice-API](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI of Data Hygiene. Lees de handleiding op [het schrappen van datasets in UI](../../catalog/datasets/user-guide.md#delete-a-dataset) voor meer informatie . |

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Alert-abonnements-API | Met Adobe Experience Platform Query Service kunt u zich abonneren op waarschuwingen voor zowel ad-hocquery&#39;s als geplande query&#39;s. Waarschuwingen kunnen via e-mail worden ontvangen, binnen de gebruikersinterface van het Platform of beide. Op dit moment kunnen querywaarschuwingen alleen worden geabonneerd op [Query Service-API](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Gegevenssetvoorbeelden | De datasetsteekproeven van de Dienst van de vraag laten u toe om verkennende vragen over grote gegevens met zeer verminderde verwerkingstijd ten koste van vraagnauwkeurigheid te leiden. Zie de [Gegevenssetvoorbeeldgids](../../query-service/sql/dataset-samples.md) voor meer informatie. |

Voor meer informatie over [!DNL Query Service], zie de [[!DNL Query Service] overzicht](../../query-service/home.md).

Zie de [documentatie met querywaarschuwingen](../../query-service/api/alert-subscriptions.md) voor meer informatie.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Audience Manager segmentpopulatie impact op Real-Time Klantprofiel | De inname van grote populaties in het Audience Manager segment heeft een directe invloed op uw totale aantal profielen wanneer u eerst een segment van de Audience Manager naar het Platform verzendt gebruikend de bron van de Audience Manager. Dit betekent dat het selecteren van alle segmenten kan leiden tot een aantal profielen dat groter is dan uw gebruiksrechten voor licenties. Lees voor meer informatie de [Overzicht van bron Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Voor informatie over uw licentiegebruik leest u de documentatie op [het gebruiken van het dashboard van het vergunningsgebruik](../../dashboards/guides/license-usage.md). |
| Ondersteuning voor Adobe Campaign Managed Cloud Service | Met de Adobe Campaign Managed Cloud Service-bron kunt u uw Adobe Campaign v8.4-gegevens voor levering en bijhouden van logbestanden naar het Experience Platform brengen. Lees de handleiding op [een Adobe Campaign Managed Cloud Service-bronverbinding maken in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/campaign.md) voor meer informatie . |
| API-ondersteuning voor inname op aanvraag voor batchbronnen | Gebruik inname op aanvraag om een ad-hocflowrun voor een bepaalde gegevensstroom te maken met de [!DNL Flow Service] API. De gecreeerde looppas van de stroom moet aan éénmalige opname worden geplaatst. Lees voor meer informatie de handleiding op [een flow-run maken voor opname op aanvraag met behulp van de API](../../sources/tutorials/api/on-demand-ingestion.md) voor meer informatie . |
| API-ondersteuning voor het opnieuw proberen van mislukte gegevensstroombewerkingen voor batchbronnen | Gebruik de `re-trigger` bewerking om de mislukte gegevensstroom opnieuw uit te voeren via de API. Lees de handleiding op [opnieuw proberen, mislukte gegevensstroombewerkingen met de API](../../sources/tutorials/api/retry-flows.md) voor meer informatie . |
| API-ondersteuning voor het filteren van gegevens op rijniveau voor de [!DNL Google BigQuery] en [!DNL Snowflake] bronnen | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de [!DNL Google BigQuery] en [!DNL Snowflake] bronnen. Lees de handleiding op [gegevens filteren voor een bron met behulp van de API](../../sources/tutorials/api/filter.md) voor meer informatie . |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
