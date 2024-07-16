---
title: Aanvullende informatie over Adobe Experience Platform
description: Aanvullende informatie voor de versie van oktober 2023 voor Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f2d0848952902d94b441566da677ef174518192e
workflow-type: tm+mt
source-wordcount: '1046'
ht-degree: 4%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 25 oktober 2023**

Updates voor bestaande functies in Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Sandboxes](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Doelen voor doelgebruik | Er zijn nieuwe metergegevens toegevoegd aan het dashboard voor licentiegebruik. De **[!UICONTROL Audience Activation Size]** - en **[!UICONTROL Data Export Size]** -gegevens bieden een handige manier om te controleren hoeveel gegevens u van Platform hebt geëxporteerd ten opzichte van uw gebruiksrechten voor licenties. Zie de [ beschikbare metriek ](../../dashboards/guides/license-usage.md#available-metrics) documentatie voor beschrijvingen van deze en andere metriek van het vergunningsgebruik. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanegidgets tot stand te brengen, begin door het [ overzicht van dashboards ](../../dashboards/home.md) te lezen.

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensies | [!DNL Meta] Verbetering van conversie-API | Er zijn drie verhogingen aan de [ Conversies API van Meta ](/help/tags/extensions/server/meta/overview.md) uitbreiding: <ul><li>Integratie met [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): maakt een naadloze aanmeldervaring doordat u uw pixelID en toegangstoken kunt delen voor de integratie van conversie-API met Adobe.</li><li>Integratie met [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): hiermee kunt u reclame maken voor mensen die een gewenste actie waarschijnlijk uitvoeren en de actie weer koppelen aan de geleverde advertenties.</li><li>Integratie met [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): hiermee kunt u de RampID van LiveRamp in het CIP-veld doorgeven, zodat u geen PII rechtstreeks met partners of Meta hoeft te delen. </li></ul> |
| Extensies | [!DNL LinkedIn] Conversies-API | De [[!DNL LinkedIn]  Conversies API ](../../tags/extensions/server/linkedin/overview.md) uitbreiding staat u toe om de doeltreffendheid van uw LinkedIn marketing campagnes te evalueren door de gebeurtenisgegevens van het Experience Platform aan LinkedIn door:sturen. |
| Geheim | [!DNL LinkedIn] OAuth 2 Secret | [[!DNL LinkedIn]  OAuth 2 Geheim ](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) staat u toe om server-server interactie naar [!DNL LinkedIn] in gebeurtenis te verzenden die door:sturen. |
| Gebeurtenis doorsturen | Bijwerken naar tags en doorsturen van gebeurtenissen | Om [ Markeringen ](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=nl) en [ Gebeurtenis te bewaren die ](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) prestaties in Platform door:sturen, slechts zullen de meest recente Ontwikkeling en het Stadium bouwt, zowel succesvol als niet succesvol, worden behouden. Alle builds die niet meer in gebruik zijn, worden verwijderd. Bovendien is het vertragen en het tarief beperken uitgevoerd om ervoor te zorgen dat een paar zwaar gebruik van API de prestaties van API voor anderen niet degraderen. |
| Extensies | Elementen, regels en extensies | [ Elementen, regels, en uitbreidingen ](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html) worden nu gesorteerd in de bibliotheekoutput om meer consistentie tussen veelvoudige bouwt en plaatsingen van de zelfde bibliotheek te verzekeren. |

Voor meer informatie over gegevensinzameling, te lezen gelieve het [ overzicht van gegevensinzamelingen ](../../tags/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integratie met bestemmingsplatforms die voor de naadloze activering van gegevens van Adobe Experience Platform toestaan. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte bestemmingen** {#new-updated-destinations}

| Doel | Nieuw of Bijgewerkt | Beschrijving |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nieuw | Gebruik de bestemming van de Moweer om uw gegevens van de Adobe (gebruikersattributen, segmenten en gebeurtenissen) aan MoEngage in real time te verbinden en in kaart te brengen. Klanten kunnen vervolgens op deze gegevens reageren en persoonlijke, doelgerichte ervaringen bieden. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nieuw | Gebruik de samenvoeging van meerdere bronnen van operationele gegevens in Adobe Experience Platform als input in de Qualtrics Experience ID om uw klanten beter te begrijpen en gerichte outreach toe te laten om de kloof te dichten wanneer het aankomt op het begrijpen van intent, emotie en ervaringsstuurprogramma&#39;s. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| (Beta) Ondersteuning voor hashfuncties in berekende velden | Naast de functies specifiek voor [ het uitvoeren van series ](../../destinations/ui/export-arrays-calculated-fields.md) of elementen van een serie, kunt u extra [ het hakken functies ](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) aan knoeiboelattributen in de uitgevoerde dossiers nu gebruiken. De ondersteunde hashingfuncties zijn: `sha`, `sha256`, `sha512`, `hash`, `md5` en `crc32` . |
| (Beperkte GA) Accountpubliek naar bepaalde bestemmingen activeren | De klanten van Real-Time CDP B2B kunnen [ rekeningspubliek ](../../segmentation/ui/account-audiences.md) aan bepaalde bestemmingen nu activeren. Voor meer informatie over deze eigenschap, gelieve te lezen [ de leerprogramma van het rekeningspubliek activeert ](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Correcties en verhogingen** {#destinations-fixes-and-enhancements}

Voor meer algemene informatie over bestemmingen, verwijs naar het [ overzicht van bestemmingen ](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Nieuwe eigenschap**

| Functie | Beschrijving |
| --- | --- |
| Gereedschap Sandbox | Met de functie voor sandboxgereedschappen kunt u de configuratienauwkeurigheid in verschillende sandboxen verbeteren en kunt u naadloos sandboxconfiguraties exporteren en importeren tussen sandboxen. U kunt de functie voor gereedschappen in de sandbox gebruiken om verschillende objecten te selecteren en deze te exporteren naar een pakket. Voor meer informatie, zie de [ zandbak tooling UI gids ](../../sandboxes/ui/sandbox-tooling.md). |

Voor meer informatie over zandbakken, te zien gelieve het [ overzicht van zandbakken ](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

Met [!DNL Segmentation Service] kunt u gegevens die zijn opgeslagen in [!DNL Experience Platform] en die betrekking hebben op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) segmenteren naar het publiek. U kunt een publiek maken via segmentdefinities of andere bronnen op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze soorten publiek worden centraal geconfigureerd en onderhouden op [!DNL Platform] en zijn gemakkelijk toegankelijk voor elke Adobe.

**Nieuwe eigenschap**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountpubliek (beperkt GA) | In Real-time Customer Data Platform B2B Edition kunt u nu de segmentering van accounts gebruiken om het volledige gemak en de verfijning van de segmentatieervaring voor marketing te bieden van publiek-private doelgroepen naar publiek in account. Voor meer informatie over deze eigenschap, te lezen gelieve het [ overzicht van het rekeningspubliek ](../../segmentation/ui/account-audiences.md). |

Om meer over de Dienst van de Segmentatie te leren, te lezen gelieve het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte verificatie voor Data Landing Zone | U kunt nu de aangewezen vervaldatum van uw Gebied van Gegevens zien Landing wanneer het bekijken van uw geloofsbrieven. U moet uw token vernieuwen vóór de vervaldatum om deze in uw toepassing te kunnen blijven gebruiken. Als u uw token niet handmatig vernieuwt vóór de opgegeven vervaldatum, wordt deze automatisch vernieuwd en krijgt u een nieuwe token wanneer u uw gegevens de volgende keer ophaalt. Voor meer informatie, lees de documentatie op [ gebruikend de Gegevens die Zone ](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md) aanvoeren. |

{style="table-layout:auto"}

Om meer over bronnen te leren, te lezen gelieve het [ overzicht van bronnen ](../../sources/home.md).
