---
title: Aanvullende informatie over Adobe Experience Platform
description: In de releaseopmerkingen van oktober 2023 voor Adobe Experience Platform.
source-git-commit: 4ab89ef7cabc9d808fd9dab24b6dbe3fe23e53f3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 3%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 oktober 2023**

Updates voor bestaande functies in Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Sandboxes](#sandboxes)
- [Segmenteringsservice](#segmentation)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden, waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe doelen.

**Nieuwe of bijgewerkte functies**

| Type | Functie | Beschrijving |
| --- | --- | --- |
| Extensie | [!DNL Meta] Verbetering conversie-API | Er zijn drie verbeteringen aangebracht in de [API voor metaconversie](/help/tags/extensions/server/meta/overview.md) extensie: <ul><li>Integratie met [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): Creeert een naadloze login ervaring door u toe te staan om uw pixelID en toegangstoken voor de integratie van Conversions API met Adobe te delen.</li><li>Integratie met [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): Hiermee kunt u reclame maken voor mensen die een gewenste actie waarschijnlijk uitvoeren en de actie terugkoppelen aan de geleverde advertenties.</li><li>Integratie met [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): Hiermee kunt u de RampID van LiveRamp in het CIP-veld doorgeven, zodat PII niet rechtstreeks met partners of Meta hoeft te worden gedeeld. </li></ul> |

Lees voor meer informatie over gegevensverzameling de [overzicht van gegevensverzamelingen](../../tags/home.md).

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
