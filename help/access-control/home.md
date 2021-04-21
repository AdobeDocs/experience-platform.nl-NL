---
keywords: Experience Platform;thuis;populaire onderwerpen;toegangsbeheer;adobe admin console
solution: Experience Platform
topic-legacy: overview
title: Overzicht van toegangsbeheer
description: Via de Adobe Admin Console wordt het toegangsbeheer voor Adobe Experience Platform verzorgd. Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden.
exl-id: 591d59ad-2784-4ae4-a509-23649ce712c9
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1181'
ht-degree: 1%

---

# Overzicht van toegangsbeheer

Toegangsbeheer voor [!DNL Experience Platform] wordt verstrekt door [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in [!DNL Admin Console], die gebruikers met toestemmingen en zandbakken verbinden.

## Toegangsbeheerhiërarchie en -workflow

Om toegangsbeheer voor [!DNL Experience Platform] te vormen, moet u beheerdervoorrechten voor een organisatie hebben die [!DNL Experience Platform] productintegratie heeft. De minimale rol die machtigingen verleent of intrekt, is een beheerder van het productprofiel. Andere beheerdersrollen die machtigingen kunnen beheren, zijn productbeheerders (die alle profielen binnen een product kunnen beheren) en systeembeheerders (geen beperkingen). Zie het Adobe Help Center-artikel over [beheerrollen](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie.

>[!NOTE]
>
>Vanaf dit punt verwijzen vermeldingen van &quot;beheerder&quot; in dit document naar een beheerder van het productprofiel of hoger (zoals hierboven beschreven).

Een werkschema op hoog niveau voor het verkrijgen en toewijzen van toegangsmachtigingen kan als volgt worden samengevat:

- Nadat u een licentie hebt verleend aan Adobe Experience Platform of een toepassings-/toepassingsservice die Experience Platform gebruikt, wordt een e-mail verzonden naar de beheerder die tijdens de licentie is opgegeven.
- De beheerder logt binnen aan [Adobe Admin Console](#adobe-admin-console) en selecteert **Adobe Experience Platform** van de lijst van producten op de overzichtspagina.
- De beheerder kan de standaard [productprofielen](#product-profiles) bekijken of nieuwe profielen van het klantenproduct tot stand brengen zoals nodig.
- De beheerder kan de machtigingen en gebruikers voor bestaande productprofielen bewerken.
- Wanneer de beheerder een productprofiel maakt of bewerkt, voegt hij gebruikers aan het profiel toe via het tabblad **[!UICONTROL users]** en verleent hij deze gebruikers machtigingen (zoals &quot;[!UICONTROL Read Datasets]&quot; of &quot;[!UICONTROL Manage Schemas]&quot;) door toegang te krijgen tot het tabblad **[!UICONTROL permissions]**. Op dezelfde manier kan de beheerder toegang tot sandboxen toewijzen via hetzelfde machtigingentabblad.
- Wanneer gebruikers zich bij het [!DNL Experience Platform] gebruikersinterface aanmelden, wordt hun toegang tot [!DNL Platform] mogelijkheden gedreven door de toestemmingen die aan hen van Stap 2 zijn verleend. Als een gebruiker bijvoorbeeld niet beschikt over de machtiging &quot;[!UICONTROL View Datasets]&quot;, is het tabblad **[!UICONTROL Datasets]** in het zijmenu niet zichtbaar voor die gebruiker.

Voor meer gedetailleerde stappen op hoe te om toegangsbeheer in [!DNL Experience Platform] te beheren, zie [toegangsbeheer gebruikershandleiding](./ui/overview.md).

Alle aanroepen naar [!DNL Experience Platform] API&#39;s worden gevalideerd voor machtigingen en retourneren fouten als de juiste machtigingen niet worden gevonden in de huidige gebruikerscontext. Binnen UI, zullen de elementen worden verborgen of worden veranderd afhankelijk van toestemmingen die aan de huidige gebruiker worden verleend.

## Adobe Admin Console

Adobe Admin Console biedt een centrale locatie voor het beheer van Adobe-productrechten en toegang voor uw organisatie. Via de console, kunt u groepen gebruikers toegangstoestemmingen voor diverse [!DNL Platform] mogelijkheden, zoals &quot;[!UICONTROL Manage Datasets]&quot;, &quot;[!UICONTROL View Datasets]&quot;, of &quot;[!UICONTROL Manage Profiles]&quot; verlenen.

### Productprofielen

In [!DNL Admin Console], worden de toestemmingen toegewezen aan gebruikers door het gebruik van productprofielen. Met productprofielen kunt u machtigingen verlenen aan een of meerdere gebruikers en ook toegang tot het bereik van de sandboxen bevatten die via productprofielen aan hen zijn toegewezen. Gebruikers kunnen worden toegewezen aan een of meerdere productprofielen die bij uw organisatie horen.

### Standaardproductprofielen

[!DNL Experience Platform] wordt geleverd met twee vooraf geconfigureerde standaardproductprofielen. De volgende tabel geeft een overzicht van de inhoud van elk standaardprofiel, inclusief de sandbox waartoe ze toegang verlenen en de machtigingen die ze binnen het bereik van die sandbox verlenen.

| Productprofiel | Toegang tot sandbox | Toestemmingen |
| --- | --- | --- |
| Standaardproductie, alle toegang | Productie | Alle toestemmingen van toepassing op [!DNL Experience Platform], behalve de toestemmingen van het Beleid Sandbox. |
| Sandbox-beheerders | N.v.t. | Verleent toegang slechts tot de toestemmingen van het Beleid Sandbox. |

## Sandboxen en machtigingen

Niet-productiesandboxen zijn een vorm van gegevensvirtualisatie waarmee u gegevens kunt isoleren van andere sandboxen. Deze sandboxen worden doorgaans gebruikt voor ontwikkelingsexperimenten, -tests of -tests. De machtigingen van een productprofiel geven de gebruikers van het profiel toegang tot [!DNL Platform]-functies binnen de sandboxomgevingen waartoe zij toegang hebben. Een standaardlicentie voor Experience Platforms geeft u vijf sandboxen (één productie en vier niet-productie). U kunt in totaal maximaal 75 sandboxen toevoegen aan pakketten van tien niet-productiesandboxen. Neem voor meer informatie contact op met uw IMS Org Administrator of uw Adobe-vertegenwoordiger.

Voor meer informatie over sandboxen in [!DNL Experience Platform] raadpleegt u het [overzicht van sandboxen](../sandboxes/home.md).

### Toegang tot sandboxen

Toegang tot sandboxen wordt beheerd via productprofielen. Voor gedetailleerde stappen op hoe te om toegang tot een zandbak voor een productprofiel toe te laten, zie [de gebruikershandleiding van de toegangscontrole](./ui/overview.md).

Gebruikers kunnen toegang krijgen tot een of meer sandboxen in een productprofiel. Als één gebruiker in twee of meer productprofielen is opgenomen, heeft die gebruiker toegang tot alle sandboxen die in die profielen zijn opgenomen.

Met de machtiging Sandboxbeheer kunnen gebruikers sandboxen beheren, weergeven of opnieuw instellen.

### Toestemmingen

Op het tabblad Machtigingen in een productprofiel worden de sandboxen en machtigingen weergegeven die actief zijn voor dat profiel:

![permissie-overzicht](./images/permissions-overview.png)

Machtigingen die via de [!DNL Admin Console] worden verleend, worden gesorteerd op categorie, met machtigingen die toegang verlenen tot verschillende functies op laag niveau.

In de volgende tabel worden de beschikbare machtigingen voor [!DNL Experience Platform] in de [!DNL Admin Console] beschreven, met beschrijvingen van de specifieke [!DNL Platform]-mogelijkheden waartoe deze toegang verlenen. Voor gedetailleerde stappen op hoe te om toestemmingen aan een productprofiel toe te voegen, zie [de gebruikershandleiding van de toegangscontrole](./ui/overview.md).

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
| [!DNL Destinations] | [!UICONTROL View Destinations] | Alleen-lezen toegang tot beschikbare doelen op het tabblad **[!UICONTROL Catalog]** en geverifieerde doelen op het tabblad **[!UICONTROL Browse]**. |
| [!DNL Destinations] | [!UICONTROL Activate Destinations] | Mogelijkheid om gegevens te activeren naar actieve doelen die zijn gemaakt. Deze toestemming vereist of &quot;de Doelen van de Mening&quot;of &quot;leidt [!UICONTROL Destinations”] om aan de gebruiker worden verleend die bestemmingen zal activeren. |
| [!DNL Data Ingestion] | [!UICONTROL Manage Sources] | Toegang tot het lezen, maken, bewerken en uitschakelen van bronnen. |
| [!DNL Data Ingestion] | [!UICONTROL View Sources] | Alleen-lezen toegang tot beschikbare bronnen op het tabblad **[!UICONTROL Catalog]** en geverifieerde bronnen op het tabblad **[!UICONTROL Browse]**. |
| [!DNL Data Science Workspace] | [!UICONTROL Manage Data Science Workspace] | Toegang tot lezen, maken, bewerken en verwijderen in [!DNL Data Science Workspace]. |
| [!DNL Data Governance] | [!UICONTROL Apply Data Usage Labels] | Toegang tot het lezen, maken en verwijderen van gebruikslabels. |
| [!DNL Data Governance] | [!UICONTROL Manage Data Usage Policies] | Toegang tot het lezen, maken, bewerken en verwijderen van beleidsregels voor gegevensgebruik. |
| [!DNL Data Governance] | [!UICONTROL View Data Usage Policies] | Alleen-lezen toegang voor beleidsregels voor gegevensgebruik die tot uw organisatie behoren. |
| [!DNL Query Service] | [!UICONTROL Manage Queries] | Toegang tot het lezen, maken, bewerken en verwijderen van gestructureerde SQL-query&#39;s voor Platform-gegevens. |

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangsbeheer in [!DNL Experience Platform]. U kunt nu doorgaan naar de [gebruikershandleiding voor toegangsbeheer](./ui/overview.md) voor gedetailleerde stappen over het gebruik van [!DNL Admin Console] om productprofielen te maken en machtigingen toe te wijzen voor [!DNL Platform].
