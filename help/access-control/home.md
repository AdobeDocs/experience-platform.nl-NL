---
keywords: Experience Platform;home;populaire onderwerpen;toegangsbeheer;adobe-beheerconsole
solution: Experience Platform
title: Overzicht van toegangsbeheer
description: Via de Adobe Admin Console wordt het toegangsbeheer voor Adobe Experience Platform verzorgd. Deze functionaliteit maakt gebruik van productprofielen in Admin Console, die gebruikers koppelen aan machtigingen en sandboxen.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 6a466770495b226f890ab67b21c5cb027fd46e02
workflow-type: tm+mt
source-wordcount: '3254'
ht-degree: 0%

---

# Overzicht van toegangsbeheer

De controle van de toegang voor Adobe Experience Platform wordt verstrekt door **[!UICONTROL Permissions]** in [&#x200B; Adobe Experience Cloud &#x200B;](https://experience.adobe.com/). Deze functionaliteit gebruikt rollen en beleid, die gebruikers met toestemmingen en zandbakken verbinden.

## Toegangsbeheerhiërarchie en -workflow

Om toegangsbeheer voor Experience Platform te configureren, moet u systeem- of productbeheerdersrechten hebben voor een organisatie die een Experience Platform-product heeft. De minimumrol die toestemmingen kan verlenen of intrekken is een productbeheerder. Andere beheerderrollen die toestemmingen kunnen beheren zijn systeembeheerders (geen beperkingen). Zie het artikel van het Centrum van de Hulp van Adobe op [&#x200B; administratieve rollen &#x200B;](https://helpx.adobe.com/nl/enterprise/using/admin-roles.html) voor meer informatie.

>[!NOTE]
>
>Vanaf dit punt verwijzen vermeldingen van &quot;beheerder&quot; in dit document naar een productbeheerder of hoger (zoals hierboven beschreven).

Een werkschema op hoog niveau voor het verkrijgen en toewijzen van toegangsmachtigingen kan als volgt worden samengevat:

- Nadat u een licentie hebt verleend aan Adobe Experience Platform of een toepassings-/toepassingsservice die gebruikmaakt van Experience Platform, wordt een e-mail verzonden naar de beheerder die tijdens de licentie is opgegeven.
- De beheerder het programma opent aan [&#x200B; Adobe Admin Console &#x200B;](#adobe-admin-console) en selecteert **Adobe Experience Platform** van de lijst van producten op de overzichtspagina.
- Als u toegang wilt verlenen tot Experience Platform, wordt aangeraden dat de beheerder gebruikers toevoegt aan het standaardproductprofiel: `AEP-Default-All-Users` .
- In de Toestemmingen van Experience Platform, kan de beheerder nieuwe rollen tot stand brengen of de toestemmingen en de gebruikers voor om het even welke bestaande rollen uitgeven.
- Wanneer het creëren van of het uitgeven van een rol, voegt de beheerder gebruikers aan de rol toe gebruikend het **[!UICONTROL users]** lusje, en verleent toestemmingen aan deze gebruikers (zoals &quot; [!UICONTROL Read Datasets]&quot; of &quot;[!UICONTROL Manage Schemas]&quot;) door de toestemmingen van de rol uit te geven. Op dezelfde manier kan de beheerder toegang tot sandboxen toewijzen met dezelfde bewerkingsoptie.
- Wanneer gebruikers zich aanmelden bij de gebruikersinterface van Experience Platform, wordt hun toegang tot Experience Platform-mogelijkheden bepaald door de machtigingen die hun uit de vorige stap zijn verleend. Als een gebruiker bijvoorbeeld niet beschikt over de machtiging [!UICONTROL View Datasets] , is de tab **[!UICONTROL Datasets]** in het zijmenu niet zichtbaar voor die gebruiker.

Voor meer gedetailleerde stappen op hoe te om toegangsbeheer in Experience Platform te beheren, zie de [&#x200B; gebruikershandleiding van de toegangscontrole &#x200B;](./ui/overview.md).

Alle aanroepen naar Experience Platform API&#39;s worden gevalideerd voor machtigingen en retourneren fouten als de juiste machtigingen niet worden gevonden in de huidige gebruikerscontext. Binnen UI, zullen de elementen worden verborgen of worden veranderd afhankelijk van toestemmingen die aan de huidige gebruiker worden verleend.

## Machtigingen {#platform-permissions}

[!UICONTROL Permissions] biedt een centrale locatie voor het beheer van Experience Platform-toegang voor uw organisatie. Via [!UICONTROL Permissions] kunt u groepen gebruikers toegangsmachtigingen verlenen voor verschillende Experience Platform-mogelijkheden, zoals [!UICONTROL Manage Datasets] , [!UICONTROL View Datasets] of [!UICONTROL Manage Profiles] .

### Rollen

In de sectie [!UICONTROL Roles] worden machtigingen aan gebruikers toegewezen via het gebruik van rollen. Rollen staan u toe om toestemmingen aan één of veelvoudige gebruikers te verlenen, en ook hun toegang tot het werkingsgebied van de zandbakken te bevatten die aan hen door rollen worden toegewezen. De gebruikers kunnen aan één of veelvoudige rollen worden toegewezen die tot uw organisatie behoren.

### Standaardrollen

Experience Platform wordt geleverd met twee vooraf geconfigureerde standaardrollen. De volgende tabel geeft een overzicht van de inhoud van elk standaardprofiel, inclusief de sandbox waartoe ze toegang verlenen en de machtigingen die ze binnen het bereik van die sandbox verlenen.

| Rol | Toegang tot sandbox | Machtigingen |
| --- | --- | --- |
| Standaardproductie, alle toegang | Prod | Alle toestemmingen van toepassing op Experience Platform, behalve de toestemmingen van het Beleid Sandbox. |
| Sandbox-beheerders | N.v.t. | Biedt toegang tot de `Prod` -sandbox en tot de bevoegdheden van Sandbox Administration. |

## Sandboxen en machtigingen

Niet-productiesandboxen zijn een vorm van gegevensvirtualisatie waarmee u gegevens kunt isoleren van andere sandboxen. Deze sandboxen worden doorgaans gebruikt voor ontwikkelingsexperimenten, -tests of -tests. Rolmachtigingen geven gebruikers van de rol toegang tot Experience Platform-functies binnen de sandboxomgevingen waartoe ze toegang hebben. Een Experience Platform-standaardlicentie geeft u vijf sandboxen (één productie en vier niet-productie). U kunt in totaal maximaal 75 sandboxen toevoegen aan pakketten van tien niet-productiesandboxen. Neem voor meer informatie contact op met de beheerder van uw organisatie of uw Adobe-vertegenwoordiger.

Voor meer informatie over zandbakken in Experience Platform, gelieve te verwijzen naar het [&#x200B; zandbakenoverzicht &#x200B;](../sandboxes/home.md).

### Toegang tot sandboxen

De toegang tot sandboxen wordt beheerd via rollen. Voor gedetailleerde stappen op hoe te om toegang tot een zandbak voor een rol toe te laten, zie de [&#x200B; attributen gebaseerde gids van de toegangsbeheerrollen &#x200B;](./abac/ui/roles.md).

Gebruikers kunnen toegang krijgen tot een of meer sandboxen binnen een rol. Als één gebruiker in twee of meer rollen inbegrepen is, zal die gebruiker toegang tot alle zandbakken hebben inbegrepen in die rollen.

Met de machtiging Sandboxbeheer kunnen gebruikers sandboxen beheren, weergeven of opnieuw instellen.

### Bronmachtigingen {#permissions}

De toestemmingen van het middel verlenen toegang tot specifieke mogelijkheden van Experience Platform. De middelen worden verdeeld in categorieën die een reeks relevante toestemmingen bevatten, die individueel aan rollen kunnen worden toegewezen.

In [!UICONTROL Permissions] worden in de werkruimte met rolbronnen de sandboxen en machtigingen weergegeven die actief zijn voor die rol:

![&#x200B; het middelwerkruimte van A rol met een lijst van geselecteerde categorieën en toestemmingen.](./images/permissions.png)

De volgende lijst schetst de beschikbare middelcategorieën voor zowel Experience Platform als toepassingen die door Toestemmingen worden beheerd:

| Categorie | Beschrijving |
| --- | --- |
| [!DNL Adobe Mix Modeler] | Machtigingen voor [!DNL Adobe Mix Modeler] configureren, beheren en weergeven. |
| [!DNL AI Assistant] | Configureer machtigingen voor [!DNL AI Assistant] . |
| [!DNL Alerts] | Configureer de machtigingen voor beheren, oplossen en weergeven voor waarschuwingen en waarschuwingen. |
| [!DNL B2B Account Lists] | Configureer beheermachtigingen, weergave- en publicatiemachtigingen voor B2B-accountlijsten, inclusief handelingen zoals het toevoegen, verwijderen, importeren en verwijderen van accounts uit accountlijsten. |
| [!DNL B2B Admin Configurations] | Configureer beheer- en weergavemachtigingen voor B2B-beheerconfiguraties, waaronder verbindingen voor digitaal middelenbeheer, opslagruimten voor bedrijfsmiddelen en gebeurtenissen. |
| [!DNL B2B Assets] | Configureer beheer- en weergavemachtigingen voor B2B-elementen, zoals e-mails, SMS, bestemmingspagina&#39;s, fragmenten, sjablonen en afbeeldingen. |
| [!DNL B2B Buying Groups] | Vorm beheer en meningstoestemmingen voor B2B het kopen groepen, met inbegrip van eigenschappen zoals oplossingsbelangen, rolmalplaatjes, en het kopen groepsstatus. |
| [!DNL B2B Channel Configurations] | Configureer beheer- en weergavemachtigingen voor B2B-kanaalconfiguraties, inclusief instellingen zoals communicatielimieten, API-referenties en beveiligingsinstellingen. |
| [!DNL B2B Dashboards] | Configureer weergavemachtigingen voor B2B-dashboards, inclusief functies zoals accountbetrokkenheid, het kopen van groepsfasen, het surfen op accounts en contactdekking. |
| [!DNL B2B Journeys] | Configureer machtigingen voor beheren, weergeven en publiceren voor B2B-reizen, inclusief functies zoals account- en persoonlijke handelingen, gebeurtenislisteners en gesplitste paden. |
| [!DNL Campaigns] | Configureer de machtigingen voor beheren, publiceren en weergeven voor campagnes in Journey Optimizer. |
| [!DNL Channel Configurations] | Configureer de functies voor het beheren, weergeven en exporteren van kanaalconfiguraties, zoals subdomeinen, IP-pools, voorinstellingen voor berichten, PTR-records, suppressielijsten, instellingen voor openingspagina&#39;s, SMS-instellingen en het routeren van bestanden. |
| [!DNL Collaborations] | Configureer beheer- en weergavemachtigingen voor Collaboration-functies voor realtime klantgegevensprofiel. |
| [!DNL Computed Attributes] | Configureer beheer- en weergavemachtigingen voor het samenstellen of publiceren van berekende kenmerken. |
| [!DNL Customer Managed Keys] | Configureer beheermachtigingen voor door de klant beheerde sleutels. |
| [!DNL Dashboards] | Configureer beheer- en weergavemachtigingen voor standaard-, aangepaste en gelicentieerde dashboards. |
| [!DNL Data Collection] | Configureer beheer- en weergavemachtigingen voor gegevensstromen. |
| [!DNL Data Governance] | Vorm leiden, toepassen, en meningstoestemmingen op de eigenschappen van de gegevensgeneratie zoals etiketten, beleid, en activiteitenlogboeken. |
| [!DNL Data Ingestion] | Configureer beheer- en weergavemachtigingen voor functies voor gegevensinvoer, zoals bronnen en gedeelde gebruikers. |
| [!DNL Data Lifecycle] | Configureer beheer- en weergavemachtigingen voor functies voor gegevenshygiëne. |
| [!DNL Data Management] | Vorm beheer en meningstoestemmingen aan gegevensbeheereigenschappen zoals datasets en controledatasets en stromen. |
| [!DNL Data Modeling] | Vorm leiden en meningstoestemmingen aan gegevens modelleringseigenschappen zoals schema&#39;s, verhoudingen, en identiteitsmeta-gegevens bekijken. |
| [!DNL Data Science Workspace] | Configureer beheermachtigingen voor [!DNL Data Science Workspace] . |
| [!DNL Decision Management] | Vorm leiden en meningstoestemmingen aan besluiten, aanbiedingen, en het rangschikken van strategieeigenschappen in besluitvormingsbeheer. |
| [!DNL Destinations] | Vorm beheer en meningstoestemmingen aan bestemmingen, met inbegrip van eigenschappen zoals activering en creatie met Doelen SDK. |
| [!DNL Federated Data] | Configureer beheer- en weergavemachtigingen voor gefederaliseerde gegevensfuncties. |
| [!DNL Identity Management] | Configureer beheer- en weergavemachtigingen voor de identiteitsfuncties, zoals naamruimten en de identiteitsgrafiek. |
| [!DNL Intelligent Service] | Configureer beheer- en weergavemachtigingen voor de toewijzing van AI en AI aan klanten in de intelligente service. |
| [!DNL IP Warmup Configurations] | Vorm leiden en meningstoestemmingen aan IP warmup plannen en meningstoestemmingen om IP warmteopwarmingsrapporten te bekijken. |
| [!DNL Journey Optimizer Library] | Configureer beheermachtigingen voor bibliotheekitems in Adobe Journey Optimizer. |
| [!DNL Journey Optimizer Rules] | Configureer beheer- en weergavemachtigingen voor frequentieregels in Adobe Journey Optimizer. |
| [!DNL Journeys] | Configureer de machtigingen voor beheren, publiceren en weergeven voor reizen, inclusief functies zoals reisrapporten, gebeurtenissen, gegevensbronnen en handelingen. |
| [!DNL Messages] | Configureer de machtigingen voor beheren, publiceren en weergeven voor berichten, inclusief functies zoals berichtvoorbeeld en testen. |
| [!DNL Privacy Service] | Configureer beheer- en weergavemachtigingen voor Privacy Service-functies. |
| [!DNL Profile Management] | Vorm leiden, mening, de uitvoer, en evaluatiemachtigingen aan de eigenschappen van de profieldienst zoals publiek, profielen, en fusiebeleid. |
| [!DNL Prospects] | Vorm leiden en meningstoestemmingen aan perspectiefschema&#39;s, profielen, en publiek, met inbegrip van eigenschappen zoals het zien van de perspectiefaccordeon. |
| [!DNL Query Service] | Vorm beheer toestemmingen aan de eigenschappen van de vraagdienst zoals niet-verkennende credentie en gestructureerde SQL vragen. |
| [!DNL Reports] | Vorm meningstoestemmingen aan kanaalrapporten. |
| [!DNL Sandbox Administration] | Configureer machtigingen voor beheren, weergeven en opnieuw instellen tijdens het beheer van sandboxen. |
| [!DNL Traits Configuration] | Configureer de functies voor beheren en weergeven via de gebruikersinterface voor berekende kenmerken. |
| [!DNL Translation Services] | Configureer beheer- en weergavemachtigingen voor vertaalservices voor projecten, taken, revisies, interne instellingen en providers. |

In de volgende tabel worden de beschikbare machtigingen voor Experience Platform in de rol beschreven, met beschrijvingen van de specifieke Experience Platform-mogelijkheden waartoe deze toegang verleent. Voor gedetailleerde stappen op hoe te om toestemmingen aan een rol toe te voegen, zie de [&#x200B; attributen gebaseerde gids van de toegangsbeheerrollen &#x200B;](./abac/ui/roles.md).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Harmonized Data] | De mogelijkheid om geharmoniseerde gegevens te bekijken en te wijzigen. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Harmonized Data] | Alleen-lezen toegang tot geharmoniseerde gegevens. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Configurations] | De capaciteit om modelconfiguraties te bekijken en te wijzigen. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Configurations] | Alleen-lezen toegang tot modelconfiguraties. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL Manage Adobe Mix Modeler Models Plans Configurations] | De capaciteit om planconfiguraties te bekijken en te wijzigen. |
| [!DNL Adobe Mix Modeler] | [!UICONTROL View Adobe Mix Modeler Models Plans Configurations] | Alleen-lezen toegang tot planningsconfiguraties. |
| [!DNL AI Assistant] | [!UICONTROL Enable AI Assistant] | Mogelijkheid om de [[!DNL [AI assistant]]](../ai-assistant/access.md) vragen te stellen. |
| [!DNL AI Assistant] | [!UICONTROL View Operational Insights] | Toegang om reacties op [&#x200B; operationele inzichten &#x200B;](../ai-assistant/home.md##operational-insights) vragen te verkrijgen. |
| [!DNL AI Assistant] | [!UICONTROL Generate Content] | Gebruikers toestaan inhoud te genereren met de [!DNL AI Assistant] . |
| [!DNL AI Assistant] | [!UICONTROL Manage Brand Kit] | Laat gebruikers toe om merkrichtlijnen tot stand te brengen gebruikend [!DNL AI Assistant]. |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | Alleen-lezen toegang voor waarschuwingsgeschiedenis. |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | Toegang tot waarschuwingen lezen, bewerken en verwijderen. |
| [!DNL Alerts] | [!UICONTROL View Alerts] | Alleen-lezen toegang voor waarschuwingen. |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | Toegang tot waarschuwingen lezen, maken, bewerken en verwijderen. |
| [!DNL B2B Account Lists] | [!UICONTROL Manage B2B Account Lists] | Mogelijkheid om **[!UICONTROL Account Lists]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Account Lists]** moeten toegang hebben tot alle CRUD-functies in accountlijsten: `/accounts-list` . |
| [!DNL B2B Admin Configurations] | [!UICONTROL Manage B2B Admin Configurations] | Mogelijkheid om **[!UICONTROL B2B Admin Configurations]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL B2B Admin Configurations]** moeten toegang hebben tot alle CRUD-functies van SMS API Credentials: `/admin-configs` . |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Assets] | Mogelijkheid om **[!UICONTROL Assets]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Assets]** moeten toegang hebben tot alle Assets CRUD-functies: `/assets-listing` . |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Templates] | Mogelijkheid om **[!UICONTROL Templates]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Templates]** moeten toegang hebben tot alle Templates CRUD-functies: `/b2b-content-templates` . |
| [!DNL B2B Assets] | [!UICONTROL Manage B2B Fragments] | Mogelijkheid om **[!UICONTROL Fragments]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Fragments]** moeten toegang hebben tot alle Fragments CRUD-functies: `/fragments` . |
| [!DNL B2B Buying Groups] | [!UICONTROL Manage B2B Buying Groups] | Mogelijkheid om **[!UICONTROL Buying Groups]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Buying Groups]** moeten toegang hebben tot alle CRUD-functies voor groepen kopen: `/buying-groups` . |
| [!DNL B2B Dashboards] | [!UICONTROL Manage B2B Engagement Dashboards] | Mogelijkheid om **[!UICONTROL Dashboard]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Dashboards]** moeten toegang hebben tot alle Dashboards CRUD-functies: `/insights-dashboard` . |
| [!DNL B2B Channel Configurations] | [!UICONTROL Manage B2B Channels Configurations] | Mogelijkheid om **[!UICONTROL Channels]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Channels]** moeten toegang hebben tot alle Kanalen CRUD-functies: `/channels-config` . |
| [!DNL B2B Journeys] | [!UICONTROL Manage B2B Account Journeys] | Mogelijkheid om **[!UICONTROL Account Journeys]** in de linkernav weer te geven en te openen. Gebruikers met toegang tot **[!UICONTROL Account Journeys]** dienen toegang te hebben tot alle CRUD-functies voor accountreizen: `/account-journeys` . |
| [!DNL Campaigns] | [!UICONTROL Manage Campaigns] | Toegang tot het lezen, maken, bewerken en verwijderen van campagnes. |
| [!DNL Campaigns] | [!UICONTROL Approve and Publish Campaigns] | De mogelijkheid om campagnes goed te keuren en te publiceren. |
| [!DNL Campaigns] | [!UICONTROL Publish Campaigns] | Mogelijkheid om campagnes te publiceren. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns] | Alleen-lezen toegang tot campagnes. |
| [!DNL Campaigns] | [!UICONTROL View Campaigns Report] | Alleen-lezen toegang tot campagnerapporten. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages General Settings] | Alleen-lezen toegang tot algemene instellingen voor berichten. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Subdomains Delegations] | Toegang tot het lezen, maken, bewerken en verwijderen van subdomeindelegaties. |
| [!DNL Channel Configurations] | [!UICONTROL Manage IP Pools] | Toegang tot gelezen, creeer, en geef IP pools uit. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages General Settings] | Toegang tot algemene instellingen voor berichten lezen, maken, bewerken en verwijderen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Messages Presets] | Toegang tot voorinstellingen voor berichten lezen, maken, bewerken en verwijderen. |
| [!DNL Channel Configurations] | [!UICONTROL View Messages Presets] | Voorinstellingen voor alleen-lezen berichten. |
| [!DNL Channel Configurations] | [!UICONTROL Manage PTR Records] | Toegang tot PTR-records lezen en bewerken. |
| [!DNL Channel Configurations] | [!UICONTROL View PTR Records] | Alleen-lezen toegang tot PTR-records. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Suppression] | Toegang tot het lezen, maken, bewerken en verwijderen van suppressieregels. |
| [!DNL Channel Configurations] | [!UICONTROL View Suppression List] | Alleen-lezen toegang tot de suppressielijst. |
| [!DNL Channel Configurations] | [!UICONTROL Export Suppression List] | Toegang tot het exporteren van de suppressielijst als een CSV-bestand. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Landing Page Settings] | Toegang tot het lezen, maken, bewerken en verwijderen van landingspagina-instellingen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Settings] | Toegang tot het lezen, maken, bewerken en verwijderen van SMS-instellingen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage SMS Subdomains] | Toegang tot het lezen, maken, bewerken en verwijderen van SMS-subdomeinen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage File Routing] | Toegang tot het lezen, maken, bewerken en verwijderen van bestandsgroepen. |
| [!DNL Channel Configurations] | [!UICONTROL View File Routing] | Alleen-lezen toegang tot bestandsgroepen. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Seedlist] | De mogelijkheid om de zaadlijst te maken en te bewerken. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Language Settings] | De mogelijkheid om de taalinstellingen te maken en te bewerken. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Web Subdomains] | De mogelijkheid om CJM-websubdomeinen te maken en te bewerken. |
| [!DNL Channel Configurations] | [!UICONTROL Manage Push Credentials] | De mogelijkheid om pushreferenties te maken, te bewerken en te verwijderen. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Instances] | De samenwerkingsinstanties van een organisatie weergeven, maken, bijwerken en verwijderen. Ontdek de samenwerkingsinstanties van andere organisaties. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Instances] | Lees de samenwerkingsinstanties van een organisatie en ontdek de samenwerkingsinstanties van andere organisaties. |
| [!DNL Collaborations] | [!UICONTROL Manage Connection Invites] | De mening, creeert, en schrapt verbindingsuitnodigingen die door uw organisatie in werking worden gesteld. Accepteer en weiger een verbindingsuitnodiging die is geïnitieerd door andere organisaties. |
| [!DNL Collaborations] | [!UICONTROL Read Connection Invites] | Alleen-lezen toegang tot verbindingsuitnodigingen. |
| [!DNL Collaborations] | [!UICONTROL Manage Collaboration Connections] | Een adverteerder kan instellingen weergeven, maken en bijwerken, en verbindingen verzenden en verwijderen. Een uitgever kan verbindingen weergeven, accepteren of weigeren. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Connections] | Alleen-lezen toegang tot verbindingen. |
| [!DNL Collaborations] | [!UICONTROL Manage Audience Data] | Aan boord en ontdek publiek. Werk publieke, persoonlijke en aangepaste doelgroepen bij en beheer de metagegevensinstellingen voor de doelinventaris. |
| [!DNL Collaborations] | [!UICONTROL Read Audience Data] | Lees en ontdek publiek. |
| [!DNL Collaborations] | [!UICONTROL Manage Measurement Data] | Metingsgegevens aan boord, bijwerken en verwijderen. |
| [!DNL Collaborations] | [!UICONTROL Read Measurement Data] | Alleen-lezen toegang tot meetgegevens. |
| [!DNL Collaborations] | [!UICONTROL Manage Projects] | Projecten weergeven, maken, bijwerken en verwijderen voor de detectie-, deelings-, activeer- en meetactiviteiten. |
| [!DNL Collaborations] | [!UICONTROL Read Projects] | Projecten weergeven voor alle detectie-, deelings-, activeer- en meetactiviteiten. |
| [!DNL Collaborations] | [!UICONTROL Read User Activities] | Alleen-lezen toegang tot gebruikersactiviteiten. |
| [!DNL Collaborations] | [!UICONTROL Export User Activities] | Gebruikersactiviteiten exporteren. |
| [!DNL Collaborations] | [!UICONTROL Read Collaboration Credit Monitoring] | Kredietcontrole op organisatorisch en instantieniveau. |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | Alleen-lezen toegang voor het tabblad, overzicht en details van berekende kenmerken. |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | Toegang tot het lezen, maken, verwijderen van concepten en het deactiveren van berekende kenmerken. |
| [!DNL Customer Managed Keys] | [!UICONTROL Manage Customer Managed Keys] | Toegang om door klanten beheerde sleutels te bekijken en te vormen. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Alleen-lezen toegang om het dashboard voor het licentiegebruik weer te geven. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Voeg douanekenmerken toe die nog niet in het gegevenspakhuis zijn. |
| [!DNL Dashboards] | [!UICONTROL View Standard Dashboards] | Alleen-lezen toegang tot de dashboards van profielen, doelen en segmenten. Biedt ook toegang tot dashboards in de linkernavigatie en het tabblad Dashboards voorraad en integratie. |
| [!DNL Dashboards] | [!UICONTROL Manage Custom Dashboards] | Toegang tot het maken of bewerken van een dashboard. |
| [!DNL Dashboards] | [!UICONTROL View Custom Dashboards] | Alleen-lezen toegang tot door de gebruiker gedefinieerde dashboards. |
| [!DNL Dashboards] | [!UICONTROL Manage Report Schedules] | Mogelijkheid om planningen te maken. |
| [!DNL Dashboards] | [!UICONTROL Export Dashboard Data] | Controls a user&#39;s ability to export tabular data from query pro mode dashboards. |
| [!DNL Data Collection] | [!UICONTROL Manage Datastreams] | Toegang tot het lezen, maken en bewerken van gegevensstromen. |
| [!DNL Data Collection] | [!UICONTROL View Datastreams] | Alleen-lezen toegang tot gegevensstreams. |
| [!DNL Data Governance] | [!UICONTROL Manage Usage Labels] | Toegang tot het lezen, maken en verwijderen van gebruikslabels. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Toegang tot het lezen, maken, bewerken en verwijderen van beleidsregels voor gegevensgebruik. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Alleen-lezen toegang voor beleidsregels voor gegevensgebruik die tot uw organisatie behoren. |
| [!DNL Data Governance] | [!UICONTROL View User Activity Log] | Read-only toegang tot mening registreerde [&#x200B; controlelogboeken &#x200B;](../landing/governance-privacy-security/audit-logs/overview.md) van de activiteiten van Experience Platform. |
| [!DNL Data Governance] | [!UICONTROL View Privacy Console] | Alleen-lezen toegang tot privacyconsoles. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Toegang tot bronnen lezen, maken, bewerken en uitschakelen. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Alleen-lezen toegang tot beschikbare bronnen op het tabblad **[!UICONTROL Catalog]** en geverifieerde bronnen op het tabblad **[!UICONTROL Browse]** . |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Toegang tot het maken, accepteren en weigeren van partners om twee organisaties te verbinden en [!DNL Segment Match] -stromen in te schakelen. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Toegang tot het lezen, maken, bewerken en publiceren van [!DNL Segment Match] -feeds met actieve partners. |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | Alleen-lezen toegang voor de levenscyclus van gegevens. |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | Toegang tot de levenscyclus van gegevens lezen, maken, bewerken en verwijderen. |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Toegang tot het lezen, maken, bewerken en verwijderen van schema&#39;s en gerelateerde bronnen. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Alleen-lezen toegang tot schema&#39;s en gerelateerde bronnen. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Toegang tot het lezen, maken, bewerken en verwijderen van schemarelaties. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Toegang tot het lezen, maken, bewerken en verwijderen van identiteitsmetagegevens voor schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Toegang tot het lezen, creëren, uitgeven, en schrappen datasets. Alleen-lezen toegang voor schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Alleen-lezen toegang voor gegevenssets en schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Alleen-lezen toegang tot gegevenssets en streams controleren. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Toegang tot lezen, maken, bewerken en verwijderen in [!DNL Data Science Workspace] . |
| [!DNL Decision Management] | [!UICONTROL Manage Experience Decisioning] | Mogelijkheid om ervaren beslissingsentiteiten te beheren. |
| [!DNL Decision Management] | [!UICONTROL View Experience Decisioning] | Alleen-lezen toegang tot ervaren beslissingsentiteiten. |
| [!DNL Decision Management] | [!UICONTROL Manage Decisions] | Toegang tot het lezen, maken, bewerken en verwijderen van beslissingsentiteiten. |
| [!DNL Decisions Management] | [!UICONTROL View Decisions] | Alleen-lezen toegang tot beslissingsentiteiten. |
| [!DNL Decision Management] | [!UICONTROL Manage Offers] | Toegang tot het lezen, maken, bewerken en verwijderen van alle aanbiedingen en componenten. Alleen-lezen toegang tot beslissingen en verzamelingen. |
| [!DNL Decsion Management] | [!UICONTROL Manage Ranking Strategies] | Toegang tot het lezen, maken, bewerken en verwijderen van aangepaste rapporten en actiefuncties. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Alleen-lezen toegang om beschikbare doelen op het tabblad **[!UICONTROL Catalog]** en geverifieerde doelen op het tabblad **[!UICONTROL Browse]** weer te geven. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Toegang tot het lezen, creëren, en schrappen van bestemmingsverbindingen en bestemmingsrekeningen. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Mogelijkheid om gegevens te activeren naar actieve doelen die zijn gemaakt. Deze toestemming vereist ook [!UICONTROL View Destinations] of [!UICONTROL Manage Destinations] om aan de gebruiker te worden verleend die bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | De capaciteit om publiek aan bestaande bestemmingen te activeren, zonder de [&#x200B; toewijzingsstap &#x200B;](../destinations/ui/activate-batch-profile-destinations.md#mapping) te tonen. Gebruikers kunnen doelgroepen toevoegen aan en verwijderen uit activeringsworkflows, maar kunnen toegewezen kenmerken of identiteiten niet toevoegen of verwijderen. Deze toestemming vereist ook dat de [!UICONTROL View Destinations] toestemming wordt verleend aan de gebruiker die gegevens aan bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | Mogelijkheid om gegevenssets te lezen, te maken, te bewerken en uit te schakelen. Mogelijkheid om gegevens ook te activeren naar actieve datasets die zijn gemaakt. Deze toestemming vereist ook dat de [!UICONTROL View Destinations] toestemming wordt verleend aan de gebruiker die gegevens aan bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Mogelijkheid aan auteursbestemmingen gebruikend [&#x200B; Adobe Experience Platform Destination SDK &#x200B;](../destinations/destination-sdk/overview.md). |
| [!DNL Federated Data] | [!UICONTROL Manage Federated Data] | De capaciteit om tot alle gefederaliseerde gegevenseigenschappen zoals het creëren van schema&#39;s, modellen, en samenstellingen toegang te hebben. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | Toegang tot het lezen, maken, bewerken en verwijderen van naamruimten. |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | Alleen-lezen toegang voor naamruimten. |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | Alleen-lezen toegang voor identiteitsgrafieken. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Settings] | Toegang tot het lezen, maken en bewerken van identiteitsinstellingen. |
| [!DNL Identity Management] | [!UICONTROL View Identity Settings] | Alleen-lezen toegang tot identiteitsinstellingen. |
| [!DNL Intelligent Services] | [!UICONTROL View Attribution AI] | Alleen-lezen toegang voor Attribution AI-instellingen en -inzichten. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Attribution AI] | Toegang tot het lezen, maken, bewerken en verwijderen van Attribution AI-modellen. |
| [!DNL Intelligent Services] | [!UICONTROL View Customer AI] | Toegang tot het lezen of bekijken van AI-modellen van de Klant. |
| [!DNL Intelligent Services] | [!UICONTROL Manage Customer AI] | Toegang tot het maken, bijwerken, verwijderen, inschakelen of uitschakelen van AI-modellen van klanten. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Plans] | Read-only toegang tot IP warmup plannen. |
| [!DNL IP Warmup Configurations] | [!UICONTROL Manage IP Warmup Plans] | De capaciteit om IP warmup plannen te beheren. |
| [!DNL IP Warmup Configurations] | [!UICONTROL View IP Warmup Reports] | Alleen-lezen toegang tot IP-warmteoprapporten. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys] | Toegang tot het lezen, maken, bewerken en verwijderen van reizen. |
| [!DNL Journeys] | [!UICONTROL View Journeys] | Alleen-lezen toegang tot reizen. |
| [!DNL Journeys] | [!UICONTROL View Journeys Report] | Alleen-lezentoegang tot reisrapporten. |
| [!DNL Journeys] | [!UICONTROL Manage Journeys Events, Data Sources and Actions] | Toegang tot het lezen, maken, bewerken en verwijderen van gebeurtenissen, gegevensbronnen of handelingen. |
| [!DNL Journeys] | [!UICONTROL View Journeys Events, Data Sources and Actions] | Alleen-lezen toegang tot gebeurtenissen, gegevensbronnen of handelingen. |
| [!DNL Journeys] | [!UICONTROL Approve and Publish Journeys] | De mogelijkheid om reizen goed te keuren en te publiceren wanneer een beleid wordt toegepast. |
| [!DNL Journeys] | [!UICONTROL Publish Journeys] | De mogelijkheid om reizen te publiceren. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Manage Library Items] | De mogelijkheid om opgeslagen expressies toe te voegen en te verwijderen. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Publish Fragments] | De mogelijkheid om inhoudsfragmenten te publiceren. |
| [!DNL Journey Optimizer Library] | [!UICONTROL Simulate Content] | Toegang tot de optie Inhoud simuleren voor voorvertonen en proefdrukken. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL View Frequency Rules] | Alleen-lezen toegang tot frequentieregels. |
| [!DNL Journey Optimizer Rules] | [!UICONTROL Manage Frequency Rules] | Toegang tot het lezen, maken, bewerken of verwijderen van frequentieregels. |
| [!DNL Messages] | [!UICONTROL Manage Messages] | Toegang tot het lezen, maken, bewerken en verwijderen van berichten. |
| [!DNL Messages] | [!UICONTROL View Messages] | Alleen-lezen toegang tot berichten. |
| [!DNL Messages] | [!UICONTROL View Messages Report] | Toegang tot berichtrapporten lezen en bewerken. |
| [!DNL Messages] | [!UICONTROL Publish Messages] | Mogelijkheid om berichten te publiceren. |
| [!DNL Messages] | [!UICONTROL Manage Messages Preview and Test] | Mogelijkheid om berichten goed te keuren en te publiceren wanneer een beleid wordt toegepast. |
| [!DNL Privacy Service] | [!UICONTROL Manage Privacy Service] | Toegang tot workflows voor het lezen en schrijven van privacy. |
| [!DNL Privacy Service] | [!UICONTROL View Privacy Service] | Alleen-lezen toegang tot privacyworkflows. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Toegang tot gelezen, creeer, geef, en schrap datasets uit die voor klantenprofielen worden gebruikt. Alleen-lezen toegang tot beschikbare profielen. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Alleen-lezen toegang tot beschikbare profielen. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Toegang tot het lezen, maken, bewerken en verwijderen van soorten publiek. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Alleen-lezen toegang tot het beschikbare publiek. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Toegang tot het lezen, maken, bewerken en verwijderen van samenvoegbeleidsregels. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Alleen-lezen toegang tot beschikbaar samenvoegbeleid. |
| [!DNL Profile Management] | [!UICONTROL Import Audiences] | Mogelijkheid om de CSV-upload-workflow te gebruiken om nieuwe doelgroepen te importeren. |
| [!DNL Profile Management] | [!UICONTROL Export Audience Segment] | Mogelijkheid om een geëvalueerd publiek naar een dataset te exporteren. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | De capaciteit om profielen voor een publiek te produceren door een segmentdefinitie te evalueren. |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | Alleen-lezen toegang tot instellingen en configuraties voor alle B2B AI/ML-services. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | Toegang tot het lezen, creëren, uitgeven, en schrappen montages en configuraties voor alle diensten B2B AI/ML. |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | Alleen-lezen toegang tot B2B-entiteitsprofielen (zoals Account, Opportunity, enzovoort), instellingen en configuraties voor alle B2B AI/ML-services en B2B-dashboardwidgets. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | Toegang tot het lezen, maken, bewerken en verwijderen van B2B-entiteitsprofielen (zoals Account, Opportunity, enzovoort). Alleen-lezen toegang voor instellingen en configuraties voor alle B2B AI/ML-services en B2B-dashboardwidgets. |
| [!DNL Profile Management] | [!UICONTROL Manage Lookalikes] | Mogelijkheid om een vergelijkbaar publiek te maken of te verwijderen. |
| [!DNL Profile Management] | [!UICONTROL View B2B Experience] | Mogelijkheid om B2B-profielen en -kenmerken weer te geven. |
| [!DNL Profile Management] | [!UICONTROL View Profile Settings] | Alleen-lezen toegang tot alle profielinstellingen. |
| [!DNL Profile Management] | [!UICONTROL Manage Profile Settings] | Toegang tot alle profielinstellingen lezen en bewerken. |
| [!DNL Prospects] | [!UICONTROL View Prospects] | Alleen-lezen toegang tot perspectiefschema&#39;s, profielen, doelgroepen en de perspectiefaccordeon. |
| [!DNL Prospects] | [!UICONTROL Manage Prospects] | Mogelijkheid om perspectiefschema&#39;s, profielen en doelgroepen te maken en te beheren. Alleen-lezen toegang tot de perspectiefaccordeon. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Toegang tot het lezen, maken, bewerken en verwijderen van gestructureerde SQL-query&#39;s voor Experience Platform-gegevens. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Toegang tot het creëren, bijwerken, en schrappen van niet-vervallende geloofsbrieven voor de toegang van de Dienst van de Vraag. |
| [!DNL Query Service] | [!UICONTROL Manage Query Sessions] | Mogelijkheid om bestaande sessies te verwijderen. |
| [!DNL Query Service] | [!UICONTROL Manage Allow List] | Mogelijkheid om IP-beperkingen voor uw organisatie te beheren. |
| [!DNL Reports] | [!UICONTROL View Channel Reports] | De capaciteit om kanaalrapporten te bekijken en te wijzigen. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Toegang tot het lezen, maken, bewerken en verwijderen van sandboxen. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Alleen-lezen toegang voor sandboxen die tot uw organisatie behoren. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Mogelijkheid om een sandbox opnieuw in te stellen. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Packages] | Toegang tot pakketten maken, importeren of exporteren. |
| [!DNL Sandbox Administration] | [!UICONTROL Share Packages] | Toegang tot pakketten delen in verschillende organisaties. |
| [!DNL Traits Configurations] | [!UICONTROL View Traits] | Alleen-lezen toegang voor kenmerken. |
| [!DNL Traits Configurations] | [!UICONTROL Manage Traits] | Toegang tot het beheren van kenmerken. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Projects] | De mogelijkheid om vertaalprojecten te beheren. |
| [!DNL Translation Service] | [!UICONTROL View Translation Projects] | Alleen-lezen toegang tot vertaalprojecten. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Tasks] | De mogelijkheid om vertaaltaken te beheren. |
| [!DNL Translation Service] | [!UICONTROL View Translation Tasks] | Alleen-lezen toegang tot vertaaltaken. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Reviews] | De mogelijkheid om vertaalbeoordelingen te beheren. |
| [!DNL Translation Service] | [!UICONTROL View Translation Reviews] | Alleen-lezen toegang tot revisies voor vertalingen. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation In-house] | De mogelijkheid om de vertaling intern te beheren. |
| [!DNL Translation Service] | [!UICONTROL View Translation In-house] | Alleen-lezen toegang tot interne vertaling. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Settings] | Beheerders kunnen de vertaalinstellingen beheren. |
| [!DNL Translation Service] | [!UICONTROL Manage Translation Providers] | De mogelijkheid om vertaalproviders te beheren. |

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd in de belangrijkste principes van toegangscontrole in Experience Platform. U kunt nu aan de [&#x200B; attributen gebaseerde gebruikershandleiding van de toegangscontrole &#x200B;](./abac/overview.md) voor gedetailleerde stappen op hoe gebruik Experience Cloud blijven om rollen tot stand te brengen en toestemmingen voor Experience Platform toe te wijzen.
