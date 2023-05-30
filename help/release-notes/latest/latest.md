---
title: Aanvullende informatie over Adobe Experience Platform
description: In de releaseopmerkingen van mei 2023 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: c2b9f01453ecbc3348675e59b75c81280eded5f8
workflow-type: tm+mt
source-wordcount: '1541'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

>[!IMPORTANT]
>
>Ter voorbereiding op de algemene beschikbaarheid van de Poortfunctie Publiek werkt Adobe Experience Platform het gebruik van &quot;publiek&quot; en &quot;segment&quot; binnen het systeem en de documentatie bij.
>
>- **Publiek**: Een reeks personen, accounts, huishoudens of andere entiteiten die gemeenschappelijke kenmerken en gedragingen delen.
>
>- **Segmentdefinitie**: In Adobe Experience Platform, de regels die worden gebruikt om zeer belangrijke eigenschappen of gedrag van een doelpubliek te beschrijven. Deze term werd voorheen &quot;segment&quot; genoemd.
>
>- **Segment**: Het scheiden van profielen in publiek. De term &quot;segment&quot; wordt nu uitsluitend als werkwoord gebruikt.
>
>- **Segmentering**: De handeling waarbij de kenmerken van de profielen die worden gegroepeerd, worden geïdentificeerd en gespecificeerd om een reeks resultaten te produceren, zoals een publiek.
>
>Dientengevolge, binnen Adobe Experience Platform UI, zult u &quot;Segmenten&quot;vervangen door &quot;Publiek&quot;zien om deze nieuwe weg van publieksverwezenlijking en beheer te weerspiegelen.

**Releasedatum: 24 mei 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Gegevensbeheer](#data-governance)
- [Gegevensopname](#data-ingestion)
- [Doelen](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Identiteitsservice](#identity-service)
- [Query-service](#query-service)
- [Bronnen](#sources)


## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL Twitter] conversie-API-extensie | De [[!DNL Twitter] Conversies-API](../../tags/extensions/server/twitter/overview.md) De gebeurtenis die uitbreiding door:sturen staat u toe om de server-kant van gebeurtenisgegevens, in real time, voor gebeurtenisomzettingen door:sturen die [!DNL Twitter] Conversies-API. |
| Padassistentie voor gegevenselement | Het pad voor het gegevenselement in de [Kernextensie](../../tags/extensions/client/core/overview.md) is nu gemakkelijker dan ooit. Deze uitbreiding biedt een formulier met instructies waarmee u het juiste pad voor gegevenselementen kunt selecteren en opmaken. |

{style="table-layout:auto"}

Voor meer informatie over gegevensverzamelingen leest u de [overzicht van gegevensverzamelingen](../../tags/home.md).

## Gegevensbeheer {#data-governance}

Adobe Experience Platform Data Governance is een reeks strategieën en technologieën die worden gebruikt om klantgegevens te beheren en naleving van regelgeving, beperkingen en beleidsregels die van toepassing zijn op gegevensgebruik te waarborgen. Het speelt een sleutelrol binnen Experience Platform op diverse niveaus, met inbegrip van catalogiseren, gegevenslijn, het etiketteren van het gegevensgebruik, het beleid van de gegevenstoegang, en toegangscontrole over gegevens voor marketing acties.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Afbeelding van labels op datumveldniveau | De mogelijkheid om labels toe te passen op afzonderlijke velden is verplaatst van datasets naar schema&#39;s. Hierdoor kunt u het beheer van veldlabels stroomopwaarts centraliseren voor gegevensbeheer, toestemming en toegangsbeheer. Eerder toegepaste labels voor gegevenssetvelden worden tijdelijk ondersteund via de gebruikersinterface van het Experience Platform. Om het even welke bestaande etiketten van het datasetgebied moeten manueel aan de etiketten van het schemagebied door u tegen 31 Mei worden gemigreerd, 2024. Lees de [end-to-end handleiding voor gegevensbeheer](../../data-governance/e2e.md) voor meer informatie over labelmigratie. |

{style="table-layout:auto"}

Lees voor meer informatie over gegevensbeheer de [gegevensbeheer - overzicht](../../data-governance/home.md).

## Gegevensopname {#data-ingestion}

Adobe Experience Platform biedt een uitgebreide reeks functies voor het invoeren van elk type en elke vertraging van gegevens. U kunt opnemen met de API&#39;s Batch of Streaming via Adobe-bronnen, partners voor gegevensintegratie of de interface van Adobe Experience Platform.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Beta beschikbaarheid van gegevensinnamesjablonen | De malplaatjes van de opname van gegevens verstrekken gegevensarchitecten en ingenieurs van standaardmalplaatjes en automatiseringshulpmiddelen om het proces van gegevensopname, met inbegrip van schema en dataset verwezenlijking en de configuratie van kaartregels te versnellen. Sjablonen voor gegevensinvoer zijn momenteel beschikbaar voor de [[!DNL Marketo Engage]](../../sources/connectors/adobe-applications/marketo/marketo.md), [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) en [[!DNL Microsoft Dynamics]](../../sources/connectors/crm/ms-dynamics.md) bronnen. Lees voor meer informatie de handleiding op [het gebruiken van malplaatjes in UI](../../sources/tutorials/ui/templates.md). |

Voor meer informatie over gegevensinvoer leest u de [gegevensinvoer - overzicht](../../ingestion/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe bestemmingen** {#new-destinations}

| Bestemming | Beschrijving |
| ----------- | ----------- |
| **[[!UICONTROL Mailchimp Interest Categories]](../../destinations/catalog/email-marketing/mailchimp-interest-categories.md)** | **[!UICONTROL Mailchimp]** is een populair platform voor marketingautomatisering en marketingservices voor e-mail die door bedrijven worden gebruikt om contactpersonen (klanten, klanten of andere belanghebbende partijen) te beheren en met hen te spreken via mailinglijsten en marketingcampagnes voor e-mail. Gebruik deze schakelaar om uw contacten te sorteren die op hun belangen en voorkeur worden gebaseerd. |

{style="table-layout:auto"}

<!--

**New or updated functionality** {#destinations-new-updated-functionality}

| Functionality | Description |
| ----------- | ----------- |
| General availability of attribute-based personalization through the [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) and [Custom personalization](../../destinations/catalog/personalization/custom-personalization.md) destinations. | Leverage profile attributes in real-time to deliver one-to-one web and mobile personalization, via Adobe Target or other custom personalization destinations in Experience Platform. See the [dedicated documentation](../../destinations/ui/activate-edge-personalization-destinations.md) for more details. |
| Destination SDK support for grouping exported audiences based on merge policy. | When building a file-based destination with Destination SDK, you can now configure the grouping of exported audiences into one or multiple files, based on merge policy. <br><br> Additionally, you can now include the merge policy ID and merge policy name in the exported file names, by using the dedicated template macros. <br><br>See the [batch configuration documentation](../../destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md) for more details on how to use the `segmentGroupingEnabled` parameter and the new file name template macros.|

{style="table-layout:auto"}

-->

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

- We hebben een beperking in de (Beta) SFTP-cloudopslagbestemming opgelost, waarbij gebruikers de waarde van de poortparameter niet konden aanpassen. De waarde is nu bewerkbaar wanneer u een (Beta) SFTP-doelverbinding instelt via de [API](/help/destinations/api/activate-segments-file-based-destinations.md) of [UI](/help/destinations/catalog/cloud-storage/sftp.md#authentication-information).

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte XDM-componenten**

| Componenttype | Naam | Beschrijving |
| --- | --- | --- |
| Veldgroep | (Meerdere) | Verschillende velden voor [Object aanbieden](https://github.com/adobe/xdm/pull/1720/files) zijn bijgewerkt om een dubbele hiërarchie uit het schema te verwijderen. |
| Veldgroep | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1721/files) | De `partnerProspect` optie voor metagegevenstags is toegevoegd aan de [!UICONTROL XDM Individual Prospect Profile] klasse. |
| Datatype | (Meerdere) | Er zijn verschillende velden toegevoegd voor de [[!UICONTROL Media details information]](https://github.com/adobe/xdm/pull/1716/files) datatype. |
| Datatype | [[!UICONTROL Session details information]](https://github.com/adobe/xdm/pull/1716/files) | Er is een nieuw veld toegevoegd om aan te geven of een omleiding heeft plaatsgevonden. |
| Veldgroep | [[!UICONTROL MediaAnalytics Interaction Details]](https://github.com/adobe/xdm/pull/1716/files) | Er is een nieuw veld voor mediarapportage toegevoegd. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, lees [XDM System, overzicht](../../xdm/home.md).

## Identiteitsservice {#identity-service}

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

**Functies bijwerken**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor partner-id&#39;s in Adobe Experience Cloud-toepassingen [!BADGE Beta]{type=Informative} | Identiteitskaart van de partner is nu beschikbaar in de Dienst van de Identiteit. Identiteitskaart van de partner is herkenningstekens die door gegevenspartners worden gebruikt om mensen te vertegenwoordigen. In Real-time Customer Data Platform, worden de Partner IDs gebruikt hoofdzakelijk voor uitgebreide publieksactivering en gegevensverrijking. Identiteitskaart van de partner wordt niet opgeslagen in de identiteitsgrafiek. Lees de documentatie over [identiteitstypen](../../identity-service/namespaces.md#identity-types). |

Voor meer informatie over Identiteitsservice leest u de [Overzicht van identiteitsservice](../../identity-service/home.md)

## Query-service {#query-service}

De Dienst van de vraag staat u toe om standaardSQL aan vraaggegevens in Adobe Experience Platform te gebruiken [!DNL data lake]. U kunt zich bij om het even welke datasets van gegevens aansluiten meer en de vraagresultaten vangen als nieuwe dataset voor gebruik in rapportering, de Werkruimte van de Wetenschap van Gegevens, of voor opname in het Profiel van de Klant in real time.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Statistieken op kolomniveau berekenen over ADLS-gegevenssets | De `ANALYZE TABLE` is uitgebreid met de `COMPUTE STATISTICS` en `SHOW STATISTICS` SQL-opdrachten. U kunt statistieken voor een ondergroep van een dataset van ADLS of voor bepaalde kolommen binnen die dataset nu gegevens verwerken. Lees voor meer informatie de [Gegevenssetstatistieken, berekeningsgids](../../query-service/essential-concepts/dataset-statistics.md). |

{style="table-layout:auto"}

Voor meer informatie over Query Services leest u de [Overzicht van Query Service](../../query-service/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens uit verschillende bronnen invoeren, zoals Adobe-toepassingen, cloudgebaseerde opslag, software van derden en uw CRM-systeem.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| API-ondersteuning voor het streamen van gegevens van een [!DNL Snowflake] database | U kunt nu gegevens streamen vanuit een [[!DNL Snowflake] bron](../../sources/connectors/databases/snowflake-streaming.md) met de [!DNL Flow Service] API. |
| Uitgebreide API-ondersteuning voor conceptmodus | U kunt de voortgang tijdens de workflow Bronnen nu pauzeren en opslaan wanneer u de functie [!DNL Flow Service] API op elk moment. Gebruik de `mode=draft` status om uw basis-, bron- en doelverbindingen als concepten op te slaan. Alle concepteigenschappen kunnen later worden herzien om te worden voltooid. Lees de handleiding op [uw [!DNL Flow Service] entiteiten in een ontwerpstaat](../../sources/tutorials/api/draft.md) voor meer informatie . |
| Algemene beschikbaarheid van de [!DNL Salesforce Marketing Cloud] bron | De [[!DNL Salesforce Marketing Cloud source] is nu in GA](../../sources/connectors/marketing-automation/salesforce-marketing-cloud.md). Gebruik deze bron om uw [!DNL Salesforce Marketing Cloud] gegevens naar Experience Platform. |
| [!DNL Google Ads] verificatie-updates | U kunt nu een aanmeldings-id opgeven wanneer u uw [!DNL Google Ads] bronrekening om rapportgegevens van een specifieke werkende klant te halen. Lees de [[!DNL Google Ads] brondocumentatie](../../sources/connectors/advertising/ads.md) voor meer informatie . |
| [!DNL Google PubSub] verificatie-updates | U kunt nu toegangsrechten definiëren voor uw [!DNL Google PubSub] bron bij het maken van een nieuwe account. Gebruik op project-gebaseerde authentificatie om toegang op hoofdniveau toe te staan, of gebruik onderwerp en op abonnement-gebaseerde authentificatie om toegang tot een bepaald onderwerp en abonnementstroom te beperken. Lees de [[!DNL Google PubSub] brondocumentatie](../../sources/connectors/cloud-storage/google-pubsub.md) voor meer informatie . |
| Nieuwe parameters voor pagineringsvelden voor `type=PAGE` in Self-Serve Sources (Batch SDK) | U kunt nu `initialPageIndex` en `endPageIndex` bij het integreren van een bron met `type=PAGE` via Batch SDK. <ul><li>`initialPageIndex`: Met deze parameter kunt u het paginanummer definiëren waarmee de paginering begint. </li><li>`endPageIndex`: Met deze parameter kunt u een eindvoorwaarde instellen en paginering stoppen.</li></ul> Lees voor meer informatie over deze nieuwe parameters de [Self-Serve Sources Batch SDK-documentatie](../../sources/sources-sdk/config/sourcespec.md#page). |
| UI-ondersteuning voor conceptmodus | U kunt de voortgang nu pauzeren en opslaan tijdens de workflow voor bronnen via de gebruikersinterface. U kunt **[!UICONTROL Save as draft]** tijdens de gegevensstroomdetails, het in kaart brengen, en het plannen stappen van het werkschema om uw gegevensstroom als ontwerp voor recentere voltooiing te bewaren. Lees de handleiding op [gegevens opslaan als concepten in de gebruikersinterface](../../sources/tutorials/ui/draft.md) voor meer informatie . |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
