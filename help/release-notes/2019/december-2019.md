---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 11 december 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 801da8a705360688f230eae5772a8bed9a1e856e
workflow-type: tm+mt
source-wordcount: '656'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 11 december 2019**

Updates voor bestaande functies in Adobe Experience Platform:

* [[!DNL Segmentation Service]](#segmentation)
* [[!DNL Decisioning Service]](#decisioning)
* [[!DNL Sources]](#sources)
* [[!DNL Experience Data Model (XDM) System]](#xdm)

## [!DNL Segmentation Service] {#segmentation}

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt bouwen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal gevormd en gehandhaafd [!DNL Platform], die hen gemakkelijk toegankelijk door om het even welke toepassing van de Adobe maken.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Het tabblad Samengevoegd publiek in [!DNL Segment Builder] | De tabbladen [!UICONTROL Segmenten] en [!UICONTROL Soorten publiek] in het dialoogvenster [!DNL Segment Builder] zijn gecombineerd tot één [!UICONTROL tabblad Soorten publiek] . Dit lusje staat u toe om naar bestaand publiek te doorbladeren en te zoeken, dat u dan en in het canvas van de regelbouwer kunt slepen om een nieuwe segmentdefinitie tot stand te brengen. Verwijzen naar een publiek kan één van de volgende reeksen regellogica aan de nieuwe segmentdefinitie toevoegen: Het lidmaatschap van het publiek als regel, de volledige reeks regellogica die het referenced publiek bepaalde. |
| Nieuwe locatie voor de kiezer voor het samenvoegbeleid | De locatie van de kiezer voor het samenvoegbeleid in de map [!DNL Segment Builder] is gewijzigd. Als u een samenvoegbeleid voor een segmentdefinitie wilt selecteren, klikt u op het tandwielpictogram op het tabblad **[!UICONTROL Velden]** en gebruikt u het vervolgkeuzemenu Beleid **** samenvoegen om het samenvoegbeleid te selecteren dat u wilt gebruiken. |

**Bekende problemen**

* Geen

Voor meer informatie, gelieve te zien het overzicht [van de Dienst van de](../../segmentation/home.md)Segmentatie.

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] biedt de mogelijkheid om programmatisch en intelligent de &quot;Next Best Experience&quot; te selecteren uit een reeks beschikbare opties voor een bepaalde persoon, deze te leveren aan een willekeurig kanaal of een toepassing en rapportage en analyse uit te voeren.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Rangschikkingsfuncties | De volgorde van de aanbiedingen voor profielen wordt nu bepaald door een rangschikkingsfunctie in plaats van een vaste set aanbiedingen voor alle profielen. |

**Bekende problemen**

* Geen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] services. U kunt gegevens van een verscheidenheid van bronnen zoals de Oplossingen van Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ---------- | ------------ |
| Streaming verbinding | Met streaming opname kunt u gegevens van client- en serverapparaten [!DNL Experience Platform] in real-time verzenden. Release omvat een nieuwe streamingverbinding, gebruikersinterface. |
| Connectorondersteuning voor [!DNL Google Cloud Store] | Ondersteuning voor het verzamelen van gegevens van [!DNL Google Cloud Store]. |

**Bekende problemen**

* Geen.

Zie het [bronoverzicht](../../sources/home.md)voor meer informatie over bronnen.

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Verbeterde schemavalidatie | Nieuwe controles om ervoor te zorgen dat de verwijzingen in extra gebieden zoals verwacht oplossen. Extra controles toegevoegd aan velden die zijn gedefinieerd als een array van objecten om te controleren of de objecten volledig zijn gedefinieerd. Verbeterde foutmeldingen voor het opsporen en verhelpen van problemen. |

**Bugfixes**

* Onderhoud en verbeteringen met betrekking tot toegangsbeheer en sandboxen.
* Ondersteuning voor `eTag` het `/descriptors` eindpunt in de [!DNL Schema Registry] API.

**Bekende problemen**

* Geen

Meer informatie over het werken met XDM die API en [!DNL Schema Registry] gebruikersinterface gebruikt, te lezen gelieve de documentatie [!DNL Schema Editor] van het [](../../xdm/home.md)Systeem XDM.