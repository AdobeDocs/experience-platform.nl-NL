---
keywords: Experience Platform;home;populaire onderwerpen;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Overzicht van Privacy Service
topic-legacy: overview
description: Met Privacy Service kunt u de automatische naleving van wettelijke privacyregels in uw gegevensbewerkingen met Experience Cloud vergemakkelijken.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1385'
ht-degree: 0%

---

# [!DNL Privacy Service] - overzicht

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform [!DNL Privacy Service] is ontwikkeld als reactie op een fundamentele verschuiving in de manier waarop bedrijven de persoonsgegevens van hun klanten moeten beheren. Het centrale doel van [!DNL Privacy Service] is om naleving van de regels van de gegevensprivacy te automatiseren die, wanneer geschonden, in grote boetes kunnen resulteren en gegevensverrichtingen voor uw zaken kunnen verstoren.

[!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u verzoeken om klantgegevens kunt beheren. Met [!DNL Privacy Service]kunt u verzoeken om toegang tot en verwijdering van persoonsgegevens van klanten uit Adobe Experience Cloud-toepassingen verzenden, zodat u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

## Aan de slag met [!DNL Privacy Service] {#getting-started}

Voor het gebruik van [!DNL Privacy Service], moeten er verschillende belangrijke beslissingen worden genomen met betrekking tot de privacyvereisten van uw organisatie, de soorten identiteitsgegevens die u van uw klanten verzamelt en de beste manier om uw CRM-systeem te koppelen aan de service.

Deze besluiten kunnen als volgt worden samengevat:

1. **Welke informatie verzamel ik van mijn klanten?**
   * Om optimaal gebruik te maken van [!DNL Privacy Service], moet u een gedetailleerd inzicht hebben in de soorten gegevens die u van uw klanten verzamelt en op welke van deze gegevens privacyregels van toepassing zijn. Zie de sectie over [privacyvereisten bepalen](#requirements) voor meer informatie .
1. **Heb ik mijn gegevens correct gelabeld?**
   * De gegevens moeten correct geëtiketteerd zijn opdat de dienst kan bepalen welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Zie de sectie over [etiketteringsgegevens](#label) voor meer informatie .
1. **Weet ik naar welke id&#39;s u wilt verzenden? [!DNL Privacy Service]?**
   * Bij het verzenden van privacyverzoeken moeten individuele klant-id&#39;s worden opgegeven die specifiek zijn voor bepaalde Adobe-toepassingen. Zie de secties op [identiteitsgegevens verstrekken](#identity)  en [indienen van privacyverzoeken](#requests) voor meer informatie .
1. **Hoe volg ik mijn privacytaken?**
   * Nadat u een privacyverzoek hebt ingediend, kunt u de status en de resultaten van dat verzoek op verschillende manieren volgen. Zie de sectie over [privacytaken controleren](#monitor) voor meer informatie .

In de onderstaande paragrafen worden algemene richtsnoeren gegeven voor deze belangrijke noodzakelijke stappen en worden ook koppelingen naar verdere stappen gegeven. [!DNL Privacy Service] voor meer informatie.

### De privacyvereisten van uw organisatie bepalen {#requirements}

Afhankelijk van de aard van uw bedrijf en de rechtsgebieden waaronder het werkt, zijn uw gegevensbewerkingen mogelijk onderworpen aan wettelijke privacyregels. Deze verordeningen geven uw klanten vaak het recht om toegang tot de gegevens te verzoeken u van hen verzamelt, en het recht om de schrapping van die opgeslagen gegevens te verzoeken. Deze verzoeken van klanten om hun persoonsgegevens worden bedoeld als &quot;privacyverzoeken&quot;door de documentatie.

Voor meer informatie over de verschillende wettelijke privacyregels die [!DNL Privacy Service] beheert aanvragen voor, inclusief sleuteltermen en antwoorden op veelgestelde vragen, raadpleegt u de [documentatie over privacyregels](./regulations/overview.md).

Als uw gegevensbewerkingen onder de ondersteunde regelgeving vallen, raadpleegt u de documentatie bij deze bewerkingen voor belangrijke informatie, zoals de specifieke privacyrechten die ze aan uw klanten verlenen en compatibiliteitsvensters voor het uitvoeren van privacyverzoeken. Met deze informatie moet rekening worden gehouden bij het bepalen van de wijze waarop [!DNL Privacy Service] in uw CRM-systeem en hoe klanten moeten communiceren met uw website om privacyverzoeken te kunnen indienen.

Naast wettelijke voorschriften, zouden om het even welke organisatie of industrienormen die op uw organisatie van toepassing zijn ook in overweging moeten worden genomen wanneer het nemen van deze besluiten.

### Gegevens labelen voor privacyverzoeken {#label}

Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, moet u de specifieke gegevensgebieden etiketteren die in antwoord op privacyverzoeken zouden moeten worden betreden of worden geschrapt. Het proces voor het etiketteren van gegevens varieert tussen toepassingen. Raadpleeg het document voor meer informatie over het labelen van gegevens voor elke ondersteunde Adobe-toepassing [Experience Cloud-toepassingen](./experience-cloud-apps.md).

### Bepaal de typen identiteitsgegevens waarnaar u wilt verzenden [!DNL Privacy Service] {#identity}

Om [!DNL Privacy Service] om een privacyverzoek van een klant te verwerken, moet minstens één unieke identiteitswaarde voor die klant in het verzoek zelf worden verstrekt. Een unieke identiteitswaarde is alle informatie die kan worden gebruikt om een individuele persoon en zijn opgeslagen persoonsgegevens in uw [!DNL Experience Cloud] gegevensopslag. [!DNL Privacy Service] gebruikt deze identiteitsgegevens om de persoonsgegevens van de klant te zoeken en te verwerken volgens de aard van de aanvraag (toegang, verwijdering of opt-out).

Afhankelijk van de [!DNL Experience Cloud] de toepassingen uw systeem van CRM gebruikt, zullen het type en het aantal identiteitswaarden u voor elke klant moet verstrekken variëren. Sommige toepassingen gebruiken hun eigen interne waarden voor de klant-id (zoals Adobe Target-id&#39;s), terwijl andere oplossingen vertrouwen op algemene id&#39;s van Adobe [!DNL Experience Cloud Identity Service] (ECID) die de klantactiviteiten in alle [!DNL Experience Cloud] toepassingen. Daarnaast kunnen algemene persoonlijke gegevens, zoals een e-mailadres of telefoonnummer, ook als geldige identiteitsgegevens worden gebruikt.

Het document op [identiteitsgegevens voor privacyverzoeken](./identity-data.md) verstrekt meer gedetailleerde informatie over de types van identiteitsinformatie die voor worden aanvaard [!DNL Privacy Service]. Het document biedt ook richtlijnen over hoe u Adobe-technologieën kunt gebruiken om de juiste identiteitsgegevens van uw klanten op te halen bij de interactie met uw website en deze gegevens naar [!DNL Privacy Service] in API-aanvragen.

### Start met het indienen van privacyaanvragen {#requests}

Nadat u de privacybehoeften van uw bedrijf hebt bepaald en hebt bepaald naar welke identiteitswaarden u wilt sturen [!DNL Privacy Service], kunt u beginnen met het indienen van privacyverzoeken. [!DNL Privacy Service] kunt u privacyverzoeken verzenden via de API of de gebruikersinterface.

>[!IMPORTANT]
>
>In de volgende secties vindt u koppelingen naar documentatie over het maken van algemene privacyverzoeken in de API of UI. Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, kunnen de velden die u in de aanvraag moet verzenden afwijken van de voorbeelden in deze handleidingen.
>
>Raadpleeg het document op [Privacy Service- en Experience Cloud-toepassingen](./experience-cloud-apps.md) voor meer documentatie over het opmaken van privacyverzoeken voor uw specifieke [!DNL Experience Cloud] toepassing(en).
>
>Het is ook belangrijk om op te merken dat de privacyverzoeken asynchroon over Experience Cloud toepassingen worden verwerkt. Zodra een verzoek door Privacy Service wordt ontvangen, kan elke toepassing overal van minuten tot weken duren om het verzoek te voltooien. De hoeveelheid tijd die nodig is om elk verzoek te voltooien, is specifiek voor de toepassing waarmee u werkt en de hoeveelheid gegevens die moet worden verwerkt.

#### De API gebruiken

De [[!DNL Privacy Service API]](https://www.adobe.io/experience-platform-apis/references/privacy-service/) biedt verschillende eindpunten voor het maken en beheren van privacytaken met behulp van RESTful API-aanroepen, zodat u programmatisch kunt voldoen aan privacyregelgeving voor uw [!DNL Experience Cloud] toepassingen. Zie voor gedetailleerde stappen over het gebruik van de API de [Handleiding Privacy Service-API](api/overview.md).

#### De gebruikersinterface gebruiken

>[!NOTE]
>
>De [!DNL Privacy Service] De gebruikersinterface ondersteunt momenteel alleen toegangs- en verwijderingsverzoeken. Alle verzoeken om te weigeren moeten in plaats daarvan via de API worden gedaan.

De [!DNL Privacy Service] UI staat u toe om privacybanen tot stand te brengen en te controleren gebruikend een grafische interface. De interface bevat een **[!UICONTROL Status Report]** widget die een visuele vertegenwoordiging van de status van alle actieve verzoeken verstrekt, en u toestaat om nieuwe verzoeken tot stand te brengen door ingebouwde **[!UICONTROL Request Builder]** of door JSON-bestanden te uploaden. Voor meer informatie bij het gebruiken van UI, zie [Gebruikershandleiding voor Privacy Service](ui/overview.md).

### Privacy-taken controleren {#monitor}

Nadat u een privacytaak hebt uitgevoerd, kunt u de status en de resultaten van deze taken op verschillende manieren controleren:

| Controlemethode | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] Gebruikersinterface | De [!DNL Privacy Service] UI verstrekt een controledashboard dat u toestaat om een visuele vertegenwoordiging van de status van alle actieve verzoeken te bekijken. Zie de [Gebruikershandleiding voor Privacy Service](ui/overview.md) voor meer informatie . |
| [!DNL Privacy Service] API | U kunt de status van de banen van de Privacy programmatically controleren door de raadplegingseindpunten te gebruiken die door worden verstrekt [!DNL Privacy Service] API. Zie de [Handleiding Privacy Service-API](./api/overview.md) voor meer informatie over het gebruik van de API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] hefboomwerking Adobe I/O Gebeurtenissen die naar een gevormde webhaak worden verzonden om efficiënte de automatisering van het baanverzoek te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API om te controleren of een baan volledig is of een bepaalde mijlpaal binnen een werkschema is bereikt. Zie de zelfstudie aan [abonneren op Privacy Events](./privacy-events.md) voor meer informatie . |

## Volgende stappen

Dit document biedt een overzicht op hoog niveau van [!DNL Privacy Service] en de belangrijkste stappen die nodig zijn om de mogelijkheden van de service te gaan gebruiken. Raadpleeg de documentatie bij het volledige overzicht voor meer informatie over de verschillende aspecten van het werken met [!DNL Privacy Service].
