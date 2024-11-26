---
keywords: Experience Platform;home;populaire onderwerpen;GDPR;gdpr;ccpa:CCPA;pdpa;PDPA;pdpa_that;PDPA_THA;lgpd;LGPD;lgpd_bra;LGPD_BRA;
solution: Experience Platform
title: Overzicht van Privacy Service
description: Ontdek hoe Privacy Service het automatisch naleven van de wettelijke privacyregels in uw gegevensverrichtingen van het Experience Cloud kan vergemakkelijken.
exl-id: 585f7619-5072-413b-9a62-be0ea0cd4d1b
source-git-commit: 61a5b4fd7af68e7379b456ddd37218d183e76256
workflow-type: tm+mt
source-wordcount: '1656'
ht-degree: 0%

---

# Overzicht van Privacy Service

Om betere klantenervaringen te leveren, moet u persoonlijke gegevens van uw klanten verzamelen en opslaan. Wanneer u deze gegevens gebruikt, is het belangrijk dat u de privacy van uw klanten begrijpt en respecteert. De nieuwe wettelijke en organisatorische verordeningen geven gebruikers het recht om tot hun persoonlijke gegevens van uw gegevensopslag toegang te hebben of te schrappen op verzoek.

Adobe Experience Platform Privacy Service is ontwikkeld als reactie op een fundamentele verschuiving in de manier waarop bedrijven de persoonsgegevens van hun klanten moeten beheren. Het centrale doel van Privacy Service is het automatiseren van naleving van de regels van de gegevensprivacy die, wanneer geschonden, in grote boetes kunnen resulteren en gegevensverrichtingen voor uw zaken kunnen verstoren.

Privacy Service verstrekt RESTful API en gebruikersinterface om u te helpen de verzoeken van klantgegevens beheren. U kunt Privacy Service gebruiken om verzoeken in te dienen om toegang te krijgen tot en persoonlijke klantgegevens te verwijderen uit Adobe Experience Cloud-toepassingen, waardoor u gemakkelijker kunt voldoen aan wettelijke en organisatorische privacyregels.

>[!IMPORTANT]
>
>Privacy Service is alleen bedoeld voor betrokkenen en verzoeken om consumentenrechten. Elk ander gebruik van Privacy Service voor het opschonen of onderhouden van gegevens wordt niet ondersteund of toegestaan. Adobe is wettelijk verplicht deze tijdig te vervullen. Als zodanig is het testen van belasting op Privacy Service niet toegestaan, omdat dit een productieomgeving is en een onnodige achterstand oplevert bij geldige privacyverzoeken.
>
>Er is nu een vaste uploadlimiet voor dagelijks gebruik om misbruik van de service te voorkomen. Gebruikers die misbruik van het systeem kunnen maken, hebben toegang tot de service uitgeschakeld. Daarna zal er een vergadering met hen worden gehouden om hun acties te bespreken en te bespreken of Privacy Service aanvaardbaar is.

## Aan de slag met Privacy Service {#getting-started}

Om optimaal gebruik van Privacy Service te maken, moeten verscheidene zeer belangrijke besluiten in termen van de privacyvereisten van uw organisatie, de soorten identiteitsgegevens worden genomen u van uw klanten verzamelt, en de beste manier om uw systeem van CRM met de dienst te verbinden.

Deze besluiten kunnen als volgt worden samengevat:

1. **welke informatie ik van mijn klanten verzamel?**
   * Om optimaal gebruik te maken van Privacy Service, moet u een gedetailleerd inzicht hebben in de soorten gegevens u van uw klanten verzamelt, en welke van het onderworpen is aan privacyverordeningen. Zie de sectie over [ bepalend privacyvereisten ](#requirements) voor meer informatie.
1. **Heb ik correct mijn gegevens geëtiketteerd?**
   * De gegevens moeten correct geëtiketteerd zijn opdat de dienst bepaalt welke gebieden om tijdens privacybanen toegang te hebben of te schrappen. Zie de sectie over [ etiketterend gegevens ](#label) voor meer informatie.
1. **weet ik welke IDs aan Privacy Service te verzenden?**
   * Wanneer het verzenden van privacyverzoeken, individuele klant IDs specifiek voor specifieke Adobe toepassingen moet worden verstrekt. Zie de secties over [ het verstrekken van identiteitsgegevens ](#identity) en [ het maken van privacyverzoeken ](#requests) voor meer informatie.
1. **Hoe volg ik mijn privacybanen?**
   * Nadat u een privacyverzoek hebt ingediend, kunt u de status en de resultaten van dat verzoek op verschillende manieren volgen. Zie de sectie over [ de banen van de controleprivacy ](#monitor) voor meer informatie.

In de volgende secties worden algemene richtsnoeren gegeven voor deze belangrijke, noodzakelijke stappen en wordt verwezen naar verdere documentatie over de Privacy Service voor meer informatie.

### De privacyvereisten van uw organisatie bepalen {#requirements}

Afhankelijk van de aard van uw bedrijf en de rechtsgebieden waaronder het werkt, zijn uw gegevensbewerkingen mogelijk onderworpen aan wettelijke privacyregels. Deze verordeningen geven uw klanten vaak het recht om toegang tot de gegevens te verzoeken u van hen verzamelt, en het recht om de schrapping van die opgeslagen gegevens te verzoeken. Deze verzoeken van klanten om hun persoonsgegevens worden bedoeld als &quot;privacyverzoeken&quot;door de documentatie.

Voor details op de verschillende wettelijke privacyverordeningen die de Privacy Service verzoeken voor, met inbegrip van zeer belangrijke termijnen en antwoorden op vaak gestelde vragen beheert, verwijs naar de [ documentatie van de privacyverordeningen ](./regulations/overview.md).

Als uw gegevensbewerkingen onder de ondersteunde regelgeving vallen, raadpleegt u de documentatie bij deze bewerkingen voor belangrijke informatie, zoals de specifieke privacyrechten die ze aan uw klanten verlenen en compatibiliteitsvensters voor het uitvoeren van privacyverzoeken. Met deze informatie moet rekening worden gehouden wanneer wordt bepaald hoe Privacy Service in uw CRM-systeem moet worden geïntegreerd en hoe klanten met uw website moeten communiceren om privacyverzoeken te kunnen indienen.

Naast wettelijke voorschriften, zouden om het even welke organisatie of industrienormen die op uw organisatie van toepassing zijn ook in overweging moeten worden genomen wanneer het nemen van deze besluiten.

### Gegevens labelen voor privacyverzoeken {#label}

Afhankelijk van de [!DNL Experience Cloud] toepassingen die u gebruikt, moet u de specifieke gegevensgebieden etiketteren die in antwoord op privacyverzoeken zouden moeten worden betreden of worden geschrapt. Het proces voor het etiketteren van gegevens varieert tussen toepassingen. Leren hoe te om gegevens voor elke gesteunde toepassing van de Adobe te etiketteren, zie het document op [ toepassingen van het Experience Cloud ](./experience-cloud-apps.md).

### De typen identiteitsgegevens bepalen die naar de Privacy Service moeten worden verzonden {#identity}

Om een privacyverzoek van een klant te kunnen verwerken, moet ten minste één unieke identiteitswaarde voor die klant in het verzoek zelf worden opgegeven. Een unieke identiteitswaarde is alle informatie die kan worden gebruikt om een individuele persoon en zijn opgeslagen persoonlijke gegevens te identificeren in de [!DNL Experience Cloud] -gegevensopslag. De Privacy Service gebruikt deze identiteitsinformatie om van de persoonsgegevens van de klant de plaats te bepalen en te verwerken volgens de aard van het verzoek (toegang, schrapping, of opt-out).

Afhankelijk van de [!DNL Experience Cloud] toepassingen die uw CRM-systeem gebruikt, variëren het type en het aantal identiteitswaarden dat u voor elke klant moet opgeven. Sommige toepassingen gebruiken hun eigen interne waarden voor de klant-id (zoals Adobe Target-id&#39;s), terwijl andere oplossingen vertrouwen op algemene id&#39;s van Adobe [!DNL Experience Cloud Identity Service] (ECID) die de activiteiten van de klant in alle [!DNL Experience Cloud] -toepassingen bijhouden. Daarnaast kunnen algemene persoonlijke gegevens, zoals een e-mailadres of telefoonnummer, ook als geldige identiteitsgegevens worden gebruikt.

Lees het document over [ identiteitsgegevens voor privacyverzoeken ](./identity-data.md) voor meer gedetailleerde informatie over de types van identiteitsinformatie die voor Privacy Service worden goedgekeurd. Het document biedt ook richtlijnen voor het toepassen van Adobe-technologieën om de juiste identiteitsgegevens van uw klanten op te halen bij de interactie met uw website en om die gegevens naar de Privacy Service te verzenden in API-verzoeken.

### Start met het indienen van privacyaanvragen {#requests}

Zodra u de privacybehoeften van uw bedrijf hebt bepaald en hebt besloten welke identiteitswaarden naar de Privacy Service moeten worden verzonden, kunt u beginnen met het indienen van privacyverzoeken. Gebruik Privacy Service om privacyverzoeken via de API of de gebruikersinterface te verzenden.

#### Gegevens van aanvraagbestand openen {#access-requests}

In de reactie op een succesvol toegangsverzoek, is er a **download URL** die veelvoudige dossiers bevat. Er wordt één bestand opgegeven voor elke Adobe-toepassing waarin gegevens zijn aangevraagd. De bestandsindeling van elke toepassing kan verschillen afhankelijk van de gegevensstructuur van de toepassing.

#### Verzoeken verwijderen - Geen download-URL {#delete-requests}

Er is **geen download URL** in de reactie voor a **schrapt verzoek**, aangezien geen klantengegevens worden teruggewonnen.

>[!IMPORTANT]
>
>In de volgende secties vindt u koppelingen naar documentatie over het maken van algemene privacyverzoeken in de API of UI. Afhankelijk van de [!DNL Experience Cloud] -toepassingen die u gebruikt, kunnen de velden die u in de aanvraag moet verzenden, echter afwijken van de voorbeelden in deze handleidingen.
>
>Aangezien u samen met de API of gidsen UI volgt, verwijs naar het document op [ Privacy Service en de toepassingen van het Experience Cloud ](./experience-cloud-apps.md) voor verdere documentatie over hoe te om privacyverzoeken voor uw bepaalde [!DNL Experience Cloud] toepassingen te formatteren.
>
>Het is ook belangrijk om op te merken dat de privacyverzoeken asynchroon over de toepassingen van het Experience Cloud worden verwerkt. Zodra een verzoek door Privacy Service wordt ontvangen, kan elke toepassing overal van minuten tot weken duren om het verzoek te voltooien. De hoeveelheid tijd die nodig is om elk verzoek te voltooien, is specifiek voor de toepassing waarmee u werkt en de hoeveelheid gegevens die moet worden verwerkt.

#### De API gebruiken {#api}

Om privacy regelnaleving voor uw [!DNL Experience Cloud] toepassingen programmatically te benaderen, kunt u RESTful API vraag aan [[!DNL Privacy Service API] gebruiken ](https://developer.adobe.com/experience-platform-apis/references/privacy-service/) eindpunten om privacybanen tot stand te brengen en te beheren. Voor gedetailleerde stappen op hoe te om API te gebruiken, zie de [ Privacy Service API gids ](api/overview.md).

#### UI gebruiken {#ui}

>[!NOTE]
>
>De Privacy Service-UI ondersteunt momenteel alleen toegangs- en verwijderingsverzoeken. Alle verzoeken om te weigeren moeten in plaats daarvan via de API worden gedaan.

U kunt privacybanen tot stand brengen en controleren gebruikend een grafische interface met Privacy Service UI. De gebruikersinterface bevat een **[!UICONTROL Status Report]** -widget die een visuele weergave biedt van de status van alle actieve aanvragen en u kunt aanvragen maken met de ingebouwde **[!UICONTROL Request Builder]** of door JSON-bestanden te uploaden. Voor meer informatie bij het gebruiken van UI, zie de [ gebruikersgids van de Privacy Service ](ui/overview.md).

### Privacy-taken controleren {#monitor}

Nadat u een privacytaak hebt uitgevoerd, kunt u de status en de resultaten van deze taken op verschillende manieren controleren:

| Controlemethode | Beschrijving |
| --- | --- |
| UI PRIVACY SERVICE | U kunt een visuele vertegenwoordiging van de status van alle actieve verzoeken met het Privacy Service UI controledashboard bekijken. Zie de [ gebruikersgids van de Privacy Service ](ui/overview.md) voor meer informatie. |
| Privacy Service-API | U kunt de status van de banen van de Privacy programmatically controleren door de raadplegingseindpunten te gebruiken die door Privacy Service API worden verstrekt. Zie de [ Privacy Service API gids ](./api/overview.md) voor gedetailleerde stappen op hoe te om API te gebruiken. |
| [!DNL Privacy Events] | [!DNL Privacy Events] gebruik Adobe I/O-gebeurtenissen die naar een geconfigureerde webhaak worden verzonden om een efficiënte automatisering van taakaanvragen te vergemakkelijken. Ze verminderen of elimineren de noodzaak om de Privacy Service-API te raadplegen om te controleren of een taak voltooid is of dat een bepaalde mijlpaal in een workflow is bereikt. Zie het leerprogramma op [ intekenend aan de Gebeurtenissen van de Privacy ](./privacy-events.md) voor meer informatie. |

#### Reacties voor niet-bestaande gebruikers {#non-existing-users}

Wanneer u een toegangs- of verwijderingsverzoek indient, zelfs als de gebruikersgegevens niet worden gevonden, retourneert de reactie altijd een `success` als de aanroep is voltooid. Dit betekent dat zelfs als de gegevens niet bestaan, een toegang of een schrapping met succes zonder enige gegevens kan voltooien die worden teruggewonnen of worden geschrapt.

## Volgende stappen

Dit document biedt een overzicht op hoog niveau van de Privacy Service en de belangrijkste stappen die nodig zijn om de mogelijkheden van de service te gaan gebruiken. Raadpleeg de documentatie bij het overzicht voor meer informatie over de verschillende aspecten van het werken met Privacy Service.
