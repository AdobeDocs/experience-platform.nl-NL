---
keywords: Experience Platform;huis;populaire onderwerpen;api;op attributen-gebaseerde toegangscontrole;Op Attribuut-Gebaseerd Toegangsbeheer
solution: Experience Platform
title: API-handleiding voor toegangsbeheer op basis van kenmerken
description: Met de API voor toegangsbeheer op basis van kenmerken kunt u rollen en toegangsbeleid in Adobe Experience Platform programmatisch beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
role: Developer
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 3%

---

# API-handleiding voor toegangsbeheer op basis van kenmerken

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

De op attribuut-gebaseerde toegangsbeheer API wordt gebruikt om tot rollen, producten, toestemmingscategorieën, en toestemmingsreeksen binnen Adobe Experience Platform toegang te hebben, die een gebruikersinterface verstrekken en RESTful API waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn.

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole moet niet met de mogelijkheden van het gegevensbeheer van het Experience Platform worden verward, die u toestaan om etiketten en beleid te gebruiken om te controleren hoe het gegeven in Platform eerder wordt gebruikt dan welke gebruikers in uw organisatie toegang tot het hebben. Zie de [ gids van de Dienst API van het Beleid ](../../../data-governance/api/overview.md) voor stappen op hoe te hefboomwerking programmatically deze mogelijkheden.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

## Rollen

De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben. Zie de [ gids van het roleindpunt ](./roles.md) voor meer informatie bij het werken met rollen in API.

## Beleid

Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. Het `/policies` eindpunt staat u toe om beleid in uw organisatie programmatically te beheren. Zie de [ gids van het beleidseindpunt ](./policies.md) voor meer informatie bij het werken met beleid in API.

## Producten

Het `/products` eindpunt in op attribuut-gebaseerde toegangsbeheer API staat u toe om producten evenals toestemmingscategorieën en toestemmingsreeksen programmatically te beheren verbonden aan producten in uw organisatie. Zie de [ gids van het producteindpunt ](./products.md) voor meer informatie bij het werken met producten en hun overeenkomstige toestemmingscategorieën en toestemmingsreeksen in API.

## Volgende stappen

Begin makend vraag gebruikend op attribuut-gebaseerde toegangscontrole API, lees [ begonnen gids ](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
