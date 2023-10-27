---
title: Aanvullende informatie over Adobe Experience Platform
description: In de releaseopmerkingen van oktober 2023 voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: fc0cb582d74f5ab52410991f65aa14ba05df3f97
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 oktober 2023**

Updates voor bestaande functies in Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensverzameling](#data-collection)
- [Doelen](#destinations)
- [Sandboxes](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Doelen voor doelgebruik | Er zijn nieuwe metergegevens toegevoegd aan het dashboard voor licentiegebruik. De **[!UICONTROL Audience Activation Size]** en **[!UICONTROL Data Export Size]** Met cijfers kunt u op een handige manier bijhouden hoeveel gegevens u van Platform hebt geëxporteerd in verhouding tot uw gebruiksrechten voor licenties. Zie de [beschikbare cijfers](../../dashboards/guides/license-usage.md#available-metrics) documentatie voor beschrijvingen van deze en andere gegevens van het vergunningsgebruik. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensie | [!DNL Meta] Verbetering conversie-API | Er zijn drie verbeteringen aangebracht in de [API voor metaconversie](/help/tags/extensions/server/meta/overview.md) extensie: <ul><li>Integratie met [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Creeert een naadloze login ervaring door u toe te staan om uw pixelID en toegangstoken voor de integratie van Conversions API met Adobe te delen.</li><li>Integratie met [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Hiermee kunt u reclame maken voor mensen die een gewenste actie waarschijnlijk uitvoeren en de actie terugkoppelen aan de geleverde advertenties.</li><li>Integratie met [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Hiermee kunt u de RampID van LiveRamp in het CIP-veld doorgeven, zodat PII niet rechtstreeks met partners of Meta hoeft te worden gedeeld. </li></ul> |
| Extensie | [!DNL LinkedIn] Conversies-API | De [[!DNL LinkedIn] Conversies-API](../../tags/extensions/server/linkedin/overview.md) Met de extensie kunt u de doeltreffendheid van uw LinkedIn-marketingcampagnes evalueren door gebeurtenisgegevens van Experience Platforms naar LinkedIn door te sturen. |
| Geheim | [!DNL LinkedIn] OAuth 2 Secret | De [[!DNL LinkedIn] OAuth 2 Secret](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) staat u toe om server-server interactie naar te verzenden [!DNL LinkedIn] in gebeurtenis door:sturen. |

Lees voor meer informatie over gegevensverzameling de [overzicht van gegevensverzamelingen](../../tags/home.md).

## Doelen {#destinations}

[!DNL Destinations] zijn vooraf gebouwde integraties met doelplatforms die het mogelijk maken gegevens van Adobe Experience Platform naadloos te activeren. U kunt bestemmingen gebruiken om uw bekende en onbekende gegevens voor kanaalmarketing campagnes, e-mailcampagnes, gerichte reclame, en vele andere gebruiksgevallen te activeren.

**Nieuwe of bijgewerkte doelen** {#new-updated-destinations}

| Bestemming | Nieuw of Bijgewerkt | Beschrijving |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Nieuw | Gebruik de bestemming van de Moweer om uw gegevens van de Adobe (gebruikersattributen, segmenten en gebeurtenissen) aan MoEngage in real time te verbinden en in kaart te brengen. Klanten kunnen vervolgens op deze gegevens reageren en persoonlijke, doelgerichte ervaringen bieden. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Nieuw | Gebruik de samenvoeging van meerdere bronnen van operationele gegevens in Adobe Experience Platform als input in de Qualtrics Experience ID om uw klanten beter te begrijpen en gerichte outreach toe te laten om de kloof te dichten wanneer het aankomt op het begrijpen van intent, emotie en ervaringsstuurprogramma&#39;s. |

{style="table-layout:auto"}

**Nieuwe of bijgewerkte functionaliteit** {#destinations-new-updated-functionality}

| Functionaliteit | Beschrijving |
| ----------- | ----------- |
| (bèta) Ondersteuning voor hashingfuncties in berekende velden | Naast de specifieke functies voor [exporteren, arrays](../../destinations/ui/export-arrays-calculated-fields.md) of elementen uit een array, kunt u nu extra [hashingfuncties](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) om kenmerken in de geëxporteerde bestanden te hashen. De ondersteunde hashingfuncties zijn: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (Beperkte GA) Accountpubliek naar bepaalde bestemmingen activeren | Real-Time CDP B2B-klanten kunnen nu activeren [accountpubliek](../../segmentation/ui/account-audiences.md) naar bepaalde bestemmingen. Lees voor meer informatie over deze functie de [zelfstudie accountpubliek activeren](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Oplossingen en verbeteringen** {#destinations-fixes-and-enhancements}

Voor meer algemene informatie over bestemmingen raadpleegt u de [Overzicht van doelen](../../destinations/home.md).

## Sandboxes {#sandboxes}

Adobe Experience Platform is ontworpen om toepassingen voor digitale beleving wereldwijd te verrijken. Bedrijven voeren vaak meerdere digitale-ervaringstoepassingen parallel uit en moeten rekening houden met de ontwikkeling, het testen en de implementatie van deze toepassingen en tegelijk de operationele compatibiliteit garanderen. Om aan deze behoefte tegemoet te komen, biedt Experience Platform sandboxen die één enkele instantie Platform in afzonderlijke virtuele omgevingen verdelen om toepassingen voor digitale ervaringen te ontwikkelen en te ontwikkelen.

**Nieuwe functie**

| Functie | Beschrijving |
| --- | --- |
| Gereedschap Sandbox | Met de functie voor sandboxgereedschappen kunt u de configuratienauwkeurigheid in verschillende sandboxen verbeteren en kunt u naadloos sandboxconfiguraties exporteren en importeren tussen sandboxen. U kunt de functie voor gereedschappen in de sandbox gebruiken om verschillende objecten te selecteren en deze te exporteren naar een pakket. Zie de klasse [UI-hulplijn voor gereedschap sandbox](../../sandboxes/ui/sandbox-tooling.md). |

Voor meer informatie over sandboxen raadpleegt u de [sandboxen, overzicht](../../sandboxes/home.md).

## Segmenteringsservice {#segmentation}

[!DNL Segmentation Service] staat u toe om gegevens te segmenteren die in worden opgeslagen [!DNL Experience Platform] die betrekking heeft op personen (zoals klanten, vooruitzichten, gebruikers of organisaties) die het publiek bereiken. U kunt publiek door segmentdefinities of andere bronnen van uw tot stand brengen [!DNL Real-Time Customer Profile] gegevens. Deze doelgroepen worden centraal geconfigureerd en onderhouden op [!DNL Platform]en gemakkelijk toegankelijk zijn via een Adobe-oplossing.

**Nieuwe functie**

| Functie | Beschrijving |
| ------- | ----------- |
| Accountpubliek (beperkt GA) | In Real-time Customer Data Platform B2B Edition kunt u nu de segmentering van accounts gebruiken om het volledige gemak en de verfijning van de segmentatieervaring voor marketing te bieden van publiek-private doelgroepen naar publiek in account. Lees voor meer informatie over deze functie de [overzicht van publiek publiek van account](../../segmentation/ui/account-audiences.md). |

Voor meer informatie over Segmentatieservice leest u de [Overzicht van segmentatieservice](../../segmentation/home.md).

## Bronnen {#sources}

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Bijgewerkte verificatie voor Data Landing Zone | U kunt nu de aangewezen vervaldatum van uw Gebied van Gegevens zien Landing wanneer het bekijken van uw geloofsbrieven. U moet uw token vernieuwen vóór de vervaldatum om deze in uw toepassing te kunnen blijven gebruiken. Als u uw token niet handmatig vernieuwt vóór de opgegeven vervaldatum, wordt deze automatisch vernieuwd en krijgt u een nieuwe token wanneer u uw gegevens de volgende keer ophaalt. Lees de documentatie over [het gebruiken van de Gebied van Gegevens](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
