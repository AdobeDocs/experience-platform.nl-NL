---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Geaccepteerde naamruimten en kwalificatietekens
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 7%

---


# Aanhangsel

## Standaardnaamruimten {#standard-namespaces}

Alle identiteiten waarnaar wordt verzonden, [!DNL Privacy Service] moeten worden opgegeven onder een specifieke naamruimte voor identiteiten. Identiteitsnaamruimten zijn een onderdeel van de [Adobe Experience Platform Identity Service](../../identity-service/home.md) dat de context aangeeft waarop een identiteit betrekking heeft.

In de volgende tabel worden diverse veelgebruikte, vooraf gedefinieerde identiteitstypen weergegeven die door [!DNL Experience Platform]en de bijbehorende `namespace` waarden beschikbaar zijn gesteld:

| Identiteitstype | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | Email | 6 |
| Telefoon | Telefoon | 7 |
| Adobe Advertising Cloud-id | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target-id | TNTID | 9 |
| [!DNL Apple] ID voor adverteerders | IDFA | 20915 |
| [!DNL Google] ID advertentie | GAID | 20914 |
| [!DNL Windows] STEUN | WAID | 8 |

>[!NOTE]
>
>Elk identiteitstype heeft ook een `namespaceId` geheel-getalwaarde, die in plaats van het `namespace` koord kan worden gebruikt wanneer het plaatsen van het bezit van de identiteit aan &quot;namespaceId&quot; `type` . Zie de sectie over [naamruimtetekens](#namespace-qualifiers) voor meer informatie.

U kunt een lijst van identiteitsnamespaces terugwinnen die door uw organisatie wordt gebruikt door een verzoek van de GET tot het `idnamespace/identities` eindpunt in [!DNL Identity Service] API te richten. Zie de ontwikkelaarsgids [van de Dienst van de](../../identity-service/api/getting-started.md) Identiteit voor meer informatie.

## Naamruimtetekens

Wanneer u een `namespace` waarde opgeeft in de [!DNL Privacy Service] API, moet een **naamruimtekwalificatie** worden opgenomen in een bijbehorende `type` parameter. In de volgende tabel worden de verschillende geaccepteerde naamruimtetekens weergegeven.

| Kwalificatie | Definitie |
| --------- | ---------- |
| standaard | Een van de standaard naamruimten die globaal is gedefinieerd en niet is gekoppeld aan een afzonderlijke gegevensset van de organisatie (bijvoorbeeld e-mail, telefoonnummer, enz.). Naamruimte-id is opgegeven. |
| aangepast | Een unieke naamruimte die is gemaakt in de context van een organisatie en die niet wordt gedeeld door de [!DNL Experience Cloud]organisatie. De waarde vertegenwoordigt de vriendschappelijke naam (&quot;naam&quot;gebied) moet worden gezocht naar. Naamruimte-id is opgegeven. |
| integrationCode | De code van de integratie - gelijkend op &quot;douane&quot;, maar specifiek bepaald als integratiecode van een gegevensbron die moet worden gezocht. Naamruimte-id is opgegeven. |
| namespaceId | Geeft aan dat de waarde de werkelijke id is van de naamruimte die is gemaakt of toegewezen via de naamruimteservice. |
| niet geregistreerd | Een vrije-vormkoord dat niet in de namespaceservice wordt bepaald en &quot;zoals is&quot;genomen. Om het even welke toepassing die deze soorten namespaces behandelt controleert tegen hen en behandelt als aangewezen voor de bedrijfcontext en gegevensreeks. Er is geen naamruimte-id opgegeven. |
| analyse | Een aangepaste naamruimte die intern wordt toegewezen in, [!DNL Analytics]niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |
| target | Een aangepaste naamruimte die intern wordt begrepen, [!DNL Target]niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |

## Geaccepteerde productwaarden

In de volgende tabel worden de geaccepteerde waarden weergegeven voor het opgeven van een Adobe-product in het `include` kenmerk van een aanvraag voor het maken van een taak.

| Product | Waarde voor gebruik in het `include` kenmerk |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Adobe Primetime-verificatie | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Customer Record-service | &quot;CRS&quot; |
| Klantprofiel in realtime | &quot;ProfileService&quot; |