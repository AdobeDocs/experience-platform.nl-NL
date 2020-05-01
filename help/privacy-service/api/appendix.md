---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Geaccepteerde naamruimten en kwalificatietekens
topic: developer guide
translation-type: tm+mt
source-git-commit: cc296670db91640e75fd7a47b874a46eaf57ecde

---


# Aanhangsel

## Standaardnaamruimten {#standard-namespaces}

Alle identiteiten die naar de Privacy Service worden verzonden moeten onder een specifieke naamruimte worden verstrekt. Identiteitsnaamruimten zijn een onderdeel van de [Adobe Experience Platform Identity Service](../../identity-service/home.md) dat de context aangeeft waarop een identiteit betrekking heeft.

In de volgende tabel worden diverse veelgebruikte, vooraf gedefinieerde identiteitstypen weergegeven die door het Experience Platform beschikbaar zijn gesteld, samen met de bijbehorende `namespace` waarden:

| Identiteitstype | `namespace` | `namespaceId` |
| --- | --- | --- |
| E-mail | E-mail | 6 |
| Telefoon | Telefoon | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| UUID Adobe Audience Manager | CORE | 0 |
| Adobe Experience Cloud-id | ECID | 4 |
| Adobe Target-id | TNTID | 9 |
| Apple ID for Advertisers | IDFA | 20915 |
| Google-advertentie-id | GAID | 20914 |
| Windows-ID | WAID | 8 |

>[!NOTE] Elk identiteitstype heeft ook een `namespaceId` geheel-getalwaarde, die in plaats van het `namespace` koord kan worden gebruikt wanneer het plaatsen van het bezit van de identiteit aan &quot;namespaceId&quot; `type` . Zie de sectie over [naamruimtetekens](#namespace-qualifiers) voor meer informatie.

U kunt een lijst van identiteitsnamespaces in gebruik door uw organisatie terugwinnen door een GET verzoek aan het `idnamespace/identities` eindpunt in de Dienst API van de Identiteit te doen. Zie de ontwikkelaarsgids [van de Dienst van de](../../identity-service/api/getting-started.md) Identiteit voor meer informatie.

## Naamruimtetekens

Wanneer het specificeren van een `namespace` waarde in de Dienst API van de Privacy, moet een **namespace kwalificfier** in een overeenkomstige `type` parameter worden omvat. In de volgende tabel worden de verschillende geaccepteerde naamruimtetekens weergegeven.

| Kwalificatie | Definitie |
| --------- | ---------- |
| standaard | Een van de standaard naamruimten die globaal is gedefinieerd en niet is gekoppeld aan een afzonderlijke gegevensset van de organisatie (bijvoorbeeld e-mail, telefoonnummer, enz.). Naamruimte-id is opgegeven. |
| aangepast | Een unieke naamruimte die is gemaakt in de context van een organisatie en die niet wordt gedeeld via de Experience Cloud. De waarde vertegenwoordigt de vriendschappelijke naam (&quot;naam&quot;gebied) moet worden gezocht naar. Naamruimte-id is opgegeven. |
| integrationCode | De code van de integratie - gelijkend op &quot;douane&quot;, maar specifiek bepaald als integratiecode van een gegevensbron die moet worden gezocht. Naamruimte-id is opgegeven. |
| namespaceId | Geeft aan dat de waarde de werkelijke id is van de naamruimte die is gemaakt of toegewezen via de naamruimteservice. |
| niet geregistreerd | Een vrije-vormkoord dat niet in de namespaceservice wordt bepaald en &quot;zoals is&quot;genomen. Om het even welke toepassing die deze soorten namespaces behandelt controleert tegen hen en behandelt als aangewezen voor de bedrijfcontext en gegevensreeks. Er is geen naamruimte-id opgegeven. |
| analyse | Een aangepaste naamruimte die intern wordt toegewezen in Analytics, niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |
| target | Een aangepaste naamruimte die intern wordt begrepen door Doel, niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |

## Geaccepteerde productwaarden

In de volgende tabel worden de geaccepteerde waarden weergegeven voor het opgeven van een Adobe-product in het `include` kenmerk van een aanvraag voor het maken van taken.

| Product | Waarde voor gebruik in het `include` kenmerk |
--- | ---
| Adobe Advertizing Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe-campagne | &quot;Campagne&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime-verificatie | &quot;primetimeAuthentication&quot; |
| Adobe-doel | &quot;Doel&quot; |
| Customer Record-service | &quot;CRS&quot; |
| Klantprofiel in realtime | &quot;ProfileService&quot; |