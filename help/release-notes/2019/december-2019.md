---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform van 11 december 2019
doc-type: release notes
last-update: December 12, 2019
author: ens71067
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
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

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt bouwen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile]-gegevens. Deze segmenten worden centraal gevormd en gehandhaafd op [!DNL Platform], die hen gemakkelijk toegankelijk maken door om het even welke toepassing van de Adobe.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. Segmenten kunnen worden gebaseerd op recordgegevens (zoals demografische informatie) of tijdreeksgebeurtenissen die klantinteracties met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Tabblad Samengevoegd publiek in [!DNL Segment Builder] | De tabbladen [!UICONTROL Segmenten] en [!UICONTROL Soorten publiek] in [!DNL Segment Builder] zijn gecombineerd tot één [!UICONTROL tabblad Soorten publiek]. Dit lusje staat u toe om naar bestaand publiek te doorbladeren en te zoeken, dat u dan en in het canvas van de regelbouwer kunt slepen om een nieuwe segmentdefinitie tot stand te brengen. Verwijzen naar een publiek kan één van de volgende reeksen regellogica aan de nieuwe segmentdefinitie toevoegen: Het lidmaatschap van het publiek als regel, de volledige reeks regellogica die het referenced publiek bepaalde. |
| Nieuwe locatie voor de kiezer voor het samenvoegbeleid | De plaats van de selecteur van het fusiebeleid in [!DNL Segment Builder] is veranderd. Als u een samenvoegbeleid voor een segmentdefinitie wilt selecteren, selecteert u het tandwielpictogram op het tabblad **[!UICONTROL Velden]** en gebruikt u het vervolgkeuzemenu **[!UICONTROL Beleid samenvoegen]** om het samenvoegbeleid te selecteren dat u wilt gebruiken. |

**Bekende problemen**

* Geen

Zie [Overzicht van de segmentatieservice](../../segmentation/home.md) voor meer informatie.

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] biedt de mogelijkheid om programmatisch en intelligent de &quot;Next Best Experience&quot; te selecteren uit een set beschikbare opties voor een bepaalde persoon, deze te leveren aan een willekeurig kanaal of een toepassing en rapportage en analyse uit te voeren.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Rangschikkingsfuncties | De volgorde van de aanbiedingen voor profielen wordt nu bepaald door een rangschikkingsfunctie in plaats van een vaste set aanbiedingen voor alle profielen. |

**Bekende problemen**

* Geen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met services van [!DNL Platform]. U kunt gegevens van een verscheidenheid van bronnen zoals de Oplossingen van Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ---------- | ------------ |
| Streaming verbinding | Met streaming opname kunt u gegevens van client- en server-side apparaten in real-time naar [!DNL Experience Platform] verzenden. Release omvat een nieuwe streamingverbinding, gebruikersinterface. |
| Connectorondersteuning voor [!DNL Google Cloud Store] | Ondersteuning voor het verzamelen van gegevens van [!DNL Google Cloud Store]. |

**Bekende problemen**

* Geen.

Voor meer informatie over bronnen, zie [bronnen overzicht](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) System  {#xdm}

Standaardisering en interoperabiliteit zijn belangrijke concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Verbeterde schemavalidatie | Nieuwe controles om ervoor te zorgen dat de verwijzingen in extra gebieden zoals verwacht oplossen. Extra controles toegevoegd aan velden die zijn gedefinieerd als een array van objecten om te controleren of de objecten volledig zijn gedefinieerd. Verbeterde foutmeldingen voor het opsporen en verhelpen van problemen. |

**Bugfixes**

* Onderhoud en verbeteringen met betrekking tot toegangsbeheer en sandboxen.
* Ondersteuning voor `eTag` voor het `/descriptors`-eindpunt in de [!DNL Schema Registry]-API.

**Bekende problemen**

* Geen

Lees de [XDM System documentatie](../../xdm/home.md) voor meer informatie over het werken met XDM met de [!DNL Schema Registry]-API en [!DNL Schema Editor]-gebruikersinterface.