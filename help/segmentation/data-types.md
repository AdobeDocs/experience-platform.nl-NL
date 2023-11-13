---
solution: Experience Platform
title: Ondersteunde gegevenstypen in Segmentatieservice
description: Alle gegevenstypes van het Model van de Gegevens van de Ervaring (XDM) worden gesteund binnen de Dienst van de Segmentatie van de Adobe. De regels die een segmentdefinitie vormen worden contextualiseerd door de volgende gegevenstypes.
exl-id: 73f932a7-f864-4566-ade7-c148a12dc83c
source-git-commit: dbb7e0987521c7a2f6512f05eaa19e0121aa34c6
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---

# Ondersteunde gegevenstypen in Segmentatieservice

Alle gegevenstypen van het Experience Data Model (XDM) worden ondersteund in Adobe Experience Platform Segmentation Service. De regels die een segmentdefinitie vormen worden contextualiseerd door de volgende gegevenstypes.

## String-gegevens

Segmentdefinities gebruiken tekenreeksgegevens om niet-numerieke beperkingen voor het publiek te definiëren, zoals &quot;naam van het land&quot; of &quot;niveau van het loyaliteitsprogramma&quot;.

Tekenreeksgegevens worden opgenomen in segmentdefinities met behulp van logische, uitsluitende en uitsluitende instructies. Zodra een koordattribuut aan uw segmentdefinitie wordt toegevoegd, kunt u koord-relevante verklaringen gebruiken om het tegen andere koordgebieden te evalueren.

| Type instructie | Voorbeelden |
| -------------- | -------- |
| Logisch | `and`, `or`, `not` |
| Inclusief/exclusief | `include`, `must` `exist`, `exclude`, `must not exist` |
| Vergelijking | `equals`, `does not equal`, `contains`, `starts with` |

## Datumgegevens

Met datumgegevens kunt u op tijd gebaseerde context toewijzen aan uw segmentdefinities door specifieke begin- en einddatums te gebruiken of door datumrelevante instructies te gebruiken, zoals in de onderstaande tabel wordt getoond. Eén implementatie zou een publiek kunnen maken van klanten die op elk moment met uw merk hebben gewerkt *dit jaar* en is ook actief *binnen* de laatste dagen.

| Voorbeeldveld | Datum-relevante verklaringen | Tijdlijn |
| ------------- | ------------------------ | --------- |
| person.firstPurchase | `today`, `yesterday`, `this month`, `this year` | Relevant aan de dag werd de segmentdefinitie gebouwd. |
| person.lastPurchase | `in last`, `during`, `before`, `after`, `within` | Relevant binnen een bepaalde week/maand. |

## Experience Events

Als Adobe Experience Platform-schema: [!DNL XDM ExperienceEvents] expliciete en impliciete klanteninteractie registreren met [!DNL Platform]- geïntegreerde toepassingen, met inbegrip van een momentopname van het systeem op het tijdstip dat de interactie plaatsvond. [!DNL ExperienceEvents] Dit zijn feiten. Als dusdanig, zijn zij een gegevensbron beschikbaar aan u tijdens segmentdefinitie.

Zoals in de onderstaande tabel wordt getoond, worden gebeurtenisgegevens weergegeven met behulp van trefwoorden die het gedrag van gebeurtenissen verfijnen en gebeurteniskenmerken opgeven.

| Trefwoord | Gebruik |
| ------- | --- |
| Opnemen/uitsluiten | Beschrijft het gedrag van de gebeurtenis door het opnemen of weglaten van gegevens. |
| Alle | Helpt het aantal kwalificerende segmentdefinities te bepalen. |
| Knop Tijdregel toepassen | Bevat datumgegevens. |
| Gelijk aan, niet gelijk aan, begint met, niet met, eindigt niet met, eindigt niet met, bevat, bevat, niet bevat, bestaat, niet bestaat | Bevat tekenreeksgegevens. |

### Doelgroepen delen

Het externe publiek kan ook als componenten van een nieuwe segmentdefinitie worden gebruikt, toevoegend hun attributenregels aan de nieuwe segmentdefinities.

Momenteel wordt alleen Adobe Audience Manager ondersteund als een extern publiek, waarbij in de toekomst extra bronnen worden ingeschakeld. Meer informatie over het gebruik van Adobe Audience Manager-soorten publiek met Platform vindt u in de [Handleiding voor het delen van publiek in de Adobe Audience Manager-documentatie](https://experienceleague.adobe.com/docs/audience-manager/user-guide/implementation-integration-guides/integration-experience-platform/aam-aep-audience-sharing.html).

### Delen van segmentdefinitie

Segmentdefinities die in Platform zijn gemaakt, kunnen binnen andere definities worden gebruikt [Adobe Experience Cloud Core Services](https://experienceleague.adobe.com/docs/core-services/interface/experience-cloud.html). Om deze functie in te schakelen, dient u contact op te nemen met uw oplossingsarchitect of uw consultant.

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
