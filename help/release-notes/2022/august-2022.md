---
title: Aanvullende informatie van augustus 2022 voor Adobe Experience Platform
description: Aanvullende informatie van augustus 2022 voor Adobe Experience Platform.
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1965'
ht-degree: 21%

---

# Aanvullende informatie voor Adobe Experience Platform

**Releasedatum: donderdag 24 augustus 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [Experience-datamodel (XDM)](#xdm)
- [Realtime-klantenprofiel](#profile)
- [Segmentatieservice](#segmentation)
- [Bronnen](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

Met AI/ML-services kunnen marketinganalisten en praktijkmensen gebruikmaken van de kracht van kunstmatige intelligentie en het leren van machines in gebruiksgevallen voor de klant. Dit staat voor marketing analisten toe om modellen op te zetten specifiek voor de behoeften van een bedrijf gebruikend zaken-vlakke configuraties zonder de behoefte aan de deskundigheid van de gegevenswetenschap.

### Attributie-AI

Attribution AI wordt gebruikt om credits toe te wijzen aan touchpoints die leiden tot conversiegebeurtenissen. Dit kan door marketeers worden gebruikt om de marketingimpact van elk individueel marketing-touchpoint in journeys van de klant te kwantificeren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor privacy | <ul><li> AI van de attributie steunt nu het bepalen van gebruikersrollen en toegangsbeleid om [ toestemmingen ](../../../help/access-control/abac/ui/permissions.md) voor eigenschappen en voorwerpen binnen een producttoepassing te beheren. </li><li>De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt.</li><li> Door [ op attribuut-gebaseerde toegangscontrole ](../../access-control/abac/overview.md), kunnen de beheerders toegang tot specifieke voorwerpen en/of mogelijkheden controleren die op bepaalde attributen worden gebaseerd, die meta-gegevens aan een voorwerp kunnen worden toegevoegd, zoals labels.Beheerders kunnen gebruikersrollen ook bepalen die toegang tot slechts specifieke gebieden en gegevens hebben die aan die gebieden beantwoorden.</li><li>Attribution AI gebruikt Experience Platform datasets. Ter ondersteuning van consumentenrechtenaanvragen die een merk kan ontvangen, dienen merken Experience Platform Privacy Service te gebruiken om verzoeken van consumenten om toegang in te dienen en te verwijderen om hun gegevens over het datumpeer, de Identity Service en het Real-Time Klantprofiel te verwijderen.  </li><li>Alle gegevenssets die voor invoer/uitvoer van modellen worden gebruikt, volgen de Experience Platform-richtlijnen. Experience Platform Data Encryption is van toepassing op gegevens in rust en in doorvoer. Zie de documentatie om meer over [ gegevensencryptie ](../../../help/landing/governance-privacy-security/encryption.md) te leren.</li></ul> |

{style="table-layout:auto"}

**Nota**: De attributie AI zal niet met bestaande klanten van het Schild van de Gezondheidszorg tot verdere kennisgeving beschikbaar zijn.

Voor meer informatie over Attributie AI, zie gelieve [ AI van de Attributie ](../../intelligent-services/attribution-ai/overview.md) overzicht.

### Customer AI

De in Real-Time Customer Data Platform beschikbare AI van de klant wordt gebruikt om aangepaste eigenschapscores zoals kurn en conversie voor individuele profielen op schaal te produceren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor privacy | <ul><li> Klant AI steunt nu het bepalen van gebruikersrollen en toegangsbeleid om [ toestemmingen ](../../../help/access-control/abac/ui/permissions.md) voor eigenschappen en voorwerpen binnen een producttoepassing te beheren. </li><li>De middelen van het logboek van de controle worden geregistreerd automatisch aangezien de activiteit voorkomt.</li><li> Door [ op attribuut-gebaseerde toegangscontrole ](../../access-control/abac/overview.md), kunnen de beheerders toegang tot specifieke voorwerpen en/of mogelijkheden controleren die op bepaalde attributen worden gebaseerd. Deze kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals labels. Beheerders kunnen ook gebruikersrollen definiëren die alleen toegang hebben tot specifieke velden en gegevens die overeenkomen met die velden.</li><li>Klant-AI maakt gebruik van Experience Platform-gegevenssets. Ter ondersteuning van consumentenrechtenaanvragen die een merk kan ontvangen, dienen merken Experience Platform Privacy Service te gebruiken om verzoeken van consumenten om toegang in te dienen en te verwijderen om hun gegevens over het datumpeer, de Identity Service en het Real-Time Klantprofiel te verwijderen. </li><li>Alle gegevenssets die voor invoer/uitvoer van modellen worden gebruikt, volgen de Experience Platform-richtlijnen. Experience Platform Data Encryption is van toepassing op gegevens in rust en in doorvoer. Zie de documentatie om meer over [ gegevensencryptie ](../../../help/landing/governance-privacy-security/encryption.md) te leren.</li></ul> |

{style="table-layout:auto"}

**Nota**: De Klant AI zal niet met bestaande klanten van het Schild van de Gezondheidszorg tot verdere kennisgeving beschikbaar zijn.

Voor meer informatie over Klant AI, gelieve te zien [ AI van de Klant ](../../intelligent-services/customer-ai/overview.md) overzicht.

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform biedt meerdere [!DNL dashboards] waarmee u belangrijke inzichten in de gegevens van uw organisatie kunt bekijken, zoals die tijdens dagelijkse momentopnamen zijn vastgelegd.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Geplande activeringswidget | De widget [!UICONTROL Scheduled activations] biedt een in tabelvorm weergegeven weergave van de laatst geactiveerde doelen. Voor elk segment bevat dit de naam, het doelplatform en de begin- en einddatum van de activering. Met deze widget kunt u in één oogopslag zien waar en wanneer het publiek wordt geactiveerd en kunt u dubbele of overbodige activeringen transparanter maken. Deze geaccumuleerde informatie benadrukt ook waar om het even welke activiteiten zijn weggelaten. |

Voor meer informatie over [!DNL Dashboards] raadpleegt u het [[!DNL Dashboards] overzicht](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om gegevens in kaart te brengen, om te zetten en te bevestigen aan en van het Model van de Gegevens van de Ervaring (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het opnemen van records met waarschuwingen | Met Data Prep worden nu waarschuwingen (niet-kritieke fouten) gelokaliseerd voor de velden en kan de rest van de rij worden ingevoegd. Alle maptransformatiefouten worden nu gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingeslikt, worden als geslaagd beschouwd, met een waarschuwing.  De bewaking wordt ook ondersteund in registers met waarschuwingen en diagnostische details. Gedeeltelijke invoer van records met waarschuwingen is momenteel alleen beschikbaar voor streaming gegevens. Herzie de documentatie over [ het opnemen verslagen met waarschuwingen ](../../sources/tutorials/ui/monitor-streaming.md) voor meer informatie. |

{style="table-layout:auto"}

Meer over [!DNL Data Prep] leren, zie het [[!DNL Data Prep]  overzicht ](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] zijn pre-built integraties met bestemmingsplatforms die de naadloze activering van gegevens van Adobe Experience Platform mogelijk maken. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens te activeren voor cross-channel marketingcampagnes, e-mailcampagnes, gerichte advertenties en vele andere gebruiksscenario&#39;s.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| ----------- | ----------- |
| (Beta) Op kenmerken gebaseerde ondersteuning voor personalisatie voor verpersoonlijkingsdoelen | Met de bètaversie van op attribuut-gebaseerde verpersoonlijking, zult u twee nieuwe kaarten in de [ bestemmingscatalogus ](../../destinations/catalog/overview.md) zien: <ul><li>**[!UICONTROL Adobe Target V2]**: Deze connector bevindt zich momenteel in bèta en is alleen beschikbaar voor een beperkt aantal klanten. Naast de functionaliteit die door de kaart van Adobe Target V1 wordt verstrekt, voegt de schakelaar van het Doel V2 a [ kaartstap ](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes) aan het activeringswerkschema toe, dat u toestaat om profielattributen aan Adobe Target in kaart te brengen, toelatend op attribuut-gebaseerde zelfde-pagina en volgende-pagina verpersoonlijking.</li><li>**[!UICONTROL Custom Personalization With Attributes]**: Deze connector bevindt zich momenteel in bèta en is alleen beschikbaar voor een beperkt aantal klanten. Naast de functionaliteit die door **[!UICONTROL Custom Personalization]** wordt verstrekt, voegt de **[!UICONTROL Custom Personalization With Attributes]** schakelaar een facultatieve [ toewijzingsstap ](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes) aan het activeringswerkschema toe, dat u toestaat om profielattributen aan uw douaneverpersoonlijkingsbestemming in kaart te brengen, toelatend op attribuut-gebaseerde zelfde-pagina en volgende-pagina verpersoonlijking.</li></ul> <br> Profielkenmerken kunnen vertrouwelijke gegevens bevatten. Om dit gegeven te beschermen, vereist de **[!UICONTROL Custom Personalization With Attributes]** bestemming u om de [ Server API van Edge Network ](../../server-api/overview.md) voor gegevensinzameling te gebruiken. Voorts moeten alle Server API vraag in een [ voor authentiek verklaarde context ](../../server-api/authentication.md) worden gemaakt. |

{style="table-layout:auto"}

**Nieuwe bestemmingen**

| Bestemming | Beschrijving |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach] ](https://www.outreach.io/) is een Experience Platform van de Uitvoering van de Verkoop met de meeste B2B koper-verkoper interactiegegevens in de wereld en significante investeringen in merkgebonden AI technologieën om verkoopgegevens in intelligentie te vertalen. [!DNL Outreach] helpt organisaties om hun verkoopbetrokkenheid te automatiseren en om hun efficiëntie, voorspelbaarheid en groei te verbeteren. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen, raadpleegt u het [overzicht van bestemmingen](../../destinations/home.md).

## Experience-datamodel (XDM) {#xdm}

XDM is een open-bronspecificatie die algemene structuren en definities (schema&#39;s) biedt voor gegevens die in Adobe Experience Platform worden geïmporteerd. Door de XDM-standaarden te hanteren, kunnen alle gegevens over de klantervaring worden opgenomen in een gemeenschappelijke weergave. Zo worden inzichten sneller en beter geïntegreerd verkregen. U kunt waardevolle inzichten verkrijgen uit klantacties, klantdoelgroepen definiëren via segmenten en klantkenmerken gebruiken voor personalisatiedoeleinden.

**Nieuwe componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Klasse | [[!UICONTROL AJO Entity Class]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | Een op record gebaseerde klasse voor het maken van opzoekschema&#39;s voor Adobe Journey Optimizer. |
| Veldgroep | [[!UICONTROL Workfront Work Objects]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | Een omvattende veldgroep die verwijst naar alle objectspecifieke veldgroepen op een lager niveau voor Adobe Workfront. |

{style="table-layout:auto"}

**Bijgewerkte componenten XDM**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | [[!UICONTROL Journey Orchestration Step Event Common Fields]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | Er zijn twee nieuwe eigenschappen toegevoegd: `origTimeStamp` en `experienceID` . |
| Veldgroep | [[!UICONTROL Segment Membership Details]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | Naast [!UICONTROL XDM Individual Profile] kan deze veldgroep nu ook worden gebruikt in schema&#39;s die zijn gebaseerd op de XDM Business Account-klasse. |
| Veldgroep | (Meerdere) | Verschillende veldgroepen met betrekking tot de B2B-activiteiten van Marketo zijn bijgewerkt naar een stabiele status. Zie het volgende [ trekkingsverzoek ](https://github.com/adobe/xdm/pull/1593/files) voor details. |
| Veldgroep | (Meerdere) | Verschillende veldgroepen met betrekking tot het weer zijn bijgewerkt om fouten te corrigeren die voorkwamen voor `uvIndex` en `sunsetTime` . Zie het volgende [ trekkingsverzoek ](https://github.com/adobe/xdm/pull/1602/files) voor details. |
| Gegevenstype | [[!UICONTROL Product list item]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | Er is een nieuwe eigenschap `productImageUrl` toegevoegd. |
| Gegevenstype | [[!UICONTROL Qoe Data details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | Er is een nieuwe eigenschap `framesPerSecond` toegevoegd. |
| Gegevenstype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | De naam van `sdkVersion` is gewijzigd in `appVersion` . `meta:enum` en `description` velden zijn ook bijgewerkt. |
| Gegevenstypen en veldgroepen | (Meerdere) | Verschillende mediatypen en veldgroepen hebben nieuwe velden en bijgewerkte beschrijvingen. Zie het volgende [ trekkingsverzoek ](https://github.com/adobe/xdm/pull/1582/files) voor details. |
| (Alle) | (Meerdere) | Alle schemaobjecten die een `enum` -veld bevatten, bevatten nu ook een bijbehorend `meta:enum` -veld om de weergavewaarden voor elke restrictie aan te geven. Zie het volgende [ trekkingsverzoek ](https://github.com/adobe/xdm/pull/1601/files) voor details. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Experience Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Realtime-klantenprofiel {#profile}

Met Adobe Experience Platform kunt u uw klanten gecoördineerde, consistente en relevante ervaringen bieden, ongeacht waar of wanneer ze met uw merk in aanraking komen. Met Real-Time Customer Profile krijgt u een holistisch beeld van elke individuele klant, waarbij gegevens uit meerdere kanalen worden gecombineerd, waaronder online, offline, CRM en gegevens van derden. Met Profile kunt u klantgegevens samenvoegen tot één overzichtelijk overzicht, dat een bruikbaar overzicht met tijdstempel biedt van elke klantinteractie.

| Functie | Beschrijving |
| ------- | ----------- |
| Harde limiet voor beleid samenvoegen | Experience Platform zal nu een harde grens van **vijf** fusiebeleid per zandbak afdwingen. Als uw zandbak momenteel meer dan vijf fusiebeleid heeft, zult u **** geen nieuw fusiebeleid kunnen tot stand brengen tot de zandbak minder dan vijf fusiebeleid heeft. |
| Opschonen van kenmerken van rand met zwevend profiel | Voor alle organisaties, verwijdert de Dienst van het Profiel nu randattributen van gebruikersactiviteitengebied op een dagelijkse basis om een nauwkeurigere vertegenwoordiging van uw profielen in uw systeem te geven. Deze opruiming vindt plaats nadat alle profielfragmenten voor een bepaald profiel zijn verwijderd en heeft invloed op profielen die worden samengevoegd uit gegevenssets waarin `com_adobe_aep_profile_region_dataset` is gemarkeerd als `true` . Dit kan een daling in &quot;Adressable publiek&quot;metrisch in het dashboard van het vergunningsgebruik tonen en kan een daling in &quot;Aantal van het Profiel&quot;metrisch in het dashboard van het Profiel tonen, aangezien deze metriek de fragmenten van het de randattribuut van het leftover voorafgaand aan deze versie omvatte. |

{style="table-layout:auto"}

Meer over het Profiel van de Klant in real time, met inbegrip van leerprogramma&#39;s en beste praktijken voor het werken met profielgegevens leren, gelieve te beginnen door het [ overzicht van het Profiel van de Klant in real time ](../../profile/home.md) te lezen.

## Segmentatieservice {#segmentation}

[!DNL Segmentation Service] definieert een specifieke subset van profielen door de criteria te beschrijven die een groep personen aan wie marketing kan worden aangeboden binnen uw klantenbestand onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Ondersteuning voor 4000 segmenten | Alle organisaties met Experience Platform kunnen nu tot 4000 segmentdefinities steunen. Voor meer informatie over hoe deze verandering de segmentbaan APIs beïnvloedt, te lezen gelieve de [ gids van het eindpunt van de segmentbaan ](../../segmentation/api/segment-jobs.md) |

Voor meer informatie over [!DNL Segmentation Service], raadpleegt u het [overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van Experience Platform-services. U kunt gegevens opnemen uit verschillende bronnen, zoals Adobe-toepassingen, cloudopslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve gebruikersinterface waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Met deze bronverbindingen kunt u externe opslagsystemen en CRM-services verifiëren en er verbinding mee maken, tijden voor opnameruns instellen en de doorvoer van gegevensopname beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Algemene beschikbaarheid van Self-Serve Bronnen (Batch SDK) | Ontwikkel, test, en integreer uw REST API-gebaseerde gegevensbron om partijgegevens in Experience Platform in te voeren gebruikend gemakkelijk om bronspecificaties te vormen. Met Bronnen SDK kunt u: <ul><li>Een nieuwe bron voor de Experience Platform-catalogus configureren.</li><li>Bepaal specificaties voor uw bron, met inbegrip van informatie betreffende gesteunde authentificatietypen, het plannen, en hoe de middelgegevens worden gehaald.</li><li>Maak gebruikersgerichte documentatie voor uw nieuwe bron.</li></ul> Voor meer informatie, lees de documentatie over [ Zelfbediening Bronnen (Partij SDK) ](../../sources/sources-sdk/overview.md). |
| Algemene beschikbaarheid van de [!DNL Google BigQuery]-bron | Gebruik de [!DNL Google BigQuery] -bron om gegevens van uw [!DNL Google BigQuery] -gegevenspakhuis in te voeren naar Experience Platform. Voor meer informatie, lees de documentatie over de [[!DNL Google BigQuery]  bron ](../../sources/connectors/databases/bigquery.md). |
| [!DNL Teradata Vantage] source (Beta) | Gebruik de [!DNL Teradata Vantage] -bron om gegevens van hybride multi-cloud omgevingen in te voeren naar Experience Platform. Voor meer informatie, lees de documentatie over de [[!DNL Teradata Vantage]  bron ](../../sources/connectors/databases/teradata-vantage.md). |
| Ondersteuning voor verschillende regio&#39;s van Adobe Analytics-bronnen | U kunt nu rapportsuites uit om het even welke regio (Verenigde Staten, Verenigd Koninkrijk, of Singapore) opnemen. Rapportsuites moeten worden toegewezen aan dezelfde organisatie als de Experience Platform Sandbox-instantie waarin de bronverbinding wordt gemaakt. Voor meer informatie, lees de gids bij [ het creëren van een Adobe Analytics bronverbinding in UI ](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style="table-layout:auto"}

Meer over bronnen leren, zie het [ overzicht van bronnen ](../../sources/home.md).
