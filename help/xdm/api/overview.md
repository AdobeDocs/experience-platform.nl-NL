---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM-systeem;ervaringsgegevensmodel;Experience gegevensmodel;Experience Data Model;Data Model;Data Model;Schema register;Schema Register
solution: Experience Platform
title: Handleiding voor schema-register
description: Met de API voor het schemaregister kunnen ontwikkelaars programmatisch alle schema's en gerelateerde XDM-bronnen (Experience Data Model) in Adobe Experience Platform beheren. Volg deze gids voor het uitvoeren van de belangrijkste bewerkingen met de API.
exl-id: 9e693d29-303e-462a-a1e2-93c0d517b8e3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1144'
ht-degree: 1%

---

# [!DNL Schema Registry] API-handleiding

[!DNL Schema Registry] wordt gebruikt om toegang te krijgen tot de Schemabibliotheek binnen Adobe Experience Platform, die een gebruikersinterface en RESTful API verstrekt waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn.

De API van de Registratie van het Schema verstrekt verscheidene eindpunten die u toestaan om alle schema&#39;s en verwante middelen van het Gegevensmodel van de Ervaring programmatically te beheren (XDM) beschikbaar aan u binnen Experience Platform. Dit zijn onder andere de gedefinieerde toepassingen door Adobe, [!DNL Experience Platform] partners en leveranciers van wie u de toepassingen gebruikt.

Deze eindpunten worden hieronder beschreven. Gelieve te bezoeken de individuele eindpuntgidsen voor details en te verwijzen naar [ begonnen gids ](./getting-started.md) voor belangrijke informatie over vereiste kopballen, lezend steekproefAPI vraag, en meer.

>[!IMPORTANT]
>
>XDM gebruikt het formatteren van het Schema JSON om de structuur van ingebedde gegevens van de klantenervaring te beschrijven en te bevestigen. Alvorens met de Registratie API van het Schema te werken, wordt het sterk geadviseerd dat u de [ officiële documentatie van het Schema JSON ](https://json-schema.org/) voor een beter inzicht in deze onderliggende technologie herziet.

Om alle beschikbare eindpunten en verrichtingen te bekijken CRUD, bezoek de [ Verwijzing van de Registratie API van het Schema ](https://www.adobe.io/experience-platform-apis/references/schema-registry/).

## Schema&#39;s

XDM-schema&#39;s vertegenwoordigen en valideren de structuur en indeling van gegevens die in Experience Platform worden ingevoerd. Een schema bestaat uit een klasse en nul of meer groepen schemavelden. U kunt schema&#39;s maken, weergeven, bewerken en verwijderen met behulp van het `/schemas` -eindpunt. Leren hoe te om dit eindpunt te gebruiken, zie de [ gids van het schemaeindpunt ](./schemas.md).

Voor een geleidelijke gids op hoe te om een volledig schema in de Registratie API van het Schema manueel tot stand te brengen, met inbegrip van het creëren van en het toevoegen van gebiedsgroepen en gegevenstypes, zie de [ API schemaverwezenlijking leerprogramma ](../tutorials/create-schema-api.md).

Als u CSV- gegevens opneemt, zie de sectie op [ CSV aan schemaomzetting ](#csv-to-schema).

## Gedrag

Gedragingen bepalen de aard van gegevens die een schema beschrijft. Elke klasse XDM moet naar een specifiek gedrag verwijzen, dat alle schema&#39;s die die klasse gebruiken zullen erven. Zie de [ gids van het gedragseindpunt ](./behaviors.md) leren hoe te om beschikbaar gedrag in API te bekijken.

## Klassen

Een klasse definieert de basisstructuur van gemeenschappelijke eigenschappen die alle schema&#39;s die op die klasse zijn gebaseerd, moeten bevatten en bepaalt welke veldgroepen in aanmerking komen voor gebruik in die schema&#39;s. Elke klasse moet aan een bestaand gedrag worden geassocieerd. Zie de [ gids van het klassen eindpunt ](./classes.md) voor details bij het werken met klassen in API.

## Veldgroepen

Veldgroepen zijn herbruikbare componenten die een of meer velden definiëren die een bepaald concept vertegenwoordigen, zoals een individuele persoon, een mailingadres of een webbrowseromgeving. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert, afhankelijk van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Zie de [ gids van het de gebiedsgroepen eindpunt ](./field-groups.md) leren hoe te met gebiedsgroepen in API te werken.

## Datatypen

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als referentietypen in klassen of veldgroepen. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Hoewel gelijkaardig aan gebiedsgroepen in zoverre zij voor het verenigbare gebruik van een multi-gebiedstructuur toestaan, zijn de gegevenstypes flexibeler omdat zij overal in de schemastructuur kunnen worden omvat terwijl de gebiedsgroepen slechts op het wortelniveau kunnen worden toegevoegd. Zie de [ gids van het gegevenstypeseindpunt ](./data-types.md) voor meer informatie bij het werken met gegevenstypes in API.

>[!NOTE]
>
>Als een veld is gedefinieerd als een specifiek gegevenstype, kunt u niet hetzelfde veld met een ander gegevenstype in een ander schema maken. Deze beperking geldt voor de huurder van uw organisatie.

## Beschrijvers

Descriptors zijn reeksen meta-gegevens die aan specifieke gebieden binnen een schema worden toegewezen, die diverse contextuele details verstrekken met inbegrip van hoe die gebieden (en het schema zelf) met andere schema&#39;s verwant zijn. Op elk schema kunnen een of meer descriptorentiteiten zijn toegepast en er zijn verschillende descriptortypen voor verschillende doeleinden. Zie de [ gids van het didentrekkereindpunt van beschrijvers ](./descriptors.md) voor meer informatie bij het werken met beschrijvers in API, en een overzicht van de verschillende beschrijvingstypes en hun gebruiksgevallen.

## Unies

Hoewel u met Experience Platform schema&#39;s kunt samenstellen voor bepaalde gebruiksgevallen, kunt u ook een &#39;samenvoeging&#39; van schema&#39;s samenstellen die tot een bepaalde klasse behoren. Een samenvoegingsschema voegt de gebieden van alle schema&#39;s samen die de zelfde klasse in één enkele vertegenwoordiging delen. Door een schema voor gebruik met [ in real time het Profiel van de Klant ](../../profile/home.md) toe te laten, wordt dat schema inbegrepen in de unie voor zijn bijzondere klasse. Als zodanig kunnen unieschema&#39;s niet rechtstreeks worden bewerkt en alleen worden beïnvloed door het opnemen of uitsluiten van schema&#39;s voor gebruik in profiel.

Leren hoe te om vakbonden in de Registratie API van het Schema te bekijken, zie de [ gids van het vakbondseindpunt ](./unions.md).

## CSV naar schemaomzetting {#csv-to-schema}

U kunt automatisch een XDM-schema genereren door een CSV-bestand als sjabloon te gebruiken, zodat u sjablonen kunt maken voor het bulksgewijs importeren van schemavelden en kunt knippen op handmatig API- of UI-werk.

Zie [ CSV aan de gids van het schemaomzettingseindpunt ](./export.md) voor meer informatie.

>[!NOTE]
>
>U kunt UI ook gebruiken om een CSV aan een schema in kaart te brengen gebruikend AI-Gegenereerde aanbevelingen [&#128279;](../../ingestion/tutorials/map-csv/recommendations.md) (momenteel in bèta).

## Exporteren {#export}

Met de API voor het schemaregister kunt u XDM-bronnen overbrengen en delen tussen sandboxen en organisaties. Voor om het even welk schema, gebiedsgroep, of gegevenstype, kunt u een de uitvoerlading produceren die de structuur van het middel en om het even welke afhankelijke middelen bevat. Deze nuttige lading kan dan worden gebruikt om het middel in een bestemmingszandbak en organisatie in te voeren.

Zie de [ gids van het uitvoereindpunt ](./export.md) voor meer informatie over hoe te om een de uitvoerlading voor een bestaand middel tot stand te brengen XDM.

## Importeren

Als u de [ uitvoer ](#export) of [ CSV aan schemaconversie ](./import.md) eindpunten gebruikt om een de uitvoerlading tot stand te brengen, kunt u die nuttige lading naar een doelorganisatie en zandbak verzenden om de gespecificeerde middelen in te voeren.

Zie de [ invoereindpuntgids ](./export.md) voor meer informatie over hoe te om middelen XDM van de uitvoerladingen te produceren.

## Voorbeeldgegevens

U kunt voorbeeldgegevens genereren voor elk opgegeven schema in de Schemabibliotheek. Het geretourneerde reactieobject kan vervolgens worden gebruikt als bron voor gegevensinvoer.

Zie de [ gids van het de eindpunt van steekproefgegevens ](./sample-data.md) voor meer informatie over het gebruik van dit eindpunt.

## Controlelogboek

De Registratie van het Schema handhaaft een logboek van alle veranderingen die aan een middel (klasse, gebiedsgroep, gegevenstype, of schema) tussen verschillende updates zijn voorgekomen. U kunt het logboek voor een bepaalde bron terugwinnen door zijn `$id` of `meta:altId` in de weg van een verzoek van GET aan dit eindpunt te verstrekken.

Zie de [ gids van het de eindpuntgids van het controlelogboek ](./audit-log.md) voor meer informatie over het gebruik van dit eindpunt.

## Volgende stappen

Begin makend vraag gebruikend de Registratie API van het Schema, lees [ begonnen gids ](./getting-started.md) dan één van de eindpuntgidsen om te leren hoe te om specifieke eindpunten te gebruiken.
