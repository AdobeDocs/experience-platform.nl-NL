---
keywords: Experience Platform;startpagina;populaire onderwerpen
solution: Experience Platform
title: Bijlage Privacy Service API-handleiding
description: Dit document bevat aanvullende informatie voor het werken met de Privacy Service API.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 3%

---

# Handleiding Privacy Service API

De volgende secties bevatten aanvullende informatie voor het werken met de Adobe Experience Platform Privacy Service API.

## Standaardnaamruimten {#standard-namespaces}

Alle identiteiten die naar [!DNL Privacy Service] worden verzonden, moeten onder een specifieke naamruimte worden opgegeven. Identiteitsnaamruimten zijn een component van [ Dienst van de Identiteit van Adobe Experience Platform ](../../identity-service/home.md) die op de context wijzen waarop een identiteit betrekking heeft.

De volgende tabel bevat een overzicht van diverse veelgebruikte, vooraf gedefinieerde identiteitstypen die door [!DNL Experience Platform] beschikbaar worden gesteld, samen met de bijbehorende `namespace` -waarden:

| Identiteitstype | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | `Email` | `6` |
| Telefoon | `Phone` | `7` |
| Adobe Advertising-id | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud-id | `ECID` | `4` |
| Adobe Target-id | `TNTID` | `9` |
| [!DNL Apple] ID voor adverteerders | `IDFA` | `20915` |
| [!DNL Google] Advertentie-id | `GAID` | `20914` |
| [!DNL Windows] STEUN | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Elk identiteitstype heeft ook een `namespaceId` geheel-getalwaarde, die kan worden gebruikt in plaats van de `namespace` -tekenreeks wanneer de eigenschap `type` van de identiteit wordt ingesteld op &quot;namespaceId&quot;. Zie de sectie op [ namespace kwalificfiers ](#namespace-qualifiers) voor meer informatie.

U kunt een lijst ophalen met naamruimten die door uw organisatie worden gebruikt door een GET-aanvraag in te dienen bij het eindpunt `idnamespace/identities` in de [!DNL Identity Service] API. Zie de [ de ontwikkelaarsgids van de Dienst van de Identiteit ](../../identity-service/api/getting-started.md) voor meer informatie.

## Naamruimtetekens {#namespace-qualifiers}

Wanneer het specificeren van a `namespace` waarde in [!DNL Privacy Service] API, a **namespace kwalificfier** moet in een overeenkomstige `type` parameter worden omvat. In de volgende tabel worden de verschillende geaccepteerde naamruimtetekens weergegeven.

| Kwalificatie | Definitie |
| --------- | ---------- |
| `standard` | Een van de standaard naamruimten die globaal is gedefinieerd en niet is gekoppeld aan een afzonderlijke gegevensset van de organisatie (bijvoorbeeld e-mail, telefoonnummer, enz.). Naamruimte-id is opgegeven. |
| `custom` | Een unieke naamruimte die is gemaakt in de context van een organisatie en die niet wordt gedeeld door de [!DNL Experience Cloud] . De waarde vertegenwoordigt de vriendschappelijke naam (&quot;naam&quot;gebied) moet worden gezocht naar. Naamruimte-id is opgegeven. |
| `integrationCode` | De code van de integratie - gelijkend op &quot;douane&quot;, maar specifiek bepaald als integratiecode van een gegevensbron die moet worden gezocht. Naamruimte-id is opgegeven. |
| `namespaceId` | Geeft aan dat de waarde de werkelijke id is van de naamruimte die is gemaakt of toegewezen via de naamruimteservice. |
| `unregistered` | Een vrije-vormkoord dat niet in de namespaceservice wordt bepaald en &quot;zoals is&quot;genomen. Om het even welke toepassing die deze soorten namespaces behandelt controleert tegen hen en behandelt als aangewezen voor de bedrijfcontext en gegevensreeks. Er is geen naamruimte-id opgegeven. |
| `analytics` | Een aangepaste naamruimte die intern wordt toegewezen in [!DNL Analytics] , niet in de naamruimtenservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |
| `target` | Een aangepaste naamruimte die intern wordt begrepen door [!DNL Target] , niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |

{style="table-layout:auto"}

## Geaccepteerde productwaarden {#accepted-product-values}

In deze sectie worden de waarden van de product-id weergegeven die in het kenmerk `include` worden geaccepteerd bij het maken van Privacy Service-taken (API of UI). Gebruik deze waarden in de `include` -array van uw taakaanvraag.

De volgende lijst maakt een lijst van de gesteunde producten, hun UI vertoningsnamen, en hun overeenkomstige codewaarden.

>[!NOTE]
>
>- Productwaarden zijn niet hoofdlettergevoelig. Voor de consistentie wordt een kamelentaal aanbevolen.
>- Alleen de hierboven vermelde producten worden ondersteund in de gebruikersinterface en de API. Als een product niet is voorzien voor uw organisatie, kan het worden genegeerd of een bevestigingsfout-verwijs naar uw contract van Adobe of leveringsdocumentatie om recht te bevestigen veroorzaken.

| Benoemde productnaam | Weergavenaam gebruikersinterface | `include` value |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (Profile Store) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform (data Lake) | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| Klantkenmerken | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| Identiteitsservice | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
