---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Beleidsgegevensmodel;Gegevensmodel;Gegevensmodel;Schema register;Schemaregister
solution: Experience Platform
title: Handleiding voor ontwikkelaars van de API voor schemaregister
description: 'Met de API voor het schemaregister kunt u programmatisch alle schema''s en gerelateerde XDM-bronnen beheren die binnen het Experience Platform beschikbaar zijn. '
topic: developer guide
translation-type: tm+mt
source-git-commit: 44a727f6ce4c2b90aa010379583c7c4d3ebd011c
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 0%

---


# [!DNL Schema Registry] Handleiding voor API-ontwikkelaars

De [!DNL Schema Registry] wordt gebruikt om tot de Bibliotheek van het Schema binnen Adobe Experience Platform toegang te hebben, die een gebruikersinterface en RESTful API verstrekken waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn.

De API van de Registratie van het Schema verstrekt verscheidene eindpunten die u toestaan om alle schema&#39;s en verwante middelen van de Gegevens van de Ervaring programmatically te beheren van het Gegevensmodel (XDM) beschikbaar aan u binnen Platform. Dit omvat die door Adobe, [!DNL Experience Platform] partners, en verkopers worden bepaald van wie toepassingen u gebruikt.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [begonnen gids](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

>[!IMPORTANT]
>
>XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Alvorens met de Registratie API van het Schema te werken, wordt het sterk geadviseerd dat u [officiële documentatie van het Schema JSON](https://json-schema.org/) voor een beter inzicht in deze onderliggende technologie herzien.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [Referentie van de API voor schemaregistratie](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/schema-registry.yaml).

## Schemas

De schema&#39;s XDM vertegenwoordigen en bevestigen de structuur en het formaat van gegevens die in Platform worden opgenomen. Een schema bestaat uit een klasse en nul of meer combinaties. U kunt schema&#39;s tot stand brengen, bekijken, uitgeven en schrappen gebruikend het `/schemas` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, zie [schemas eindgids](./schemas.md).

Voor een geleidelijke gids op hoe te om een volledig schema in de Registratie API van het Schema tot stand te brengen, met inbegrip van het creëren van en het toevoegen van mengen en gegevenstypes, zie [API schemaverwezenlijking zelfstudie](../tutorials/create-schema-api.md).

## Gedrag

Het gedrag bepaalt de aard van gegevens die een schema beschrijft. Elke klasse XDM moet naar een specifiek gedrag verwijzen, dat alle schema&#39;s die die klasse gebruiken zullen erven. Zie [eindpuntgids voor gedrag](./behaviors.md) om te leren hoe te om beschikbaar gedrag in API te bekijken.

## Klassen

Een klasse definieert de basisstructuur van gemeenschappelijke eigenschappen die alle schema&#39;s die op die klasse zijn gebaseerd, moeten bevatten en bepaalt welke mixins in aanmerking komen voor gebruik in die schema&#39;s. Elke klasse moet aan een bestaand gedrag worden geassocieerd. Zie [de gids van het klassen eindpunt](./classes.md) voor details bij het werken met klassen in API.

## Mixins

Mixins zijn herbruikbare componenten die een of meer velden definiëren die een bepaald concept vertegenwoordigen, zoals een individuele persoon, een mailingadres of een webbrowseromgeving. Mixins zijn bedoeld om te worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert, afhankelijk van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Zie [mixins eindpuntgids](./mixins.md) om te leren hoe te met mixins in API werken.

## Datatypen

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als velden van het verwijzingstype in klassen of mixen. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Hoewel gelijkaardig aan mengelingen in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de mengelingen slechts op het wortelniveau kunnen worden toegevoegd. Zie [gegevenstypes eindgids](./data-types.md) voor meer informatie over het werken met gegevenstypes in API.

## Beschrijvers

Descriptors zijn reeksen meta-gegevens die aan specifieke gebieden binnen een schema worden toegewezen, die diverse contextuele details verstrekken met inbegrip van hoe die gebieden (en het schema zelf) met andere schema&#39;s verwant zijn. Op elk schema kunnen een of meer descriptorentiteiten zijn toegepast en er zijn verschillende descriptortypen voor verschillende doeleinden. Zie [descriptoreindhulplijn](./descriptors.md) voor meer informatie over het werken met descriptoren in de API en een overzicht van de verschillende descriptortypen en hun gebruiksgevallen.

## Unies

Terwijl het Platform u toestaat om schema&#39;s voor bepaalde gebruiksgevallen samen te stellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s samen te stellen die tot een specifieke klasse behoren. Een samenvoegingsschema voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkele vertegenwoordiging delen. Door een schema voor gebruik met [Real-time Profiel van de Klant ](../../profile/home.md) toe te laten, wordt dat schema inbegrepen in de unie voor zijn bepaalde klasse. Als zodanig kunnen unieschema&#39;s niet rechtstreeks worden bewerkt en alleen worden beïnvloed door het opnemen of uitsluiten van schema&#39;s voor gebruik in profiel.

Leren hoe te om vakbonden in de Registratie API van het Schema te bekijken, zie [de gids van het uniepunteindpunt](./unions.md).

## Exporteren/importeren

Met de API voor schemaregistratie kunt u XDM-bronnen overbrengen en delen tussen sandboxen en IMS-organisaties. Voor om het even welk schema, mengsel, of gegevenstype, kunt u een de uitvoerlading produceren die de structuur van het middel en om het even welke afhankelijke middelen bevat. Deze nuttige lading kan dan worden gebruikt om het middel in een bestemmingszandbak en IMS Org in te voeren.

Zie [export/import eindpunten guide](./export-import.md) voor meer informatie over hoe te om deze eindpunten te gebruiken.

## Voorbeeldgegevens

U kunt steekproefgegevens voor om het even welk gespecificeerd schema binnen de Bibliotheek van het Schema produceren. Het geretourneerde reactieobject kan vervolgens worden gebruikt als bron voor gegevensinvoer.

Zie [de gids van het eindpunt van steekproefgegevens](./sample-data.md) voor meer informatie over het gebruik van dit eindpunt.

## Controlelogboek

De Registratie van het Schema handhaaft een logboek van alle veranderingen die aan een middel (klasse, mixin, gegevenstype, of schema) tussen verschillende updates zijn voorgekomen. U kunt het logboek voor een bepaalde middel terugwinnen door zijn `$id` of `meta:altId` in de weg van een verzoek van de GET aan dit eindpunt te verstrekken.

Zie [de eindpuntgids van het controlelogboek](./audit-log.md) voor meer informatie over het gebruik van dit eindpunt.

## Volgende stappen

Begin makend vraag gebruikend de Registratie API van het Schema, lees [begonnen gids](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.