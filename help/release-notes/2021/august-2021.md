---
title: Opmerkingen bij de release van Adobe Experience Platform
description: Opmerkingen bij de release van Experience Platform voor 25 augustus 2021.
doc-type: release notes
last-update: August 25, 2021
author: ens28527
source-git-commit: bd3d60e1960b1f4c32ade8c4070d7c1b01e5ba07
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 3%

---


# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 25 augustus 2021**

Updates voor bestaande functies in Adobe Experience Platform:

- [Waarnembaarheidsinzichten](#observability)
- [Klantprofiel in realtime](#profile)
- [Bronnen](#sources)

## Waarnembaarheidsinzichten {#observability}

Met behulp van observability Insights kunt u de activiteiten van Platforms volgen aan de hand van statistische gegevens en gebeurtenismeldingen.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Waarschuwingen | U kunt zich nu abonneren op belangrijke waarschuwingen met betrekking tot workflows die op het Platform worden uitgevoerd. Nadat u zich hebt geabonneerd op specifieke waarschuwingsregels, ontvangt u meldingen en e-mails in de gebruikersinterface wanneer een belangrijke levenscyclusgebeurtenis plaatsvindt (zoals het opnemen van gegevens) of als er problemen zijn die uw aandacht vereisen (zoals het mislukken van een innamestroom of het langer duren dan u had verwacht van een segmenttaak). Voor meer informatie, zie [alarm overzicht](../../observability/alerts/overview.md). |

Zie [Overzicht van de Inzichten van de Waarnembaarheid](../../observability/home.md) voor meer informatie over de dienst.

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

| Functie | Beschrijving |
| ------- | ----------- |
| Bladeren door profielen op samenvoegbeleid of identiteit | Wanneer u door profielen in Experience Platform bladert, kunt u nu door samenvoegbeleid bladeren om een voorvertoning weer te geven van 20 voorbeeldprofielen op basis van het geselecteerde samenvoegbeleid. U kunt ook op identiteit bladeren om naar een specifiek profiel te zoeken dat een naamruimte van de identiteit en verwante identiteitswaarde gebruikt. Voor meer informatie, zie [Realtime gids UI van het Profiel van de Klant](../../profile/ui/user-guide.md). |

Als u meer wilt weten over Real-time klantprofiel, inclusief zelfstudies en aanbevolen procedures voor het werken met profielgegevens, leest u eerst het [Real-time Customer Profile overview](../../profile/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

| Functie | Beschrijving |
| ------- | ----------- |
| Bronaansluiting voor lokale bestandsupload | De categorie voor het opnemen van bestanden is hernoemd naar het lokale systeem, zodat u lokale bestanden rechtstreeks naar het Platform kunt brengen via de lokale connector voor het uploaden van bestanden. De gegevens die door deze schakelaar worden opgenomen kunnen door het Dashboard van de Controle worden gecontroleerd. Zie het [overzicht van de bron voor het uploaden van lokale bestanden](../../sources/connectors/local-system/local-file-upload.md) voor meer informatie. |

Meer over bronnen leren, zie [bronnen overzicht](../../sources/home.md).
