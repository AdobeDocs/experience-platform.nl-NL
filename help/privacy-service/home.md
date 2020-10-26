---
keywords: Experience Platform;home;popular topics;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: f3872d433949e6c14c28c6833b8498d4d01b8de3
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Adobe Experience Platform [!DNL Privacy Service] overview

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform [!DNL Privacy Service] is ontwikkeld als reactie op een fundamentele verschuiving in de manier waarop bedrijven de persoonsgegevens van hun klanten moeten beheren. Het centrale doel van [!DNL Privacy Service] is het automatiseren van naleving van de regels van de gegevensprivacy die, wanneer geschonden, in grote boetes kunnen resulteren en gegevensverrichtingen voor uw zaken kunnen verstoren.

[!DNL Privacy Service] biedt een RESTful-API en -gebruikersinterface waarmee u verzoeken om klantgegevens kunt beheren. Met [!DNL Privacy Service]kunt u verzoeken indienen om toegang te krijgen tot persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

## Aan de slag met [!DNL Privacy Service] {#getting-started}

Om van gebruik te maken [!DNL Privacy Service], moeten verscheidene zeer belangrijke besluiten in termen van de privacyvereisten van uw organisatie, de soorten identiteitsgegevens worden genomen u van uw klanten verzamelt, en de beste manier om uw systeem van CRM met de dienst te verbinden.

Deze besluiten kunnen als volgt worden samengevat:

1. **Welke informatie verzamel ik van mijn klanten?**
   * Om optimaal gebruik te maken van [!DNL Privacy Service], moet u een gedetailleerd inzicht hebben in de soorten gegevens u van uw klanten verzamelt, en welke van het onderworpen is aan privacyverordeningen. Zie de sectie over het [bepalen van privacyvereisten](#requirements) voor meer informatie.
1. **Heb ik mijn gegevens correct gelabeld?**
   * De gegevens moeten correct geëtiketteerd zijn opdat de dienst kan bepalen welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Zie de sectie over [etiketteringsgegevens](#label) voor meer informatie.
1. **Weet ik naar welke id&#39;s u wilt verzenden [!DNL Privacy Service]?**
   * Bij het verzenden van privacyverzoeken moeten individuele klant-id&#39;s worden opgegeven die specifiek zijn voor bepaalde Adobe-toepassingen. Zie de secties over het [verstrekken van identiteitsgegevens](#identity) en het [maken van privacyverzoeken](#requests) voor meer informatie.
1. **Hoe volg ik mijn privacytaken?**
   * Nadat u een privacyverzoek hebt ingediend, kunt u de status en de resultaten van dat verzoek op verschillende manieren volgen. Zie de sectie over het [controleren van privacytaken](#monitor) voor meer informatie.

In de volgende secties worden algemene richtsnoeren gegeven voor deze belangrijke, noodzakelijke stappen en worden ook links naar verdere [!DNL Privacy Service] documentatie gegeven voor meer informatie.

### De privacyvereisten van uw organisatie bepalen {#requirements}

Afhankelijk van de aard van uw bedrijf en de rechtsgebieden waaronder het werkt, zijn uw gegevensbewerkingen mogelijk onderworpen aan wettelijke privacyregels. Deze verordeningen geven uw klanten vaak het recht om toegang tot de gegevens te verzoeken u van hen verzamelt, en het recht om de schrapping van die opgeslagen gegevens te verzoeken. Deze verzoeken van klanten om hun persoonsgegevens worden bedoeld als &quot;privacyverzoeken&quot;door de documentatie.

In de volgende tabel worden de wettelijke privacyregels beschreven die aanvragen [!DNL Privacy Service] beheren, waaronder koppelingen naar documentatie voor meer informatie:

| Verordening | Beschrijving |
| --- | --- |
| CCPA (Californië) | De [!DNL California Consumer Privacy Act] (CCPA) verbetert de privacyrechten en de consumentenbescherming voor inwoners van Californië in de Verenigde Staten. De CCPA biedt de inwoners van Californië nieuwe privacyrechten op het gebied van gegevens, waaronder het recht op toegang tot en verwijdering van hun persoonsgegevens, om te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie), en het recht om te weigeren hun gegevens aan derden te laten verkopen.<br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://oag.ca.gov/privacy/ccpa)</li><li>[Veelgestelde vragen over CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Europese Unie) | De [!DNL General Data Protection Regulation] (GDPR, ofwel Algemene verordening gegevensbescherming (AVG)) heeft diverse nieuwe dataprivacyrechten geïntroduceerd voor leden van de Europese Unie, waaronder het **recht op toegang** en het **recht om vergeten te worden**. Dit betekent dat iedere EU-burger wiens persoonlijke data door uw bedrijf zijn verzameld, op elk moment kan vragen om toegang tot of verwijdering van zijn of haar data. <br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://gdpr-info.eu/)</li><li>[Veelgestelde vragen over GDPR](gdpr/faq.md)</li><li>[GDPR-terminologie](gdpr/terminology.md)</li></ul> |
| LGPD (Brazilië) | De [!DNL Lei Geral de Proteção de Dados] (GPD) heeft tot doel de behandeling van persoonsgegevens van alle natuurlijke personen of natuurlijke personen in Brazilië te reguleren. De LGPD geeft de burgers van Brazilië het recht om hun persoonsgegevens te raadplegen en te wissen, te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie), en het recht om te weigeren hun gegevens aan derden te laten verkopen.<br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://gdpr.eu/gdpr-vs-lgpd/)</li></ul> |
| PDPA (Thailand) | De [!DNL Personal Data Protection Act] Thaise gegevensbezitters werden beschermd tegen het illegaal verzamelen, gebruiken of openbaar maken van hun persoonsgegevens. De verordening is geïnspireerd door de GDPR van de Europese Unie en verleent Thaise burgers het recht om toegang te vragen tot of te verwijderen van hun opgeslagen persoonsgegevens.<br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Veelgestelde vragen PDPA](pdpa-tha/faq.md)</li><li>[terminologie PDPA](pdpa-tha/terminology.md)</li></ul> |

Als uw gegevensbewerkingen onder een van de bovenstaande verordeningen vallen, raadpleegt u de documentatie bij deze bewerkingen voor belangrijke informatie, zoals de specifieke privacyrechten die zij aan uw klanten verlenen, en compatibiliteitsvensters voor het uitvoeren van privacyverzoeken. Met deze informatie moet rekening worden gehouden wanneer u bepaalt hoe u uw CRM-systeem kunt integreren en hoe klanten met uw website moeten communiceren om privacyverzoeken te kunnen indienen. [!DNL Privacy Service]

Naast wettelijke voorschriften, zouden om het even welke organisatie of industrienormen die op uw organisatie van toepassing zijn ook in overweging moeten worden genomen wanneer het nemen van deze besluiten.

### Gegevens labelen voor privacyverzoeken {#label}

Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, moet u de specifieke gegevensgebieden etiketteren die in antwoord op privacyverzoeken zouden moeten worden betreden of worden geschrapt. Het proces voor het etiketteren van gegevens varieert tussen toepassingen. Zie het document over [Experience Cloud-toepassingen](./experience-cloud-apps.md)voor meer informatie over het labelen van gegevens voor elke ondersteunde Adobe-toepassing.

### Bepaal de typen identiteitsgegevens waarnaar u wilt verzenden [!DNL Privacy Service] {#identity}

Om een privacyverzoek van een klant [!DNL Privacy Service] te verwerken, moet minstens één unieke identiteitswaarde voor die klant in het verzoek zelf worden verstrekt. Een unieke identiteitswaarde is alle informatie die kan worden gebruikt om een individuele persoon en zijn opgeslagen persoonlijke gegevens in uw [!DNL Experience Cloud] gegevensopslag te identificeren. [!DNL Privacy Service] gebruikt deze identiteitsgegevens om de persoonsgegevens van de klant te zoeken en te verwerken volgens de aard van de aanvraag (toegang, verwijdering of opt-out).

Afhankelijk van de [!DNL Experience Cloud] toepassingen uw systeem van CRM gebruikt, zullen het type en het aantal identiteitswaarden u voor elke klant moet verstrekken variëren. Sommige toepassingen gebruiken hun eigen interne waarden van klantidentiteitskaart (zoals Adobe Target IDs), terwijl andere oplossingen op globale herkenningstekens van Adobe [!DNL Experience Cloud Identity Service] (ECID) vertrouwen die klantenactiviteit over alle [!DNL Experience Cloud] toepassingen volgen. Daarnaast kunnen algemene persoonlijke gegevens, zoals een e-mailadres of telefoonnummer, ook als geldige identiteitsgegevens worden gebruikt.

Het document over [identiteitsgegevens voor privacyverzoeken](./identity-data.md) bevat gedetailleerdere informatie over de typen identiteitsgegevens die worden geaccepteerd voor [!DNL Privacy Service]. Het document biedt ook richtlijnen voor het gebruik van Adobe-technologieën om de juiste identiteitsgegevens van uw klanten op te halen bij de interactie met uw website en om die gegevens naar [!DNL Privacy Service] in API-verzoeken te verzenden.

### Start met het indienen van privacyaanvragen {#requests}

Nadat u de privacybehoeften van uw bedrijf hebt bepaald en hebt bepaald naar welke identiteitswaarden u wilt verzenden, kunt u beginnen met het indienen van privacyverzoeken. [!DNL Privacy Service] [!DNL Privacy Service] kunt u privacyverzoeken verzenden via de API of de gebruikersinterface.

>[!IMPORTANT]
>
>In de volgende secties vindt u koppelingen naar documentatie over het maken van algemene privacyverzoeken in de API of UI. Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, kunnen de velden die u in de aanvraag moet verzenden, echter afwijken van de voorbeelden in deze handleidingen.
>
>Als u de API- of UI-handleidingen volgt, raadpleegt u het document over [Privacy Service- en Experience Cloud-toepassingen](./experience-cloud-apps.md) voor meer documentatie over het opmaken van privacyverzoeken voor uw specifieke [!DNL Experience Cloud] toepassing(en).
>
>Het is ook belangrijk om op te merken dat de privacyverzoeken asynchroon over Experience Cloud toepassingen worden verwerkt. Zodra een verzoek door Privacy Service wordt ontvangen, kan elke toepassing overal van minuten tot weken duren om het verzoek te voltooien. De hoeveelheid tijd die nodig is om elk verzoek te voltooien, is specifiek voor de toepassing waarmee u werkt en de hoeveelheid gegevens die moet worden verwerkt.

#### De API gebruiken

Het [[!DNL Privacy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) biedt verschillende eindpunten voor het maken en beheren van privacytaken met behulp van RESTful API-aanroepen, waarmee u programmatisch de naleving van privacyregelgeving voor uw [!DNL Experience Cloud] toepassingen kunt benaderen. Zie de handleiding voor ontwikkelaars van de [Privacy Service-API voor meer informatie over het gebruik van de API](api/getting-started.md).

#### De gebruikersinterface gebruiken

>[!NOTE]
>
>De [!DNL Privacy Service] UI steunt momenteel slechts toegang en schrappingsverzoeken. Alle verzoeken om te weigeren moeten in plaats daarvan via de API worden gedaan.

Met de [!DNL Privacy Service] interface kunt u met een grafische interface privacytaken maken en controleren. UI omvat een widget van het Rapport **[!UICONTROL van de]** Status die een visuele vertegenwoordiging van de status van alle actieve verzoeken verstrekt, en staat u toe om nieuwe verzoeken tot stand te brengen door de ingebouwde **[!UICONTROL Bouwer]** van het Verzoek te gebruiken of door JSON- dossiers te uploaden. Raadpleeg de gebruikershandleiding bij de [Privacy Service voor meer informatie over het gebruik van de gebruikersinterface](ui/overview.md).

### Privacy-taken controleren {#monitor}

Nadat u een privacytaak hebt uitgevoerd, kunt u de status en de resultaten van deze taken op verschillende manieren controleren:

| Controlemethode | Beschrijving |
| --- | --- |
| [!DNL Privacy Service] UI | De [!DNL Privacy Service] UI verstrekt een controledashboard dat u toestaat om een visuele vertegenwoordiging van de status van alle actieve verzoeken te bekijken. Raadpleeg de gebruikershandleiding [bij de](ui/overview.md) Privacy Service voor meer informatie. |
| [!DNL Privacy Service] API | U kunt de status van de banen van de Privacy programmatically controleren door de raadplegingseindpunten te gebruiken die door [!DNL Privacy Service] API worden verstrekt. Zie de handleiding voor ontwikkelaars van [Privacys Service](./api/getting-started.md) voor gedetailleerde stappen over het gebruik van de API. |
| [!DNL Privacy Events] | [!DNL Privacy Events] hefboomwerking I/O Gebeurtenissen van Adobe die naar een gevormde webhaak worden verzonden om efficiënte baanverzoekautomatisering te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de [!DNL Privacy Service] API te raadplegen om te controleren of een taak voltooid is of dat een bepaalde mijlpaal in een werkstroom is bereikt. Zie de zelfstudie over het [abonneren op Privacy Events](./privacy-events.md) voor meer informatie. |

## Volgende stappen

Dit document biedt een overzicht op hoog niveau van [!DNL Privacy Service] en de belangrijkste stappen die nodig zijn om de mogelijkheden van de service te gaan gebruiken. Raadpleeg de documentatie bij het volledige overzicht voor meer informatie over de verschillende aspecten van het werken met [!DNL Privacy Service].
