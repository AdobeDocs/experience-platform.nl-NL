---
title: Opmerkingen bij de release van Adobe Experience Platform, september 2022
description: In de release van september 2022 staat een opmerking voor Adobe Experience Platform.
source-git-commit: 61b3799a4d8c8b6682babd85b6f50a7e69778553
workflow-type: tm+mt
source-wordcount: '2272'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 28 september 2022**

Nieuwe functies in Adobe Experience Platform:

- [Op kenmerken gebaseerd toegangsbeheer](#abac)
- [Gegevenshygiëne](#data-hygiene)
- [[!UICONTROL Privacy Console]](#privacy-console)

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [Controlelogboeken](#audit-logs)
- [Gegevensverzameling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
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

## Gegevenshygiëne {#data-hygiene}

Adobe Experience Platform biedt een robuuste set hulpmiddelen voor het beheer van grote, gecompliceerde gegevensbewerkingen om de ervaringen van de consument te kunnen indelen. Aangezien het gegeven in tijd in het systeem wordt opgenomen, wordt het steeds belangrijker om uw gegevensopslag te beheren zodat de gegevens zoals verwacht worden gebruikt, wordt bijgewerkt wanneer de onjuiste gegevens moeten verbeteren, en wordt geschrapt wanneer het organisatorische beleid het noodzakelijk acht.

Met de Adobe Experience Platform-mogelijkheden voor gegevenshygiëne kunt u uw gegevens opschonen door automatische gegevenssetvervaldatums te plannen en via programmacode consumentengegevens te verwijderen op basis van identiteit.

>[!NOTE]
>
>Consumentenverwijderingsmogelijkheden zijn alleen beschikbaar voor organisaties die Adobe Healthcare Shield of Privacy Shield hebben aangeschaft.

Raadpleeg de volgende documentatie om aan de slag te gaan met gegevenshygiëne:

- [Overzicht van gegevenshygiëne](../../hygiene/home.md): Leer de grondbeginselen van de mogelijkheden van de Platform van de gegevenshygiëne.
- [[!UICONTROL Data Hygiene] UI-hulplijn](../../hygiene/ui/overview.md): Leer hoe te om datasetvervaldatums te plannen en de consument schrapt verzoeken binnen het gebruikersinterface van de Platform.
- [Handleiding voor API voor gegevenshygiëne](../../hygiene/api/overview.md): Alle activiteiten van de gegevenshygiëne die u in UI kunt uitvoeren kunnen ook programmatically zijn

## [!UICONTROL Privacy Console] {#privacy-console}

De [!UICONTROL Privacy Console] in de interface van het Experience Platform biedt een dashboardweergave van belangrijke inzichten van privacygerelateerde functies, zoals [verzoeken van de betrokkene van Privacy Service], [gegevenshygiëne-werkorders], en [auditlogboeken]. De console biedt ook verschillende gebruiksaanwijzingen voor in-product toepassingen om u te helpen bij het doorlopen van gebruikelijke workflows voor privacy.

Zie de [Overzicht van de privacyconsole](../../landing/governance-privacy-security/privacy-console.md) voor meer informatie over de functie.

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Met AI/ML-services kunnen marketinganalisten en praktijkmensen gebruikmaken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen voor de klant. Dit staat voor marketing analisten toe om modellen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Attribution AI

Attribution AI wordt gebruikt om credits toe te wijzen aan aanraakpunten die leiden tot conversiegebeurtenissen. Dit kan door marketers worden gebruikt om het marketing effect van elk individueel marketing aanraakpunt over klantenreizen te kwantificeren.

| Functie | Beschrijving |
| --- | --- |
| Concept-instantie opslaan | Met deze nieuwe functie kunnen marketinganalisten de modelconfiguratie tijdens configuraties opslaan als een concept-instantie en het concept blijven bewerken tot de voltooiing is voltooid voordat ze training en scoring volgen. Scenario&#39;s waar deze eigenschap nuttig is omvatten, maar niet beperkt tot, wanneer de gebruikers veelvoudige gebieden in het configuratiewerkschema hebben te bepalen dat zij niet in één gaan kunnen voltooien of wanneer één of meerdere datasetstatistieken (zoals kolomvolledigheid) tijd om nemen te worden verwerkt alvorens zij beschikbaar worden. Lees de [Gebruikershandleiding voor Attribution AI](../../intelligent-services/attribution-ai/user-guide.md) voor meer informatie. |
| Beleid inzake governance | Nadat de gebruikers voorleggen om een geval door het configuratiewerkschema tot stand te brengen, controleert de nieuwe dienst van de beleidshandhaving of er om het even welke beleidsschendingen van gegevensgebruik zijn en toont de details in popover. Het zorgt ervoor dat de gegevensverrichtingen en de marketing acties met het beleid van het gegevensgebruik verenigbaar zijn dat op Adobe Experience Platform wordt gevormd. |

Voor meer informatie over Attribution AI, [Overzicht van Attribution AI](../../intelligent-services/attribution-ai/overview.md). Voor informatie over het beleid inzake gegevensbeheer, lees [beleidsoverzicht](../../data-governance/policies/overview.md).

### Customer AI

De in Real-time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren.

| Functie | Beschrijving |
| --- | --- |
| Concept-instantie opslaan | Met deze nieuwe functie kunnen marketinganalisten de modelconfiguratie tijdens configuraties opslaan als een concept-instantie en het concept blijven bewerken tot de voltooiing is voltooid voordat ze training en scoring volgen. Scenario&#39;s waar deze eigenschap nuttig is omvatten, maar niet beperkt tot, wanneer de gebruikers veelvoudige gebieden in het configuratiewerkschema hebben te bepalen dat zij niet in één gaan kunnen voltooien of wanneer één of meerdere datasetstatistieken (zoals kolomvolledigheid) tijd om nemen te worden verwerkt alvorens zij beschikbaar worden. Lees de [Handleiding voor AI-gebruikers van klant](../../intelligent-services/customer-ai/user-guide/configure.md) voor meer informatie. |
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

## Gegevensverzameling

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Integratie van linkernavigatie in de gebruikersinterface van het Platform | Alle mogelijkheden die eerder exclusief waren aan de UI van de Inzameling van Gegevens (met inbegrip van markeringen, gebeurtenis door:sturen, en gegevensstromen) zijn nu ook beschikbaar door de linkernavigatie in Experience Platform, onder de categorie **[!UICONTROL Data Collection]**. Dit elimineert de behoefte om tussen UIs te schakelen wanneer het werken met de mogelijkheden van de gegevensinzameling in Platform. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over gegevensverzameling in Platform raadpleegt u de [overzicht van gegevensverzameling](../../collection/home.md).

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

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Audience Manager segmentpopulatie impact op Real-time klantprofiel | De inname van grote populaties in het Audience Manager segment heeft een directe invloed op uw totale aantal profielen wanneer u eerst een segment van de Audience Manager naar het Platform verzendt gebruikend de bron van de Audience Manager. Dit betekent dat het selecteren van alle segmenten kan leiden tot een aantal profielen dat groter is dan uw gebruiksrechten voor licenties. Lees voor meer informatie de [Overzicht van bron Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Voor informatie over uw licentiegebruik leest u de documentatie op [het gebruiken van het dashboard van het vergunningsgebruik](../../dashboards/guides/license-usage.md). |
| Ondersteuning voor Adobe Campaign Managed Cloud Service | Met de Adobe Campaign Managed Cloud Service-bron kunt u uw Adobe Campaign v8.4-gegevens voor levering en bijhouden van logbestanden naar het Experience Platform brengen. Lees de handleiding op [een Adobe Campaign Managed Cloud Service-bronverbinding maken in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/campaign.md) voor meer informatie . |
| API-ondersteuning voor inname op aanvraag voor batchbronnen | Gebruik inname op aanvraag om een ad-hocflowrun voor een bepaalde gegevensstroom te maken met de [!DNL Flow Service] API. De gecreeerde looppas van de stroom moet aan éénmalige opname worden geplaatst. Lees voor meer informatie de handleiding op [een flow-run maken voor opname op aanvraag met behulp van de API](../../sources/tutorials/api/on-demand-ingestion.md) voor meer informatie . |
| API-ondersteuning voor het opnieuw proberen van mislukte gegevensstroombewerkingen voor batchbronnen | Gebruik de `re-trigger` bewerking om de mislukte gegevensstroom opnieuw uit te voeren via de API. Lees de handleiding op [opnieuw proberen, mislukte gegevensstroombewerkingen met de API](../../sources/tutorials/api/retry-flows.md) voor meer informatie . |
| API-ondersteuning voor het filteren van gegevens op rijniveau voor de [!DNL Google BigQuery] en [!DNL Snowflake] bronnen | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de [!DNL Google BigQuery] en [!DNL Snowflake] bronnen. Lees de handleiding over het filteren van gegevens voor een bron met behulp van de API voor meer informatie. |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).