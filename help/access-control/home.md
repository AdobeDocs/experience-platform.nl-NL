---
keywords: Experience Platform;thuis;populaire onderwerpen;toegangsbeheer;adobe admin console
solution: Experience Platform
title: Overzicht van toegangsbeheer
description: Via de Adobe Admin Console wordt het toegangsbeheer voor Adobe Experience Platform verzorgd. Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: df24799e4644a98941b707bb216a4ad434f5ebf9
workflow-type: tm+mt
source-wordcount: '1537'
ht-degree: 1%

---

# Overzicht van toegangsbeheer

Toegangscontrole voor Adobe Experience Platform wordt verleend via de **[!UICONTROL Permissions]** in [Adobe Experience Cloud](https://experience.adobe.com/). Deze functionaliteit gebruikt rollen en beleid, die gebruikers met toestemmingen en zandbakken verbinden.

## Toegangsbeheerhiërarchie en -workflow

Om toegangsbeheer voor Experience Platform te vormen, moet u systeem of productbeheerdervoorrechten voor een organisatie hebben die een product van de Experience Platform heeft. De minimumrol die toestemmingen kan verlenen of intrekken is een productbeheerder. Andere beheerderrollen die toestemmingen kunnen beheren zijn systeembeheerders (geen beperkingen). Zie het Adobe Help Center-artikel op [administratieve taken](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie .

>[!NOTE]
>
>Vanaf dit punt verwijzen vermeldingen van &quot;beheerder&quot; in dit document naar een productbeheerder of hoger (zoals hierboven beschreven).

Een werkschema op hoog niveau voor het verkrijgen en toewijzen van toegangsmachtigingen kan als volgt worden samengevat:

- Nadat u een licentie hebt verleend aan Adobe Experience Platform of een toepassings-/toepassingsservice die Experience Platform gebruikt, wordt een e-mail verzonden naar de beheerder die tijdens de licentie is opgegeven.
- De beheerder meldt zich aan aan [Adobe Admin Console](#adobe-admin-console) en selecteert **Adobe Experience Platform** in de lijst met producten op de overzichtspagina.
- Om toegang tot Experience Platform te verlenen, adviseert men dat de beheerder gebruikers aan het standaardproductprofiel toevoegt: `AEP-Default-All-Users`.
- In de Toestemmingen van het Experience Platform, kan de beheerder nieuwe rollen tot stand brengen of de toestemmingen en de gebruikers voor om het even welke bestaande rollen uitgeven.
- Bij het maken of bewerken van een rol voegt de beheerder gebruikers aan de rol toe met behulp van de **[!UICONTROL users]** en verleent machtigingen aan deze gebruikers (zoals &quot;[!UICONTROL Read Datasets]&quot; of &quot;[!UICONTROL Manage Schemas]&quot;) door de machtigingen voor de rol te bewerken. Op dezelfde manier kan de beheerder toegang tot sandboxen toewijzen met dezelfde bewerkingsoptie.
- Wanneer de gebruikers login aan het gebruikersinterface van het Experience Platform, hun toegang tot de mogelijkheden van het Experience Platform door de toestemmingen worden gedreven die aan hen van de vorige stap zijn verleend. Als een gebruiker bijvoorbeeld niet beschikt over de [!UICONTROL View Datasets] toestemming, de **[!UICONTROL Datasets]** in het zijmenu is niet zichtbaar voor die gebruiker.

Voor meer gedetailleerde stappen op hoe te om toegangsbeheer in Experience Platform te beheren, zie [gebruikershandleiding voor toegangsbeheer](./ui/overview.md).

Alle aanroepen naar Experience Platform-API&#39;s worden gevalideerd voor machtigingen en retourneren fouten als de juiste machtigingen niet worden gevonden in de huidige gebruikerscontext. Binnen UI, zullen de elementen worden verborgen of worden veranderd afhankelijk van toestemmingen die aan de huidige gebruiker worden verleend.

## Machtigingen {#platform-permissions}

[!UICONTROL Permissions] verstrekt een centrale plaats voor het beheren van de toegang van het Experience Platform voor uw organisatie. Doorheen [!UICONTROL Permissions]kunt u groepen gebruikers toegangsmachtigingen verlenen voor verschillende mogelijkheden van het Experience Platform, zoals [!UICONTROL Manage Datasets], [!UICONTROL View Datasets], of [!UICONTROL Manage Profiles].

### Rollen

In de [!UICONTROL Roles] sectie, worden de toestemmingen toegewezen aan gebruikers door het gebruik van rollen. Rollen staan u toe om toestemmingen aan één of veelvoudige gebruikers te verlenen, en ook hun toegang tot het werkingsgebied van de zandbakken te bevatten die aan hen door rollen worden toegewezen. De gebruikers kunnen aan één of veelvoudige rollen worden toegewezen die tot uw organisatie behoren.

### Standaardrollen

Experience Platform komt met twee pre-gevormde standaardrollen. De volgende tabel geeft een overzicht van de inhoud van elk standaardprofiel, inclusief de sandbox waartoe ze toegang verlenen en de machtigingen die ze binnen het bereik van die sandbox verlenen.

| Rol | Toegang tot sandbox | Machtigingen |
| --- | --- | --- |
| Standaardproductie, alle toegang | Productie | Alle toestemmingen van toepassing op Experience Platform, behalve de toestemmingen van het Beleid Sandbox. |
| Sandbox-beheerders | N.v.t. | Verleent toegang slechts tot de toestemmingen van het Beleid Sandbox. |

## Sandboxen en machtigingen

Niet-productiesandboxen zijn een vorm van gegevensvirtualisatie waarmee u gegevens kunt isoleren van andere sandboxen. Deze sandboxen worden doorgaans gebruikt voor ontwikkelingsexperimenten, -tests of -tests. De toestemmingen van een rol geven de gebruikers van de rol toegang tot de eigenschappen van het Experience Platform binnen de zandbakmilieu&#39;s waartot zij toegang hebben gekregen tot. Een standaardlicentie voor Experience Platforms geeft u vijf sandboxen (één productie en vier niet-productie). U kunt in totaal maximaal 75 sandboxen toevoegen aan pakketten van tien niet-productiesandboxen. Neem voor meer informatie contact op met de beheerder van uw organisatie of uw Adobe-vertegenwoordiger.

Voor meer informatie over sandboxen in Experience Platform raadpleegt u de [sandboxen, overzicht](../sandboxes/home.md).

### Toegang tot sandboxen

De toegang tot sandboxen wordt beheerd via rollen. Zie voor gedetailleerde stappen over het inschakelen van toegang tot een sandbox voor een rol de optie [kenmerkgebaseerde handleiding voor toegangsbeheerrollen](./abac/ui/roles.md).

Gebruikers kunnen toegang krijgen tot een of meer sandboxen binnen een rol. Als één gebruiker in twee of meer rollen inbegrepen is, zal die gebruiker toegang tot alle zandbakken hebben inbegrepen in die rollen.

Met de machtiging Sandboxbeheer kunnen gebruikers sandboxen beheren, weergeven of opnieuw instellen.

### Bronmachtigingen {#permissions}

De bron [!UICONTROL Permissions] tabblad in een rol geeft de sandboxen en machtigingen weer die actief zijn voor die rol:

![permissie-overzicht](./images/permissions.png)

Machtigingen die worden verleend via de bronmachtigingen worden gesorteerd op categorie, waarbij sommige machtigingen toegang verlenen tot verschillende functies op laag niveau.

De volgende lijst schetst de beschikbare toestemmingen voor Experience Platform in de rol, met beschrijvingen van de specifieke mogelijkheden van het Experience Platform zij toegang tot verlenen. Zie voor gedetailleerde stappen over het toevoegen van machtigingen aan een rol de [kenmerkgebaseerde handleiding voor toegangsbeheerrollen](./abac/ui/roles.md).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| [!DNL Alerts] | [!UICONTROL View Alerts History] | Alleen-lezen toegang voor waarschuwingsgeschiedenis. |
| [!DNL Alerts] | [!UICONTROL Resolve Alerts] | Toegang tot waarschuwingen lezen, bewerken en verwijderen. |
| [!DNL Alerts] | [!UICONTROL View Alerts] | Alleen-lezen toegang voor waarschuwingen. |
| [!DNL Alerts] | [!UICONTROL Manage Alerts] | Toegang tot het lezen, maken, bewerken en verwijderen van waarschuwingsgeschiedenis. |
| [!DNL Computed Attributes] | [!UICONTROL View Computed attributes] | Alleen-lezen toegang voor het tabblad, overzicht en details van berekende kenmerken. |
| [!DNL Computed Attributes] | [!UICONTROL Manage Computed attributes] | Toegang tot het lezen, maken, verwijderen van concepten en het deactiveren van berekende kenmerken. |
| [!DNL Data Lifecycle] | [!UICONTROL View Data Lifecycle] | Alleen-lezen toegang voor de levenscyclus van gegevens. |
| [!DNL Data Lifecycle] | [!UICONTROL Manage Data Lifecycle] | Toegang tot de levenscyclus van gegevens lezen, maken, bewerken en verwijderen. |
| [!DNL Data Modeling] | [!UICONTROL Manage Schemas] | Toegang tot het lezen, maken, bewerken en verwijderen van schema&#39;s en gerelateerde bronnen. |
| [!DNL Data Modeling] | [!UICONTROL View Schemas] | Alleen-lezen toegang tot schema&#39;s en gerelateerde bronnen. |
| [!DNL Data Modeling] | [!UICONTROL Manage Relationships] | Toegang tot het lezen, maken, bewerken en verwijderen van schemarelaties. |
| [!DNL Data Modeling] | [!UICONTROL Manage Identity Metadata] | Toegang tot het lezen, maken, bewerken en verwijderen van identiteitsmetagegevens voor schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL Manage Datasets] | Toegang tot het lezen, creëren, uitgeven, en schrappen datasets. Alleen-lezen toegang voor schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL View Datasets] | Alleen-lezen toegang voor gegevenssets en schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL Data Monitoring] | Alleen-lezen toegang tot gegevenssets en streams controleren. |
| [!DNL Profile Management] | [!UICONTROL Manage Profiles] | Toegang tot gelezen, creeer, geef, en schrap datasets uit die voor klantenprofielen worden gebruikt. Alleen-lezen toegang tot beschikbare profielen. |
| [!DNL Profile Management] | [!UICONTROL View Profiles] | Alleen-lezen toegang tot beschikbare profielen. |
| [!DNL Profile Management] | [!UICONTROL Manage Segments] | Toegang tot het lezen, maken, bewerken en verwijderen van segmenten. |
| [!DNL Profile Management] | [!UICONTROL View Segments] | Alleen-lezen toegang tot beschikbare segmenten. |
| [!DNL Profile Management] | [!UICONTROL Manage Merge Policies] | Toegang tot het lezen, maken, bewerken en verwijderen van samenvoegbeleidsregels. |
| [!DNL Profile Management] | [!UICONTROL View Merge Policies] | Alleen-lezen toegang tot beschikbaar samenvoegbeleid. |
| [!DNL Profile Management] | [!UICONTROL Export Audience for Segment] | Capaciteit om een geëvalueerd publiekssegment naar een dataset uit te voeren. |
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | De capaciteit om profielen voor een publiek te produceren door een segmentdefinitie te evalueren. |
| [!DNL Profile Management] | [!UICONTROL View B2B AI] | Alleen-lezen toegang tot instellingen en configuraties voor alle B2B AI/ML-services. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B AI] | Toegang tot het lezen, creëren, uitgeven, en schrappen montages en configuraties voor alle diensten B2B AI/ML. |
| [!DNL Profile Management] | [!UICONTROL View B2B Profile] | Alleen-lezen toegang tot B2B-entiteitsprofielen (zoals Account, Opportunity, enzovoort), instellingen en configuraties voor alle B2B AI/ML-services en B2B-dashboardwidgets. |
| [!DNL Profile Management] | [!UICONTROL Manage B2B Profile] | Toegang tot het lezen, maken, bewerken en verwijderen van B2B-entiteitsprofielen (zoals Account, Opportunity, enzovoort). Alleen-lezen toegang voor instellingen en configuraties voor alle B2B AI/ML-services en B2B-dashboardwidgets. |
| [!DNL Identity Management] | [!UICONTROL Manage Identity Namespaces] | Toegang tot het lezen, maken, bewerken en verwijderen van naamruimten. |
| [!DNL Identity Management] | [!UICONTROL View Identity Namespaces] | Alleen-lezen toegang voor naamruimten. |
| [!DNL Identity Management] | [!UICONTROL View Identity Graph] | Alleen-lezen toegang voor identiteitsgrafieken. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Toegang tot het lezen, maken, bewerken en verwijderen van sandboxen. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Alleen-lezen toegang voor sandboxen die tot uw organisatie behoren. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Mogelijkheid om een sandbox opnieuw in te stellen. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Alleen-lezen toegang tot beschikbare weergavedoelen in de **[!UICONTROL Catalog]** tab en geverifieerde doelen in het dialoogvenster **[!UICONTROL Browse]** tab. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Toegang tot het lezen, creëren, en schrappen van bestemmingsverbindingen en bestemmingsrekeningen. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Biedt gebruikers de capaciteit om segmenten aan bestaande bestemmingen te activeren. Hiermee schakelt u de toewijzingsstap in de activeringsworkflow in. Deze toestemming vereist ook [!UICONTROL View Destinations] Toestemming om aan de gebruiker te worden verleend die gegevens aan bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Activate Segment without Mapping] | Biedt gebruikers de capaciteit om segmenten aan bestaande bestemmingen te activeren, zonder het tonen van [toewijzingsstap](../destinations/ui/activate-batch-profile-destinations.md#mapping). Gebruikers kunnen segmenten toevoegen en verwijderen in activeringsworkflows, maar kunnen toegewezen kenmerken of identiteiten niet toevoegen of verwijderen. Deze toestemming vereist ook [!UICONTROL View Destinations] Toestemming om aan de gebruiker te worden verleend die gegevens aan bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Manage and Activate Dataset Destinations] | Mogelijkheid om gegevenssets te lezen, te maken, te bewerken en uit te schakelen. Mogelijkheid om gegevens ook te activeren naar actieve datasets die zijn gemaakt. Deze toestemming vereist ook [!UICONTROL View Destinations] Toestemming om aan de gebruiker te worden verleend die gegevens aan bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Mogelijkheid om doelen te ontwerpen met [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Toegang tot bronnen lezen, maken, bewerken en uitschakelen. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Alleen-lezen toegang tot beschikbare bronnen in het dialoogvenster **[!UICONTROL Catalog]** tabblad en geverifieerde bronnen in het dialoogvenster **[!UICONTROL Browse]** tab. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Toegang tot creëren, goedkeuren, en de handvatten van de partner verwerpen om twee organisaties te verbinden en toe te laten [!DNL Segment Match] stromen. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Toegang tot lezen, maken, bewerken en publiceren [!DNL Segment Match] voert met actieve partners uit. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Toegang tot lezen, maken, bewerken en verwijderen in [!DNL Data Science Workspace]. |
| Gegevensbeheer | [!UICONTROL Manage Usage Labels] | Toegang tot het lezen, maken en verwijderen van gebruikslabels. |
| Gegevensbeheer | [!UICONTROL Manage Data Usage Policies] | Toegang tot het lezen, maken, bewerken en verwijderen van beleidsregels voor gegevensgebruik. |
| Gegevensbeheer | [!UICONTROL View Data Usage Policies] | Alleen-lezen toegang voor beleidsregels voor gegevensgebruik die tot uw organisatie behoren. |
| Gegevensbeheer | [!UICONTROL View User Activity Log] | Alleen-lezen toegang tot opgenomen weergave [auditlogboeken](../landing/governance-privacy-security/audit-logs/overview.md) van platformactiviteiten. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Alleen-lezen toegang om het dashboard voor het licentiegebruik weer te geven. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Voeg douanekenmerken toe die nog niet in het gegevenspakhuis zijn. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Toegang tot het lezen, creëren, uitgeven, en schrappen van gestructureerde SQL vragen voor de gegevens van het Platform. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Toegang tot het creëren, bijwerken, en schrappen van niet-vervallende geloofsbrieven voor de toegang van de Dienst van de Vraag. |

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangscontrole in Experience Platform. U kunt nu doorgaan naar het dialoogvenster [gebruikershandleiding voor op kenmerken gebaseerde toegangsbeheer](./abac/overview.md) voor gedetailleerde stappen op hoe gebruik Experience Cloud om rollen tot stand te brengen en toestemmingen voor Experience Platform toe te wijzen.
