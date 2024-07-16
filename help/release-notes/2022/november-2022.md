---
title: Opmerkingen bij de release van Adobe Experience Platform november 2022
description: De release van november 2022 bevat notities voor Adobe Experience Platform.
exl-id: 1048cfae-6e7a-4d05-a004-c5c095a17fc4
source-git-commit: ccfc46714069e8c29f1777dea5ba73e318c0a4a6
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: donderdag 23 november 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar de Adobe Experience Platform-Edge Network kunt sturen waar deze verrijkt, getransformeerd en gedistribueerd kan worden naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| [!DNL AWS] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens [!DNL Amazon Web Services] ([!DNL AWS]) nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL AWS]  uitbreidingsoverzicht ](../../tags/extensions/server/aws/overview.md) voor meer informatie. |
| [!DNL Google Ads Enhanced Conversions] extensie voor het doorsturen van gebeurtenissen | U kunt omzettingsgegevens aan [!DNL Google Ads] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Google Ads Enhanced Conversions]  uitbreidingsoverzicht ](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor meer informatie. |
| [!DNL Microsoft Azure] extensie voor het doorsturen van gebeurtenissen | U kunt gegevens aan [!DNL Microsoft Azure] nu verzenden gebruikend een [ gebeurtenis die ](../../tags/ui/event-forwarding/overview.md) uitbreiding door:sturen. Zie het [[!DNL Microsoft Azure]  uitbreidingsoverzicht ](../../tags/extensions/server/azure/overview.md) voor meer informatie. |

Voor meer informatie over de mogelijkheden van de de gegevensinzameling van het Platform, zie het [ overzicht van de gegevensinzameling ](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe of bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- |
| Velden toewijzen aan aangepaste klassen wanneer deze rechtstreeks aan een schema worden toegevoegd | Wanneer [ toevoegend direct een individueel gebied aan een schema ](../../xdm/ui/resources/schemas.md#add-individual-fields), eerder kon u het gebied aan een gebiedsgroep als zijn oudermiddel slechts toewijzen. Nu, naast gebiedsgroepen, kunt u [ het gebied aan een douaneklasse ](../../xdm/ui/resources/schemas.md#add-to-class) als zijn oudermiddel in plaats daarvan toewijzen. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, zie het [ XDM overzicht van het Systeem ](../../xdm/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van de platformservices. U kunt gegevens van een verscheidenheid van bronnen zoals de toepassingen van de Adobe, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte eigenschappen**

| Functie | Beschrijving |
| --- | --- | 
| Beta-beschikbaarheid van Oracle Service Cloud-bron | Gebruik de Cloud-bron van de service Oracle om gegevens van uw Oracle Service Cloud-account in te voeren naar Experience Platform. Voor meer informatie, lees de documentatie over de [ bron van de Wolk van de Dienst van het Oracle ](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Meer over bronnen leren, lees het [ overzicht van bronnen ](../../sources/home.md).
