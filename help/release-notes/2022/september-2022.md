---
title: Aanvullende informatie van september 2022 voor Adobe Experience Platform
description: Aanvullende informatie voor de versie van september 2022 voor Adobe Experience Platform.
exl-id: a7a4dcf8-2cf3-4e39-879d-bdfcbacb737a
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 20%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 28 september 2022**

Nieuwe functies in Adobe Experience Platform:

- [Toegangsbeheer op basis van kenmerken](#abac)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Controlelogboeken](#audit-logs)
- [[!DNL Dashboards]](#dashboards)
- [Dataverzameling](#data-collection)
- [Bestemmingen](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Query-service](#query-service)
- [Bronnen](#sources)

## Toegangsbeheer op basis van kenmerken {#abac}

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangsbeheer zal met ingang van Oktober 2022 worden toegelaten. Neem contact op met uw Adobe-vertegenwoordiger als u een vroege adoptietechnicus wilt zijn.

Toegangsbeheer op basis van kenmerken is een functionaliteit van Adobe Experience Platform waarmee merken die aandacht hebben voor privacy, meer flexibiliteit krijgen bij toegangsbeheer voor gebruikers. Individuele objecten, zoals schemavelden en segmenten, kunnen aan gebruikersrollen worden toegewezen. Met deze functie kunt u toegang tot afzonderlijke objecten verlenen of intrekken voor specifieke Experience Platform-gebruikers in uw organisatie.

Via attribuut-gebaseerde toegangscontrole, kunnen de beheerders van uw organisatie gebruikers&#39; toegang tot, gevoelige persoonlijke gegevens (SPD), persoonlijk identificeerbare informatie (PII) en ander aangepast type van gegevens over alle werkschema&#39;s en middelen van Experience Platform controleren. Beheerders kunnen gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die bij die velden horen.

| Functie | Beschrijving |
| --- | --- |
| Toegangsbeheer op basis van kenmerken | Op attribuut-gebaseerde toegangscontrole staat u toe om het schemagebieden en de segmenten van het Model van de Gegevens van de Ervaring (XDM) met etiketten te etiketteren die organisatorische of gegevensgebruikswerkingsgebied bepalen. Parallel hieraan kunnen beheerders de gebruiker en de interface van het rolbeleid gebruiken om toegangsbeleid te bepalen dat XDM schemagebieden en segmenten behandelt om de toegang beter te beheren die aan gebruikers of groepen gebruikers (interne, externe, of derdegebruikers) wordt gegeven. Voor meer informatie, zie het [ op attributen-gebaseerde overzicht van de toegangscontrole ](../../access-control/abac/overview.md). |
| Machtigingen | Machtigingen zijn het gebied van Experience Cloud waar beheerders gebruikersrollen en toegangsbeleid kunnen definiëren om toegangsmachtigingen voor functies en objecten binnen een producttoepassing te beheren. Door Toestemmingen, kunt u rollen tot stand brengen en beheren, de gewenste middeltoestemmingen voor deze rollen toewijzen, en beleid bouwen aan hefboomwerkings etiketten en bepalen welke gebruikersrollen toegang tot specifieke middelen van Experience Platform hebben. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld. Voor meer informatie, zie de [ gids UI van Toestemmingen ](../../access-control/abac/ui/browse.md). |

Zie het [overzicht van toegangsbeheer op basis van kenmerken](../../access-control/abac/overview.md) voor meer informatie over toegangsbeheer op basis van kenmerken. Voor een uitgebreide handleiding over de workflow voor toegangsbeheer op basis van kenmerken raadpleegt u de [end-to-end handleiding voor toegangsbeheer op basis van kenmerken](../../access-control/abac/end-to-end-guide.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Met AI/ML-services kunnen marketinganalisten en praktijkmensen gebruikmaken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen voor de klant. Dit staat voor marketing analisten toe om modellen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Attributie-AI

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

| Functie | Beschrijving |
| --- | --- |
| Concept-instantie opslaan | Met deze nieuwe functie kunnen marketinganalisten een modelconfiguratie opslaan als een conceptversie en deze blijven bewerken totdat deze voltooid is voordat ze training en scoring volgen. Scenario&#39;s waar deze functie nuttig is, zijn onder andere wanneer een gebruiker meerdere velden heeft die in de workflow moeten worden gedefinieerd, maar die vanwege tijdbeperkingen niet kunnen worden voltooid. Een ander scenario is wanneer één of meerdere datasetstatistieken worden verwerkt en nog niet beschikbaar. Lees de [ gebruikersgids van AI van de Attributie ](../../intelligent-services/attribution-ai/user-guide.md#governance-policies) om meer te leren. |
| Beleid inzake governance | Nadat de gebruikers voorleggen om een geval door het configuratiewerkschema tot stand te brengen, controleert de nieuwe dienst van de beleidshandhaving of er om het even welke beleidsschendingen van gegevensgebruik zijn en toont de details in popover. Het zorgt ervoor dat de gegevensverrichtingen en de marketing acties met het beleid van het gegevensgebruik verenigbaar zijn dat op Adobe Experience Platform wordt gevormd. |

Voor meer informatie over Attributie AI, het [ overzicht van AI van de Attributie ](../../intelligent-services/attribution-ai/overview.md). Voor informatie over het beleid van het gegevensbeheer, lees het [ beleidsoverzicht ](../../data-governance/policies/overview.md).

### Customer AI

De in Real-Time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren.

| Functie | Beschrijving |
| --- | --- |
| Concept-instantie opslaan | Met deze nieuwe functie kunnen marketinganalisten een modelconfiguratie opslaan als een conceptversie en deze blijven bewerken totdat deze voltooid is voordat ze training en scoring volgen. Scenario&#39;s waar deze functie nuttig is, zijn onder andere wanneer een gebruiker meerdere velden heeft die in de workflow moeten worden gedefinieerd, maar die vanwege tijdbeperkingen niet kunnen worden voltooid. Een ander scenario is wanneer één of meerdere datasetstatistieken worden verwerkt en nog niet beschikbaar. Lees de [ AI gebruikersgids van de Klant ](../../intelligent-services/customer-ai/user-guide/configure.md#governance-policies) om meer te leren. |
| Beleid inzake governance | Nadat de gebruikers voorleggen om een geval door het configuratiewerkschema tot stand te brengen, controleert de nieuwe dienst van de beleidshandhaving of er om het even welke beleidsschendingen van gegevensgebruik zijn en toont de details in popover. Het zorgt ervoor dat de gegevensverrichtingen en de marketing acties met het beleid van het gegevensgebruik verenigbaar zijn dat op Adobe Experience Platform wordt gevormd. |

Voor meer informatie over Klant AI, lees het [ overzicht van AI van de Klant ](../../intelligent-services/customer-ai/overview.md). Voor informatie over het beleid van het gegevensbeheer, lees het [ beleidsoverzicht ](../../data-governance/policies/overview.md).

## Auditlogboeken {#audit-logs}

Met Experience Platform kunt u gebruikersactiviteiten controleren op verschillende services en mogelijkheden. De auditlogboeken bevatten informatie over wie wat heeft gedaan en wanneer.

**Bijgewerkte functies**

| Functie | Naam | Beschrijving |
| --- | --- | --- |
| Toegevoegde bronnen | <ul><li>Attribution AI-instantie</li><li>AI-exemplaar van klant</li><li>DataStream</li></ul> | De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt. Als de eigenschap wordt toegelaten moet u niet manueel logboekinzameling toelaten. |

{style="table-layout:auto"}

Voor meer informatie over de verschillende middel-specifieke gebeurtenistypen die door controlelogboeken in Experience Platform worden gevolgd, verwijs naar het [ overzicht van controlelogboeken ](../../landing/governance-privacy-security/audit-logs/overview.md).

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten kunt bekijken over de gegevens van uw organisatie, zoals vastgelegd tijdens dagelijkse momentopnamen.

| Functie | Beschrijving |
| --- | --- |
| Label tijdens gebruik | Wanneer het label in de widgetbibliotheek wordt weergegeven, identificeert het in-use-label gemakkelijk de aanwezigheid van bestaande widgets in het dashboard. Hierdoor kunt u dubbel werk gemakkelijk voorkomen, maar u kunt nog steeds dezelfde widget meer dan één keer toevoegen als u wilt. |
| Door gebruiker gedefinieerde dashboards | Door de gebruiker gedefinieerde dashboards helpen u om inzichten te versnellen en visualisaties aan te passen door u in staat te stellen aangepaste dashboards te maken en te beheren. Met door de gebruiker gedefinieerde dashboards kunt u op maat gemaakte widgets maken, toevoegen en bewerken om belangrijke metriek die voor uw organisatie van belang is, zichtbaar te maken. Lees de [ eigenschapgids ](../../dashboards/standard-dashboards.md) om meer te leren. |
| Gegevensmodel van gegevensplatform van klant | De eigenschap van het Model van Gegevens van het Platform van Gegevens van de Klant van Gegevens (CDP) stelt de gegevensmodellen en SQL bloot die de inzichten voor diverse profiel, bestemming, en segmentatiewidgets macht. U kunt deze SQL vraagmalplaatjes aanpassen om CDP- rapporten voor uw marketing en zeer belangrijke gebruiksgevallen van de prestatiesindicator tot stand te brengen. Deze inzichten kunnen dan als douanewidgets voor uw user-defined dashboards worden gebruikt. Lees de [ CDP eigenschapgids van het Model van Gegevens van Inzichten ](../../dashboards/data-models/cdp-insights-data-model-b2c.md) om meer te leren. |
| De widget Rapport voor publiek-overlap | Deze widget is beschikbaar voor zowel [!UICONTROL Profiles] als [!UICONTROL Segments] -dashboards. Het rapport bevat een geordende lijst met soorten publiek die worden gerangschikt op basis van de hoogste of laagste overlappende percentages voor het gekozen segment. Vanuit het dashboard van [!UICONTROL Profiles] kunt u filteren en de overlappingen van uw publiek bekijken door beleid van alle beschikbare segmenten samen te voegen. Met de dashboards van [!UICONTROL Segments] kunt u de publieksoverlap filteren op een bepaald segment.<br> gebruik deze analyse om nieuwe, krachtige segmenten te bouwen en te vermijden verzendend het zelfde publiek naar verschillende bestemmingen. Het verslag helpt ook verborgen inzichten te identificeren om segmentatie te verbeteren of unieke profielen te vinden om na te streven. Lees de respectieve [ profielen ](../../dashboards/guides/profiles.md#audience-overlap-report) en [ segmenten ](../../dashboards/guides/audiences.md#audience-overlap-report) widgetgidsen om meer te leren. |

Voor meer informatie over [!DNL Dashboards] raadpleegt u het [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## Dataverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u klantervaringsgegevens aan de klantzijde kunt verzamelen en deze naar het Adobe Experience Platform Edge Network kunt verzenden. Daar kunnen ze worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Integratie van linkernavigatie in de gebruikersinterface van Experience Platform | Alle mogelijkheden die voorheen exclusief waren voor de gebruikersinterface voor gegevensverzameling (inclusief tags, gebeurtenissen doorsturen en gegevensstromen) zijn nu ook beschikbaar via de linkernavigatie in Experience Platform, onder de categorie **[!UICONTROL Data Collection]** . Dit elimineert de behoefte om tussen UIs te schakelen wanneer het werken met de mogelijkheden van de gegevensinzameling in Experience Platform. |
| Toewijzing door gebruiker in tags en gebeurtenis doorsturen | Wanneer een lijst beschikbaar [!UICONTROL Properties] in markeringen en gebeurtenis door:sturen, toont elk vermeld bezit nu wanneer het laatst werd bijgewerkt, en welke gebruiker de update maakte. |
| [[!DNL Snap Conversions API]  uitbreiding ](https://exchange.adobe.com/apps/ec/108550) voor gebeurtenis door:sturen | U kunt gegevens naar [!DNL Snapchat Conversions API] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Raadpleeg de [[!DNL Snapchat Marketing API] documentatie](https://marketingapi.snapchat.com/docs/conversion.html) voor meer informatie over het verifiëren en gebruiken van de API. |
| [ gebruiker-agent de Hints van de Cliënt in SDK van het Web ](/help/web-sdk/use-cases/client-hints.md) | SDK van het Web steunt nu [ gebruiker-Agent de wenken van de Cliënt ](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Met clienttips hebben eigenaars van websites toegang tot veel van dezelfde informatie die beschikbaar is in de [!DNL User-Agent] -tekenreeks, maar op een meer privacyvriendelijke manier. |
| [ SDK van het Web pagina-door-pagina migratie ](../../web-sdk/home.md#migrating-to-web-sdk) | U kunt uw bestaande wegeigenschappen nu van andere bibliotheken van Experience Cloud, zoals [!DNL at.js], aan Web SDK, één pagina tegelijk migreren. Dit maakt een gefaseerde benadering van de migratie van Web SDK mogelijk, zonder de noodzaak om al uw pagina&#39;s in één keer te migreren. |
| [[!DNL Adobe Journey Optimizer]  steun voor gegevensstromen ](../../datastreams/overview.md#aep) | De Adobe Experience Platform-service voor gegevensstromen ondersteunt nu [!DNL Adobe Journey Optimizer] . Met deze optie kunt u inkomende kanalen via het web en op apps gebaseerde kanalen gebruiken in [!DNL Adobe Journey Optimizer] . |

{style="table-layout:auto"}

Voor meer informatie over gegevensinzameling in Experience Platform, te zien gelieve het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| Destination SDK | Destination SDK biedt nu volledige ondersteuning voor partners en klanten die batchgewijze (of op bestanden gebaseerde) of persoonlijke doelen maken. Lees de volgende documentatiepagina&#39;s voor meer informatie: <ul><li>[ het Overzicht van Destination SDK ](../../destinations/destination-sdk/overview.md)</li><li>[ vorm een op dossier-gebaseerde bestemming ](../../destinations/destination-sdk/guides/configure-file-based-destination-instructions.md)</li><li>[ vorm dossier het formatteren opties voor op dossier-gebaseerde bestemmingen ](../../destinations/destination-sdk/guides/batch/configure-file-formatting-options.md)</li><li>[ Test uw op dossier-gebaseerde bestemmingen ](../../destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md)</li></ul> |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Adobe Campaign Managed Cloud Services]](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | Adobe Campaign Managed Cloud Services biedt een platform voor het ontwerpen van de ervaringen van klanten over meerdere kanalen en een omgeving voor visuele campagneorchestratie, real-time interactiebeheer en uitvoering via meerdere kanalen. [ krijgt Begonnen met Campagne ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/start/get-started.html). Merk op dat deze integratie met [ versie 8.4 van Adobe Campaign of hoger ](https://experienceleague.adobe.com/docs/campaign/campaign-v8/new/release-notes.html#release-8-4-1) werkt. |
| [[!DNL Salesforce CRM]](../../destinations/catalog/crm/salesforce.md) | Het doel van [!DNL Salesforce CRM] is bijgewerkt ter ondersteuning van zowel contactpersonen en leads-updates als prestatieverbeteringen voor snellere updates. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte documentatie**

| Documentatie | Beschrijving |
| ----------- | ----------- |
| API-documentatie voor Doelen Flow Service | De [ API van Doelen verwijzingsdocumentatie ](https://developer.adobe.com/experience-platform-apis/references/destinations/) werd bijgewerkt om begeleiding op te nemen hoe te handelingen op op dossier-gebaseerde bestemmingen uit te voeren. Bewerkingen voor streamingdoelen worden later toegevoegd. |

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| UI-ondersteuning voor opsommingen en voorgestelde waarden | Naast lijsten die gegevensbevestiging toelaten, kunt u voorgestelde waarden [&#128279;](../../xdm/ui/fields/enum.md) voor standaard of douanekoordgebieden nu toevoegen of verwijderen zodat de gebruikers van Experience Platform een vriendschappelijke lijst van te selecteren waarden hebben wanneer het creëren van segmenten. |

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | Eigenschappen van een specifiek element waarmee interactie heeft plaatsgevonden die ertoe heeft geleid dat de proposition-gebeurtenis werd geactiveerd. |
| Veldgroep | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-media-analytics.schema.json) | Mediainteracties worden in de loop der tijd bijgehouden. |
| Veldgroep | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | Hier vindt u informatie over mediagegevens. |
| Veldgroep | [[!UICONTROL Adobe CJM ExperienceEvent - Surfaces]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/surfaces.schema.json) | Beschrijft oppervlakken voor Experience Events in Adobe Journey Optimizer. |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Gedrag | [[!UICONTROL Time series]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | <ul><li>Toegevoegde waarden voor `eventType`:<ul><li>`decisioning.propositionSend`</li><li>`decisioning.propositionDismiss`</li><li>`decisioning.propositionTrigger`</li><li>`media.downloaded`</li><li>`location.entry`</li><li>`location.exit`</li></ul></li><li>Verwijderde waarden voor `eventType`:<ul><li>`decisioning.propositionDeliver`</li><li>`media.stateStart`</li><li>`media.stateEnd`</li></ul></li></ul> |
| Veldgroep | (Meerdere) | [ werkte verscheidene gebiedsbeschrijvingen ](https://github.com/adobe/xdm/pull/1628/files) over de componenten van Journey Orchestration bij. |
| Veldgroep | (Meerdere) | [ werkte de titels voor verscheidene componenten van Adobe Workfront ](https://github.com/adobe/xdm/pull/1634/files) voor consistentie bij. |
| Veldgroep | [[!UICONTROL AJO Classification Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | De naamruimten van verschillende velden zijn bijgewerkt naar `xdm` . |
| Veldgroep | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Er is een nieuw veld toegevoegd, `isReadSegmentTriggerStartEvent` . |
| Veldgroep | [[!UICONTROL Forecasted Weathers]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/forecasted-weather.schema.json) | Het veld `xdm:uvIndex` is gewijzigd in een geheel-getaltype en de naamruimte `xdm` is toegevoegd aan verschillende velden waarin deze ontbreekt. |
| Veldgroep | [[!UICONTROL Media details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/mediadetails.schema.json) | `xdm:endUserIDs` en `xdm:implementationDetails` zijn verwijderd uit de veldgroep. |
| Gegevenstype | (Meerdere) | [ werkte verscheidene namen van media bezit ](https://github.com/adobe/xdm/pull/1626/files) over verscheidene gegevenstypes voor consistentie bij. |
| Gegevenstype | [[!UICONTROL Implementation details]](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/implementationdetails.schema.json) | Toegevoegde bekende namen voor flutter. |
| Gegevenstype | [[!UICONTROL Point of interest details]](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-detail.schema.json) | Het gegevenstype kan nu een lijst met sleutelwaardeparen voor metagegevens accepteren die zijn gekoppeld aan het betreffende punt. |
| Gegevenstype | [[!UICONTROL Proposition Action]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-action.schema.json) | De naam van [!DNL AJO Classification Fields] is gewijzigd in [!UICONTROL Proposition Action] . |
| Gegevenstype | [[!UICONTROL Proposition Event Type]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/decisioning/proposition-event-type.schema.json) | De naam van [!DNL AJO Classification Fields] is gewijzigd in [!UICONTROL Proposition Action] . |
| (Meerdere) | (Meerdere) | De experimentele eigenschappen zijn [ gestabiliseerd over alle B2B componenten ](https://github.com/adobe/xdm/pull/1617/files). |
| (Meerdere) | (Meerdere) | De entiteiten van Adobe Journey Optimizer zijn [ gestabiliseerd ](https://github.com/adobe/xdm/pull/1625/files). |
| (Meerdere) | (Meerdere) | De namespaces van bepaalde gebieden over verscheidene experimentele componenten zijn [ bijgewerkt voor consistentie ](https://github.com/adobe/xdm/pull/1626/files). |

{style="table-layout:auto"}

Voor meer informatie over XDM in Experience Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Identiteitsservice {#identity-service}

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen gefragmenteerd zijn, die elke klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het verwijderen van gegevenssets | De Dienst van de identiteit steunt nu datasetschrapping wanneer het verzoeken door de [ Dienst API van de Catalogus ](https://developer.adobe.com/experience-platform-apis/references/catalog/), UI, of de Hygiëne van Gegevens. Lees de gids bij [ het schrappen van datasets in UI ](../../catalog/datasets/user-guide.md#delete-a-dataset) voor meer informatie. |

Meer over de Dienst van de Identiteit leren, lees het [ overzicht van de Dienst van de Identiteit ](../../identity-service/home.md).

## Query-service {#query-service}

Met de Query-service kunt u standaard SQL gebruiken om query&#39;s uit te voeren op gegevens in Adobe Experience Platform [!DNL Data Lake]. U kunt willekeurige datasets van [!DNL Data Lake] combineren en de queryresultaten vastleggen als nieuwe dataset voor gebruik in rapportage, de werkruimte voor datawetenschappen, of voor opname in het Real-Time Customer Profile.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Alert-abonnements-API | Met Adobe Experience Platform Query Service kunt u zich abonneren op waarschuwingen voor zowel ad-hocquery&#39;s als geplande query&#39;s. Waarschuwingen kunnen via e-mail worden ontvangen, binnen de gebruikersinterface van Experience Platform of beide. Momenteel, kunnen het vraagalarm slechts aan het gebruiken van de [ Dienst API van de Vraag worden ingetekend ](https://developer.adobe.com/experience-platform-apis/references/query-service/). |
| Gegevenssetvoorbeelden | De datasetsteekproeven van de Dienst van de vraag laten u toe om verkennende vragen over grote gegevens met zeer verminderde verwerkingstijd ten koste van vraagnauwkeurigheid te leiden. Zie de [ gids van de datasetsteekproeven ](../../query-service/key-concepts/dataset-samples.md) om meer te leren. |

Voor meer informatie over [!DNL Query Service] raadpleegt u het [[!DNL Query Service] overzicht](../../query-service/home.md).

Zie [ documentatie van het vraagalarm ](../../query-service/api/alert-subscriptions.md) om meer te leren.

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Audience Manager-segmentpopulatieeffect op realtime-klantprofiel | De opname van grote Audience Manager-segmentpopulaties heeft een directe invloed op het totale aantal profielen wanneer u eerst een Audience Manager-segment naar Experience Platform verzendt met de Audience Manager-bron. Dit betekent dat het selecteren van alle segmenten kan leiden tot een aantal profielen dat groter is dan uw gebruiksrechten voor licenties. Voor meer informatie, lees het [ bronOverzicht van Audience Manager ](../../sources/connectors/adobe-applications/audience-manager.md). Voor informatie over uw vergunningsgebruik, lees de documentatie op [ gebruikend het dashboard van het vergunningsgebruik ](../../dashboards/guides/license-usage.md). |
| Ondersteuning voor Adobe Campaign Managed Cloud Service | Gebruik de Adobe Campaign Managed Cloud Service-bron om uw gegevens over de levering en het bijhouden van logboekbestanden voor Adobe Campaign v8.4 naar Experience Platform over te brengen. Lees de gids bij [ het creëren van een Adobe Campaign Beheerde Cloud Service bronverbinding in UI ](../../sources/tutorials/ui/create/adobe-applications/campaign.md) voor meer informatie. |
| API-ondersteuning voor inname op aanvraag voor batchbronnen | Gebruik inname op aanvraag om een ad-hocflowuitvoering te maken voor een bepaalde gegevensstroom met de API [!DNL Flow Service] . De gecreeerde looppas van de stroom moet aan éénmalige opname worden geplaatst. Voor meer informatie, leest de gids op [ creërend een stroom die voor op bestelling wordt in werking gesteld het gebruiken van API ](../../sources/tutorials/api/on-demand-ingestion.md) voor meer informatie. |
| API-ondersteuning voor het opnieuw proberen van mislukte gegevensstroombewerkingen voor batchbronnen | Gebruik de bewerking `re-trigger` om de mislukte gegevensstroom opnieuw uit te voeren via de API. Lees de gids op [ opnieuw probeert ontbroken dataflow looppas gebruikend API ](../../sources/tutorials/api/retry-flows.md) voor meer informatie. |
| API-ondersteuning voor het filteren van gegevens op rijniveau voor de bronnen [!DNL Google BigQuery] en [!DNL Snowflake] | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de bronnen [!DNL Google BigQuery] en [!DNL Snowflake] . Lees de gids over [ het filtreren gegevens voor een bron gebruikend API ](../../sources/tutorials/api/filter.md) voor meer informatie. |

Voor meer informatie over bronnen leest u het [overzicht van bronnen](../../sources/home.md).
