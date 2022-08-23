---
title: Opmerkingen bij de release van Adobe Experience Platform, augustus 2022
description: De release van augustus 2022 bevat opmerkingen voor Adobe Experience Platform.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 24 augustus 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensprep](#data-prep)
- [Bronnen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] staat gegevensingenieurs toe om, gegevens aan en van het Model van Gegevens van de Ervaring in kaart te brengen om te zetten en te bevestigen (XDM).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor het opnemen van records met waarschuwingen | Met Data Prep worden nu waarschuwingen (niet-kritieke fouten) gelokaliseerd voor de velden en kan de rest van de rij worden ingevoegd. Alle maptransformatiefouten worden nu gerapporteerd als waarschuwingen en rijen die gedeeltelijk worden ingepakt, worden als geslaagd beschouwd, met een waarschuwing.  De bewaking wordt ook ondersteund in registers met waarschuwingen en diagnostische details. Gedeeltelijke invoer van records met waarschuwingen is momenteel alleen beschikbaar voor streaming gegevens. Raadpleeg de documentatie over [opnemen, records met waarschuwingen](../../sources/tutorials/ui/monitor-streaming.md) voor meer informatie . |

{style=&quot;table-layout:auto&quot;}

Meer informatie over [!DNL Data Prep], zie de [[!DNL Data Prep] overzicht](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Nieuwe functies**

| Functie | Beschrijving |
| --- | --- |
| Ondersteuning voor verschillende regio&#39;s van Adobe Analytics-bronnen | U kunt nu rapportsuites uit om het even welke regio (Verenigde Staten, Verenigd Koninkrijk, of Singapore) opnemen. Rapportsuites moeten worden toegewezen aan dezelfde organisatie als de Sandbox-instantie van het Experience Platform waarin de bronverbinding wordt gemaakt. Zie de handleiding voor meer informatie over [een Adobe Analytics-bronverbinding maken in de gebruikersinterface](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Zie voor meer informatie over bronnen de [overzicht van bronnen](../../sources/home.md).
