---
keywords: Experience Platform;huis;populaire onderwerpen;api;op attributen-gebaseerde toegangscontrole;Op Attribuut-Gebaseerd Toegangsbeheer
solution: Experience Platform
title: API-handleiding voor toegangsbeheer op basis van kenmerken
description: Met de API voor toegangsbeheer op basis van kenmerken kunt u rollen en beleid in Adobe Experience Platform programmatisch beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
exl-id: 0fc32354-4869-4392-9501-b1dbea1bc55e
source-git-commit: 567bfe089fd96cb08cb8ea7c90d065c804be9413
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# API-handleiding voor toegangsbeheer op basis van kenmerken

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven.

Toegangsbeheer op basis van kenmerken is een mogelijkheid van Adobe Experience Platform waarmee beheerders de toegang tot specifieke objecten en/of mogelijkheden kunnen beheren op basis van kenmerken. Kenmerken kunnen metagegevens zijn die aan een object worden toegevoegd, zoals een label dat aan een schemaveld of -segment wordt toegevoegd. Een beheerder bepaalt toegangsbeleid dat attributen omvat om de toestemmingen van de gebruikerstoegang te beheren.

De op attribuut-gebaseerde toegangsbeheer API wordt gebruikt om tot rollen, producten, toestemmingscategorieën, en toestemmingsreeksen binnen Adobe Experience Platform toegang te hebben, die een gebruikersinterface verstrekken en RESTful API waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn.

Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

## Rollen

De rollen bepalen de toegang die een beheerder, een specialist, of een eindgebruiker aan middelen in uw organisatie moet hebben. In een op rol-gebaseerd milieu van het toegangsbeheer, is de levering van de gebruikerstoegang groepering door gemeenschappelijke verantwoordelijkheden en behoeften. Een rol heeft een bepaalde reeks toestemmingen en de leden van uw organisatie kunnen aan één of meerdere rollen, afhankelijk van het werkingsgebied van mening worden toegewezen of toegang schrijven zij nodig hebben. Zie de [hulplijn voor roleindpunt](./roles.md) voor meer informatie over het werken met rollen in API.

## Beleid

Het beleid is verklaringen die attributen samenbrengen om toegelaten en ontoelaatbare acties te vestigen. Het beleid kan of lokaal of globaal zijn, en kan ander beleid met voeten treden. De `/policies` het eindpunt staat u toe om beleid in uw organisatie programmatically te beheren. Zie de [leidraad voor beleidseindpunten](./policies.md) voor meer informatie over het werken met beleid in API.

## Producten

De `/products` eindpunt in op attribuut-gebaseerde toegangsbeheer API staat u toe om producten evenals toestemmingscategorieën en toestemmingsreeksen programmatically te beheren verbonden aan producten in uw organisatie. Zie de [eindgebruikergids voor producten](./products.md) voor meer informatie over het werken met producten en hun overeenkomstige toestemmingscategorieën en toestemmingsreeksen in API.

## Volgende stappen

Beginnen het maken van vraag gebruikend op attribuut-gebaseerde toegangsbeheer API, lees [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.
