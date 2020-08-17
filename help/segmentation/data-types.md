---
keywords: Experience Platform;home;popular topics;data type;data types;Data types;Data type
solution: Experience Platform
title: Gegevenstypen Adobe Experience Platform Segmentation Service
topic: overview
description: Alle XDM gegevenstypes worden gesteund binnen de Dienst van de Segmentatie. De regels die een segmentdefinitie vormen worden contextualiseerd door de volgende gegevenstypes.
translation-type: tm+mt
source-git-commit: 23516c66a67ae5663dcf90a40ccba98bfd266ab0
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---


# Door Adobe Experience Platform [!DNL Segmentation Service] ondersteunde gegevenstypen

Alle XDM-gegevenstypen worden ondersteund binnen [!DNL Segmentation Service]. De regels die een segmentdefinitie vormen worden contextualiseerd door de volgende gegevenstypes.

## Tekenreeksgegevens

Segmentdefinities gebruiken tekenreeksgegevens om niet-numerieke beperkingen voor segmentpubliek te definiëren, zoals &quot;landnaam&quot; of &quot;niveau van loyaliteitsprogramma&quot;.

Tekenreeksgegevens worden opgenomen in segmentdefinities met behulp van logische, uitsluitende en uitsluitende instructies. Zodra een koordattribuut aan uw segmentdefinitie wordt toegevoegd, kunt u koord-relevante verklaringen gebruiken om het tegen andere koordgebieden te evalueren.

| Type instructie | Voorbeelden |
| -------------- | -------- |
| Logisch | `and`, `or`, `not` |
| Inclusief/exclusief | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergelijking | `equals`, `does not equal`, `contains`, `starts with` |

## Datumgegevens

Met datumgegevens kunt u op tijd gebaseerde context toewijzen aan uw segmentdefinities door specifieke begin- en einddatums te gebruiken of door datumrelevante instructies te gebruiken, zoals in de onderstaande tabel wordt getoond. Eén implementatie zou kunnen leiden tot een publiek van klanten die op elk moment *dit jaar* met uw merk hebben gewerkt en ook *in de afgelopen dagen* actief zijn geweest.

| Voorbeeldveld | Datum-relevante verklaringen | Tijdlijn |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant aan de dag het segment werd gebouwd. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant binnen een bepaalde week/maand. |

## Experience Events

Als schema van Adobe Experience Platform, [!DNL XDM ExperienceEvents] registreer expliciete en impliciete klanteninteractie met [!DNL Platform]-geïntegreerde toepassingen, met inbegrip van een momentopname van het systeem op het tijdstip dat de interactie plaatsvond. [!DNL ExperienceEvents] Dit zijn feiten. Als dusdanig, zijn zij een gegevensbron beschikbaar aan u tijdens segmentdefinitie.

Zoals in de onderstaande tabel wordt getoond, worden gebeurtenisgegevens weergegeven met behulp van trefwoorden die het gedrag van gebeurtenissen verfijnen en gebeurteniskenmerken opgeven.

| Trefwoord | Gebruik |
| ------- | --- |
| Opnemen/uitsluiten | Beschrijft het gedrag van de gebeurtenis door het opnemen of weglaten van gegevens. |
| Alle | Helpt het aantal in aanmerking komende segmenten te bepalen. |
| Knop Tijdregel toepassen | Bevat datumgegevens. |
| Gelijk aan, niet gelijk aan, begint met, niet met, eindigt niet met, eindigt niet met, bevat, bevat, niet bevat, bestaat, niet bestaat | Bevat tekenreeksgegevens. |

### Delen van doelgroepen

Het externe publiek kan ook als componenten van een nieuwe segmentdefinitie worden gebruikt, toevoegend hun attributenregels aan het nieuwe segment.

Momenteel wordt alleen Adobe Audience Manager ondersteund als een extern publiek, waarbij in de toekomst extra bronnen worden ingeschakeld. Meer informatie over het gebruik van Adobe Audience Manager-soorten publiek met Platform vindt u in de handleiding voor het delen van [publiek in de documentatie](https://docs.adobe.com/content/help/en/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html)van Adobe Audience Manager.

### Segment delen

Segmenten die in Platform zijn gemaakt, kunnen binnen andere [Adobe Experience Cloud Core Services](https://docs.adobe.com/content/help/nl-NL/core-services/interface/experience-cloud.html)worden gebruikt. Om deze functie in te schakelen, dient u contact op te nemen met uw oplossingsarchitect of uw consultant.

## Andere gegevenstypen

Naast de hierboven vermelde gegevenstypen bevat de lijst met ondersteunde gegevenstypen ook:

- Uniform resource identifier (URI)
- Enum
- Getal
- Lang
- Geheel
- Kort
- Byte
- Boolean
- Array
- Object
- Kaart