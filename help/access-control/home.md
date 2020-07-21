---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van toegangsbeheer
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '1097'
ht-degree: 1%

---


# Overzicht van toegangsbeheer

Toegangsbeheer voor [!DNL Experience Platform] is beschikbaar via de [Adobe Admin Console](https://adminconsole.adobe.com). Deze functionaliteit gebruikt productprofielen in [!DNL Admin Console], die gebruikers met toestemmingen en zandbakken verbinden.

## Toegangsbeheerhiërarchie en -workflow

Om toegangsbeheer voor te vormen, moet u beheerdervoorrechten voor een organisatie hebben die een [!DNL Experience Platform][!DNL Experience Platform] productintegratie heeft. De minimale rol die machtigingen verleent of intrekt, is een beheerder **[!UICONTROL van het]** productprofiel. Andere beheerdersrollen die machtigingen kunnen beheren, zijn **[!UICONTROL productbeheerders]** (die alle profielen binnen een product kunnen beheren) en **[!UICONTROL systeembeheerders]** (geen beperkingen). Zie het artikel in Adobe Help Center over [beheerrollen](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie.

>[!NOTE]
>
>Vanaf dit punt verwijzen vermeldingen van &quot;beheerder&quot; in dit document naar een beheerder van het productprofiel of hoger (zoals hierboven beschreven).

Een werkschema op hoog niveau voor het verkrijgen en toewijzen van toegangsmachtigingen kan als volgt worden samengevat:

- Nadat u zich hebt geabonneerd op een Adobe Experience Platform, wordt een e-mail verzonden naar de beheerder die is opgegeven in het registratieformulier.
- De beheerder meldt zich aan bij de Admin Console [van](#adobe-admin-console) Adobe en selecteert **Adobe Experience Platform** van de lijst van producten op de overzichtspagina.
- De beheerder kan de standaardprofielen [van het](#product-profiles) product bekijken of nieuwe profielen van het klantenproduct tot stand brengen zoals nodig.
- De beheerder kan de machtigingen en gebruikers voor bestaande productprofielen bewerken.
- Wanneer de beheerder een productprofiel maakt of bewerkt, voegt hij gebruikers aan het profiel toe met behulp van het tabblad **[!UICONTROL Gebruikers]** en verleent hij deze gebruikers machtigingen (zoals &quot;Datasetslezen&quot; of &quot;Schema&#39;sbeheren&quot;) via het tabblad **[!UICONTROL machtigingen]** . Op dezelfde manier kan de beheerder toegang tot sandboxen toewijzen via hetzelfde machtigingentabblad.
- Wanneer de gebruikers login aan het [!DNL Experience Platform] gebruikersinterface, hun toegang tot [!DNL Platform] mogelijkheden wordt gedreven door de toestemmingen die aan hen van Stap 2 zijn verleend. Als een gebruiker bijvoorbeeld niet beschikt over de machtiging &quot;Datasetsweergeven&quot;, is het tabblad *[!UICONTROL Datasets]* in het zijmenu niet zichtbaar voor die gebruiker.

Voor meer gedetailleerde stappen op hoe te om toegangsbeheer binnen te beheren, zie de [!DNL Experience Platform]gebruikershandleiding [](./ui/overview.md)van de toegangscontrole.

Alle aanroepen van [!DNL Experience Platform] API&#39;s worden gevalideerd voor machtigingen en retourneren fouten als de juiste machtigingen niet worden gevonden in de huidige gebruikerscontext. Binnen UI, zullen de elementen worden verborgen of worden veranderd afhankelijk van toestemmingen die aan de huidige gebruiker worden verleend.

## Adobe Admin Console

Adobe Admin Console biedt een centrale locatie voor het beheer van Adobe-productrechten en -toegang voor uw organisatie. Via de console kunt u groepen gebruikers toegangsmachtigingen verlenen voor verschillende [!DNL Platform] mogelijkheden, zoals &quot;[!UICONTROL Datasets]beheren&quot;, &quot;Datasetsweergeven&quot; of &quot;Profielenbeheren&quot;.

### Productprofielen

In de [!DNL Admin Console]sectie worden machtigingen aan gebruikers toegewezen via het gebruik van **[!UICONTROL productprofielen]**. Met productprofielen kunt u machtigingen verlenen aan een of meerdere gebruikers en ook toegang tot het bereik van de sandboxen bevatten die via productprofielen aan hen zijn toegewezen. Gebruikers kunnen worden toegewezen aan een of meerdere productprofielen die bij uw organisatie horen.

### Standaardproductprofielen

[!DNL Experience Platform] wordt geleverd met twee vooraf geconfigureerde standaardproductprofielen. De volgende tabel geeft een overzicht van de inhoud van elk standaardprofiel, inclusief de sandbox waartoe ze toegang verlenen en de machtigingen die ze binnen het bereik van die sandbox verlenen.

| Productprofiel | Toegang tot sandbox | Toestemmingen |
| --- | --- | --- |
| Standaardproductie - Alle toegang | Productie | Alle toestemmingen van toepassing op [!DNL Experience Platform], behalve de toestemmingen van het Beleid Sandbox. |
| Standaardsandboxbeheer | N.v.t. | Verleent toegang slechts tot de toestemmingen van het Beleid Sandbox. |

## Sandboxen en machtigingen

[!DNL Experience Platform] biedt toegang tot één productiesandbox en stelt u in staat niet-productiesandboxen **te maken**. Niet-productiesandboxen zijn een vorm van gegevensvirtualisatie waarmee u gegevens kunt isoleren van andere sandboxen. Deze sandboxen worden doorgaans gebruikt voor ontwikkelingsexperimenten, -tests of -tests. De **[!UICONTROL machtigingen]** van een productprofiel geven de gebruikers van het profiel toegang tot [!DNL Platform] functies in de sandboxomgevingen waartoe zij toegang hebben.

Raadpleeg het overzicht [!DNL Experience Platform]van de [sandboxen voor meer informatie over de sandboxen in](../sandboxes/home.md)de.

### Toegang tot sandboxen

Toegang tot sandboxen wordt beheerd via productprofielen. Voor gedetailleerde stappen op hoe te om toegang tot een zandbak voor een productprofiel toe te laten, zie de [gebruikershandleiding](./ui/overview.md)van de toegangscontrole.

Gebruikers kunnen toegang krijgen tot een of meer sandboxen in een productprofiel. Als één gebruiker in twee of meer productprofielen is opgenomen, heeft die gebruiker toegang tot alle sandboxen die in die profielen zijn opgenomen.

Met de machtiging Sandboxbeheer kunnen gebruikers sandboxen beheren, weergeven of opnieuw instellen.

### Toestemmingen

Op het tabblad **Machtigingen** in een productprofiel worden de sandboxen en machtigingen weergegeven die actief zijn voor dat profiel:

![](./images/permissions-overview.png)

Machtigingen die via de methode worden verleend, [!DNL Admin Console] worden gesorteerd op categorie, waarbij bepaalde machtigingen toegang verlenen tot verschillende functies op laag niveau.

De volgende lijst schetst de beschikbare toestemmingen voor [!DNL Experience Platform] in het [!DNL Admin Console], met beschrijvingen van de specifieke [!DNL Platform] mogelijkheden zij toegang tot verlenen. Voor gedetailleerde stappen op hoe te om toestemmingen aan een productprofiel toe te voegen, zie de gebruikershandleiding van de [toegangscontrole](./ui/overview.md).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| [!DNL Data Modeling] | [!UICONTROL Schema&#39;s beheren] | Toegang tot het lezen, maken, bewerken en verwijderen van schema&#39;s en gerelateerde bronnen. |
| [!DNL Data Modeling] | [!UICONTROL Schema&#39;s weergeven] | Alleen-lezen toegang tot schema&#39;s en gerelateerde bronnen. |
| [!DNL Data Management] | [!UICONTROL Gegevensbestanden beheren] | Toegang tot het lezen, creëren, uitgeven, en schrappen datasets. Alleen-lezen toegang voor schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL Gegevensbestanden weergeven] | Alleen-lezen toegang voor gegevenssets en schema&#39;s. |
| [!DNL Data Management] | [!UICONTROL Gegevenscontrole] | Alleen-lezen toegang tot gegevenssets en streams controleren. |
| [!DNL Profile Management] | [!UICONTROL Profielen beheren] | Toegang tot gelezen, creeer, geef, en schrap datasets uit die voor klantenprofielen worden gebruikt. Alleen-lezen toegang tot beschikbare profielen. |
| [!DNL Profile Management] | [!UICONTROL Profielen weergeven] | Alleen-lezen toegang tot beschikbare profielen. |
| [!DNL Profile Management] | [!UICONTROL Publiek exporteren voor segment] | Capaciteit om een geëvalueerd publiekssegment naar een dataset uit te voeren. |
| [!DNL Identities] | [!UICONTROL Identiteitsnaamruimten beheren] | Toegang tot het lezen, maken, bewerken en verwijderen van naamruimten. |
| [!DNL Identities] | [!UICONTROL Identiteitsnaamruimten weergeven] | Alleen-lezen toegang voor naamruimten. |
| [!DNL Sandbox Administration] | [!UICONTROL Sandboxen beheren] | Toegang tot het lezen, maken, bewerken en verwijderen van sandboxen. |
| [!DNL Sandbox Administration] | [!UICONTROL Sandboxen weergeven] | Alleen-lezen toegang voor sandboxen die tot uw organisatie behoren. |
| [!DNL Sandbox Administration] | [!UICONTROL Een sandbox opnieuw instellen] | Mogelijkheid om een sandbox opnieuw in te stellen. |
| [!DNL Destinations] | [!UICONTROL Doelen beheren] | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen.* |
| [!DNL Destinations] | [!UICONTROL Doelen weergeven] | Alleen-lezen toegang tot beschikbare doelen op het tabblad *[!UICONTROL Catalogus]* en geverifieerde doelen op het tabblad *[!UICONTROL Bladeren]* .* |
| [!DNL Destinations] | [!UICONTROL Doelen activeren] | Mogelijkheid om gegevens te activeren naar actieve doelen die zijn gemaakt. Voor deze machtiging is het vereist dat &quot;Doelen weergeven&quot; of &quot; [!UICONTROL Doelen beheren&quot;] wordt toegekend aan de gebruiker die bestemmingen activeert.* |
| [!DNL Data Ingestion] | [!UICONTROL Bronnen beheren] | Toegang tot het lezen, maken, bewerken en uitschakelen van bronnen. |
| [!DNL Data Ingestion] | [!UICONTROL Bronnen weergeven] | Alleen-lezen toegang tot beschikbare bronnen op het tabblad *[!UICONTROL Catalogus]* en geverifieerde bronnen op het tabblad *[!UICONTROL Bladeren]* . |
| [!DNL Data Science Workspace] | [!UICONTROL Werkruimte voor gegevenswetenschap beheren] | Toegang tot lezen, maken, bewerken en verwijderen [!DNL Data Science Workspace]. |

_(*) Deze toestemming vereist bepalingen aan[!DNL Real-time Customer Data Platform]. Voor meer informatie betreffende real time CDP, gelieve te beginnen door het[overzicht](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)in real time te lezen CDP._

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangscontrole in [!DNL Experience Platform]. U kunt nu doorgaan naar de gebruikershandleiding [voor](./ui/overview.md) toegangsbeheer voor gedetailleerde stappen met betrekking tot het gebruik van de handleiding [!DNL Admin Console] om productprofielen te maken en machtigingen toe te wijzen voor [!DNL Platform].