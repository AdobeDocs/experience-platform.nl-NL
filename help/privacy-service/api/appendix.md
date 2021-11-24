---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Bijlage Privacy Service API-handleiding
topic-legacy: developer guide
description: Dit document bevat aanvullende informatie voor het werken met de Privacy Service-API.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 445c8158dbf012defb32e9cd7aa4c27c6be1fb88
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 3%

---

# Handleiding Privacy Service-API

De volgende secties bevatten aanvullende informatie voor het werken met de Adobe Experience Platform Privacy Service API.

## Standaardnaamruimten {#standard-namespaces}

Alle identiteiten waarnaar wordt verzonden [!DNL Privacy Service] moet worden opgegeven onder een specifieke naamruimte voor identiteiten. Identiteitsnaamruimten zijn een component van [Adobe Experience Platform Identity Service](../../identity-service/home.md) die de context aangeven waarop een identiteit betrekking heeft.

In de volgende tabel worden diverse veelgebruikte, vooraf gedefinieerde identiteitstypen weergegeven die beschikbaar zijn gesteld door [!DNL Experience Platform], samen met de bijbehorende `namespace` waarden:

| Identiteitstype | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | `Email` | `6` |
| Telefoon | `Phone` | `7` |
| Adobe Advertising Cloud-id | `AdCloud` | `411` |
| Adobe Audience Manager UUID | `CORE` | `0` |
| Adobe Experience Cloud-id | `ECID` | `4` |
| Adobe Target-id | `TNTID` | `9` |
| [!DNL Apple] ID voor adverteerders | `IDFA` | `20915` |
| [!DNL Google] ID advertentie | `GAID` | `20914` |
| [!DNL Windows] STEUN | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Elk identiteitstype heeft ook een `namespaceId` geheel getal, dat kan worden gebruikt in plaats van de waarde `namespace` tekenreeks bij het instellen van de identiteit `type` eigenschap aan &quot;namespaceId&quot;. Zie de sectie over [naamruimtetekens](#namespace-qualifiers) voor meer informatie .

U kunt een lijst met naamruimten ophalen die door uw organisatie worden gebruikt door een GET-aanvraag in te dienen bij de `idnamespace/identities` in de [!DNL Identity Service] API. Zie de [Handleiding voor ontwikkelaars van Identity Service](../../identity-service/api/getting-started.md) voor meer informatie .

## Naamruimtetekens

Wanneer u een `namespace` in de [!DNL Privacy Service] API, a **naamruimtekwalificatie** moet in een overeenkomstige `type` parameter. In de volgende tabel worden de verschillende geaccepteerde naamruimtetekens weergegeven.

| Kwalificatie | Definitie |
| --------- | ---------- |
| `standard` | Een van de standaard naamruimten die globaal is gedefinieerd en niet is gekoppeld aan een afzonderlijke gegevensset van de organisatie (bijvoorbeeld e-mail, telefoonnummer, enz.). Naamruimte-id is opgegeven. |
| `custom` | Een unieke naamruimte die is gemaakt in de context van een organisatie en die niet wordt gedeeld door de [!DNL Experience Cloud]. De waarde vertegenwoordigt de vriendschappelijke naam (&quot;naam&quot;gebied) moet worden gezocht naar. Naamruimte-id is opgegeven. |
| `integrationCode` | De code van de integratie - gelijkend op &quot;douane&quot;, maar specifiek bepaald als integratiecode van een gegevensbron die moet worden gezocht. Naamruimte-id is opgegeven. |
| `namespaceId` | Geeft aan dat de waarde de werkelijke id is van de naamruimte die is gemaakt of toegewezen via de naamruimteservice. |
| `unregistered` | Een vrije-vormkoord dat niet in de namespaceservice wordt bepaald en &quot;zoals is&quot;genomen. Om het even welke toepassing die deze soorten namespaces behandelt controleert tegen hen en behandelt als aangewezen voor de bedrijfcontext en gegevensreeks. Er is geen naamruimte-id opgegeven. |
| `analytics` | Een aangepaste naamruimte die intern is toegewezen in [!DNL Analytics], niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |
| `target` | Een aangepaste naamruimte die intern wordt begrepen door [!DNL Target], niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |

{style=&quot;table-layout:auto&quot;}

## Geaccepteerde productwaarden

In de volgende tabel worden de toegestane waarden voor het opgeven van een Adobe-product in de `include` kenmerk van een aanvraag voor het maken van een baan.

| Product | Waarde voor gebruik in de `include` attribute |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Primetime-verificatie | `primetimeAuthentication` |
| Adobe Target | `target` |
| Automatiseringsproduct | `automationProduct` |
| Klantkenmerken (CRS) | `CRS` |
| Identiteitsservice | `Identity` |
| Klantprofiel in realtime | `profileService` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
