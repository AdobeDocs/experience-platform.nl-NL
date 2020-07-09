---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: d358b200d574ca8de77ee2274836c03f7cc84c40
workflow-type: tm+mt
source-wordcount: '1587'
ht-degree: 3%

---


# Overzicht van Adobe Experience Platform Privacy Service

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform Privacy Service is ontwikkeld als reactie op een fundamentele verschuiving in de manier waarop bedrijven de persoonsgegevens van hun klanten moeten beheren. Het centrale doel van Privacy Service is het automatiseren van naleving van de regels van de gegevensprivacy die, wanneer geschonden, in grote boetes kunnen resulteren en gegevensverrichtingen voor uw zaken kunnen verstoren.

Privacy Service verstrekt RESTful API en gebruikersinterface om u te helpen de verzoeken van klantgegevens beheren. Met Privacy Service kunt u verzoeken indienen om toegang te krijgen tot persoonlijke klantgegevens en deze te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

## Aan de slag met Privacy Service {#getting-started}

Om van Privacy Service gebruik te maken, moeten verscheidene zeer belangrijke besluiten in termen van de privacyvereisten van uw organisatie, de soorten identiteitsgegevens worden genomen u van uw klanten verzamelt, en de beste manier om uw systeem van CRM met de dienst te verbinden.

Deze besluiten kunnen als volgt worden samengevat:

1. **Welke informatie verzamel ik van mijn klanten?**
   * Om optimaal gebruik te maken van Privacy Service, moet u een gedetailleerd inzicht hebben in de soorten gegevens u van uw klanten verzamelt, en welke van het onderworpen is aan privacyverordeningen. Zie de sectie over het [bepalen van privacyvereisten](#requirements) voor meer informatie.
1. **Heb ik mijn gegevens correct gelabeld?**
   * De gegevens moeten correct geëtiketteerd zijn opdat de dienst kan bepalen welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Zie de sectie over [etiketteringsgegevens](#label) voor meer informatie.
1. **Weet ik welke id&#39;s naar de Privacy Service moeten worden verzonden?**
   * Wanneer u een privacyverzoek verzendt, moet u afzonderlijke klant-id&#39;s opgeven die specifiek zijn voor bepaalde Adobe-toepassingen. Zie de secties over het [verstrekken van identiteitsgegevens](#identity) en het [maken van privacyverzoeken](#requests) voor meer informatie.
1. **Hoe volg ik mijn privacytaken?**
   * Nadat u een privacyverzoek hebt ingediend, kunt u de status en de resultaten van dat verzoek op verschillende manieren volgen. Zie de sectie over het [controleren van privacytaken](#monitor) voor meer informatie.

In de volgende secties worden algemene richtsnoeren gegeven voor deze belangrijke, noodzakelijke stappen en wordt verwezen naar verdere documentatie bij de Privacy Service voor meer informatie.

### De privacyvereisten van uw organisatie bepalen {#requirements}

Afhankelijk van de aard van uw bedrijf en de rechtsgebieden waaronder het werkt, zijn uw gegevensbewerkingen mogelijk onderworpen aan wettelijke privacyregels. Deze verordeningen geven uw klanten vaak het recht om toegang tot de gegevens te verzoeken u van hen verzamelt, en het recht om de schrapping van die opgeslagen gegevens te verzoeken. Deze verzoeken van klanten om hun persoonsgegevens worden bedoeld als &quot;privacyverzoeken&quot;door de documentatie.

In de volgende tabel worden de wettelijke privacyregels beschreven die Privacy Service aanvraagt, waaronder koppelingen naar documentatie voor meer informatie:

| Verordening | Beschrijving |
| --- | --- |
| CCPA (Californië) | De California Consumer Privacy Act (CCPA) verbetert de privacyrechten en consumentenbescherming voor inwoners van Californië in de Verenigde Staten. De CCPA biedt de inwoners van Californië nieuwe privacyrechten op het gebied van gegevens, waaronder het recht op toegang tot en verwijdering van hun persoonsgegevens, om te weten of hun persoonsgegevens worden verkocht of openbaar gemaakt (en aan wie), en het recht om te weigeren hun gegevens aan derden te laten verkopen.<br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://oag.ca.gov/privacy/ccpa)</li><li>[Veelgestelde vragen over CCPA](ccpa/faq.md)</li></ul> |
| GDPR (Europese Unie) | De General Data Protection Regulation (GDPR, ofwel Algemene verordening gegevensbescherming (AVG)) heeft diverse nieuwe dataprivacyrechten geïntroduceerd voor leden van de Europese Unie, waaronder het **recht op toegang** en het **recht om vergeten te worden**. Dit betekent dat iedere EU-burger wiens persoonlijke data door uw bedrijf zijn verzameld, op elk moment kan vragen om toegang tot of verwijdering van zijn of haar data. <br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://gdpr-info.eu/)</li><li>[Veelgestelde vragen over GDPR](gdpr/faq.md)</li><li>[GDPR-terminologie](gdpr/terminology.md)</li></ul> |
| PDPA_THA (Thailand) | De Thaise gegevensbeschermingswet (PDPA) is ingevoerd om Thaise gegevensbezitters te beschermen tegen het illegaal verzamelen, gebruiken of openbaar maken van hun persoonsgegevens. De verordening is geïnspireerd door de GDPR van de Europese Unie en verleent Thaise burgers het recht om toegang te vragen tot of te verwijderen van hun opgeslagen persoonsgegevens.<br/><br/>Koppelingen voor nadere documentatie: <ul><li>[Juridisch overzicht](https://www.dataprotectionreport.com/2020/02/thailand-personal-data-protection-law/)</li><li>[Veelgestelde vragen over PDPA_THA](pdpa-tha/faq.md)</li><li>[terminologie PDPA_THA](pdpa-tha/terminology.md)</li></ul> |

Als uw gegevensbewerkingen onder een van de bovenstaande verordeningen vallen, raadpleegt u de documentatie bij deze bewerkingen voor belangrijke informatie, zoals de specifieke privacyrechten die zij aan uw klanten verlenen, en compatibiliteitsvensters voor het uitvoeren van privacyverzoeken. Met deze informatie moet rekening worden gehouden wanneer wordt bepaald hoe Privacy Service in uw CRM-systeem moet worden geïntegreerd en hoe klanten met uw website moeten communiceren om privacyverzoeken te kunnen indienen.

Naast wettelijke voorschriften, zouden om het even welke organisatie of industrienormen die op uw organisatie van toepassing zijn ook in overweging moeten worden genomen wanneer het nemen van deze besluiten.

### Gegevens labelen voor privacyverzoeken {#label}

Afhankelijk van de Experience Cloud-toepassingen die u gebruikt, moet u een label toewijzen aan de specifieke gegevensvelden die moeten worden geopend of verwijderd als reactie op privacyverzoeken. Het proces voor het etiketteren van gegevens varieert tussen toepassingen. Raadpleeg het document over [Experience Cloud-toepassingen](./experience-cloud-apps.md)voor meer informatie over het labelen van gegevens voor elke ondersteunde Adobe-toepassing.

### De typen identiteitsgegevens bepalen die naar de Privacy Service moeten worden verzonden {#identity}

Om een privacyverzoek van een klant te kunnen verwerken, moet ten minste één unieke identiteitswaarde voor die klant in het verzoek zelf worden opgegeven. Een unieke identiteitswaarde is alle informatie die kan worden gebruikt om een individuele persoon en zijn opgeslagen persoonsgegevens te identificeren in uw Experience Cloud-gegevensopslag. De Privacy Service gebruikt deze identiteitsinformatie om van de persoonsgegevens van de klant de plaats te bepalen en te verwerken volgens de aard van het verzoek (toegang, schrapping, of opt-out).

Afhankelijk van de Experience Cloud-toepassingen die uw CRM-systeem gebruikt, variëren het type en het aantal identiteitswaarden dat u voor elke klant moet opgeven. Sommige toepassingen gebruiken hun eigen interne waarden voor de klant-id (zoals Adobe Target-id&#39;s), terwijl andere oplossingen vertrouwen op algemene id&#39;s van Adobe Experience Cloud Identity Service (ECID) die de activiteiten van klanten in alle Experience Cloud-toepassingen volgen. Daarnaast kunnen algemene persoonlijke gegevens, zoals een e-mailadres of telefoonnummer, ook als geldige identiteitsgegevens worden gebruikt.

Het document over [identiteitsgegevens voor privacyverzoeken](./identity-data.md) bevat gedetailleerdere informatie over de typen identiteitsgegevens die voor Privacy Service worden geaccepteerd. Het document biedt ook richtlijnen over hoe u Adobe-technologieën kunt gebruiken om de juiste identiteitsgegevens van uw klanten op te halen bij hun interactie met uw website en deze gegevens naar de Privacy Service te verzenden in API-aanvragen.

### Start met het indienen van privacyaanvragen {#requests}

Zodra u de privacybehoeften van uw bedrijf hebt bepaald en hebt besloten welke identiteitswaarden naar de Privacy Service moeten worden verzonden, kunt u beginnen met het indienen van privacyverzoeken. Met Privacy Service kunt u privacyverzoeken verzenden via de API of de gebruikersinterface.

>[!IMPORTANT]
>
>In de volgende secties vindt u koppelingen naar documentatie over het maken van algemene privacyverzoeken in de API of UI. Afhankelijk van de Experience Cloud-toepassingen die u gebruikt, kunnen de velden die u in de aanvraag moet verzenden, afwijken van de voorbeelden in deze handleidingen.
>
>Als u de API- of UI-handleidingen volgt, raadpleegt u het document over [Privacy Service- en Experience Cloud-toepassingen](./experience-cloud-apps.md) voor meer documentatie over het opmaken van privacyverzoeken voor uw specifieke Experience Cloud-toepassing(en).

#### De API gebruiken

De [Privacy Service-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) biedt verschillende eindpunten voor het maken en beheren van privacytaken met behulp van RESTful API-aanroepen, zodat u programmatisch kunt voldoen aan de privacyregels voor uw Experience Cloud-toepassingen. Zie de handleiding voor ontwikkelaars van de [Privacy Service-API voor meer informatie over het gebruik van de API](api/getting-started.md).

#### De gebruikersinterface gebruiken

>[!NOTE]
>
>De Privacy Service-UI ondersteunt momenteel alleen toegangs- en verwijderingsverzoeken. Alle verzoeken om te weigeren moeten in plaats daarvan via de API worden gedaan.

Met de interface van de Privacy Service kunt u met een grafische interface privacytaken maken en controleren. UI omvat een widget van het Rapport **van de** Status die een visuele vertegenwoordiging van de status van alle actieve verzoeken verstrekt, en staat u toe om nieuwe verzoeken tot stand te brengen door de ingebouwde **Bouwer** van het Verzoek te gebruiken of door JSON- dossiers te uploaden. Raadpleeg de gebruikershandleiding bij de [Privacy Service voor meer informatie over het gebruik van de gebruikersinterface](ui/overview.md).

### Privacy-taken controleren {#monitor}

Nadat u een privacytaak hebt uitgevoerd, kunt u de status en de resultaten van deze taken op verschillende manieren controleren:

| Controlemethode | Beschrijving |
| --- | --- |
| UI Privacy Service | De Privacy Service UI verstrekt een controledashboard dat u toestaat om een visuele vertegenwoordiging van de status van alle actieve verzoeken te bekijken. Raadpleeg de gebruikershandleiding [bij de](ui/overview.md) Privacy Service voor meer informatie. |
| Privacy Service-API | U kunt de status van de banen van de Privacy programmatically controleren door de raadplegingseindpunten te gebruiken die door Privacy Service API worden verstrekt. Zie de handleiding voor ontwikkelaars van [Privacys Service](./api/getting-started.md) voor gedetailleerde stappen over het gebruik van de API. |
| Privacy-gebeurtenissen | Privacy-gebeurtenissen maken gebruik van Adobe I/O-gebeurtenissen die naar een geconfigureerde webhaak zijn verzonden om efficiënte automatisering van taakaanvragen te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de Privacy Service-API te raadplegen om te controleren of een taak voltooid is of dat een bepaalde mijlpaal in een werkstroom is bereikt. Zie de zelfstudie over het [abonneren op Privacy Events](./privacy-events.md) voor meer informatie. |

## Volgende stappen

Dit document biedt een overzicht op hoog niveau van de Privacy Service en de belangrijkste stappen die nodig zijn om de mogelijkheden van de service te gaan gebruiken. Raadpleeg de documentatie bij het volledige overzicht voor meer informatie over de verschillende aspecten van het werken met Privacy Service.
