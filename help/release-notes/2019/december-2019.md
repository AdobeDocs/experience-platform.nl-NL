---
title: Adobe Experience Platform Release Notes December 2019
description: In de release van december 2019 staat Adobe Experience Platform vermeld.
doc-type: release notes
last-update: December 12, 2019
author: ens71067
exl-id: 98d50b90-38ed-4cc2-ad48-78b712b453f7
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '655'
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

Adobe Experience Platform Segmentation Service biedt een gebruikersinterface en RESTful API waarmee u segmenten kunt samenstellen en doelgroepen kunt genereren op basis van uw [!DNL Real-time Customer Profile] gegevens. Deze segmenten worden centraal geconfigureerd en onderhouden op [!DNL Platform], zodat ze gemakkelijk toegankelijk zijn voor elke Adobe-toepassing.

[!DNL Segmentation Service] definieert een bepaalde subset van profielen door de criteria te beschrijven die een verhandelbare groep personen binnen uw klantenbasis onderscheiden. De segmenten kunnen op verslaggegevens (zoals demografische informatie) of tijdreeksgebeurtenissen worden gebaseerd die klanteninteractie met uw merk vertegenwoordigen.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Het tabblad Samengevoegd publiek in [!DNL Segment Builder] | De [!UICONTROL Segments] en [!UICONTROL Audiences] tabbladen in het dialoogvenster [!DNL Segment Builder] zijn gecombineerd tot één [!UICONTROL Audiences] tab. Dit lusje staat u toe om naar bestaand publiek te doorbladeren en te zoeken, dat u dan en in het canvas van de regelbouwer kunt slepen om een nieuwe segmentdefinitie tot stand te brengen. Verwijzen naar een publiek kan één van de volgende reeksen regellogica aan de nieuwe segmentdefinitie toevoegen: Het lidmaatschap van het publiek als regel, de volledige reeks regellogica die het referenced publiek bepaalde. |
| Nieuwe locatie voor de kiezer voor het samenvoegbeleid | De locatie van de kiezer voor het samenvoegbeleid in het dialoogvenster [!DNL Segment Builder] is gewijzigd. Als u een samenvoegbeleid voor een segmentdefinitie wilt selecteren, selecteert u het tandwielpictogram in het dialoogvenster **[!UICONTROL Fields]** gebruikt u vervolgens de **[!UICONTROL Merge Policy]** vervolgkeuzelijst om het samenvoegbeleid te selecteren dat u wilt gebruiken. |

**Bekende problemen**

* Geen

Zie voor meer informatie de [Overzicht van segmentatieservice](../../segmentation/home.md).

## [!DNL Decisioning Service] {#decisioning}

Adobe Experience Platform [!DNL Decisioning Service] biedt de mogelijkheid om programmatisch en intelligent de &quot;Next Best Experience&quot; te selecteren uit een set beschikbare opties voor een bepaalde persoon, deze te leveren aan een willekeurig kanaal of een willekeurige toepassing en rapportage en analyse uit te voeren.

**Nieuwe functies**

| Functie | Beschrijving |
| -----------| ---------- |
| Rangschikkingsfuncties | De volgorde van de aanbiedingen voor profielen wordt nu bepaald door een rangschikkingsfunctie in plaats van een vaste set aanbiedingen voor alle profielen. |

**Bekende problemen**

* Geen.

## [!DNL Sources] {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met [!DNL Platform] diensten. U kunt gegevens van een verscheidenheid van bronnen zoals de Oplossingen van Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

[!DNL Experience Platform] biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om aan uw opslagsystemen en de diensten van CRM voor authentiek te verklaren, tijden voor inname looppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| ---------- | ------------ |
| Streaming verbinding | Met streaming invoer kunt u gegevens van client- en serverapparaten naar [!DNL Experience Platform] in real time. Release omvat een nieuwe streamingverbinding, gebruikersinterface. |
| Connectorondersteuning voor [!DNL Google Cloud Store] | Ondersteuning voor het verzamelen van gegevens van [!DNL Google Cloud Store]. |

**Bekende problemen**

* Geen.

Voor meer informatie over bronnen raadpleegt u de [overzicht van bronnen](../../sources/home.md).

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standaardisering en interoperabiliteit zijn de belangrijkste concepten achter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), gedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en schema&#39;s voor het beheer van de klantenervaring te bepalen.

XDM is een openbaar gedocumenteerde specificatie die wordt ontworpen om de macht van digitale ervaringen te verbeteren. Het verstrekt gemeenschappelijke structuren en definities voor om het even welke toepassing om met de diensten op Adobe Experience Platform te communiceren. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen die inzichten op een snellere, meer geïntegreerde manier levert. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe functies**

| Functie | Beschrijving |
|--- | ---|
| Verbeterde schemavalidatie | Nieuwe controles om ervoor te zorgen dat de verwijzingen in extra gebieden zoals verwacht oplossen. Extra controles toegevoegd aan velden die zijn gedefinieerd als een array van objecten om te controleren of de objecten volledig zijn gedefinieerd. Verbeterde foutmeldingen voor het opsporen en verhelpen van problemen. |

**Bugfixes**

* Onderhoud en verbeteringen met betrekking tot toegangsbeheer en sandboxen.
* Ondersteuning voor `eTag` voor de `/descriptors` in de [!DNL Schema Registry] API.

**Bekende problemen**

* Geen

Meer informatie over het werken met XDM [!DNL Schema Registry] API en [!DNL Schema Editor] gebruikersinterface, lees de [XDM System-documentatie](../../xdm/home.md).
