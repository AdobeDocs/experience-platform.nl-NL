---
title: Adobe Experience Platform Release Notes April 2024
description: In de release van april 2024 staat een opmerking voor Adobe Experience Platform.
source-git-commit: 6ad7d55ca0a544879db9738c0a4ab914fdc363bd
workflow-type: tm+mt
source-wordcount: '1728'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: woensdag 30 april 2024**

>[!TIP]
>
>Gebruik de [Adobe Experience Platform glossary](/help/landing/glossary.md) om vertrouwd te raken met de terminologie die in Real-time Customer Data Platform en Adobe Experience Platform wordt gebruikt. Als u een bepaalde term die u zoekt niet kunt vinden, gebruikt u de feedbackopties op de pagina om te vragen dat nieuwe termen aan de verklarende woordenlijst worden toegevoegd.

Updates voor bestaande functies in Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Identiteitsservice](#identity-service)
- [Bewaking](#monitoring)
- [Query-service](#query-service)
- [Sandboxes](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Real-time Customer Data Platform B2B-inzichten | Bekijk vooraf geconfigureerde Real-Time CDP B2B-gegevensinzichten van accounts en mogelijkheden om u te helpen uw gegevens te begrijpen en uw bedrijfsbeslissingen te informeren. U kunt ook uw eigen inzichten maken met het Real-Time CDP B2B-gegevensmodel om uw gegevens te visualiseren en te verkennen en uw aangepaste visualisaties in het dashboard op te slaan. |

{style=“table-layout:auto”}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Edge Network van het Experience Platform kunt verzenden waar het kan worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Inzichten | [!DNL Acxiom] Anoniem bezoekersvenster | Ontdek waar uw websitebezoekers vandaan komen [!DNL Acxiom's] Bezoekersinzichten. Door geo IP raadplegingstechnologie te gebruiken, wijzen wij de plaats van anonieme browsers aan. Zodra geïdentificeerd, geeft een snel onderzoek in onze georganiseerde gegevensbestand extra inzichten die naar browser worden teruggestuurd. Voor makers van inhoud betekent dit een gouden kans om hun inhoud af te stemmen op deze datapunten en bezoekers een meer persoonlijke en boeiende ervaring te bieden, ook al begonnen ze als vreemden. |
| Gegevensstromen | [detectie van Edge Network bot](../../datastreams/bot-detection.md) | Verkeer afkomstig van niet-menselijke entiteiten, zoals geautomatiseerde programma&#39;s, webschrapers, spinnen, scanners met scripts, kan het moeilijker maken om gebeurtenissen die plaatsvinden bij bezoekers van het menselijk publiek te identificeren. Dit type van verkeer kan belangrijke bedrijfsmetriek negatief beïnvloeden, die tot onjuist verkeer leiden meldend. <br>Met beide detectie kunt u gebeurtenissen identificeren die door de [Web SDK](../../web-sdk/home.md), [Mobile SDK](https://developer.adobe.com/client-sdks/home/) en [[!DNL Server API]](../../server-api/overview.md) als gegenereerd door bekende spinnen en bots. Door beide detectie voor uw gegevensstromen te configureren, kunt u specifieke IP-adressen, IP-bereiken en aanvraagheaders identificeren die u als beide gebeurtenissen wilt classificeren. <br> De identificatie van beide verkeer kan u een nauwkeurigere meting van gebruikersactiviteit op uw plaats of mobiele toepassing verstrekken. |
| Mobiele SDK | Primaire release | Nieuwe grote versies van de Mobile SDK zijn uitgebracht voor de volgende platforms: iOS Mobile Core 5.x en compatibele iOS-extensies, Android Mobile Core 3.x en compatibele Android-extensies, React Native Core 6.x en compatibele React Native-extensies, Flutter Core 4.x en compatibele Flutter-extensies. Deze release biedt verschillende nieuwe functies en verbeteringen, waaronder ondersteuning in de Android SDK voor Jetpack Compose, ondersteuning voor op Adobe Journey Optimizer gebaseerde ervaringen en algemene beschikbaarheid van de Adobe Journey Optimizer Messaging-extensie voor Flutter. Zie voor meer gedetailleerde opmerkingen bij de release [Opmerkingen bij de release van Mobile SDK](https://developer.adobe.com/client-sdks/home/release-notes/). |
| Mobiele SDK | Privacy | Vanwege de beleidsupdate van Apple, die op 1 mei 2024 begint, moeten ontwikkelaars nieuwe privacyfuncties implementeren om zich bij de App Store in te dienen. Alle klanten van de Adobe die de Mobile SDK gebruiken, moeten een upgrade uitvoeren naar versie 5.x van de SDK als ze na 1 mei App Store-goedkeuring willen ontvangen. |
| Roku SDK | Roku SDK | De eerste grote versie van de Roku SDK is vrijgegeven met ondersteuning voor de Streaming Media voor de Platform Edge Network. |
| Tags en doorsturen van gebeurtenissen | Richtlijnen voor producten | Experience Platform [Tags](../../tags/home.md) en [Gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) bieden een nieuwe reeks ervaringen die u kunnen helpen snel aan de slag te gaan en een snelle prijs-kwaliteitstijd te realiseren. Deze ervaringen omvatten nieuwe instapschermen, zelfstudies in producten en knopinfo. <br>![Gebeurtenis doorsturen met de aanwijzingen voor in-product gemarkeerd.](../2024/assets/april/event-forwarding.png "De Schema-editor met de velden Type- en Kaartwaardetype gemarkeerd."){width="100" zoomable="yes"}<br> |
| Web SDK | Vereenvoudigde toepassing van SDK van het Web voor klanten van de Audience Manager | De veelvoudige updates van SDK van het Web vereenvoudigen nu goedkeuring van Web SDK zonder het Model van de Gegevens van de Ervaring (XDM) voor de Oplossingen van het Experience Cloud, zoals Audience Manager, Analytics en Doel te gebruiken. Meer over de goedkeuring van SDK van het Web van de Audience Manager van de volgende gidsen: <ul><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/dil-extension-to-web-sdk">Werk uw bibliotheek van de gegevensinzameling voor Audience Manager van de de markeringsuitbreiding van de Audience Manager aan de de markeringsuitbreiding van SDK van het Web bij</li><li><a href="https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/migrate-to-web-sdk/appmeasurement-to-web-sdk">Werk uw bibliotheek van de gegevensinzameling voor Audience Manager van de bibliotheek van AppMeasurement JavaScript aan de bibliotheek van SDK JavaScript van het Web bij</li></ul> |

{style="table-layout:auto"}

<!--| Web SDK | [Streaming Media Collection support in Web SDK](../../web-sdk/commands/configure/streamingmedia.md) | You can now use Experience Platform Web SDK to collect data related to media sessions on your website. The collected data can include information about media playbacks, pauses, completions, and other related events. Once collected, you can send this data to Adobe Experience Platform and/or Adobe Analytics, to generate reports. This feature provides a comprehensive solution for tracking and understanding media consumption behavior on your website. <br>See the [Web SDK](../../web-sdk/commands/configure/streamingmedia.md) documentation to learn how to configure the `streamingMedia` component. <br>See the guide on [migrating your Analytics for Streaming Media implementation from Media JS to Web SDK](https://experienceleague.adobe.com/en/docs/media-analytics/using/implementation/edge-recommended/media-edge-sdk/edge-web-sdk) for more details.|-->

Voor meer informatie over gegevensverzamelingen leest u de [overzicht van gegevensverzameling](../../collection/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| `isRequired` parameter nu beschikbaar voor geneste gegevensvelden van klanten in Destination SDK | Wanneer het vormen van een bestemming in Destination SDK, kunt u nu [geneste gegevensvelden voor klanten instellen als dat vereist is](/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md#nested-fields). Op deze manier kunnen gebruikers die uw bestemming instellen, pas verdergaan met hun activeringsstroom als ze een waarde voor dat veld selecteren. |

{style="table-layout:auto"}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

<!--| [!BADGE Beta]{type=Informative} Remove multiple audiences and datasets from activation flows | You can now select and remove multiple audiences and datasets from destination activation flows. See the [destination details](../../destinations/ui/destination-details-page.md#bulk-remove) and [dataset export](../../destinations/ui/export-datasets.md) documentation for more details. |-->

## Identiteitsservice {#identity-service}

Gebruik Adobe Experience Platform Identity Service om een uitgebreide weergave van uw klanten en hun gedrag te maken door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Verdringing van de `/orgs/{ORG}/` eindpunten in de API | De volgende eindpunten in de [[!DNL Identity Service] API](https://developer.adobe.com/experience-platform-apis/references/identity-service/) zijn afgekeurd:<ul><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities`</li><li>`https://platform.adobe.io/data/core/idnamespace/orgs/{ORG}/identities/{ID}`</li></ul> U kunt de `/idnamespace/identities` en de `/idnamespace/identities/{ID}` eindpunten om de zelfde taken te verwezenlijken en of alle namespaces in een organisatie, of een specifieke namespace in een organisatie terug te winnen. |

{style="table-layout:auto"}

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md).

## Bewaking {#monitoring}

Gebruik het controledashboard in de UI van het Experience Platform om de reis van uw gegevens van Bronnen, de Dienst van de Identiteit, het Profiel van de Klant in real time, Soorten, en Doelen te controleren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Uitbreiding van dashboard controleren | U kunt nu het controledashboard voor verschillende gegevenstypes gebruiken die op uw bedrijfs gebruikscase worden gebaseerd. Gebruik het controledashboard om persoon, rekening, en de activiteiten van het vooruitgangsgegevenstype in bronnen, publiek, en bestemmingen te controleren. |

{style="table-layout:auto"}

Lees voor meer informatie de handleiding op [het gebruiken van het controledashboard](../../dataflows/ui/monitor.md).

## Query-service {#query-service}

Met Query Service kunt u standaard-SQL gebruiken om gegevens in Adobe Experience Platform op te vragen [!DNL Data Lake]. U kunt zich bij om het even welke datasets van aansluiten [!DNL Data Lake] en leg de vraagresultaten als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time vast.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Query Quarantine | Sluit mislukte query-uitvoeringen automatisch af om onderbrekingen te voorkomen en consistente prestaties te behouden. |
| Query annuleren | Neem controle van vraaguitvoering en verbeter uw productiviteit door langdurige vragen te annuleren. |
| Geplande querywaarschuwingen | Blijf op de hoogte van proactieve meldingen tijdens het plannen van query&#39;s, zodat u over een efficiënt en tijdig taakbeheer beschikt. U kunt aan alarm of intekenen wanneer het creëren van een vraag of het gebruiken van de gealigneerde acties voor bestaande geplande vragen. |
| Verbeterde geplande querynavigatie | Navigeer gemakkelijk tussen vraagmalplaatjes en geplande looppas voor verhoogde productiviteit. |
| Uitgebreide query-uitvoer | Toegang tot tot maximaal 500 rijen vraagresultaten binnen de console voor diepere analyse van uw gegevens. |
| Oudere versie van Query Editor | Vanaf 30-april-2024 is de Verbeterde Redacteur van de Vraag de standaardeditor voor alle gebruikers geworden. De erfenisredacteur zal op 30-mei-2024 worden afgekeurd en niet meer voor gebruik beschikbaar zijn. |

{style=“table-layout:auto”}

Raadpleeg voor meer informatie over Query Services de [Overzicht van Query Service](../../query-service/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [Gereedschap Sandbox](../../sandboxes/ui/sandbox-tooling.md) | Gereedschap sandbox gebruiken voor [export](../../sandboxes/ui/sandbox-tooling.md#export-entire-sandbox) alle ondersteunde objecttypen in een volledig sandboxpakket, en vervolgens [import](../../sandboxes/ui/sandbox-tooling.md#import-entire-sandbox) het pakket in verschillende sandboxen om objectconfiguraties te repliceren. |

{style="table-layout:auto"}

Voor meer informatie over sandboxen leest u de [sandboxen, overzicht](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Bijgewerkte functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Status van levenscyclus van het publiek | De levenscyclusstaten van de doelgroep zijn gestroomlijnd om het levenscyclusbeheer te vereenvoudigen. Voor meer informatie over deze levenscyclusstaten leest u de [Veelgestelde vragen over segmentatieservice](../../segmentation/faq.md#lifecycle-states). |

{style="table-layout:auto"}

Voor meer informatie over [!DNL Segmentation Service], zie de [Overzicht van segmentatie](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

Gebruik bronnen in Experience Platform om gegevens van een Adobe of een gegevensbron van derden in te voeren.

**Nieuwe bronnen**

| Nieuwe bronnen | Beschrijving |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL PathFactory] | Gebruik de [[!DNL PathFactory] bron](../../sources/tutorials/ui/create/marketing-automation/pathfactory.md) om de gegevens van uw bezoeker, sessie en paginaweergave te integreren vanuit [!DNL PathFactory] naar Experience Platform. Lees de [[!DNL PathFactory] overzicht](../../sources/connectors/marketing-automation/pathfactory.md) voor informatie over hoe te beginnen. |
| [!DNL Teradata Vantage] | Gebruik de [[!DNL Teradata Vantage] bron](../../sources/tutorials/ui/create/databases/teradata-vantage.md) om gegevens van hybride multi-wolkmilieu&#39;s aan Experience Platform in te voeren. Lees de [[!DNL Teradata Vantage] overzicht](../../sources/connectors/databases/teradata-vantage.md) voor informatie over hoe te beginnen. |

{style="table-layout:auto"}

**Nieuwe en bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates voor IP-adressen voor het toestaan van lijsten in VA7 | De volgende IP adressen zijn toegevoegd aan de lijst van IP adressen om aan uw lijst van gewenste personen voor VA7 (Noord-Amerika) toe te voegen: <ul><li>`20.98.198.224/29`</li><li>`20.119.28.57/32`</li><li>`20.232.89.104/29`</li><li>`20.98.195.172/32`</li><li>`172.210.218.144/28`</li></ul> Voor een uitvoerige lijst van IP adressen om aan uw lijst van gewenste personen toe te voegen, lees [IP Document van de lijst van gewenste personen van het Adres](../../sources/ip-address-allow-list.md). |
| Ondersteuning voor nieuwe verificatietypen met de [!DNL Azure Event Hubs] bron | U kunt nu verbinding maken met uw [!DNL Event Hubs] bron naar Experience Platform met behulp van [!DNL Azure Active Directory Authentication] of [!DNL Scoped Azure Active Directory Authentication]. Lees de handleiding op [verbinden [!DNL Event Hubs] naar Experience Platform](../../sources/tutorials/ui/create/cloud-storage/eventhub.md) voor meer informatie . |
| Updates voor [!DNL Data Landing Zone] terugwinning van referenties | U kunt nu de juiste rail in de bronwerkruimte gebruiken om uw [!DNL Data Landing Zone] referenties. U kunt nu ook de juiste rail gebruiken om uw referenties te vernieuwen. Lees de [[!DNL Data Landing Zone] UI-hulplijn](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) voor meer informatie . |

{style="table-layout:auto"}

<!--| Enhanced filtering and navigation in the sources UI workspace | Use the enhanced filtering, search, and inline action tools in the sources UI workspace to streamline your workflow. <ul><li>Use filtering and search capabilities to navigate your way through sources accounts and dataflows in your organization.</li><li>Use inline actions to modify configuration settings applied to your dataflows and improve organizational workflows. You can use inline actions to apply tags, set up alerts, or create ingestion jobs on demand.</li></ul> For more information, read the guide on [filtering sources objects in the UI](../../sources/tutorials/ui/filter.md).|-->

Lees voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
