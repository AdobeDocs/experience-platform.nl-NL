---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;enum;mixin;Field groep;Field groepen;mixins;data type;Data types;Gegevenstype;primaire identiteit;primaire identiteit;XDM individueel profiel;XDM gebieden;enum datatype;Experience gebeurtenis;XDM Experience Event;XDM ExperienceEvent;ExperienceEvent;ExperienceEvent;XDM ExperienceEvent;schema ontwerp;class;Class;Klassen;datatype;Datatype;gegevenstype;Gegevenstype;schema's;Schema's;Identiteitskaart;Identiteitskaart;Schemaontwerp;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: Basisbeginselen van de schemacompositie
description: Leer over de schema's van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema's in Adobe Experience Platform.
exl-id: d449eb01-bc60-4f5e-8d6f-ab4617878f7e
source-git-commit: 5b59d491834854829a89a240ccd612367cf558d4
workflow-type: tm+mt
source-wordcount: '4291'
ht-degree: 0%

---

# Basisbeginselen van de schemacompositie

Leer over de schema&#39;s van de Gegevens van de Ervaring van het Model (XDM) en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s in Adobe Experience Platform. Voor algemene informatie over XDM en hoe het binnen Experience Platform wordt gebruikt, zie het [&#x200B; overzicht van het Systeem XDM &#x200B;](../home.md).

## Schema&#39;s begrijpen {#understanding-schemas}

Een schema is een set regels die de structuur en indeling van gegevens vertegenwoordigen en valideren. Op een hoog niveau, verstrekken de schema&#39;s een abstracte definitie van een real-world voorwerp (zoals een persoon) en schetsen welke gegevens in elke instantie van dat voorwerp (zoals voornaam, achternaam, verjaardag, etc.) zouden moeten worden omvat.

Naast het beschrijven van de structuur van gegevens, passen de schema&#39;s beperkingen en verwachtingen op gegevens toe zodat het kan worden bevestigd aangezien het zich tussen systemen beweegt. Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen.

Experience Platform handhaaft deze semantische normalisatie door schema&#39;s te gebruiken. Schema&#39;s zijn de standaardmanier om gegevens in Experience Platform te beschrijven, zodat alle gegevens die aan schema&#39;s voldoen, opnieuw kunnen worden gebruikt in een organisatie zonder conflicten, of zelfs kunnen worden gedeeld tussen meerdere organisaties.

XDM-schema&#39;s zijn ideaal voor het opslaan van grote hoeveelheden complexe gegevens in een op zichzelf staand formaat. Zie de secties op [&#x200B; ingebedde voorwerpen &#x200B;](#embedded) en [&#x200B; grote gegevens &#x200B;](#big-data) in het bijlage aan dit document voor meer informatie over hoe XDM dit verwezenlijkt.

### Workflows op basis van schema&#39;s in Experience Platform {#schema-based-workflows}

Standaardisering is een sleutelbegrip van Experience Platform. XDM, aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en standaardschema&#39;s voor het beheer van de klantenervaring te bepalen.

De infrastructuur waarop Experience Platform is gebouwd, ook wel [!DNL XDM System] genoemd, vereenvoudigt workflows op basis van schema&#39;s en omvat de [!DNL Schema Registry] , [!DNL Schema Editor] , schema-metagegevens en het serviceconsumptiepatroon. Zie het [&#x200B; XDM overzicht van het Systeem &#x200B;](../home.md) voor meer informatie.

Er zijn verschillende belangrijke voordelen verbonden aan het gebruik van schema&#39;s in Experience Platform. In de eerste plaats zorgen schema&#39;s voor een beter gegevensbeheer en gegevensminimalisering, wat vooral belangrijk is bij privacyregels. Ten tweede, staan de bouwschema&#39;s met Adobe standaardcomponenten voor uit-van-de-doosinzichten en gebruik van de diensten van AI/ML met minimale aanpassingen toe. Ten slotte bieden schema&#39;s infrastructuren voor het uitwisselen van inzichten in gegevens en een efficiënte orchestratie.

## Uw schema plannen {#planning}

De eerste stap in het bouwen van een schema is het concept, of real-world voorwerp, te bepalen dat u binnen het schema probeert te vangen. Zodra u het concept identificeert dat u probeert te beschrijven, begin plannend uw schema door over dingen zoals het type van gegevens, potentiële identiteitsgebieden te denken, en hoe het schema in de toekomst kan evolueren.

### Gedrag van gegevens in Experience Platform {#data-behaviors}

Gegevens die bestemd zijn voor gebruik in Experience Platform worden gegroepeerd in twee gedragstypen:

* **gegevens van het Verslag**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **de reeksgegevens van de Tijd**: Verstrekt een momentopname van het systeem in de tijd dat een actie of direct of indirect door een verslagonderwerp werd genomen.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd.

Zowel bevatten de verslag als de tijdreeksenschema&#39;s een kaart van identiteiten (`xdm:identityMap`). Dit veld bevat de identiteitsrepresentatie van een onderwerp, getekend vanuit velden die zijn gemarkeerd als Identiteit zoals beschreven in de volgende sectie.

### [!UICONTROL Identity] {#identity}

>[!CONTEXTUALHELP]
>id="platform_schemas_identities"
>title="Identiteiten in schema&#39;s"
>abstract="Identiteiten zijn sleutelvelden in een schema die kunnen worden gebruikt om een onderwerp te identificeren, zoals een e-mailadres of een marketing-id. Deze gebieden worden gebruikt om de identiteitsgrafiek voor elk individu te construeren en klantenprofielen te bouwen. Zie de documentatie voor meer informatie over identiteiten in schema&#39;s."

Schema&#39;s definiëren de structuur van gegevens die in Experience Platform worden ingevoerd. Die gegevens machtigen veelvoudige diensten binnen het Platform, en helpen om één enkele, verenigde mening van elk individu tot stand te brengen. Zo wanneer het ontwerpen van schema&#39;s, denk zorgvuldig over welke gebieden om als identiteit-deze controle te merken hoe de profielen over datasets worden vastgemaakt.

Om dit proces te helpen, kunnen de belangrijkste gebieden binnen uw schema&#39;s als identiteiten worden gemerkt. Op gegevensopname, worden de gegevens in die gebieden opgenomen in &quot;[!UICONTROL Identity Graph]&quot;voor dat individu. De grafiekgegevens kunnen vervolgens worden benaderd door [[!DNL Real-Time Customer Profile]](../../profile/home.md) en andere Experience Platform-services om een samengevoegde weergave van elke afzonderlijke klant te bieden.

Velden die algemeen als &quot;[!UICONTROL Identity]&quot;worden gemerkt omvatten: e-mailadres, telefoonaantal, [[!DNL Experience Cloud ID (ECID)] &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/home.html), identiteitskaart van CRM, of andere unieke gebieden van identiteitskaart Overweeg om het even welke unieke herkenningstekens specifiek voor uw organisatie, aangezien zij ook goede &quot;[!UICONTROL Identity]&quot;gebieden kunnen zijn.

Meer over leren hoe de identiteitsinformatie u kan helpen digitale ervaringen aan uw klanten leveren, zie het [&#x200B; overzicht van de Dienst van de Identiteit &#x200B;](../../identity-service/home.md). Zie het gegevens modellerend beste praktijkdocument voor [&#x200B; uiteinden op het gebruik van identiteiten wanneer het creëren van een schema &#x200B;](./best-practices.md#data-validation-fields).

Er zijn twee manieren om identiteitsgegevens naar Experience Platform te verzenden:

1. Toevoegend identiteitsbeschrijvers aan individuele gebieden, of door [&#x200B; de Redacteur UI van het Schema &#x200B;](../ui/fields/identity.md) of het gebruiken van de [&#x200B; Registratie API van het Schema &#x200B;](../api/descriptors.md#create)
2. Een [`identityMap` veld &#x200B;](#identityMap) gebruiken

#### `identityMap` {#identityMap}

`identityMap` is een map-type gebied dat de diverse identiteitswaarden voor een individu, samen met hun bijbehorende namespaces beschrijft. Dit gebied kan worden gebruikt om identiteitsinformatie voor uw schema&#39;s te verstrekken, in plaats van het bepalen van identiteitswaarden binnen de structuur van het schema zelf.

Het belangrijkste nadeel van het gebruik van `identityMap` is dat identiteitswaarden genest zijn en moeilijker te werken met hulpmiddelen die identiteitsgebieden op het hoogste niveau, zoals de Bouwer van het Segment of sommige derdesintegraties verwachten.

>[!NOTE]
>
>Een schema dat `identityMap` gebruikt kan als bronschema in een verhouding worden gebruikt, maar kan niet als verwijzingsschema worden gebruikt. Dit komt omdat alle verwijzingsschema&#39;s een zichtbare identiteit moeten hebben die op een verwijzingsgebied binnen het bronschema kan worden in kaart gebracht. Verwijs naar de gids UI op [&#x200B; verhoudingen &#x200B;](../tutorials/relationship-ui.md) voor meer informatie over de vereisten van bron en verwijzingsschema&#39;s.

Identiteitskaarten kunnen echter nuttig zijn als er een variabel aantal identiteiten voor een schema is of als u gegevens opneemt uit bronnen die identiteiten samen opslaan (zoals [!DNL Airship] of Adobe Audience Manager). Bovendien worden de identiteitskaarten vereist als u [&#x200B; Experience Platform Mobile SDK &#x200B;](https://developer.adobe.com/client-sdks/home/) gebruikt.

Een voorbeeld van een eenvoudige identiteitskaart zou als het volgende kijken:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": true
    }
  ],
  "ECID": [
    {
      "id": "87098882279810196101440938110216748923",
      "primary": false
    },
    {
      "id": "55019962992006103186215643814973128178",
      "primary": false
    }
  ],
  "CRMID": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": false
    }
  ]
}
```

Zoals in het bovenstaande voorbeeld wordt getoond, vertegenwoordigt elke sleutel in het `identityMap` -object een naamruimte voor de identiteit. De waarde voor elke sleutel is een serie van voorwerpen, die de identiteitswaarden (`id`) voor respectieve namespace vertegenwoordigen. Verwijs naar de [!DNL Identity Service] documentatie voor a [&#x200B; lijst van standaard identiteitsnamespaces &#x200B;](../../identity-service/troubleshooting-guide.md#standard-namespaces) die door de toepassingen van Adobe wordt erkend.

>[!NOTE]
>
>Een booleaanse waarde voor het feit of de waarde een primaire identiteit (`primary`) is, kan ook worden opgegeven voor elke identiteitswaarde. U hoeft alleen primaire identiteiten in te stellen voor schema&#39;s die bedoeld zijn voor gebruik in [!DNL Real-Time Customer Profile] .

### Beginselen voor de ontwikkeling van schema&#39;s {#evolution}

Naarmate de aard van de digitale ervaringen zich blijft ontwikkelen, moeten de schema&#39;s die gebruikt worden om ze te vertegenwoordigen ook worden gebruikt. Een goed ontworpen schema kan daarom aanpassen en evolueren zoals nodig, zonder destructieve veranderingen in vorige versies van het schema te veroorzaken.

Aangezien het handhaven van achterwaartse verenigbaarheid essentieel voor schemaevolutie is, handhaaft Experience Platform een zuiver additief versieringsbeginsel. Dit beginsel zorgt ervoor dat om het even welke revisies aan het schema slechts in niet-destructieve updates en veranderingen resulteren. Met andere woorden, **wordt het breken veranderingen niet gesteund.**

>[!NOTE]
>
>U kunt een het breken verandering in een schema slechts introduceren als het nog niet is gebruikt om gegevens in Experience Platform in te voeren en niet voor gebruik in het Profiel van de Klant in real time is toegelaten. Nochtans, zodra het schema in Experience Platform is gebruikt, moet het aan het additieve versieringsbeleid houden.

In de volgende tabel wordt aangegeven welke wijzigingen worden ondersteund bij het bewerken van schema&#39;s, veldgroepen en gegevenstypen:

| Ondersteunde wijzigingen | Wijzigingen doorlopen (niet ondersteund) |
| --- | --- |
| <ul><li>Nieuwe velden toevoegen aan de bron</li><li>Een vereist veld optioneel maken</li><li>Nieuwe vereiste velden maken*</li><li>De weergavenaam en beschrijving van de bron wijzigen</li><li>Het schema toestaan om aan Profiel deel te nemen</li></ul> | <ul><li>Eerder gedefinieerde velden verwijderen</li><li>Bestaande velden hernoemen of opnieuw definiëren</li><li>Eerder ondersteunde veldwaarden verwijderen of beperken</li><li>Bestaande velden verplaatsen naar een andere locatie in de structuur</li><li>Het schema verwijderen</li><li>Het schema uitschakelen om deel te nemen aan profiel</li><li>Het primaire identiteitsveld wijzigen in een schema dat is ingeschakeld voor Profiel en waarin gegevens zijn opgenomen</li></ul> |

\* *verwijs naar de sectie hieronder voor belangrijke overwegingen betreffende [&#x200B; het plaatsen van nieuwe vereiste gebieden &#x200B;](#post-ingestion-required-fields).*

### Vereiste velden

De individuele schemagebieden kunnen [&#x200B; zoals vereist &#x200B;](../ui/fields/required.md) worden gemerkt, zo betekent het dat om het even welke ingebedde verslagen gegevens op die gebieden moeten bevatten om bevestiging over te gaan. Bijvoorbeeld, kan het plaatsen van het primaire identiteitsgebied van een schema zoals vereist helpen ervoor zorgen dat alle ingebedde verslagen aan het Profiel van de Klant in real time zullen deelnemen. Op dezelfde manier zorgt het plaatsen van een timestamp gebied zoals vereist ervoor dat alle tijd-reeksgebeurtenissen chronologisch worden bewaard.

>[!IMPORTANT]
>
>Ongeacht of een schemaveld verplicht is of niet, accepteert Experience Platform geen `null` of lege waarden voor een veld dat wordt ingevoerd. Als er geen waarde is voor een bepaald veld in een record of gebeurtenis, moet de sleutel voor dat veld worden uitgesloten van de inlaatlading.

#### Velden instellen zoals vereist na invoegen {#post-ingestion-required-fields}

Als een veld is gebruikt om gegevens in te voeren en oorspronkelijk niet is ingesteld als vereist, heeft dat veld mogelijk een null-waarde voor sommige records. Als u dit veld na invoer als vereist instelt, moeten alle toekomstige records een waarde voor dit veld bevatten, ook al kunnen historische records null zijn.

Houd rekening met het volgende wanneer u een eerder optioneel veld naar wens instelt:

1. Als u historische gegevens controleert en de resultaten in een nieuwe dataset schrijft, zullen sommige rijen ontbreken omdat zij ongeldige waarden voor het vereiste gebied bevatten.
1. Als het veld deelneemt aan het realtime-klantprofiel en u gegevens exporteert voordat u het naar wens instelt, is het mogelijk null voor bepaalde profielen.
1. U kunt de API voor schemaregistratie gebruiken om een tijdstempelwijziging voor alle XDM-bronnen in Experience Platform weer te geven, inclusief nieuwe vereiste velden. Zie de gids op het [&#x200B; eindpunt van het controlelogboek &#x200B;](../api/audit-log.md) voor meer informatie.

### Schema&#39;s en gegevensinvoer

Om gegevens in Experience Platform in te voeren, moet eerst een dataset worden gecreeerd. Datasets zijn de bouwstenen voor gegevenstransformatie en -tracking voor [[!DNL Catalog Service]](../../catalog/home.md) en vertegenwoordigen over het algemeen tabellen of bestanden die ingesloten gegevens bevatten. Alle datasets zijn gebaseerd op bestaande schema&#39;s XDM, die beperkingen voor wat verstrekken de ingebedde gegevens zouden moeten bevatten en hoe het zou moeten worden gestructureerd. Zie het overzicht op [&#x200B; Ingestie van Gegevens van Experience Platform &#x200B;](../../ingestion/home.md) voor meer informatie.

## Bouwstenen van een schema {#schema-building-blocks}

Experience Platform gebruikt een compositiebenadering waarin de standaard bouwstenen worden gecombineerd om schema&#39;s tot stand te brengen. Deze benadering bevordert de herbruikbaarheid van bestaande componenten en drijft normalisatie over de industrie om verkopersschema&#39;s en componenten in Experience Platform te steunen.

De schema&#39;s worden samengesteld gebruikend de volgende formule:

**Klasse + de Groef&amp;amp van het Gebied van het Schema;ast; = XDM Schema**

&ast;Een schema bestaat uit een klasse en nul of meer groepen schemavelden. Dit betekent dat u een datasetschema kon samenstellen zonder gebiedsgroepen bij allen te gebruiken.

### Klasse {#class}

>[!CONTEXTUALHELP]
>id="platform_schemas_class"
>title="Klasse"
>abstract="Elk schema is gebaseerd op één klasse. De klasse definieert het gedrag van het schema en de algemene eigenschappen die alle schema&#39;s die op die klasse zijn gebaseerd, moeten bevatten. Zie de documentatie om meer over te leren hoe de klassen in schemacompositie betrokken zijn."

>[!CONTEXTUALHELP]
>id="platform_schemas_class_industries"
>title="Industrietype"
>abstract="Als u een relevante industrie voor uw zaken selecteert, kan het machine het leren model betere gegevensorganisatie verstrekken door de brongebieden met standaardgebiedsgroepen nauwkeuriger in kaart te brengen die zich aan industriestandaarden richten. Dit zorgt ervoor dat de gegevensintegratie is afgestemd op uw specifieke behoeften in de branche en resulteert in nauwkeurigere en relevante gegevensinzichten."

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens die het schema (verslag of tijdreeks) zal bevatten. Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

De klasse van een schema bepaalt welke gebiedsgroepen voor gebruik in dat schema in aanmerking komen.

Adobe biedt verschillende standaard XDM-klassen (&quot;core&quot;). Twee van deze klassen, [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent] , zijn vereist voor bijna alle Experience Platform-processen stroomafwaarts. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven. Aangepaste klassen worden gedefinieerd door een organisatie wanneer er geen door Adobe gedefinieerde kernklassen beschikbaar zijn om een uniek geval van gebruik te beschrijven.

In de volgende schermafbeelding ziet u hoe klassen worden weergegeven in de gebruikersinterface van Experience Platform. Aangezien het getoonde voorbeeldschema geen gebiedsgroepen bevat, worden alle getoonde gebieden verstrekt door de klasse van het schema ([!UICONTROL XDM Individual Profile]).

![&#x200B; [!UICONTROL XDM Individual Profile] binnen de Redacteur van het Schema.](../images/schema-composition/class.png)

Voor de meest bijgewerkte lijst van beschikbare standaardXDM klassen, verwijs naar de [&#x200B; officiële bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/tree/master/components/classes). Alternatief, kunt u naar de gids verwijzen bij [&#x200B; het onderzoeken van componenten XDM &#x200B;](../ui/explore.md) als u verkiest om middelen in UI te bekijken.

### Veldgroepen {#field-group}

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup"
>title="Veldgroepen"
>abstract="Veldgroepen zijn herbruikbare componenten waarmee u schema&#39;s met extra kenmerken kunt uitbreiden. De meeste veldgroepen zijn alleen compatibel met bepaalde klassen. U kunt standaardveldgroepen gebruiken die door Adobe zijn gedefinieerd, of u kunt handmatig uw eigen aangepaste veldgroepen definiëren. Zie de documentatie om meer over te leren hoe de gebiedsgroepen in schemacompositie betrokken zijn."

>[!CONTEXTUALHELP]
>id="platform_schemas_fieldgroup_requiredFieldgroup"
>title="Vereiste veldgroep"
>abstract="Deze veldgroep wordt vereist door de bron die u gebruikt. Om deze reden, kunt u niet het van uw schema schrappen."

Een veldgroep is een herbruikbare component die een of meer velden definieert die bepaalde functies implementeren, zoals persoonlijke gegevens, hotelvoorkeuren of adres. Veldgroepen moeten worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Veldgroepen definiëren met welke klasse of klassen ze compatibel zijn, op basis van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Dit betekent dat niet alle veldgroepen beschikbaar zijn voor gebruik met alle klassen.

Experience Platform bevat veel standaard Adobe-veldgroepen en biedt leveranciers ook de mogelijkheid om veldgroepen voor hun gebruikers te definiëren, en afzonderlijke gebruikers om veldgroepen voor hun eigen specifieke concepten te definiëren.

Bijvoorbeeld, om details zoals &quot;[!UICONTROL First Name]&quot;en &quot;[!UICONTROL Home Address]&quot;voor uw &quot;[!UICONTROL Loyalty Members]&quot;schema te vangen, zou u standaardgebiedsgroepen kunnen gebruiken die die gemeenschappelijke concepten bepalen. Nochtans, concepten die specifieker voor uw organisatie (zoals de details van het douaneloyaliteitsprogramma of productattributen) zijn die niet door standaardgebiedsgroepen kunnen worden behandeld. In dit geval moet u uw eigen veldgroep definiëren om deze gegevens vast te leggen.

>[!NOTE]
>
>U wordt ten zeerste aangeraden om waar mogelijk standaardveldgroepen in uw schema&#39;s te gebruiken, aangezien deze velden impliciet worden begrepen door Experience Platform-services en een grotere consistentie bieden bij gebruik in Experience Platform-componenten.
>
>Velden die worden geleverd door standaardcomponenten (zoals &quot;Voornaam&quot; en &quot;E-mailadres&quot;), bevatten aanvullende aantekeningen die verdergaan dan de elementaire scalaire veldtypen. Ze vertellen Experience Platform dat velden die hetzelfde gegevenstype delen, zich op dezelfde manier gedragen. Dit gedrag kan worden vertrouwd om verenigbaar te zijn ongeacht waar de gegevens uit komen, of waarin de dienst van Experience Platform de gegevens wordt gebruikt.

Herinner dat de schema&#39;s uit &quot;nul of meer&quot;gebiedsgroepen worden samengesteld, zodat betekent dit dat u een geldig schema kon samenstellen zonder enige gebiedsgroepen bij allen te gebruiken.

In de volgende schermafbeelding ziet u hoe veldgroepen worden weergegeven in de gebruikersinterface van Experience Platform. Één enkele gebiedsgroep ([!UICONTROL Demographic Details]) wordt toegevoegd aan een schema in dit voorbeeld, dat een groepering van gebieden aan de structuur van het schema verstrekt.

![&#x200B; de Redacteur van het Schema met de [!UICONTROL Demographic Details] gebiedsgroep die in een voorbeeldschema wordt benadrukt.](../images/schema-composition/field-group.png)

Voor de meest bijgewerkte lijst van beschikbare standaard XDM gebiedsgroepen, verwijs naar de [&#x200B; officiële XDM bewaarplaats &#x200B;](https://github.com/adobe/xdm/tree/master/components/fieldgroups). Alternatief, kunt u naar de gids verwijzen bij [&#x200B; het onderzoeken van componenten XDM &#x200B;](../ui/explore.md) als u verkiest om middelen in UI te bekijken.

>[!NOTE]
>
> Standaard XDM gebiedsgroepen evolueren altijd en sommige gebiedsgroepen zijn afgekeurd. Voor de meest bijgewerkte lijst van afgekeurde gebiedsgroepen, verwijs naar de [&#x200B; afgekeurde sectie van gebiedsgroepen &#x200B;](https://github.com/adobe/xdm/tree/master/components/fieldgroups/deprecated) in de officiële bewaarplaats XDM.

### Gegevenstype {#data-type}

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als referentieveldtypen in klassen of schema&#39;s. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden op dezelfde manier kunnen definiëren als veldgroepen. Het belangrijkste verschil tussen hen, is dat de gegevenstypes overal in een schema kunnen worden omvat door het als &quot;gegevenstype&quot;van een gebied toe te voegen. Veldgroepen zijn alleen compatibel met bepaalde klassen, maar gegevenstypen kunnen in elke bovenliggende klasse of veldgroep worden opgenomen.

>[!NOTE]
>
>Als een veld is gedefinieerd als een specifiek gegevenstype, kunt u niet hetzelfde veld met een ander gegevenstype in een ander schema maken. Deze beperking geldt voor de huurder van uw organisatie.

Experience Platform biedt een aantal gangbare gegevenstypen als onderdeel van de [!DNL Schema Registry] voor ondersteuning van het gebruik van standaardpatronen voor het beschrijven van algemene gegevensstructuren. Dit wordt verklaard meer in detail in de [&#x200B; leerprogramma&#39;s van de Registratie van het Schema &#x200B;](../tutorials/create-schema-api.md) en zal duidelijker worden aangezien u door de stappen loopt om gegevenstypes te bepalen.

De volgende schermafbeelding laat zien hoe gegevenstypen worden weergegeven in de gebruikersinterface van Experience Platform. Een van de velden in de veldgroep [!UICONTROL Demographic Details] gebruikt het gegevenstype [!UICONTROL Object] , zoals wordt aangegeven door de tekst na het verticale streepje (`|` ) naast de naam van het veld. Dit specifieke gegevenstype biedt verschillende subvelden die betrekking hebben op de naam van een individuele persoon, een constructie die opnieuw kan worden gebruikt voor andere velden waarin de naam van een persoon moet worden vastgelegd.

![&#x200B; A diagram in de Redacteur van het Schema voor een individuele persoon met het Volledige benadrukte naamobject en de attributen.](../images/schema-composition/data-type.png)

Voor de meest bijgewerkte lijst van beschikbare standaard XDM gegevenstypes, verwijs naar de [&#x200B; officiële XDM bewaarplaats &#x200B;](https://github.com/adobe/xdm/tree/master/components/datatypes). Alternatief, kunt u naar de gids verwijzen bij [&#x200B; het onderzoeken van componenten XDM &#x200B;](../ui/explore.md) als u verkiest om middelen in UI te bekijken.

>[!NOTE]
>
> De standaard gegevenstypes XDM evolueren altijd en sommige gegevenstypes zijn afgekeurd. Voor de meest bijgewerkte lijst van afgekeurde gegevenstypes, verwijs naar de [&#x200B; afgekeurde sectie van gegevenstypes &#x200B;](https://github.com/adobe/xdm/tree/master/components/datatypes/deprecated) in de officiële bewaarplaats XDM.

### Veld {#field}

Een veld is de eenvoudigste bouwsteen van een schema. Velden bieden beperkingen met betrekking tot het type gegevens dat ze kunnen bevatten door een specifiek gegevenstype te definiëren. Deze basistypen definiëren één veld, terwijl u met de eerder vermelde gegevenstypen meerdere subvelden kunt definiëren en dezelfde structuur voor meerdere velden opnieuw kunt gebruiken in verschillende schema&#39;s. Naast het definiëren van het &quot;gegevenstype&quot; van een veld als een van de gegevenstypen die in het register zijn gedefinieerd, ondersteunt Experience Platform dus elementaire scalaire typen, zoals:

* String
* Geheel
* Dubbel
* Boolean
* Array
* Object

>[!TIP]
>
>Zie [&#x200B; bijlage &#x200B;](#objects-v-freeform) voor informatie over de voor- en nadelen van het gebruiken van vrije-vormgebieden over voorwerp-type gebieden.

De geldige waaiers van deze scalaire types kunnen verder tot bepaalde patronen, formaten, minimum/maximum, of vooraf bepaalde waarden worden beperkt. Gebruikend deze beperkingen, kan een brede waaier van specifiekere gebiedstypes worden vertegenwoordigd, die omvatten:

* Enum
* Lang
* Kort
* Byte
* Datum
* Datum/tijd
* Kaart

>[!NOTE]
>
>Het &quot;kaart&quot;gebiedstype staat voor sleutel-waarde paargegevens, met inbegrip van veelvoudige waarden voor één enkele sleutel toe. Kaarten vindt u in standaard XDM-klassen en -veldgroepen, maar u kunt ook aangepaste toewijzingen definiëren. Zie het API leerprogramma op [&#x200B; bepalend de gebieden van de douanekaart &#x200B;](../tutorials/custom-fields-api.md#custom-maps) of de gids op [&#x200B; bepalend kaartgebieden in UI &#x200B;](../ui/fields/map.md) voor meer informatie.

## Compositievoorbeeld {#composition-example}

De schema&#39;s worden gebouwd gebruikend een samenstellingsmodel en vertegenwoordigen het formaat en de structuur van gegevens die in Experience Platform moeten worden opgenomen. Zoals eerder vermeld, zijn deze schema&#39;s samengesteld uit een klasse en nul of meer gebiedsgroepen die met die klasse compatibel zijn.

Bijvoorbeeld, zou een schema beschrijvend aankopen die bij een detailhandel worden gemaakt &quot;[!UICONTROL Store Transactions]&quot;kunnen worden genoemd. Het schema implementeert de klasse [!DNL XDM ExperienceEvent] in combinatie met de standaard [!UICONTROL Commerce] veldgroep en een door de gebruiker gedefinieerde [!UICONTROL Product Info] veldgroep.

Een ander schema dat websiteverkeer volgt zou &quot;[!UICONTROL Web Visits]&quot;kunnen worden genoemd. De klasse [!DNL XDM ExperienceEvent] wordt ook geïmplementeerd, maar deze keer wordt de standaardveldgroep van [!UICONTROL Web] gecombineerd.

In het onderstaande diagram worden deze schema&#39;s en de velden weergegeven die door elke veldgroep worden bijgedragen. Het bevat ook twee schema&#39;s die op de [!DNL XDM Individual Profile] klasse worden gebaseerd, met inbegrip van het &quot;[!UICONTROL Loyalty Members]&quot;schema dat eerder in deze gids wordt vermeld.

![&#x200B; A stroomdiagram van vier schema&#39;s en de gebiedsgroepen die tot hen bijdragen.](../images/schema-composition/composition.png)

### Samenvoegen {#union}

Hoewel Experience Platform u toestaat om schema&#39;s voor bepaalde gebruiksgevallen samen te stellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s voor een specifiek klassentype te zien. In het vorige diagram worden twee schema&#39;s weergegeven op basis van de klasse XDM ExperienceEvent en twee schema&#39;s op basis van de klasse [!DNL XDM Individual Profile] . De samenvoeging, die hieronder wordt weergegeven, aggregeert de velden van alle schema&#39;s die dezelfde klasse delen ([!DNL XDM ExperienceEvent] respectievelijk [!DNL XDM Individual Profile] ).

![&#x200B; de stroomdiagram van het unieschema dat de gebieden portretteert die hen samenstellen.](../images/schema-composition/union.png)

Wanneer u een schema inschakelt voor gebruik met [!DNL Real-Time Customer Profile] , wordt dit opgenomen in de union voor dat klassetype. [!DNL Profile] biedt robuuste, gecentraliseerde profielen van klantkenmerken en een tijdstempelaccount voor elke gebeurtenis die de klant heeft gehad in een systeem dat is geïntegreerd met Experience Platform. [!DNL Profile] gebruikt de verenigingsmening om deze gegevens te vertegenwoordigen en een holistische mening van elke individuele klant te verstrekken.

Voor meer informatie bij het werken met [!DNL Profile], zie het [&#x200B; Real-Time overzicht van het Profiel van de Klant &#x200B;](../../profile/home.md).

## Gegevensbestanden toewijzen aan XDM-schema&#39;s {#mapping-datafiles}

Alle gegevensbestanden die in Experience Platform worden opgenomen, moeten de structuur van een XDM-schema hebben. Voor meer informatie over hoe te om gegevensbestanden te formatteren om aan hiërarchieën XDM (met inbegrip van steekproefdossiers) te voldoen, zie het document op [&#x200B; transformaties van steekproefETL &#x200B;](../../etl/transformations.md). Voor algemene informatie over het opnemen van gegevensbestanden in Experience Platform, zie het [&#x200B; overzicht van partijingestitie &#x200B;](../../ingestion/batch-ingestion/overview.md).

## Schema&#39;s voor extern publiek

Als u publiek van externe systemen naar Experience Platform brengt, moet u de volgende componenten gebruiken om hen in uw schema&#39;s te vangen:

* [[!UICONTROL Segment definition] class &#x200B;](../classes/segment-definition.md): Gebruik deze standaardklasse om zeer belangrijke attributen van een externe segmentdefinitie te vangen.
* [[!UICONTROL Segment Membership Details] veldgroep &#x200B;](../field-groups/profile/segmentation.md): voeg deze veldgroep toe aan uw [!UICONTROL XDM Individual Profile] -schema om klantprofielen aan specifieke doelgroepen te koppelen.

## Volgende stappen

Nu u de grondbeginselen van schemacompositie begrijpt, bent u bereid beginnen het onderzoeken van en het bouwen van schema&#39;s gebruikend [!DNL Schema Registry].

Raadpleeg de volgende documentatie voor informatie over de structuur van de twee belangrijkste XDM-klassen en hun veelgebruikte compatibele veldgroepen:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry] wordt gebruikt om [!DNL Schema Library] binnen Experience Platform te openen, en verstrekt een gebruikersinterface en RESTful API waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn. [!DNL Schema Library] bevat de middelen van de Industrie die door Adobe worden bepaald, de middelen van de Leverancier door de partners van Experience Platform worden bepaald, en klassen, gebiedsgroepen, gegevenstypes, en schema&#39;s die door leden van uw organisatie zijn samengesteld.

Beginnen samenstellend schema gebruikend UI, volg samen met het [&#x200B; leerprogramma van de Redacteur van het Schema &#x200B;](../tutorials/create-schema-ui.md) om het schema van de &quot;Leden van de Loyaliteit&quot;te bouwen dat door dit document wordt vermeld.

Beginnen gebruikend [!DNL Schema Registry] API, begin door de [&#x200B; gids van de ontwikkelaar van de Registratie API van het Schema te lezen &#x200B;](../api/getting-started.md). Na het lezen van de ontwikkelaarsgids, volg de stappen die in het leerprogramma worden geschetst op [&#x200B; creërend een schema gebruikend de Registratie API van het Schema &#x200B;](../tutorials/create-schema-api.md).

## Bijlage

De volgende secties bevatten extra informatie betreffende de beginselen van schemacompositie.

### Relatieve tabellen versus ingesloten objecten {#embedded}

Wanneer het werken met relationele gegevensbestanden, impliceren de beste praktijken het normaliseren van gegevens, of het nemen van een entiteit en het verdelen van het in discrete stukken die dan over veelvoudige lijsten worden getoond. Om de gegevens als geheel te lezen of de entiteit bij te werken, lees en schrijf verrichtingen over vele individuele lijsten moeten worden gemaakt gebruikend JOIN.

Door ingebedde voorwerpen te gebruiken, kunnen de schema&#39;s XDM complexe gegevens direct vertegenwoordigen en het opslaan in op zichzelf staande documenten met een hiërarchische structuur. Één van de belangrijkste voordelen aan deze structuur is dat het u toestaat om de gegevens te vragen zonder het moeten de entiteit door dure verbindingen aan veelvoudige gedenormaliseerde lijsten reconstrueren. Er zijn geen harde beperkingen aan hoeveel niveaus uw schemahiërarchie kan zijn.

### Schema&#39;s en grote gegevens {#big-data}

Moderne digitale systemen genereren enorme hoeveelheden gedragssignalen (transactiegegevens, weblogbestanden, internet van dingen, weergave, enzovoort). Deze grote gegevens bieden buitengewone mogelijkheden om ervaringen te optimaliseren, maar zijn lastig te gebruiken vanwege de schaal en de verscheidenheid van de gegevens. Om waarde te kunnen halen uit de gegevens, moeten de structuur, indeling en definities ervan worden gestandaardiseerd, zodat deze consistent en efficiënt kunnen worden verwerkt.

De schema&#39;s lossen dit probleem op door gegevens toe te laten om uit veelvoudige bronnen worden geïntegreerd, door gemeenschappelijke structuren en definities worden gestandaardiseerd, en over oplossingen worden gedeeld. Dit staat verdere processen en de diensten toe om het even welk type van vraag te beantwoorden die van de gegevens wordt gesteld. Het verschuift van de traditionele benadering naar gegevensmodellering, waarbij alle vragen die over de gegevens moeten worden gesteld van tevoren bekend zijn, en de gegevens worden gemodelleerd om aan die verwachtingen te voldoen.

### Objecten versus vrije-formuliervelden {#objects-v-freeform}

Bij het ontwerpen van uw schema&#39;s moet u rekening houden met een aantal belangrijke factoren wanneer u objecten kiest op vrije-formuliervelden:

| Objecten | Velden met vrije vorm |
| --- | --- |
| Meer nesten | Minder of geen nesten |
| Hiermee maakt u logische veldgroepen | Velden worden op ad-hoclocaties geplaatst |

{style="table-layout:auto"}

#### Objecten

Hieronder ziet u de voor- en nadelen van het gebruik van objecten op vrije-formuliervelden.

**Pros**:

* Objecten kunt u het beste gebruiken als u een logische groepering van bepaalde velden wilt maken.
* Objecten ordenen het schema op een meer gestructureerde manier.
* Objecten helpen indirect bij het maken van een goede menustructuur in de gebruikersinterface van Segment Builder. De gegroepeerde velden in het schema worden direct weerspiegeld in de mappenstructuur die is opgegeven in de gebruikersinterface van Segment Builder.

**Kons**:

* Velden worden meer genest.
* Wanneer het gebruiken van [&#x200B; de Dienst van de Vraag van Experience Platform &#x200B;](../../query-service/home.md), langere verwijzingskoorden moeten aan vraaggebieden worden verstrekt die in voorwerpen worden genesteld.

#### Velden met vrije vorm

De voor- en nadelen van het gebruik van vrije-formuliervelden op objecten worden hieronder weergegeven.

**Pros**:

* Vrije-vormgebieden worden gecreeerd direct onder het wortelvoorwerp van het schema (`_tenantId`), verhogend zicht.
* De koorden van de verwijzing voor vrije-vormgebieden zijn gewoonlijk korter wanneer het gebruiken van de Dienst van de Vraag.

**Kons**:

* De locatie van vrije-formuliervelden in het schema is ad hoc. Dit betekent dat deze velden in alfabetische volgorde worden weergegeven in de Schema-editor. Hierdoor kunnen schema&#39;s minder gestructureerd worden, en vergelijkbare vrije-vormgebieden kunnen uiteindelijk ver worden gescheiden afhankelijk van hun namen.
