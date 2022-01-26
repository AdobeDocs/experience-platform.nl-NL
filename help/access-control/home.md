---
keywords: Experience Platform;thuis;populaire onderwerpen;toegangsbeheer;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: Overzicht van toegangsbeheer
description: Via de Adobe Admin Console wordt het toegangsbeheer voor Adobe Experience Platform verzorgd. Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
source-git-commit: 2677d5f0c4369ab692f9e4b16710098a359402d7
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 1%

---

# Overzicht van toegangsbeheer

Toegangsbeheer voor [!DNL Experience Platform] wordt verstrekt via [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in [!DNL Admin Console], waarmee gebruikers worden gekoppeld aan machtigingen en sandboxen.

## Toegangsbeheerhiërarchie en -workflow

Om toegangsbeheer voor te vormen [!DNL Experience Platform], moet u beheerdersrechten hebben voor een organisatie die een [!DNL Experience Platform] productintegratie. De minimale rol die machtigingen verleent of intrekt, is een beheerder van het productprofiel. Andere beheerdersrollen die machtigingen kunnen beheren, zijn productbeheerders (die alle profielen binnen een product kunnen beheren) en systeembeheerders (geen beperkingen). Zie het Adobe Help Center-artikel op [administratieve taken](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie .

>[!NOTE]
>
>Vanaf dit punt verwijzen vermeldingen van &quot;beheerder&quot; in dit document naar een beheerder van het productprofiel of hoger (zoals hierboven beschreven).

Een werkschema op hoog niveau voor het verkrijgen en toewijzen van toegangsmachtigingen kan als volgt worden samengevat:

- Nadat u een licentie hebt verleend aan Adobe Experience Platform of een toepassings-/toepassingsservice die Experience Platform gebruikt, wordt een e-mail verzonden naar de beheerder die tijdens de licentie is opgegeven.
- De beheerder meldt zich aan aan [Adobe Admin Console](#adobe-admin-console) en selecteert **Adobe Experience Platform** in de lijst met producten op de overzichtspagina.
- De beheerder kan het gebrek bekijken [productprofielen](#product-profiles) of maak zo nodig nieuwe profielen voor klantproducten.
- De beheerder kan de machtigingen en gebruikers voor bestaande productprofielen bewerken.
- Bij het maken of bewerken van een productprofiel voegt de beheerder gebruikers aan het profiel toe met de opdracht **[!UICONTROL users]** en verleent machtigingen aan deze gebruikers (zoals &quot;[!UICONTROL Read Datasets]&quot; of &quot;[!UICONTROL Manage Schemas]&quot;) door de **[!UICONTROL permissions]** tab. Op dezelfde manier kan de beheerder toegang tot sandboxen toewijzen via hetzelfde machtigingentabblad.
- Wanneer gebruikers zich aanmelden bij de [!DNL Experience Platform] gebruikersinterface, hun toegang tot [!DNL Platform] De mogelijkheden worden gedreven door de toestemmingen die aan hen van Stap 2 zijn verleend. Als een gebruiker bijvoorbeeld niet beschikt over &quot;[!UICONTROL View Datasets]&quot; toestemming, de **[!UICONTROL Datasets]** in het zijmenu is niet zichtbaar voor die gebruiker.

Voor meer gedetailleerde stappen op hoe te om toegangsbeheer binnen te beheren [!DNL Experience Platform], zie de [gebruikershandleiding voor toegangsbeheer](./ui/overview.md).

Alle vraag aan [!DNL Experience Platform] API&#39;s worden gevalideerd voor machtigingen en retourneren fouten als de juiste machtigingen niet worden gevonden in de huidige gebruikerscontext. Binnen UI, zullen de elementen worden verborgen of worden veranderd afhankelijk van toestemmingen die aan de huidige gebruiker worden verleend.

## Adobe Admin Console

Adobe Admin Console biedt een centrale locatie voor het beheer van Adobe-productrechten en toegang voor uw organisatie. Via de console, kunt u groepen gebruikers toegangstoestemmingen voor diverse verlenen [!DNL Platform] mogelijkheden, zoals &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot;, of &quot;[!UICONTROL Manage Profiles]&quot;.

### Productprofielen

In de [!DNL Admin Console], worden machtigingen aan gebruikers toegewezen via het gebruik van productprofielen. Met productprofielen kunt u machtigingen verlenen aan een of meerdere gebruikers en ook toegang tot het bereik van de sandboxen bevatten die via productprofielen aan hen zijn toegewezen. Gebruikers kunnen worden toegewezen aan een of meerdere productprofielen die bij uw organisatie horen.

### Standaardproductprofielen

[!DNL Experience Platform] wordt geleverd met twee vooraf geconfigureerde standaardproductprofielen. De volgende tabel geeft een overzicht van de inhoud van elk standaardprofiel, inclusief de sandbox waartoe ze toegang verlenen en de machtigingen die ze binnen het bereik van die sandbox verlenen.

| Productprofiel | Toegang tot sandbox | Toestemmingen |
| --- | --- | --- |
| Standaardproductie, alle toegang | Productie | Alle machtigingen die van toepassing zijn op [!DNL Experience Platform], behalve de bevoegdheden van Sandbox Administration. |
| Sandbox-beheerders | N.v.t. | Verleent toegang slechts tot de toestemmingen van het Beleid Sandbox. |

## Sandboxen en machtigingen

Niet-productiesandboxen zijn een vorm van gegevensvirtualisatie waarmee u gegevens kunt isoleren van andere sandboxen. Deze sandboxen worden doorgaans gebruikt voor ontwikkelingsexperimenten, -tests of -tests. De machtigingen van een productprofiel geven de gebruikers van het profiel toegang tot [!DNL Platform] functies binnen de sandboxomgevingen waartoe ze toegang hebben. Een standaardlicentie voor Experience Platforms geeft u vijf sandboxen (één productie en vier niet-productie). U kunt in totaal maximaal 75 sandboxen toevoegen aan pakketten van tien niet-productiesandboxen. Neem voor meer informatie contact op met uw IMS Org Administrator of uw Adobe-vertegenwoordiger.

Voor meer informatie over sandboxen in [!DNL Experience Platform], gelieve de [sandboxen, overzicht](../sandboxes/home.md).

### Toegang tot sandboxen

Toegang tot sandboxen wordt beheerd via productprofielen. Voor gedetailleerde stappen over het inschakelen van toegang tot een sandbox voor een productprofiel raadpleegt u de [gebruikershandleiding voor toegangsbeheer](./ui/overview.md).

Gebruikers kunnen toegang krijgen tot een of meer sandboxen in een productprofiel. Als één gebruiker in twee of meer productprofielen is opgenomen, heeft die gebruiker toegang tot alle sandboxen die in die profielen zijn opgenomen.

Met de machtiging Sandboxbeheer kunnen gebruikers sandboxen beheren, weergeven of opnieuw instellen.

### Toestemmingen {#permissions}

Op het tabblad Machtigingen in een productprofiel worden de sandboxen en machtigingen weergegeven die actief zijn voor dat profiel:

![permissie-overzicht](./images/permissions.png)

Machtigingen die worden verleend via de [!DNL Admin Console] worden gesorteerd op categorie, met sommige machtigingen die toegang verlenen tot verschillende functies op laag niveau.

In de volgende tabel worden de beschikbare machtigingen voor [!DNL Experience Platform] in de [!DNL Admin Console], met een beschrijving van de specifieke [!DNL Platform] capaciteiten die zij toegang verlenen tot. Zie voor gedetailleerde stappen over het toevoegen van machtigingen aan een productprofiel de [gebruikershandleiding voor toegangsbeheer](./ui/overview.md).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
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
| [!DNL Profile Management] | [!UICONTROL Evaluate a Segment to an Audience] | Mogelijkheid om profielen te genereren voor een publiek door een segmentdefinitie te evalueren. |
| [!DNL Identities] | [!UICONTROL Manage Identity Namespaces] | Toegang tot het lezen, maken, bewerken en verwijderen van naamruimten. |
| [!DNL Identities] | [!UICONTROL View Identity Namespaces] | Alleen-lezen toegang voor naamruimten. |
| [!DNL Sandbox Administration] | [!UICONTROL Manage Sandboxes] | Toegang tot het lezen, maken, bewerken en verwijderen van sandboxen. |
| [!DNL Sandbox Administration] | [!UICONTROL View Sandboxes] | Alleen-lezen toegang voor sandboxen die tot uw organisatie behoren. |
| [!DNL Sandbox Administration] | [!UICONTROL Reset a Sandbox] | Mogelijkheid om een sandbox opnieuw in te stellen. |
| [!DNL Destinations] | [!UICONTROL Manage Destinations] | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen. |
| [!DNL Destinations] | [!UICONTROL View Destinations] | Alleen-lezen toegang tot beschikbare doelen in de **[!UICONTROL Catalog]** tab en geverifieerde doelen in het dialoogvenster **[!UICONTROL Browse]** tab. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Mogelijkheid om gegevens te activeren naar actieve doelen die zijn gemaakt. Voor deze machtiging is &quot;Doelen weergeven&quot; of &quot;Beheren&quot; vereist [!UICONTROL Destinations”] toe te kennen aan de gebruiker die bestemmingen zal activeren. |
| [!DNL Destinations] | [!UICONTROL Destination Authoring] | Mogelijkheid om doelen te ontwerpen met [Adobe Experience Platform Destination SDK](../destinations/destination-sdk/overview.md). |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Toegang tot het lezen, maken, bewerken en uitschakelen van bronnen. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Alleen-lezen toegang tot beschikbare bronnen in het dialoogvenster **[!UICONTROL Catalog]** tabblad en geverifieerde bronnen in het dialoogvenster **[!UICONTROL Browse]** tab. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share Connections] | Toegang om partnerhandvatten te creëren, goed te keuren en te verwerpen om twee organisaties te verbinden IMS en toe te laten [!DNL Segment Match] stromen. |
| [!DNL Data Ingestion] | [!DNL Manage Audience Share] | Toegang tot lezen, maken, bewerken en publiceren [!DNL Segment Match] voert met actieve partners uit. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Toegang tot lezen, maken, bewerken en verwijderen in [!DNL Data Science Workspace]. |
| Data Governance | [!UICONTROL Apply Data Usage Labels] | Toegang tot het lezen, maken en verwijderen van gebruikslabels. |
| Gegevensbeheer | [!UICONTROL Manage Data Usage Policies] | Toegang tot het lezen, maken, bewerken en verwijderen van beleidsregels voor gegevensgebruik. |
| Gegevensbeheer | [!UICONTROL View Data Usage Policies] | Alleen-lezen toegang voor beleidsregels voor gegevensgebruik die tot uw organisatie behoren. |
| Gegevensbeheer | [!UICONTROL View User Activity Log] | Alleen-lezen toegang tot opgenomen weergave [auditlogboeken](../landing/governance-privacy-security/audit-logs/overview.md) van de activiteiten van de Platform. |
| [!DNL Dashboards] | [!UICONTROL View License Usage Dashboard] | Alleen-lezen toegang om het dashboard voor het licentiegebruik weer te geven. |
| [!DNL Dashboards] | [!UICONTROL Manage Standard Dashboards] | Voeg douanekenmerken toe die nog niet in het gegevenspakhuis zijn. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Toegang tot het lezen, maken, bewerken en verwijderen van gestructureerde SQL-query&#39;s voor Platform-gegevens. |
| [!DNL Query Service] | [!UICONTROL Manage Query Service Integration] | Toegang tot het creëren, bijwerken, en schrappen van niet-vervallende geloofsbrieven voor de toegang van de Dienst van de Vraag. |

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangscontrole in [!DNL Experience Platform]. U kunt nu doorgaan naar het dialoogvenster [gebruikershandleiding voor toegangsbeheer](./ui/overview.md) voor gedetailleerde stappen over het gebruik van de [!DNL Admin Console] om productprofielen te maken en machtigingen toe te wijzen voor [!DNL Platform].
