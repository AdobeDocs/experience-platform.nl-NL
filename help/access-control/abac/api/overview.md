---
keywords: Experience Platform;home;populaire onderwerpen;api;op attributen-gebaseerd toegangsbeheer;Op attributen-Gebaseerd Toegangsbeheer
solution: Experience Platform
title: API-handleiding voor toegangsbeheer op basis van kenmerken
description: Met de API voor toegangsbeheer op basis van kenmerken kunt u rollen en toegangsbeleid in Adobe Experience Platform programmatisch beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 3%

---

# API-handleiding voor toegangsbeheer op basis van kenmerken

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

De op attribuut-gebaseerde toegangsbeheer API wordt gebruikt om tot rollen, producten, toestemmingscategorieën, en toestemmingsreeksen binnen Adobe Experience Platform toegang te hebben, die een gebruikersinterface verstrekken en RESTful API waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn.

>[!IMPORTANT]
>
>Toegangsbeheer op basis van kenmerken mag niet worden verward met Experience Platform-mogelijkheden voor gegevensbeheer, waardoor u labels en beleidsregels kunt gebruiken om te bepalen hoe gegevens in Experience Platform worden gebruikt en niet welke gebruikers in uw organisatie er toegang toe hebben. Zie de [&#x200B; gids van de Dienst API van het Beleid &#x200B;](../../../data-governance/api/overview.md) voor stappen op hoe te hefboomwerking programmatically deze mogelijkheden.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [&#x200B; begonnen gids &#x200B;](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

## Rollen

De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben. Zie de [&#x200B; gids van het roleindpunt &#x200B;](./roles.md) voor meer informatie bij het werken met rollen in API.

## Beleid

Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. Het `/policies` eindpunt staat u toe om beleid in uw organisatie programmatically te beheren. Zie de [&#x200B; gids van het beleidseindpunt &#x200B;](./policies.md) voor meer informatie bij het werken met beleid in API.

## Producten

Het `/products` eindpunt in op attribuut-gebaseerde toegangsbeheer API staat u toe om producten evenals toestemmingscategorieën en toestemmingsreeksen programmatically te beheren verbonden aan producten in uw organisatie. Zie de [&#x200B; gids van het producteindpunt &#x200B;](./products.md) voor meer informatie bij het werken met producten en hun overeenkomstige toestemmingscategorieën en toestemmingsreeksen in API.

## Volgende stappen

Begin makend vraag gebruikend op attribuut-gebaseerde toegangscontrole API, lees [&#x200B; begonnen gids &#x200B;](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
