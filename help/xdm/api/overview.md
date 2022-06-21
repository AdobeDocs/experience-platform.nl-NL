---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;Ervaring gegevensmodel;Beleidsgegevensmodel;Gegevensmodel;Gegevensmodel;Schema register;Schemaregister
solution: Experience Platform
title: Handleiding voor schema-registratie-API
description: Met de API voor het schemaregister kunnen ontwikkelaars programmatisch alle schema's en gerelateerde XDM-bronnen (Experience Data Model) in Adobe Experience Platform beheren. Volg deze handleiding voor het uitvoeren van toetsbewerkingen met de API.
topic-legacy: developer guide
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: 2a58236031834bbe298576e2fcab54b04ec16ac3
workflow-type: tm+mt
source-wordcount: '1084'
ht-degree: 0%

---

# [!DNL Schema Registry] API-handleiding

De [!DNL Schema Registry] wordt gebruikt om toegang te krijgen tot de Schemabibliotheek in Adobe Experience Platform, die een gebruikersinterface en RESTful API verstrekt waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn.

De API van de Registratie van het Schema verstrekt verscheidene eindpunten die u toestaan om alle schema&#39;s en verwante middelen van de Gegevens van de Ervaring programmatically te beheren van het Gegevensmodel (XDM) beschikbaar aan u binnen Platform. Hieronder vallen ook de definities van Adobe, [!DNL Experience Platform] partners, en verkopers waarvan toepassingen u gebruikt.

Deze eindpunten worden hieronder beschreven. Ga naar de afzonderlijke eindpunthulplijnen voor meer informatie en raadpleeg de [gids Aan de slag](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lees steekproefAPI vraag, en meer.

>[!IMPORTANT]
>
>XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Voordat u gaat werken met de API voor het schemaregister, wordt u ten zeerste aangeraden de [Officiële JSON-schemadocumentatie](https://json-schema.org/) voor een beter inzicht in deze onderliggende technologie.

Als u alle beschikbare eindpunten en CRUD-bewerkingen wilt weergeven, gaat u naar de [Referentie voor schema-register-API](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schema&#39;s

De schema&#39;s XDM vertegenwoordigen en bevestigen de structuur en het formaat van gegevens die in Platform worden opgenomen. Een schema bestaat uit een klasse en nul of meer groepen schemavelden. U kunt schema&#39;s maken, weergeven, bewerken en verwijderen met de opdracht `/schemas` eindpunt. Om te leren hoe te om dit eindpunt te gebruiken, zie [schema&#39;s eindpuntgids](./schemas.md).

Voor een geleidelijke gids over hoe te om een volledig schema in de Registratie API van het Schema tot stand te brengen, met inbegrip van het creëren van en het toevoegen van gebiedsgroepen en gegevenstypes, zie [Zelfstudie over het maken van API-schema](../tutorials/create-schema-api.md).

## Gedrag

Gedragingen bepalen de aard van gegevens die een schema beschrijft. Elke klasse XDM moet naar een specifiek gedrag verwijzen, dat alle schema&#39;s die die klasse gebruiken zullen erven. Zie de [gedragseindpunt-hulplijn](./behaviors.md) voor meer informatie over het weergeven van beschikbare gedragingen in de API.

## Klassen

Een klasse definieert de basisstructuur van gemeenschappelijke eigenschappen die alle schema&#39;s die op die klasse zijn gebaseerd, moeten bevatten en bepaalt welke veldgroepen in aanmerking komen voor gebruik in die schema&#39;s. Elke klasse moet aan een bestaand gedrag worden geassocieerd. Zie de [hulplijn voor klassen eindpunt](./classes.md) voor meer informatie over het werken met klassen in de API.

## Veldgroepen

Veldgroepen zijn herbruikbare componenten die een of meer velden definiëren die een bepaald concept vertegenwoordigen, zoals een individuele persoon, een mailingadres of een webbrowseromgeving. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert, afhankelijk van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Zie de [eindgids voor veldgroepen](./field-groups.md) voor meer informatie over het werken met veldgroepen in de API.

## Datatypen

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als referentietypen in klassen of veldgroepen. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Hoewel gelijkaardig aan gebiedsgroepen in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de gebiedsgroepen slechts op het wortelniveau kunnen worden toegevoegd. Zie de [eindhulplijn gegevenstypen](./data-types.md) voor meer informatie over het werken met gegevenstypen in de API.

## Beschrijvers

Descriptors zijn reeksen meta-gegevens die aan specifieke gebieden binnen een schema worden toegewezen, die diverse contextuele details verstrekken met inbegrip van hoe die gebieden (en het schema zelf) met andere schema&#39;s verwant zijn. Op elk schema kunnen een of meer descriptorentiteiten zijn toegepast en er zijn verschillende descriptortypen voor verschillende doeleinden. Zie de [eindhulplijn descriptorpunt](./descriptors.md) voor meer informatie over het werken met beschrijvers in API, en een overzicht van de verschillende beschrijvingstypes en hun gebruiksgevallen.

## Unies

Terwijl het Platform u toestaat om schema&#39;s voor bepaalde gebruiksgevallen samen te stellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s samen te stellen die tot een specifieke klasse behoren. Een samenvoegingsschema voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkele vertegenwoordiging delen. Door een schema in te schakelen voor gebruik met [Klantprofiel in realtime](../../profile/home.md), wordt dat schema opgenomen in de union voor de desbetreffende klasse. Als zodanig kunnen unieschema&#39;s niet rechtstreeks worden bewerkt en alleen worden beïnvloed door het opnemen of uitsluiten van schema&#39;s voor gebruik in profiel.

Zie voor meer informatie over het weergeven van vakbonden in de API voor schemaregistratie [Punthandleiding voor vakbonden](./unions.md).

## CSV naar schemaomzetting {#csv-to-schema}

U kunt automatisch een XDM-schema genereren door een CSV-bestand als sjabloon te gebruiken, zodat u sjablonen kunt maken voor het bulksgewijs importeren van schemavelden en kunt knippen op handmatig API- of UI-werk.

Zie de [CSV aan de eindgids van de schemaomzetting](./export.md) voor meer informatie .

## Exporteren {#export}

Met de API voor schemaregistratie kunt u XDM-bronnen overbrengen en delen tussen sandboxen en IMS-organisaties. Voor om het even welk schema, gebiedsgroep, of gegevenstype, kunt u een de uitvoerlading produceren die de structuur van het middel en om het even welke afhankelijke middelen bevat. Deze nuttige lading kan dan worden gebruikt om het middel in een bestemmingszandbak en IMS Org in te voeren.

Zie de [eindgebruikershandleiding exporteren](./export.md) voor meer informatie over hoe te om een de uitvoerlading voor een bestaand middel tot stand te brengen XDM.

## Importeren

Als u het [export](#export) of [CSV naar schemaomzetting](./import.md) eindpunten om een exportlading te creëren, kunt u die lading naar een doelorganisatie en zandbak verzenden om de gespecificeerde middelen in te voeren.

Zie de [hulplijn voor importeindpunt](./export.md) voor meer informatie over hoe u XDM-bronnen kunt genereren op basis van exportladingen.

## Voorbeeldgegevens

U kunt steekproefgegevens voor om het even welk gespecificeerd schema binnen de Bibliotheek van het Schema produceren. Het geretourneerde reactieobject kan vervolgens worden gebruikt als bron voor gegevensinvoer.

Zie de [eindgids met voorbeeldgegevens](./sample-data.md) voor meer informatie over het gebruik van dit eindpunt.

## Controlelogboek

De Registratie van het Schema handhaaft een logboek van alle veranderingen die aan een middel (klasse, gebiedsgroep, gegevenstype, of schema) tussen verschillende updates zijn voorgekomen. U kunt het logboek voor een bepaalde bron terugwinnen door zijn te verstrekken `$id` of `meta:altId` in de weg van een verzoek van de GET aan dit eindpunt.

Zie de [eindhandleiding van auditlogboek](./audit-log.md) voor meer informatie over het gebruik van dit eindpunt.

## Volgende stappen

Beginnen het maken van vraag gebruikend de Registratie API van het Schema, lees [gids Aan de slag](./getting-started.md) Selecteer vervolgens een van de eindpunthulplijnen om te leren hoe u specifieke eindpunten kunt gebruiken.
