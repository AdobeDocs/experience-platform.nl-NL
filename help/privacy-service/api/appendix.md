---
keywords: Experience Platform;home;populaire onderwerpen
solution: Experience Platform
title: Handleiding Privacy Service API-ontwikkelaar
topic: developer guide
description: Dit document bevat aanvullende informatie voor het werken met de Privacy Service-API.
translation-type: tm+mt
source-git-commit: 5dad1fcc82707f6ee1bf75af6c10d34ff78ac311
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 6%

---


# Aanhangsel

De volgende secties bevatten aanvullende informatie voor het werken met de Adobe Experience Platform Privacy Service API.

## Standaard naamruimten {#standard-namespaces}

Alle identiteiten die naar [!DNL Privacy Service] worden verzonden moeten onder een specifieke identiteitsnaamruimte worden verstrekt. Identiteitsnaamruimten zijn een onderdeel van [Adobe Experience Platform Identity Service](../../identity-service/home.md) dat de context aangeeft waarop een identiteit betrekking heeft.

In de volgende tabel worden diverse veelgebruikte, vooraf gedefinieerde identiteitstypen weergegeven die door [!DNL Experience Platform] beschikbaar zijn gesteld, samen met de bijbehorende `namespace`-waarden:

| Identiteitstype | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | E-mail | 6 |
| Telefoon | Telefoon | 7 |
| Adobe Advertising Cloud-id | AdCloud | 411 |
| Adobe Audience Manager UUID | CORE | 0 |
| Adobe Experience Cloud-id | ECID | 4 |
| Adobe Target-id | TNTID | 9 |
| [!DNL Apple] ID voor adverteerders | IDFA | 20915 |
| [!DNL Google] ID advertentie | GAID | 20914 |
| [!DNL Windows] STEUN | WAID | 8 |

>[!NOTE]
>
>Elk identiteitstype heeft ook een `namespaceId` geheelwaarde, die in plaats van het `namespace` koord kan worden gebruikt wanneer het plaatsen van het `type` bezit van de identiteit aan &quot;namespaceId&quot;. Zie de sectie over [naamruimteaanduidingen](#namespace-qualifiers) voor meer informatie.

U kunt een lijst van identiteitsnamespaces terugwinnen die door uw organisatie door een GET verzoek aan het `idnamespace/identities` eindpunt in [!DNL Identity Service] API wordt gebruikt. Raadpleeg de [Handleiding voor ontwikkelaars van Identity Service](../../identity-service/api/getting-started.md) voor meer informatie.

## Naamruimtetekens

Wanneer u een `namespace`-waarde opgeeft in de [!DNL Privacy Service]-API, moet een **naamruimtekwalificatie** worden opgenomen in een corresponderende `type`-parameter. In de volgende tabel worden de verschillende geaccepteerde naamruimtetekens weergegeven.

| Kwalificatie | Definitie |
| --------- | ---------- |
| standaard | Een van de standaard naamruimten die globaal is gedefinieerd en niet is gekoppeld aan een afzonderlijke gegevensset van de organisatie (bijvoorbeeld e-mail, telefoonnummer, enz.). Naamruimte-id is opgegeven. |
| aangepast | Een unieke naamruimte die is gemaakt in de context van een organisatie en die niet wordt gedeeld door [!DNL Experience Cloud]. De waarde vertegenwoordigt de vriendschappelijke naam (&quot;naam&quot;gebied) moet worden gezocht naar. Naamruimte-id is opgegeven. |
| integrationCode | De code van de integratie - gelijkend op &quot;douane&quot;, maar specifiek bepaald als integratiecode van een gegevensbron die moet worden gezocht. Naamruimte-id is opgegeven. |
| namespaceId | Geeft aan dat de waarde de werkelijke id is van de naamruimte die is gemaakt of toegewezen via de naamruimteservice. |
| niet geregistreerd | Een vrije-vormkoord dat niet in de namespaceservice wordt bepaald en &quot;zoals is&quot;genomen. Om het even welke toepassing die deze soorten namespaces behandelt controleert tegen hen en behandelt als aangewezen voor de bedrijfcontext en gegevensreeks. Er is geen naamruimte-id opgegeven. |
| analyse | Een aangepaste naamruimte die intern wordt toegewezen in [!DNL Analytics], niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |
| target | Een aangepaste naamruimte die intern wordt begrepen door [!DNL Target], niet in de naamruimteservice. Dit wordt direct doorgegeven zoals opgegeven door de oorspronkelijke aanvraag, zonder naamruimte-id |

## Geaccepteerde productwaarden

In de volgende tabel worden de geaccepteerde waarden voor het opgeven van een Adobe-product in het kenmerk `include` van een aanvraag voor het maken van een taak weergegeven.

| Product | Waarde voor gebruik in het `include`-kenmerk |
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