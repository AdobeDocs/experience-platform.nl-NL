---
title: Adobe Experience Platform Release Notes December 2019
description: In de release van december 2019 staat Adobe Experience Platform vermeld.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '657'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 11 december 2019**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful-API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-Time Customer Profile] -gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
|--- | ---|
| Tabblad Samengevoegd publiek in [!DNL Segment Builder] | De tabbladen [!UICONTROL Segments] en [!UICONTROL Audiences] in [!DNL Segment Builder] zijn gecombineerd tot één [!UICONTROL Audiences] -tabblad. Dit lusje staat u toe om naar bestaand publiek te doorbladeren en te zoeken, dat u dan en in het canvas van de regelbouwer kunt slepen om een nieuwe segmentdefinitie tot stand te brengen. Verwijzen naar een publiek kan één van de volgende reeksen regellogica aan de nieuwe segmentdefinitie toevoegen: het lidmaatschap van de Publiek als regel, de volledige reeks regellogica die het referenced publiek bepaalde. |
| Nieuwe locatie voor de kiezer voor het samenvoegbeleid | De locatie van de kiezer voor het samenvoegbeleid in de [!DNL Segment Builder] is gewijzigd. Als u een samenvoegbeleid voor een segmentdefinitie wilt selecteren, selecteert u het tandwielpictogram op het tabblad **[!UICONTROL Fields]** en selecteert u het samenvoegbeleid dat u wilt gebruiken in het vervolgkeuzemenu **[!UICONTROL Merge Policy]** . |

**Bekende kwesties**

* Geen

Voor meer informatie, gelieve te zien het [ overzicht van de Dienst van de Segmentatie ](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] biedt de mogelijkheid om programmatisch en intelligent de &quot;Next Best Experience&quot; te selecteren uit een set beschikbare opties voor een bepaalde persoon, deze te leveren aan een willekeurig kanaal of een toepassing en rapportage en analyse uit te voeren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| -----------| ---------- |
| Rangschikkingsfuncties | De volgorde van de aanbiedingen voor profielen wordt nu bepaald door een rangschikkingsfunctie in plaats van een vaste set aanbiedingen voor alle profielen. |

**Bekende kwesties**

* Geen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] -services. U kunt gegevens van een verscheidenheid van bronnen zoals de Oplossingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
| ---------- | ------------ |
| Streaming verbinding | Met streaming opname kunt u gegevens van client- en server-side apparaten in real-time naar [!DNL Experience Platform] verzenden. Release omvat een nieuwe streamingverbinding, gebruikersinterface. |
| Connectorondersteuning voor [!DNL Google Cloud Store] | Ondersteuning voor het verzamelen van gegevens van [!DNL Google Cloud Store] . |

**Bekende kwesties**

* Geen.

Voor meer informatie over bronnen, zie het [ overzicht van bronnen ](../../sources/home.md).

## [!DNL Experience Data Model] (XDM)-systeem {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform] . [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe eigenschappen**

| Functie | Beschrijving |
|--- | ---|
| Verbeterde schemavalidatie | Nieuwe controles om ervoor te zorgen dat de verwijzingen in extra gebieden zoals verwacht oplossen. Extra controles toegevoegd aan velden die zijn gedefinieerd als een array van objecten om te controleren of de objecten volledig zijn gedefinieerd. Verbeterde foutmeldingen voor het opsporen en verhelpen van problemen. |

**Bugfixes**

* Onderhoud en verbeteringen met betrekking tot toegangsbeheer en sandboxen.
* Ondersteuning voor `eTag` voor het `/descriptors` -eindpunt in de [!DNL Schema Registry] -API.

**Bekende kwesties**

* Geen

Om meer over het werken met XDM te leren gebruikend [!DNL Schema Registry] API en [!DNL Schema Editor] gebruikersinterface, te lezen gelieve de [ documentatie van het Systeem XDM ](../../xdm/home.md).
