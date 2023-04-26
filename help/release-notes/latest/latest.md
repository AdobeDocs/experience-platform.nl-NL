---
title: Aanvullende informatie over Adobe Experience Platform
description: In de release van maart 2023 staat Adobe Experience Platform vermeld.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 938b4ba7affadc7ad0eca086d7cc2c9ce1a54a83
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 2%

---

# Opmerkingen bij de release van Adobe Experience Platform

**Releasedatum: 26 april 2023**

Updates voor bestaande functies in Adobe Experience Platform:

- [Dashboards](#dashboards)
- [Gegevensvoorbereiding](#data-prep)
- [Experience Data Model](#xdm)
- [Klantprofiel in realtime](#profile)
- [Bronnen](#sources)

## Dashboards {#dashboards}

Adobe Experience Platform biedt meerdere dashboards waarmee u belangrijke inzichten over de gegevens van uw organisatie kunt bekijken, zoals vastgelegd tijdens dagelijkse momentopnamen.

**Nieuwe of bijgewerkte functies** {#dashboards-new-updated-features}

| Functie | Beschrijving |
| --- | --- |
| Door gebruiker gedefinieerde dashboards | U kunt nu **historische gegevens filteren** vanuit uw widgetinzichten en gebruik recente gegevens of een aangepaste analyseperiode.<br>U kunt nu ook **bestaande widgets dupliceren**. Door een duplicaat aan te passen en de kenmerken ervan te bewerken, kunt u voorkomen dat u bij het maken van een nieuwe, unieke widget opnieuw begint. |

{style="table-layout:auto"}

Voor meer informatie over dashboards, met inbegrip van hoe te om toegangstoestemmingen te verlenen en douanewidgets tot stand te brengen, begin door te lezen [overzicht van dashboards](../../dashboards/home.md).

## Gegevensvoorbereiding {#data-prep}

Met Data Prep kunnen gegevensengineers gegevens toewijzen, transformeren en valideren van en naar het XDM-model (Experience Data Model).

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Updates van de back-upperiode voor Adobe Analytics in niet-productiesandboxen | De periode voor het terugvullen van Adobe Analytics in niet voor de productie bestemde sandboxen is teruggebracht tot drie maanden. De back-up van productiesandboxen blijft na 13 maanden ongewijzigd. Deze wijziging geldt alleen voor nieuwe stromen en heeft geen invloed op bestaande stromen. Lees voor meer informatie de [Adobe Analytics-overzicht](../../sources/connectors/adobe-applications/analytics.md). |
| Nieuwe mapfunctie om FPID-tekenreeksen om te zetten in ECID | Gebruik de `fpid_to_ecid` FPID-tekenreeksen converteren naar ECID voor gebruik in Experience Platform- en Experience Cloud-toepassingen. Lees voor meer informatie de [Handleiding voor functies Data Prep](../../data-prep/functions.md). |

{style="table-layout:auto"}

Voor meer informatie over Data Prep, gelieve te lezen [Overzicht van Data Prep](../../data-prep/home.md).

## Experience Data Model (XDM) {#xdm}

XDM is een open-bronspecificatie die gemeenschappelijke structuren en definities (schema&#39;s) voor gegevens verstrekt die in Adobe Experience Platform worden gebracht. Door zich aan de normen van XDM te houden, kunnen alle gegevens van de klantenervaring in een gemeenschappelijke vertegenwoordiging worden opgenomen om inzichten op een snellere, meer geïntegreerde manier te leveren. U kunt waardevolle inzichten van klantenacties bereiken, klantenpubliek door segmenten bepalen, en klantenattributen voor verpersoonlijkingsdoeleinden gebruiken.

**Bijgewerkte functies**

| Functie | Beschrijving |
| --- | --- |
| Schakelen tussen weergavenamen | De Schema-editor biedt nu een schakeloptie tussen de oorspronkelijke veldnamen en de meer leesbare weergavenamen. Dankzij deze flexibiliteit is het mogelijk uw schema&#39;s beter te detecteren en te bewerken. De weergavenamen voor standaardveldgroepen worden gegenereerd door het systeem, maar kunnen indien nodig ook via de gebruikersinterface worden aangepast. |

{style="table-layout:auto"}

Voor meer informatie over XDM in Platform, lees [XDM System, overzicht](../../xdm/home.md).

## Klantprofiel in realtime {#profile}

Met Adobe Experience Platform kunt u zorgen voor gecoördineerde, consistente en relevante ervaringen voor uw klanten, ongeacht waar of wanneer ze met uw merk communiceren. Met het Profiel van de Klant in real time, kunt u een holistische mening van elke individuele klant zien die gegevens van veelvoudige kanalen, met inbegrip van online, off-line, CRM, en derdegegevens combineert. Het profiel staat u toe om klantengegevens in een verenigde mening te consolideren die een actionable, timestamped rekening van elke klanteninteractie aanbiedt.

**Bijgewerkte functies**

| Functie | Beschrijving |
| ------- | ----------- |
| Vervaldatum van pseudoniem profielgegevens | De vervaldatum van pseudoniem profielgegevens is nu over het algemeen beschikbaar. Deze release verwijdert ononderbroken pseudoniem-profielen uit uw Experience Platform-exemplaar als deze zijn ingeschakeld. Lees voor meer informatie over deze functie en Pseudoniem-profielen de [Handleiding voor het verlopen van Pseudoniem-profielgegevens](../../profile/pseudonymous-profiles.md). |

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