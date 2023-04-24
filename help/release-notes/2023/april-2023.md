---
title: Opmerkingen bij de release van Adobe Experience Platform, april 2023
description: In de releaseopmerkingen van april 2023 voor Adobe Experience Platform.
source-git-commit: 9f50ca4b2a4c576af5ce8ee5c085a7603fed2560
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 april 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Gegevensvoorbereiding](#data-prep)
- [Bronnen](#sources)

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates van de back-upperiode voor Adobe Analytics in niet-productiesandboxen | De periode voor het terugvullen van Adobe Analytics in niet voor de productie bestemde sandboxen is teruggebracht tot drie maanden. De back-up van productiesandboxen blijft na 13 maanden ongewijzigd. Deze wijziging geldt alleen voor nieuwe stromen en heeft geen invloed op bestaande stromen. Lees voor meer informatie de [Adobe Analytics-overzicht](../../sources/connectors/adobe-applications/analytics.md). |
| Nieuwe mapfunctie om FPID-tekenreeksen om te zetten in ECID | Gebruik de `fpid_to_ecid` FPID-tekenreeksen converteren naar ECID voor gebruik in Experience Platform- en Experience Cloud-toepassingen. Lees voor meer informatie de [Handleiding voor functies Data Prep](../../data-prep/functions.md). |

{style="table-layout:auto"}

Voor meer informatie over Data Prep, gelieve te lezen [Overzicht van Data Prep](../../data-prep/home.md).

## Bronnen {#sources}

Adobe Experience Platform kan gegevens uit externe bronnen invoeren en maakt het mogelijk die gegevens te structureren, te labelen en te verbeteren met behulp van services voor Platforms. U kunt gegevens van een verscheidenheid van bronnen zoals Adobe toepassingen, op wolk-gebaseerde opslag, derdesoftware, en uw systeem van CRM opnemen.

Experience Platform biedt een RESTful-API en een interactieve UI waarmee u eenvoudig bronverbindingen voor verschillende gegevensproviders kunt instellen. Deze bronverbindingen staan u toe om met externe opslagsystemen en de diensten van CRM voor authentiek te verklaren en te verbinden, tijden voor ingestiingslooppas te plaatsen, en gegevensinvoer te beheren.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| API steun voor het filtreren van rij-vlakke gegevens voor de Dynamica van Microsoft, Salesforce CRM, en Marketing Cloud Salesforce | Gebruik logische operatoren en vergelijkingsoperatoren om gegevens op rijniveau te filteren voor de bronnen van de Marketing Cloud Microsoft Dynamics, Salesforce CRM en Salesforce. Lees de handleiding op [gegevens filteren voor een bron met behulp van de API](../../sources/tutorials/api/filter.md) voor meer informatie . |
| Beta beschikbaarheid van Shopify Streaming | De [Streaming bron optimaliseren](../../sources/connectors/ecommerce/shopify-streaming.md) is nu beschikbaar in bèta. Gebruik de Shopify Streaming bron om gegevens van uw Shopify partnerrekening aan Experience Platform te stromen. |
| Algemene beschikbaarheid van OneTrust Integration | De [OneTrust Integration-bron](../../sources/connectors/consent-and-preferences/onetrust.md) is nu GA. Gebruik de OneTrust Integration-bron om toestemmings- en voorkeursgegevens van uw OneTrust Integration-account naar Experience Platform te verzenden. |
| Algemene beschikbaarheid van Oracle Service Cloud | De [Cloud-bron voor oracle Service](../../sources/connectors/customer-success/oracle-service-cloud.md) is nu GA. Gebruik de Cloud-bron van de service Oracle om uw Oracle Service Cloud-gegevens naar het Experience Platform te brengen. |

{style="table-layout:auto"}

Voor meer informatie over bronnen leest u de [overzicht van bronnen](../../sources/home.md).
