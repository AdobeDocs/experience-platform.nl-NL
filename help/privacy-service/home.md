---
keywords: Experience Platform;home;populaire onderwerpen;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Overzicht van Privacy Service
topic: overview
description: Met Privacy Service kunt u de automatische naleving van wettelijke privacyregels in uw gegevensbewerkingen met Experience Cloud vergemakkelijken.
translation-type: tm+mt
source-git-commit: 37c1c98ccba50fa917acc5e93763294f4dde5c36
workflow-type: tm+mt
source-wordcount: '1394'
ht-degree: 0%

---


# [!DNL Privacy Service] - overzicht

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform [!DNL Privacy Service] is ontwikkeld als reactie op een fundamentele verandering in de manier waarop bedrijven de persoonlijke gegevens van hun klanten moeten beheren. Het centrale doel van [!DNL Privacy Service] is het automatiseren van naleving van de regels van de gegevensprivacy die, wanneer geschonden, in grote boetes en gegevensverrichtingen voor uw zaken kunnen resulteren.

[!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u verzoeken om klantgegevens kunt beheren. Met [!DNL Privacy Service] kunt u verzoeken indienen om toegang te krijgen tot en gegevens van persoonlijke klanten te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

## Aan de slag met [!DNL Privacy Service] {#getting-started}

Als u gebruik wilt maken van [!DNL Privacy Service], moeten verschillende belangrijke beslissingen worden genomen met betrekking tot de privacyvereisten van uw organisatie, het soort identiteitsgegevens dat u van uw klanten verzamelt en de beste manier om uw CRM-systeem te koppelen aan de service.

Deze besluiten kunnen als volgt worden samengevat:

1. **Welke informatie verzamel ik van mijn klanten?**
   * Om optimaal gebruik te kunnen maken van [!DNL Privacy Service], moet u een gedetailleerd inzicht hebben in de typen gegevens die u van uw klanten verzamelt en op welke gegevens privacyregels van toepassing zijn. Zie de sectie over [het bepalen van privacyvereisten](#requirements) voor meer informatie.
1. **Heb ik mijn gegevens correct gelabeld?**
   * De gegevens moeten correct geëtiketteerd zijn opdat de dienst kan bepalen welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Zie de sectie over [gegevens labelen](#label) voor meer informatie.
1. **Weet ik naar welke id&#39;s u wilt verzenden  [!DNL Privacy Service]?**
   * Bij het verzenden van privacyverzoeken moeten individuele klant-id&#39;s worden opgegeven die specifiek zijn voor bepaalde Adobe-toepassingen. Zie de secties over [het verstrekken van identiteitsgegevens](#identity) en [het maken van privacyverzoeken](#requests) voor meer informatie.
1. **Hoe volg ik mijn privacytaken?**
   * Nadat u een privacyverzoek hebt ingediend, kunt u de status en de resultaten van dat verzoek op verschillende manieren volgen. Zie de sectie over [privacytaken controleren](#monitor) voor meer informatie.

De onderstaande secties bieden algemene richtlijnen voor deze belangrijke stappen die aan de voorwaarde voldoen en bevatten ook koppelingen naar verdere documentatie [!DNL Privacy Service] voor meer informatie.

### De privacyvereisten van uw organisatie bepalen {#requirements}

Afhankelijk van de aard van uw bedrijf en de rechtsgebieden waaronder het werkt, zijn uw gegevensbewerkingen mogelijk onderworpen aan wettelijke privacyregels. Deze verordeningen geven uw klanten vaak het recht om toegang tot de gegevens te verzoeken u van hen verzamelt, en het recht om de schrapping van die opgeslagen gegevens te verzoeken. Deze verzoeken van klanten om hun persoonsgegevens worden bedoeld als &quot;privacyverzoeken&quot;door de documentatie.

Raadpleeg de [documentatie over privacyregels](./regulations/overview.md) voor meer informatie over de verschillende wettelijke privacyregels die [!DNL Privacy Service] beheert voor het beheren van aanvragen, waaronder belangrijke termen en antwoorden op veelgestelde vragen.

Als uw gegevensbewerkingen onder de ondersteunde regelgeving vallen, raadpleegt u de documentatie bij deze bewerkingen voor belangrijke informatie, zoals de specifieke privacyrechten die ze aan uw klanten verlenen en compatibiliteitsvensters voor het uitvoeren van privacyverzoeken. Met deze informatie moet rekening worden gehouden wanneer wordt bepaald hoe [!DNL Privacy Service] in uw CRM-systeem moet worden geïntegreerd en hoe klanten met uw website moeten communiceren om privacyverzoeken te kunnen indienen.

Naast wettelijke voorschriften, zouden om het even welke organisatie of industrienormen die op uw organisatie van toepassing zijn ook in overweging moeten worden genomen wanneer het nemen van deze besluiten.

### Gegevens labelen voor privacyverzoeken {#label}

Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, moet u de specifieke gegevensgebieden etiketteren die in antwoord op privacyverzoeken zouden moeten worden betreden of worden geschrapt. Het proces voor het etiketteren van gegevens varieert tussen toepassingen. Meer informatie over het labelen van gegevens voor elke ondersteunde Adobe-toepassing vindt u in het document op [Experience Cloud-toepassingen](./experience-cloud-apps.md).

### Bepaal de soorten identiteitsgegevens die naar [!DNL Privacy Service] {#identity} moeten worden verzonden

Als [!DNL Privacy Service] een privacyverzoek van een klant moet verwerken, moet ten minste één unieke identiteitswaarde voor die klant in het verzoek zelf worden opgegeven. Een unieke identiteitswaarde is alle informatie die kan worden gebruikt om een individuele persoon en zijn opgeslagen persoonlijke gegevens in uw [!DNL Experience Cloud] gegevensopslag te identificeren. [!DNL Privacy Service] gebruikt deze identiteitsgegevens om de persoonsgegevens van de klant te zoeken en te verwerken volgens de aard van de aanvraag (toegang, verwijdering of opt-out).

Afhankelijk van de [!DNL Experience Cloud] toepassingen uw systeem van CRM gebruikt, zullen het type en het aantal identiteitswaarden u voor elke klant moet verstrekken variëren. Sommige toepassingen gebruiken hun eigen interne waarden voor de klant-id (zoals Adobe Target-id&#39;s), terwijl andere oplossingen vertrouwen op algemene id&#39;s van Adobe [!DNL Experience Cloud Identity Service] (ECID) die de activiteiten van de klant in alle [!DNL Experience Cloud]-toepassingen bijhouden. Daarnaast kunnen algemene persoonlijke gegevens, zoals een e-mailadres of telefoonnummer, ook als geldige identiteitsgegevens worden gebruikt.

Het document over [identiteitsgegevens voor privacyverzoeken](./identity-data.md) bevat gedetailleerdere informatie over de typen identiteitsgegevens die worden geaccepteerd voor [!DNL Privacy Service]. Het document biedt ook richtlijnen over hoe u Adobe-technologieën kunt gebruiken om de juiste identiteitsgegevens van uw klanten op te halen bij hun interactie met uw website en deze gegevens naar [!DNL Privacy Service] te verzenden in API-aanvragen.

### Start met het indienen van privacyverzoeken {#requests}

Zodra u de privacybehoeften van uw bedrijf hebt bepaald en hebt besloten welke identiteitswaarden naar [!DNL Privacy Service] moeten worden verzonden, kunt u beginnen met het indienen van privacyverzoeken. [!DNL Privacy Service] kunt u privacyverzoeken verzenden via de API of de gebruikersinterface.

>[!IMPORTANT]
>
>In de volgende secties vindt u koppelingen naar documentatie over het maken van algemene privacyverzoeken in de API of UI. Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, kunnen de velden die u in de aanvraag moet verzenden, echter afwijken van de voorbeelden in deze handleidingen.
>
>Als u de API- of UI-handleidingen volgt, raadpleegt u het document op [Privacy Service- en Experience Cloud-toepassingen](./experience-cloud-apps.md) voor meer informatie over het opmaken van privacyverzoeken voor uw specifieke [!DNL Experience Cloud]-toepassing(en).
>
>Het is ook belangrijk om op te merken dat de privacyverzoeken asynchroon over Experience Cloud toepassingen worden verwerkt. Zodra een verzoek door Privacy Service wordt ontvangen, kan elke toepassing overal van minuten tot weken duren om het verzoek te voltooien. De hoeveelheid tijd die nodig is om elk verzoek te voltooien, is specifiek voor de toepassing waarmee u werkt en de hoeveelheid gegevens die moet worden verwerkt.

#### De API gebruiken

[[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) verstrekt verscheidene eindpunten voor het creëren van en het beheren van privacybanen gebruikend RESTful API vraag, die u toestaat om privacyregelgevende naleving voor uw [!DNL Experience Cloud] toepassingen programmatically te benaderen. Zie de [Handleiding voor ontwikkelaars van API voor Privacy Service](api/getting-started.md) voor gedetailleerde stappen over het gebruik van de API.

#### De gebruikersinterface gebruiken

>[!NOTE]
>
>De [!DNL Privacy Service] UI steunt momenteel slechts toegang en schrappingsverzoeken. Alle verzoeken om te weigeren moeten in plaats daarvan via de API worden gedaan.

Met de interface [!DNL Privacy Service] kunt u met een grafische interface privacytaken maken en controleren. UI omvat een **[!UICONTROL Rapport van de Status]** widget die een visuele vertegenwoordiging van de status van alle actieve verzoeken verstrekt, en staat u toe om nieuwe verzoeken tot stand te brengen door ingebouwde **[!UICONTROL de Bouwer van het Verzoek te gebruiken]** of door JSON dossiers te uploaden. Voor meer informatie bij het gebruiken van UI, zie [Privacy Service gebruikersgids](ui/overview.md).

### Privacytaken controleren {#monitor}

Nadat u een privacytaak hebt uitgevoerd, kunt u de status en de resultaten van deze taken op verschillende manieren controleren:

| Controlemethode | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] UI | De interface [!DNL Privacy Service] verstrekt een controledashboard dat u toestaat om een visuele vertegenwoordiging van de status van alle actieve verzoeken te bekijken. Zie [Gebruikershandleiding voor Privacys Service](ui/overview.md) voor meer informatie. |
| [!DNL Privacy Service] API | U kunt de status van de banen van de Privacy programmatically controleren door de raadplegingseindpunten te gebruiken die door [!DNL Privacy Service] API worden verstrekt. Zie de [Privacy Service-ontwikkelaarshandleiding](./api/getting-started.md) voor gedetailleerde stappen over het gebruik van de API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] hefboomwerking Adobe I/O Gebeurtenissen die naar een gevormde webhaak worden verzonden om efficiënte baanverzoekautomatisering te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API te raadplegen om te controleren of een taak voltooid is of of een bepaalde mijlpaal binnen een workflow is bereikt. Zie de zelfstudie over [het abonneren op de Gebeurtenissen van de Privacy](./privacy-events.md) voor meer informatie. |

## Volgende stappen

Dit document biedt een overzicht op hoog niveau van [!DNL Privacy Service] en de belangrijkste stappen die zijn vereist om de mogelijkheden van de service te gaan gebruiken. Raadpleeg de documentatie bij het volledige overzicht voor meer informatie over de verschillende aspecten van het werken met [!DNL Privacy Service].
