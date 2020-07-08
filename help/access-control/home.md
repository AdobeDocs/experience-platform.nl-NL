---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Overzicht van toegangsbeheer
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 1%

---


# Overzicht van toegangsbeheer

Via de [Adobe-Admin Console](https://adminconsole.adobe.com)hebt u toegang tot het Experience Platform. Deze functionaliteit gebruikt productprofielen in Admin Console, die gebruikers met toestemmingen en zandbakken verbinden.

## Toegangsbeheerhiërarchie en -workflow

Om toegangsbeheer voor Experience Platform te vormen, moet u beheerdervoorrechten voor een organisatie hebben die een de productintegratie van het Experience Platform heeft. De minimale rol die machtigingen verleent of intrekt, is een beheerder **van het** productprofiel. Andere beheerdersrollen die machtigingen kunnen beheren, zijn **productbeheerders** (die alle profielen binnen een product kunnen beheren) en **systeembeheerders** (geen beperkingen). Zie het artikel in Adobe Help Center over [beheerrollen](https://helpx.adobe.com/enterprise/using/admin-roles.html) voor meer informatie.

>[!NOTE]
>
>Vanaf dit punt verwijzen vermeldingen van &quot;beheerder&quot; in dit document naar een beheerder van het productprofiel of hoger (zoals hierboven beschreven).

Een werkschema op hoog niveau voor het verkrijgen en toewijzen van toegangsmachtigingen kan als volgt worden samengevat:

- Nadat u zich hebt geabonneerd op een Adobe Experience Platform, wordt een e-mail verzonden naar de beheerder die is opgegeven in het registratieformulier.
- De beheerder meldt zich aan bij de Admin Console [van](#adobe-admin-console) Adobe en selecteert **Adobe Experience Platform** van de lijst van producten op de overzichtspagina.
- De beheerder kan de standaardprofielen [van het](#product-profiles) product bekijken of nieuwe profielen van het klantenproduct tot stand brengen zoals nodig.
- De beheerder kan de machtigingen en gebruikers voor bestaande productprofielen bewerken.
- Wanneer de beheerder een productprofiel maakt of bewerkt, voegt hij gebruikers aan het profiel toe via het tabblad **Gebruikers** en verleent hij deze gebruikers machtigingen (zoals &quot;Datasets lezen&quot; of &quot;Schema&#39;s beheren&quot;) via het tabblad **machtigingen** . Op dezelfde manier kan de beheerder toegang tot sandboxen toewijzen via hetzelfde machtigingentabblad.
- Wanneer de gebruikers login aan het gebruikersinterface van het Experience Platform, hun toegang tot de mogelijkheden van het Platform door de toestemmingen worden gedreven die aan hen van Stap 2 zijn verleend. Als een gebruiker bijvoorbeeld niet beschikt over de machtiging Datasets weergeven, is het tabblad *Datasets* in het zijmenu niet zichtbaar voor die gebruiker.

Voor meer gedetailleerde stappen op hoe te om toegangsbeheer in Experience Platform te beheren, zie de gebruikershandleiding van de [toegangscontrole](./ui/overview.md).

Alle aanroepen naar Experience Platform-API&#39;s worden gevalideerd voor machtigingen en retourneren fouten als de juiste machtigingen niet worden gevonden in de huidige gebruikerscontext. Binnen UI, zullen de elementen worden verborgen of worden veranderd afhankelijk van toestemmingen die aan de huidige gebruiker worden verleend.

## Adobe Admin Console

Adobe Admin Console biedt een centrale locatie voor het beheer van Adobe-productrechten en -toegang voor uw organisatie. Via de console kunt u groepen gebruikers toegangsmachtigingen verlenen voor verschillende functies van het Platform, zoals &quot;Datasets beheren&quot;, &quot;Gegevensbestanden weergeven&quot; of &quot;Profielen beheren&quot;.

### Productprofielen

In de Admin Console worden machtigingen aan gebruikers toegewezen via het gebruik van **productprofielen**. Met productprofielen kunt u machtigingen verlenen aan een of meerdere gebruikers en ook toegang tot het bereik van de sandboxen bevatten die via productprofielen aan hen zijn toegewezen. Gebruikers kunnen worden toegewezen aan een of meerdere productprofielen die bij uw organisatie horen.

### Standaardproductprofielen

Experience Platform wordt geleverd met twee vooraf geconfigureerde standaardproductprofielen. De volgende tabel geeft een overzicht van de inhoud van elk standaardprofiel, inclusief de sandbox waartoe ze toegang verlenen en de machtigingen die ze binnen het bereik van die sandbox verlenen.

| Productprofiel | Toegang tot sandbox | Toestemmingen |
| --- | --- | --- |
| Standaardproductie - Alle toegang | Productie | Alle toestemmingen van toepassing op Experience Platform, behalve de toestemmingen van het Beleid Sandbox. |
| Standaardsandboxbeheer | N.v.t. | Verleent toegang slechts tot de toestemmingen van het Beleid Sandbox. |

## Sandboxen en machtigingen

Met Experience Platform hebt u toegang tot één productiesandbox en kunt u niet-productiesandboxen **maken**. Niet-productiesandboxen zijn een vorm van gegevensvirtualisatie waarmee u gegevens kunt isoleren van andere sandboxen. Deze sandboxen worden doorgaans gebruikt voor ontwikkelingsexperimenten, -tests of -tests. De **machtigingen** van een productprofiel geven de gebruikers van het profiel toegang tot de functies van het Platform in de sandbox-omgevingen waartoe zij toegang hebben.

Raadpleeg het [sandboxoverzicht](../sandboxes/home.md)voor meer informatie over sandboxen in Experience Platform.

### Toegang tot sandboxen

Toegang tot sandboxen wordt beheerd via productprofielen. Voor gedetailleerde stappen op hoe te om toegang tot een zandbak voor een productprofiel toe te laten, zie de [gebruikershandleiding](./ui/overview.md)van de toegangscontrole.

Gebruikers kunnen toegang krijgen tot een of meer sandboxen in een productprofiel. Als één gebruiker in twee of meer productprofielen is opgenomen, heeft die gebruiker toegang tot alle sandboxen die in die profielen zijn opgenomen.

Met de machtiging Sandboxbeheer kunnen gebruikers sandboxen beheren, weergeven of opnieuw instellen.

### Toestemmingen

Op het tabblad **Machtigingen** in een productprofiel worden de sandboxen en machtigingen weergegeven die actief zijn voor dat profiel:

![](./images/permissions-overview.png)

Machtigingen die via de Admin Console worden verleend, worden gesorteerd op categorie, waarbij bepaalde machtigingen toegang verlenen tot verschillende functies op laag niveau.

De volgende lijst schetst de beschikbare toestemmingen voor Experience Platform in de Admin Console, met beschrijvingen van de specifieke mogelijkheden van het Platform zij toegang tot verlenen. Voor gedetailleerde stappen op hoe te om toestemmingen aan een productprofiel toe te voegen, zie de gebruikershandleiding van de [toegangscontrole](./ui/overview.md).

| Categorie | Machtiging | Beschrijving |
| --- | --- | --- |
| Gegevensmodellering | Schema&#39;s beheren | Toegang tot het lezen, maken, bewerken en verwijderen van schema&#39;s en gerelateerde bronnen. |
| Gegevensmodellering | Schema&#39;s weergeven | Alleen-lezen toegang tot schema&#39;s en gerelateerde bronnen. |
| Gegevensbeheer | Gegevensbestanden beheren | Toegang tot het lezen, creëren, uitgeven, en schrappen datasets. Alleen-lezen toegang voor schema&#39;s. |
| Gegevensbeheer | Gegevensbestanden weergeven | Alleen-lezen toegang voor gegevenssets en schema&#39;s. |
| Gegevensbeheer | Gegevenscontrole | Alleen-lezen toegang tot gegevenssets en streams controleren. |
| Profielbeheer | Profielen beheren | Toegang tot gelezen, creeer, geef, en schrap datasets uit die voor klantenprofielen worden gebruikt. Alleen-lezen toegang tot beschikbare profielen. |
| Profielbeheer | Profielen weergeven | Alleen-lezen toegang tot beschikbare profielen. |
| Profielbeheer | Publiek exporteren voor segment | Capaciteit om een geëvalueerd publiekssegment naar een dataset uit te voeren. |
| Identiteiten | Identiteitsnaamruimten beheren | Toegang tot het lezen, maken, bewerken en verwijderen van naamruimten. |
| Identiteiten | Identiteitsnaamruimten weergeven | Alleen-lezen toegang voor naamruimten. |
| Sandbox-beheer | Sandboxen beheren | Toegang tot het lezen, maken, bewerken en verwijderen van sandboxen. |
| Sandbox-beheer | Sandboxen weergeven | Alleen-lezen toegang voor sandboxen die tot uw organisatie behoren. |
| Sandbox-beheer | Een sandbox opnieuw instellen | Mogelijkheid om een sandbox opnieuw in te stellen. |
| Doelen | Doelen beheren | Toegang tot het lezen, creëren, uitgeven, en onbruikbaar maken bestemmingen.* |
| Doelen | Doelen weergeven | Alleen-lezen toegang tot beschikbare doelen op het tabblad *Catalogus* en geverifieerde doelen op het tabblad *Bladeren* .* |
| Doelen | Doelen activeren | Mogelijkheid om gegevens te activeren naar actieve doelen die zijn gemaakt. Deze toestemming vereist of &quot;de Doelen van de Mening&quot;of &quot;Beheert Doelen&quot;om aan de gebruiker te worden verleend die bestemmingen zal activeren.* |
| Gegevensinname | Bronnen beheren | Toegang tot het lezen, maken, bewerken en uitschakelen van bronnen. |
| Gegevensinname | Bronnen weergeven | Alleen-lezen toegang tot beschikbare bronnen op het tabblad *Catalogus* en geverifieerde bronnen op het tabblad *Bladeren* . |
| Werkruimte voor gegevenswetenschap | Werkruimte voor gegevenswetenschap beheren | Toegang tot het lezen, maken, bewerken en verwijderen van gegevens in de wetenschappelijke werkruimte. |

_(*) Deze toestemming vereist bepalingen aan het Platform van de Gegevens van de Klant in real time. Voor meer informatie betreffende real time CDP, gelieve te beginnen door het[overzicht](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/overview.html)in real time te lezen CDP._

## Volgende stappen

Door deze gids te lezen, bent u geïntroduceerd aan de belangrijkste principes van toegangscontrole in Experience Platform. U kunt nu doorgaan naar de gebruikershandleiding voor [toegangsbeheer](./ui/overview.md) voor gedetailleerde stappen over hoe u de Admin Console gebruikt om productprofielen te maken en machtigingen voor Platform toe te wijzen.