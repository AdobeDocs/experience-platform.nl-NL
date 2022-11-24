---
title: Opmerkingen bij de release van Adobe Experience Platform
description: De meest recente releaseopmerkingen voor Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f8e8ec0fb13fc988d47bb3bbe85f953e66b33f13
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 1%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 23 november 2022**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensverzameling](#data-collection)
- [Experience Data Model (XDM)](#xdm)
- [Bronnen](#sources)

## Gegevensverzameling {#data-collection}

Adobe Experience Platform biedt een reeks technologieën waarmee u gegevens over klantervaringen aan de clientzijde kunt verzamelen en naar het Adobe Experience Platform Edge Network kunt verzenden waar deze kunnen worden verrijkt, getransformeerd en gedistribueerd naar Adobe- of niet-Adobe-bestemmingen.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| [!DNL AWS] extensie voor het doorsturen van gebeurtenissen | U kunt nu gegevens verzenden naar [!DNL Amazon Web Services] ([!DNL AWS]) met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL AWS] extensieoverzicht](../../tags/extensions/server/aws/overview.md) voor meer informatie . |
| [!DNL Google Ads Enhanced Conversions] extensie voor het doorsturen van gebeurtenissen | U kunt nu conversiegegevens verzenden naar [!DNL Google Ads] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Google Ads Enhanced Conversions] extensieoverzicht](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md) voor meer informatie . |
| [!DNL Microsoft Azure] extensie voor het doorsturen van gebeurtenissen | U kunt nu gegevens verzenden naar [!DNL Microsoft Azure] met een [gebeurtenis doorsturen](../../tags/ui/event-forwarding/overview.md) extensie. Zie de [[!DNL Microsoft Azure] extensieoverzicht](../../tags/extensions/server/azure/overview.md) voor meer informatie . |

Voor meer informatie over de mogelijkheden van de gegevensinzameling van het Platform, zie [overzicht van gegevensverzameling](../../collection/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Nieuwe of bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Velden toewijzen aan aangepaste klassen wanneer deze rechtstreeks aan een schema worden toegevoegd | Wanneer [een afzonderlijk veld rechtstreeks aan een schema toevoegen](../../xdm/ui/resources/schemas.md#add-individual-fields), voorheen kon u het veld alleen aan een veldgroep toewijzen als bovenliggende bron. Naast veldgroepen kunt u nu [het veld toewijzen aan een aangepaste klasse](../../xdm/ui/resources/schemas.md#add-to-class) als bovenliggende bron. |

{style=&quot;table-layout:auto&quot;}

Voor meer informatie over XDM in Platform, zie [XDM System, overzicht](../../xdm/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren, terwijl u die gegevens kunt structureren, labelen en verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- | 
| Beta beschikbaarheid van Oracle Service Cloud-bron | Gebruik de Cloud-bron van de service Oracle om gegevens van uw Oracle Service Cloud-account in te voeren naar Experience Platform. Voor meer informatie leest u de documentatie op het tabblad [Cloud-bron voor oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md). |

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).