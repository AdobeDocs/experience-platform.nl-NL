---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;
solution: Experience Platform
title: Handleiding voor ontwikkelaars van de API voor schemaregister
description: 'Met de API voor het schemaregister kunt u programmatisch alle schema''s en gerelateerde XDM-bronnen beheren die binnen het Experience Platform beschikbaar zijn. '
topic: developer guide
translation-type: tm+mt
source-git-commit: d0e5865fddcf2592e9b6d8d4b2747bdceee6bda7
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 0%

---


# [!DNL Schema Registry] Handleiding voor API-ontwikkelaars

Het [!DNL Schema Registry] wordt gebruikt om toegang te krijgen tot de Schemabibliotheek in Adobe Experience Platform, waarbij een gebruikersinterface en de RESTful-API worden opgegeven die toegang bieden tot alle beschikbare bibliotheekbronnen.

De API van de Registratie van het Schema verstrekt verscheidene eindpunten die u toestaan om alle schema&#39;s en verwante middelen van de Gegevens van de Ervaring programmatically te beheren van het Gegevensmodel (XDM) beschikbaar aan u binnen Platform. Dit omvat die door Adobe, [!DNL Experience Platform] partners, en verkopers worden bepaald waarvan toepassingen u gebruikt.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar de [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

>[!IMPORTANT]
>
>XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Voordat u gaat werken met de Schema Registry API, wordt u ten zeerste aangeraden de [officiële JSON-schemadocumentatie](https://json-schema.org/) te raadplegen voor een beter inzicht in deze onderliggende technologie.

Ga naar de API-naslaggids voor [schema&#39;s om alle beschikbare eindpunten en CRUD-bewerkingen weer te geven](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schemas

De schema&#39;s XDM vertegenwoordigen en bevestigen de structuur en het formaat van gegevens die in Platform worden opgenomen. Een schema bestaat uit een klasse en nul of meer combinaties. U kunt schema&#39;s tot stand brengen, bekijken, uitgeven en schrappen gebruikend het `/schemas` eindpunt. Leren hoe te om dit eindpunt te gebruiken, zie de gids [van het](./schemas.md)schemaeindpunt.

Voor een geleidelijke gids op hoe te om een volledig schema in de Registratie API van het Schema tot stand te brengen, met inbegrip van het creëren van en het toevoegen van mengen en gegevenstypes, zie de [API schemaverwezenlijking zelfstudie](../tutorials/create-schema-api.md).

## Klassen

De klassen bepalen de gedragsaspecten van de gegevens die een schema (verslag of tijdreeks) zal bevatten. Bovendien bepaalt een klasse de basisstructuur van gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd moeten bevatten. De klasse van een schema bepaalt welke mengen voor gebruik in dat schema geschikt zijn. Zie de gids [van het](./classes.md) klassen eindpunt voor details bij het werken met klassen in API.

## Mixins

Mixins zijn herbruikbare componenten die een of meer velden definiëren die een bepaald concept vertegenwoordigen, zoals een individuele persoon, een mailingadres of een webbrowseromgeving. Mixins zijn bedoeld om te worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert, afhankelijk van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Zie de gids [van het](./mixins.md) mixineindpunt om te leren hoe te met mixins in API werken.

## Datatypen

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als velden van het verwijzingstype in klassen of mixen. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Hoewel gelijkaardig aan mengelingen in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de mengelingen slechts op het wortelniveau kunnen worden toegevoegd. Zie de gids [van het](./data-types.md) gegevenstypeseindpunt voor meer informatie over het werken met gegevenstypes in API.

## Beschrijvers

Descriptors zijn reeksen meta-gegevens die specifieke gebieden binnen een schema worden toegewezen, die diverse contextuele details verstrekken met inbegrip van hoe die gebieden (en het schema zelf) met andere schema&#39;s verwant zijn. Op elk schema kunnen een of meer descriptorentiteiten zijn toegepast en er zijn verschillende descriptortypen voor verschillende doeleinden. Zie de gids [voor](./descriptors.md) descriptoreindpunten voor meer informatie over het werken met descriptoren in de API en een overzicht van de verschillende descriptortypen en hun gebruiksgevallen.

## Unies

Terwijl het Platform u toestaat om schema&#39;s voor bepaalde gebruiksgevallen samen te stellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s samen te stellen die tot een specifieke klasse behoren. Een samenvoegingsschema voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkele vertegenwoordiging delen. Door een schema voor gebruik met het Profiel [van de Klant in](../../profile/home.md)real time toe te laten, wordt dat schema inbegrepen in de unie voor zijn bepaalde klasse. Als zodanig kunnen unieschema&#39;s niet rechtstreeks worden bewerkt en alleen worden beïnvloed door het opnemen of uitsluiten van schema&#39;s voor gebruik in profiel.

Leren hoe te om vakbonden in de Registratie API van het Schema te bekijken, zie de gids [van het](./unions.md)uniepunteindpunt.

## Exporteren/importeren

Met de API voor schemaregistratie kunt u XDM-bronnen overbrengen en delen tussen sandboxen en IMS-organisaties. Voor om het even welk schema, mengsel, of gegevenstype, kunt u een de uitvoerlading produceren die de structuur van het middel en om het even welke afhankelijke middelen bevat. Deze nuttige lading kan dan worden gebruikt om het middel in een bestemmingszandbak en IMS Org in te voeren.

Zie de [Referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van de Registratie van het Schema API voor meer informatie over het gebruik van dit eindpunt.

## Voorbeeldgegevens

U kunt steekproefgegevens voor om het even welk gespecificeerd schema binnen de Bibliotheek van het Schema produceren. Het geretourneerde reactieobject kan vervolgens worden gebruikt als bron voor gegevensinvoer.

Zie de [Referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van de Registratie van het Schema API voor meer informatie over het gebruik van dit eindpunt.

## Controlelogboek

De Registratie van het Schema handhaaft een logboek van alle veranderingen die aan een middel (klasse, mixin, gegevenstype, of schema) tussen verschillende updates zijn voorgekomen. U kunt het logboek voor een bepaald middel terugwinnen door zijn `$id` of `meta:altId` in de weg van een verzoek van de GET aan dit eindpunt te verstrekken.

Zie de [Referentie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml) van de Registratie van het Schema API voor meer informatie over het gebruik van dit eindpunt.

## Volgende stappen

Beginnen het maken vraag gebruikend de Registratie API van het Schema, lees de [begonnen gids](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.