---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gegevenstypen Adobe Experience Platform Segmentation Service
topic: overview
translation-type: tm+mt
source-git-commit: cb6a2f91eb6c18835bd9542e5b66af4682227491
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 0%

---


# Ondersteunde gegevenstypen in de Adobe Experience Platform Segmentation Service

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

Als schema van het Adobe Experience Platform, registreert XDM ExperienceEvents expliciete en impliciete klanteninteractie met [!DNL Platform]-geïntegreerde toepassingen, met inbegrip van een momentopname van het systeem op het tijdstip dat de interactie plaatsvond. ExperienceEvents zijn feitenverslagen. Als dusdanig, zijn zij een gegevensbron beschikbaar aan u tijdens segmentdefinitie.

Zoals in de onderstaande tabel wordt getoond, worden gebeurtenisgegevens weergegeven met behulp van trefwoorden die het gedrag van gebeurtenissen verfijnen en gebeurteniskenmerken opgeven.

| Trefwoord | Gebruik |
| ------- | --- |
| Opnemen/uitsluiten | Beschrijft het gedrag van de gebeurtenis door het opnemen of weglaten van gegevens. |
| Alle | Helpt het aantal in aanmerking komende segmenten te bepalen. |
| Knop Tijdregel toepassen | Bevat datumgegevens. |
| Gelijk aan, niet gelijk aan, begint met, niet met, eindigt niet met, eindigt niet met, bevat, bevat, niet bevat, bestaat, niet bestaat | Bevat tekenreeksgegevens. |

## Segmenten

De bestaande segmentdefinities kunnen ook als componenten van een nieuwe segmentdefinitie worden gebruikt, toevoegend hun attributen en op gebeurtenis-gebaseerde regels aan het nieuwe segment.

## Soorten publiek

Het externe publiek kan ook als componenten van een nieuwe segmentdefinitie worden gebruikt, toevoegend hun attributenregels aan het nieuwe segment.

Momenteel wordt alleen Adobe Audience Manager ondersteund als publiek. Extra bronnen worden in de toekomst ingeschakeld.

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