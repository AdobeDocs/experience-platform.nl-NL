---
title: Ondersteunde gebruiksgevallen met de Adobe Experience Platform Web SDK
description: Leer welke gebruiksgevallen worden ondersteund met de Adobe Experience Platform Web SDK.
keywords: web sdk;use cases
exl-id: e0643c2c-ceb3-4ea2-aafa-1e18e0c66453
source-git-commit: ed092b85d74eaa0fdc29f3a8d28f84fe81ccca17
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 10%

---

# Ondersteunde gebruiksgevallen

Deze pagina maakt een lijst van de gesteunde gebruiksgevallen voor Web SDK, met verbindingen aan extra informatie.

## Algemeen

| Gebruiksscenario | Meer informatie |
| --- | --- |
| Enkele gestroomlijnde SDK |  |
| Globaal netwerk voor gegevensverzameling |  |
| Cursustoestemming |  |
| Verzamel toestemming van de klant volgens verschillende normen | <ul><li>[Adobe-ondersteuning 2.0](../../landing/governance-privacy-security/consent/adobe/overview.md)</li><li>[IAB TCF 2.0-ondersteuning](../../landing/governance-privacy-security/consent/iab/overview.md)</li><li>[Integreer SDK om toestemmingssignalen naar het Netwerk van Edge te verzenden](../../landing/governance-privacy-security/consent/sdk.md)</li></ul> |
| ECID-ondersteuning | Zie de documentatie [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#first-party-identity) en [hier](https://experienceleague.adobe.com/docs/experience-platform/edge/extension/accessing-the-ecid.html?lang=en#extension) voor informatie over het ophalen van de ECID |
| Meerdere entiteiten verzamelen |  |
| Ondersteuning voor apparaatgrafiek (openbaar/privé) | [Documentatie](https://experienceleague.adobe.com/docs/analytics/components/cda/device-graph.html?lang=en) |
| Gegevens verzenden naar meerdere organen op de pagina | [Documentatie](./interacting-with-multiple-properties.md) |
| Gedetailleerde foutmeldingen en logbestanden |  |
| Traceerverzoeken om client en server |  |
| tagextensie | [Web SDK-uitbreidingsdocumenten](../../tags/extensions/web/sdk/overview.md) |
| Foutopsporingsgereedschappen beschikbaar | [Foutopsporingsextensie ](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) en  [Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon) |

{style=&quot;table-layout:auto&quot;}

## Adobe Experience Platform

| Gebruiksscenario | Meer informatie |
| --- | --- |
| Gebeurtenissen verzenden |  |
| offer decisioning | [Documentatie](../personalization/offer-decisioning/offer-decisioning-overview.md) |
| Als dataset voor profiel wordt toegelaten, capaciteit om gegevens naar het Profiel van de Gegevens van de Klant in real time in real time te verzenden |  |
| Gegevens in realtime naar Customer Journey Analytics verzenden |  |
| Goedkeuring voor profiel schrijven | [Documentatie](../../landing/governance-privacy-security/consent/sdk.md) |
| Gegevensserver-kant in real-time doorsturen naar derden | [Documentatie](../../tags/ui/event-forwarding/overview.md) |
| Ondersteuning voor naamruimte van identiteit |  |

{style=&quot;table-layout:auto&quot;}

## Adobe Analytics

| Gebruiksscenario | Meer informatie |
| --- | --- |
| Analyses voor doel (A4T) |  |
| Geen analyse voor doellatentie (A4T) |  |
| Tags toevoegen met meerdere suite |  |
| Bot filteren |  |
| Props, eVars en gebeurtenissen |  |
| ListVar-ondersteuning voor Adobe Analytics |  |
| Versie van besturingssysteem en browser |  |
| Variabelen van het type Out-of-the-box | [Automatisch toegewezen variabelen](../data-collection/adobe-analytics/automatically-mapped-vars.md) |
| VISTA-regels/verwerkingsregels |  |
| Ondersteuning voor bezoekerkenmerken |  |
| Ondersteuning voor Afsluiten |  |
| Aangepaste koppelingen/downloadkoppelingen |  |
| Status en handeling bijhouden |  |
| Serienummering voor gebeurtenissen van het type Standaard |  |
| Variabele voor producten | [Documentatie](../data-collection/collect-commerce-data.md#actions-related-to-products) |

{style=&quot;table-layout:auto&quot;}

## Adobe Target

| Gebruiksscenario | Meer informatie |
| --- | --- |
| Alle activiteitstypen |  |
| Ondersteuning van native en SPA Visual Experience Composer | [Documentatie](../personalization/adobe-target/spa-implementation.md) |
| Op formulieren gebaseerde composer |  |
| Ondersteuning voor algemene box | [Documentatie](../personalization/rendering-personalization-content.md#automatically-rendering-content) |
| Aangepaste vakjes | [Documentatie](../personalization/rendering-personalization-content.md#manually-rendering-content) |
| Analyses voor doel (A4T) |  |
| Omgevingsondersteuning |  |
| Werkruimteresupport |  |
| QA-koppelingen in Adobe Target |  |
| Doel gebaseerd op geo/apparaat in Adobe Target |  |
| Ondersteuning voor bezoekerkenmerken |  |
| Profielscripts |  |
| XDM wordt mbox-parameters |  |
| Aanbiedingen doorsturen die worden ondersteund met A4T-rapportage | [Documentatie](https://experienceleague.adobe.com/docs/target/using/experiences/offers/offer-redirect.html?lang=en) |
| Het doelprofiel bijwerken | [Documentatie](../personalization/adobe-target/target-overview.md#single-profile-update) |
| Aanbevelingen |  |
| mBox-id van derden |  |
| Reactietokens | [Documentatie](../personalization/adobe-target/accessing-response-tokens.md) |

{style=&quot;table-layout:auto&quot;}

## Adobe Audience Manager

| Gebruiksscenario | Meer informatie |
| --- | --- |
| Audience Analytics |  |
| Delen van segmenten naar Adobe Analytics |  |
| Ondersteuning voor bezoekerkenmerken |  |
| Partnersynchronisaties |  |
| URL-doelen |  |
| Cookie-bestemmingen |  |
| Omgevingsondersteuning |  |
| Adobe Experience Platform-naamruimten synchroniseren met Audience Manager-gegevensbronnen |  |
| Geverifieerde of bekende id&#39;s |  |

{style=&quot;table-layout:auto&quot;}
