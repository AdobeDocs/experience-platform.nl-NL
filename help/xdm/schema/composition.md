---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;enum;mixin;Mixin;Mixins;gegevenstype;gegevenstypen;Gegevenstypen;Gegevenstype;primaire identiteit;XDM individueel profiel;XDM velden;enum datatype;Experience gebeurtenis;XDM Experience Event;XDM ExperienceEvent;ExperienceEvent;ExperienceEvent;XDM ExperienceEvent;schema;design;klasse;Class klassen;Klassen;datatype;Datatype;gegevenstype;Gegevenstype;schema's;Schema's;Identiteitskaart;Identiteitskaart;Schemaontwerp;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: Basisbeginselen van de schemacompositie
topic: overview
description: Dit document verstrekt een inleiding aan de schema's van het Gegevensmodel van de Ervaring (XDM) en de bouwstenen, de beginselen, en beste praktijken voor het samenstellen van schema's die in Adobe Experience Platform moeten worden gebruikt.
translation-type: tm+mt
source-git-commit: ae2c5f9fa4e732fefe55a8536894844986aea1e2
workflow-type: tm+mt
source-wordcount: '3461'
ht-degree: 0%

---


# Basisbeginselen van de schemacompositie

Dit document verstrekt een inleiding aan [!DNL Experience Data Model] (XDM) schema&#39;s en de bouwstenen, de beginselen, en de beste praktijken voor het samenstellen van schema&#39;s die in Adobe Experience Platform moeten worden gebruikt. Voor algemene informatie over XDM en hoe het binnen [!DNL Platform] wordt gebruikt, zie [XDM System overview](../home.md).

## Schema&#39;s begrijpen

Een schema is een set regels die de structuur en indeling van gegevens vertegenwoordigen en valideren. Op een hoog niveau, verstrekken de schema&#39;s een abstracte definitie van een real-world voorwerp (zoals een persoon) en schetsen welke gegevens in elke instantie van dat voorwerp (zoals voornaam, achternaam, verjaardag, etc.) zouden moeten worden omvat.

Naast het beschrijven van de structuur van gegevens, passen de schema&#39;s beperkingen en verwachtingen op gegevens toe zodat het kan worden bevestigd aangezien het zich tussen systemen beweegt. Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen.

[!DNL Experience Platform] handhaaft deze semantische normalisatie door schema&#39;s te gebruiken. Schema&#39;s zijn de standaardmanier om gegevens te beschrijven in [!DNL Experience Platform], zodat alle gegevens die aan schema&#39;s voldoen opnieuw kunnen worden gebruikt in een organisatie zonder conflicten, of zelfs kunnen worden gedeeld tussen meerdere organisaties.

XDM-schema&#39;s zijn ideaal voor het opslaan van grote hoeveelheden complexe gegevens in een op zichzelf staand formaat. Zie de secties over [ingesloten objecten](#embedded) en [grote gegevens](#big-data) in de bijlage bij dit document voor meer informatie over hoe XDM dit verwezenlijkt.

### Workflows op basis van schema&#39;s in [!DNL Experience Platform]

Standaardisering is een essentieel concept achter [!DNL Experience Platform]. XDM, die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en standaardschema&#39;s voor het beheer van de klantenervaring te bepalen.

De infrastructuur waarop [!DNL Experience Platform] wordt gebouwd, die als [!DNL XDM System] wordt bekend, vergemakkelijkt op schema-gebaseerde werkschema&#39;s en omvat [!DNL Schema Registry], [!DNL Schema Editor], schemameta-gegevens, en de patronen van het de dienstconsumptie. Zie [XDM System overview](../home.md) voor meer informatie.

Er zijn verscheidene belangrijke voordelen aan de bouw en het gebruiken van schema&#39;s in [!DNL Experience Platform]. In de eerste plaats zorgen schema&#39;s voor een beter gegevensbeheer en gegevensminimalisering, wat vooral belangrijk is met privacyregels. Ten tweede, staat het bouwen van schema&#39;s met standaard componenten Adobe voor uit-van-de-doos inzichten en gebruik van de diensten AI/ML met minimale aanpassingen toe. Ten slotte bieden schema&#39;s infrastructuren voor het uitwisselen van inzichten in gegevens en een efficiënte orchestratie.

## Uw schema plannen

De eerste stap in het bouwen van een schema is het concept, of real-world voorwerp, te bepalen dat u binnen het schema probeert te vangen. Zodra u het concept identificeert u probeert te beschrijven, kunt u beginnen uw schema te plannen door over dingen zoals het type van gegevens, potentiële identiteitsgebieden, en te denken hoe het schema in de toekomst kan evolueren.

### Gedrag van gegevens in [!DNL Experience Platform]

Gegevens die bestemd zijn voor gebruik in [!DNL Experience Platform] worden gegroepeerd in twee gedragstypen:

* **Opnamegegevens**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **Gegevens** tijdreeks: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. XDM-klassen worden later in dit document nader beschreven.

Zowel bevatten de verslag als de tijdreeksschema&#39;s een kaart van identiteiten (`xdm:identityMap`). Dit veld bevat de identiteitsrepresentatie van een onderwerp, getekend vanuit velden die zijn gemarkeerd als Identiteit zoals beschreven in de volgende sectie.

### [!UICONTROL Identity] {#identity}

Schema&#39;s worden gebruikt voor het opnemen van gegevens in [!DNL Experience Platform]. Deze gegevens kunnen over de veelvoudige diensten worden gebruikt om één enkele, verenigde mening van een individuele entiteit tot stand te brengen. Daarom is het belangrijk wanneer het denken over schema&#39;s om over klantenidentiteiten te denken en welke gebieden kunnen worden gebruikt om een onderwerp te identificeren ongeacht waar de gegevens uit kunnen komen.

Om dit proces te helpen, kunnen de belangrijkste gebieden binnen uw schema&#39;s als identiteiten worden gemerkt. Bij gegevensinvoer worden de gegevens in die velden ingevoegd in &quot;[!UICONTROL Identity Graph]&quot; voor die persoon. De grafiekgegevens kunnen dan door [[!DNL Real-time Customer Profile]](../../profile/home.md) en andere [!DNL Experience Platform] diensten worden betreden om een genaast-samen mening van elke individuele klant te verstrekken.

Velden die algemeen als &quot;[!UICONTROL Identity]&quot;worden gemerkt omvatten: e-mailadres, telefoonnummer, [[!DNL Experience Cloud ID (ECID)]](https://experienceleague.adobe.com/docs/id-service/using/home.html), CRM-id of andere unieke id-velden. U zou ook om het even welke unieke herkenningstekens moeten overwegen specifiek voor uw organisatie, aangezien zij ook goede &quot;[!UICONTROL Identity]&quot;gebieden kunnen zijn.

Het is belangrijk om over klantenidentiteiten tijdens de schema planningsfase te denken helpen ervoor zorgen dat de gegevens worden samengebracht om het meest robuuste profiel mogelijk te bouwen. Zie het overzicht op [Adobe Experience Platform Identity Service](../../identity-service/home.md) voor meer informatie over hoe identiteitsgegevens u kunnen helpen uw klanten digitale ervaringen te bieden.

#### `xdm:identityMap` {#identityMap}

`xdm:identityMap` is een map-type gebied dat de diverse identiteitswaarden voor een individu, samen met hun bijbehorende namespaces beschrijft. Dit gebied kan worden gebruikt om identiteitsinformatie voor uw schema&#39;s te verstrekken, in plaats van het bepalen van identiteitswaarden binnen de structuur van het schema zelf.

Een voorbeeld van een eenvoudige identiteitskaart zou als het volgende kijken:

```json
"identityMap": {
  "email": [
    {
      "id": "jsmith@example.com",
      "primary": false
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
  "loyaltyId": [
    {
      "id": "2e33192000007456-0365c00000000000",
      "primary": true
    }
  ]
}
```

Zoals in het bovenstaande voorbeeld wordt getoond, vertegenwoordigt elke sleutel in het `identityMap`-object een naamruimte van de identiteit. De waarde voor elke sleutel is een array van objecten die de identiteitswaarden (`id`) voor de respectievelijke naamruimte vertegenwoordigt. Raadpleeg de [!DNL Identity Service] documentatie voor een [lijst met standaardnaamruimten](../../identity-service/troubleshooting-guide.md#standard-namespaces) die door Adobe-toepassingen worden herkend.

>[!NOTE]
>
>Een booleaanse waarde waarmee kan worden opgegeven of de waarde een primaire identiteit (`primary`) is, kan ook worden opgegeven voor elke identiteitswaarde. Primaire identiteiten hoeven alleen te worden vastgesteld voor schema&#39;s die bedoeld zijn om te worden gebruikt in [!DNL Real-time Customer Profile]. Zie de sectie over [union schema&#39;s](#union) voor meer informatie.

### Beginselen van de schemaevolutie {#evolution}

Naarmate de aard van de digitale ervaringen zich blijft ontwikkelen, moeten de schema&#39;s die gebruikt worden om ze te vertegenwoordigen ook worden gebruikt. Een goed ontworpen schema kan daarom aanpassen en evolueren zoals nodig, zonder destructieve veranderingen in vorige versies van het schema te veroorzaken.

Aangezien het handhaven van achterwaartse verenigbaarheid essentieel voor schemaevolutie is, [!DNL Experience Platform] handhaaft een zuiver additief versieringsbeginsel om ervoor te zorgen dat om het even welke herzieningen aan het schema slechts in niet-destructieve updates en veranderingen resulteren. Met andere woorden: **afbrekende wijzigingen worden niet ondersteund.**

| Ondersteunde wijzigingen | Wijzigingen doorlopen (niet ondersteund) |
|------------------------------------|---------------------------------|
| <ul><li>Nieuwe velden toevoegen aan een bestaand schema</li><li>Een verplicht veld optioneel maken</li></ul> | <ul><li>Eerder gedefinieerde velden verwijderen</li><li>Nieuwe verplichte velden invoegen</li><li>Bestaande velden hernoemen of opnieuw definiëren</li><li>Eerder ondersteunde veldwaarden verwijderen of beperken</li><li>Kenmerken verplaatsen naar een andere locatie in de structuur</li></ul> |

>[!NOTE]
>
>Als een schema nog niet is gebruikt om gegevens in [!DNL Experience Platform] op te nemen, kunt u een breekverandering in dat schema introduceren. Nochtans, zodra het schema in [!DNL Platform] is gebruikt, moet het aan het additieve versieringsbeleid houden.

### Schema&#39;s en gegevensinvoer

Om gegevens in [!DNL Experience Platform] in te voeren, moet eerst een dataset worden gecreeerd. Datasets zijn de bouwstenen voor gegevenstransformatie en -tracking voor [[!DNL Catalog Service]](../../catalog/home.md) en vertegenwoordigen over het algemeen tabellen of bestanden die ingesloten gegevens bevatten. Alle datasets zijn gebaseerd op bestaande schema&#39;s XDM, die beperkingen voor wat verstrekken de ingebedde gegevens zouden moeten bevatten en hoe het zou moeten worden gestructureerd. Zie het overzicht op [Adobe Experience Platform Data Ingestie](../../ingestion/home.md) voor meer informatie.

## Bouwstenen van een schema

[!DNL Experience Platform] gebruikt een compositiebenadering waarin de standaard bouwstenen worden gecombineerd om schema&#39;s tot stand te brengen. Deze benadering bevordert de herbruikbaarheid van bestaande componenten en drijft standaardisatie over de industrie om verkopersschema&#39;s en componenten in [!DNL Platform] te steunen.

De schema&#39;s worden samengesteld gebruikend de volgende formule:

**Klasse + mixin&amp;ast; = XDM-schema**

&amp;ast;Een schema bestaat uit een klasse en nul of meer mixins. Dit betekent dat u een datasetschema kon samenstellen zonder mixins bij allen te gebruiken.

### Klasse {#class}

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

De klasse van een schema bepaalt welke mengen voor gebruik in dat schema in aanmerking komen. Dit wordt meer gedetailleerd besproken in [volgende sectie](#mixin).

Adobe biedt verschillende standaard XDM-klassen (&quot;core&quot;). Twee van deze klassen, [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent], zijn vereist voor bijna alle stroomafwaartse processen van het Platform. Naast deze kernklassen kunt u ook uw eigen aangepaste klassen maken om specifieke gebruiksgevallen voor uw organisatie te beschrijven. Aangepaste klassen worden gedefinieerd door een organisatie wanneer er geen door Adobe gedefinieerde kernklassen beschikbaar zijn om een uniek gebruiksgeval te beschrijven.

De volgende schermafbeelding toont hoe klassen worden weergegeven in de gebruikersinterface van het Platform. Aangezien het getoonde voorbeeldschema geen mengen bevat, worden alle getoonde gebieden verstrekt door de klasse van het schema ([!UICONTROL XDM Individual Profile]).

![](../images/schema-composition/class.png)

Raadpleeg de [officiële XDM-opslagruimte](https://github.com/adobe/xdm/tree/master/components/classes) voor de meest actuele lijst met beschikbare standaard XDM-klassen. Alternatief, kunt u naar de gids op [het onderzoeken van componenten XDM](../ui/explore.md) verwijzen als u verkiest om middelen in UI te bekijken.

### Mengsel {#mixin}

Een mix is een herbruikbare component die een of meer velden definieert die bepaalde functies implementeren, zoals persoonlijke gegevens, hotelvoorkeuren of adres. Mixins zijn bedoeld om te worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Mixins definiëren met welke klasse(n) ze compatibel zijn op basis van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Dit betekent dat niet alle mengsels beschikbaar zijn voor gebruik met alle klassen.

[!DNL Experience Platform] omvat vele standaard Adobe mixins terwijl ook het toestaan van verkopers om mengsels voor hun gebruikers te bepalen, en individuele gebruikers om mengsels voor hun eigen specifieke concepten te bepalen.

Bijvoorbeeld, om details zoals &quot;[!UICONTROL First Name]&quot;en &quot;[!UICONTROL Home Address]&quot;voor uw &quot;[!UICONTROL Loyalty Members]&quot;schema te vangen, zou u standaardmengen kunnen gebruiken die die gemeenschappelijke concepten bepalen. Nochtans, hebben de concepten die voor minder vaak gebruiksgevallen specifiek zijn (zoals &quot;[!UICONTROL Loyalty Program Level]&quot;) vaak geen vooraf bepaalde mengeling. In dit geval moet u uw eigen mix definiëren om deze informatie vast te leggen.

Herinner dat de schema&#39;s uit &quot;nul of meer&quot;mengen bestaan, zodat betekent dit dat u een geldig schema kon samenstellen zonder enige mengen bij allen te gebruiken.

Het volgende schermafbeelding toont hoe mixins worden weergegeven in de gebruikersinterface van het Platform. In dit voorbeeld wordt één enkele mix ([!UICONTROL Demographic Details]) toegevoegd aan een schema, dat een groepering van gebieden aan de structuur van het schema verstrekt.

![](../images/schema-composition/mixin.png)

Raadpleeg de [officiële XDM-opslagruimte](https://github.com/adobe/xdm/tree/master/components/mixins) voor de meest actuele lijst met beschikbare standaard XDM-mixen. Alternatief, kunt u naar de gids op [het onderzoeken van componenten XDM](../ui/explore.md) verwijzen als u verkiest om middelen in UI te bekijken.

### Gegevenstype {#data-type}

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als referentieveldtypen in klassen of schema&#39;s. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Vergelijkbaar met een mixin, staat een gegevenstype voor het verenigbare gebruik van een multi-gebiedstructuur toe, maar heeft meer flexibiliteit dan een mixin omdat een gegevenstype overal in een schema kan worden omvat door het als &quot;gegevenstype&quot;van een gebied toe te voegen.

[!DNL Experience Platform] bevat een aantal gangbare gegevenstypen als onderdeel van het programma  [!DNL Schema Registry] ter ondersteuning van het gebruik van standaardpatronen voor het beschrijven van gemeenschappelijke gegevensstructuren. Dit wordt meer gedetailleerd uitgelegd in de [!DNL Schema Registry] zelfstudies, waar het duidelijker wordt wanneer u door de stappen gaat om gegevenstypen te definiëren.

De volgende schermafbeelding toont hoe gegevenstypen worden weergegeven in de gebruikersinterface van het Platform. Een van de velden die wordt verschaft door de [!UICONTROL Demographic Details]-mix gebruikt het gegevenstype &quot;[!UICONTROL Person name]&quot;, zoals wordt aangegeven door de tekst na het pipe-teken (`|`) naast de naam van het veld. Dit specifieke gegevenstype biedt verschillende subvelden die betrekking hebben op de naam van een individuele persoon, een constructie die opnieuw kan worden gebruikt voor andere velden waarin de naam van een persoon moet worden vastgelegd.

![](../images/schema-composition/data-type.png)

Raadpleeg de [officiële XDM-opslagruimte](https://github.com/adobe/xdm/tree/master/components/datatypes) voor de meest actuele lijst met beschikbare standaard XDM-gegevenstypen. Alternatief, kunt u naar de gids op [het onderzoeken van componenten XDM](../ui/explore.md) verwijzen als u verkiest om middelen in UI te bekijken.

### Veld

Een veld is de eenvoudigste bouwsteen van een schema. Velden bieden beperkingen met betrekking tot het type gegevens dat ze kunnen bevatten door een specifiek gegevenstype te definiëren. Deze basisgegevenstypen definiëren één veld, terwijl u met de eerder genoemde [gegevenstypen](#data-type) meerdere subvelden kunt definiëren en dezelfde structuur voor meerdere velden kunt gebruiken in verschillende schema&#39;s. Naast het definiëren van het &quot;gegevenstype&quot; van een veld als een van de gegevenstypen die in het register zijn gedefinieerd, ondersteunt [!DNL Experience Platform] basistypen van scalaire aard, zoals:

* Tekenreeks
* Geheel
* Dubbel
* Boolean
* Array
* Object

>[!TIP]
>
>Zie [appendix](#objects-v-freeform) voor informatie over de voor- en nadelen van het gebruik van vrije-formuliervelden boven objecttypevelden.

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
>Het &quot;kaart&quot;gebiedstype staat voor sleutel-waarde paargegevens, met inbegrip van veelvoudige waarden voor één enkele sleutel toe. Kaarten kunnen alleen op systeemniveau worden gedefinieerd. Dit betekent dat u een kaart in een door de industrie of leverancier gedefinieerd schema tegenkomt, maar dat deze kaart niet beschikbaar is voor gebruik in velden die u definieert. De [Handleiding voor ontwikkelaars van de API voor schemaregistratie](../api/getting-started.md) bevat meer informatie over het definiëren van veldtypen.

Sommige gegevensverrichtingen die door stroomafwaartse diensten en toepassingen worden gebruikt dwingen beperkingen op specifieke gebiedstypes af. De betrokken diensten omvatten, maar zijn niet beperkt tot:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Alvorens een schema voor gebruik in de stroomafwaartse diensten te creëren, te herzien gelieve de aangewezen documentatie voor die diensten om de gebiedsvereisten en de beperkingen voor de gegevensverrichtingen beter te begrijpen het schema voor bedoeld is.

### XDM-velden

Naast basisvelden en de mogelijkheid om uw eigen gegevenstypen te definiëren, biedt XDM een standaardset velden en gegevenstypen die impliciet worden begrepen door [!DNL Experience Platform]-services en die zorgen voor grotere consistentie bij gebruik in [!DNL Platform]-componenten.

Deze velden, zoals &quot;Voornaam&quot; en &quot;E-mailadres&quot;, bevatten extra aantekeningen die verder gaan dan de elementaire scalaire veldtypen en die [!DNL Platform] aangeven dat velden die hetzelfde XDM-gegevenstype delen, zich op dezelfde manier gedragen. Dit gedrag kan worden vertrouwd om verenigbaar te zijn ongeacht waar de gegevens uit komen, of waarin [!DNL Platform] dienst de gegevens wordt gebruikt.

Zie [XDM gebiedwoordenboek](field-dictionary.md) voor een volledige lijst van beschikbare gebieden XDM. Aanbevolen wordt om XDM-velden en gegevenstypen waar mogelijk te gebruiken ter ondersteuning van consistentie en standaardisering in [!DNL Experience Platform].

## Compositievoorbeeld

De schema&#39;s vertegenwoordigen het formaat en de structuur van gegevens die in [!DNL Platform] zullen worden opgenomen, en gebruikend een samenstellingsmodel worden gebouwd. Zoals eerder vermeld, zijn deze schema&#39;s samengesteld uit een klasse en nul of meer mengsels die met die klasse compatibel zijn.

Bijvoorbeeld, zou een schema beschrijvend aankopen die bij een detailhandel worden gemaakt &quot;[!UICONTROL Store Transactions]&quot;kunnen worden genoemd. Het schema implementeert de klasse [!DNL XDM ExperienceEvent] in combinatie met de standaardmix [!UICONTROL Commerce] en een door de gebruiker gedefinieerde mix [!UICONTROL Product Info].

Een ander schema dat websiteverkeer volgt zou &quot;[!UICONTROL Web Visits]&quot;kunnen worden genoemd. De klasse [!DNL XDM ExperienceEvent] wordt ook geïmplementeerd, maar deze keer wordt de standaardmix [!UICONTROL Web] gecombineerd.

In het onderstaande diagram ziet u deze schema&#39;s en de velden die door elke mix worden ingebracht. Het bevat ook twee schema&#39;s die op de [!DNL XDM Individual Profile] klasse worden gebaseerd, met inbegrip van het &quot;[!UICONTROL Loyalty Members]&quot;schema dat eerder in deze gids wordt vermeld.

![](../images/schema-composition/composition.png)

### Samenvoegen {#union}

Hoewel [!DNL Experience Platform] u toestaat om schema&#39;s voor bepaalde gebruiksgevallen samen te stellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s voor een specifiek klassentype te zien. Het vorige diagram toont twee schema&#39;s die op de klasse XDM ExperienceEvent en twee schema&#39;s worden gebaseerd die op [!DNL XDM Individual Profile] klasse worden gebaseerd. De Vereniging, hieronder getoond, voegt de gebieden van alle schema&#39;s samen die de zelfde klasse ([!DNL XDM ExperienceEvent] en [!DNL XDM Individual Profile], respectievelijk) delen.

![](../images/schema-composition/union.png)

Door een schema voor gebruik met [!DNL Real-time Customer Profile] toe te laten, zal het in de unie voor dat klassentype worden omvat. [!DNL Profile] levert robuuste, gecentraliseerde profielen van klantenattributen evenals een timestamped rekening van elke gebeurtenis die de klant over om het even welk systeem heeft gehad dat met  [!DNL Platform]wordt geïntegreerd. [!DNL Profile] gebruikt de verenigingsmening om deze gegevens te vertegenwoordigen en een holistische mening van elke individuele klant te verstrekken.

Voor meer informatie bij het werken met [!DNL Profile], zie [Overzicht van het Profiel van de Klant in real time](../../profile/home.md).

## Gegevensbestanden toewijzen aan XDM-schema&#39;s

Alle gegevensbestanden die in [!DNL Experience Platform] worden opgenomen moeten met de structuur van een XDM- schema in overeenstemming zijn. Voor meer informatie over hoe te om gegevensdossiers te formatteren om aan hiërarchieën XDM (met inbegrip van steekproefdossiers) te voldoen, zie het document op [steekproefETL transformaties](../../etl/transformations.md). Voor algemene informatie over het opnemen van gegevensbestanden in [!DNL Experience Platform], zie [batch ingestion overview](../../ingestion/batch-ingestion/overview.md).

## Schema&#39;s voor externe segmenten

Als u segmenten van externe systemen in Platform brengt, moet u de volgende componenten gebruiken om hen in uw schema&#39;s te vangen:

* [[!UICONTROL Segment definition] klasse](../classes/segment-definition.md): Gebruik deze standaardklasse om zeer belangrijke attributen van een externe segmentdefinitie te vangen.
* [[!UICONTROL Segment Membership Details] mengsel](../mixins/profile/segmentation.md): Voeg deze mix aan uw  [!UICONTROL XDM Individual Profile] schema toe om klantenprofielen met specifieke segmenten te associëren.

## Volgende stappen

Nu u de grondbeginselen van schemacompositie begrijpt, bent u bereid beginnen het onderzoeken en het bouwen van schema&#39;s gebruikend [!DNL Schema Registry].

Zie de volgende referentiedocumentatie voor een overzicht van de structuur van de twee belangrijkste XDM-klassen en hun algemeen gebruikte compatibele mixen:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

[!DNL Schema Registry] wordt gebruikt om tot [!DNL Schema Library] binnen Adobe Experience Platform toegang te hebben, en verstrekt een gebruikersinterface en RESTful API waarvan alle beschikbare bibliotheekmiddelen toegankelijk zijn. [!DNL Schema Library] bevat de middelen van de Industrie die door Adobe worden bepaald, de middelen van de Leverancier door partners [!DNL Experience Platform] worden bepaald, en klassen, mengen, gegevenstypes, en schema&#39;s die door leden van uw organisatie zijn samengesteld.

Als u wilt beginnen met het samenstellen van het schema met de gebruikersinterface, volgt u de zelfstudie [Schema-editor](../tutorials/create-schema-ui.md) om het schema &quot;Loyalty-leden&quot; te bouwen dat in dit document wordt vermeld.

Als u de [!DNL Schema Registry]-API wilt gebruiken, begint u met het lezen van de [Handleiding voor ontwikkelaars van de API voor schemaregistratie](../api/getting-started.md). Na het lezen van de ontwikkelaarsgids, volg de stappen die in de zelfstudie worden geschetst op [het creëren van een schema gebruikend de Registratie API](../tutorials/create-schema-api.md) van het Schema.

## Aanhangsel

De volgende secties bevatten extra informatie betreffende de beginselen van schemacompositie.

### Relatieve tabellen versus ingesloten objecten {#embedded}

Wanneer het werken met relationele gegevensbestanden, impliceren de beste praktijken het normaliseren van gegevens, of het nemen van een entiteit en het verdelen van het in discrete stukken die dan over veelvoudige lijsten worden getoond. Om de gegevens als geheel te lezen of de entiteit bij te werken, lees en schrijf verrichtingen over vele individuele lijsten moeten worden gemaakt gebruikend JOIN.

Door het gebruik van ingebedde voorwerpen, kunnen de schema&#39;s XDM complexe gegevens direct vertegenwoordigen en het opslaan in op zichzelf staande documenten met een hiërarchische structuur. Één van de belangrijkste voordelen aan deze structuur is dat het u toestaat om de gegevens te vragen zonder het moeten de entiteit door dure verbindingen aan veelvoudige gedenormaliseerde lijsten reconstrueren. Er zijn geen harde beperkingen aan hoeveel niveaus uw schemahiërarchie kan zijn.

### Schema&#39;s en grote gegevens {#big-data}

Moderne digitale systemen genereren enorme hoeveelheden gedragssignalen (transactiegegevens, weblogbestanden, internet van dingen, weergave, enzovoort). Deze grote gegevens bieden buitengewone mogelijkheden om ervaringen te optimaliseren, maar zijn lastig te gebruiken vanwege de schaal en de verscheidenheid van de gegevens. Om waarde te kunnen halen uit de gegevens, moeten de structuur, de indeling en de definities ervan worden gestandaardiseerd, zodat ze consistent en efficiënt kunnen worden verwerkt.

De schema&#39;s lossen dit probleem op door gegevens toe te laten om uit veelvoudige bronnen worden geïntegreerd, door gemeenschappelijke structuren en definities worden gestandaardiseerd, en over oplossingen worden gedeeld. Op die manier kunnen verdere processen en services elk type vraag van de gegevens beantwoorden, waarbij van de traditionele benadering naar gegevensmodellering wordt overgeschakeld, waarbij alle vragen die van de gegevens worden gesteld van tevoren bekend zijn en de gegevens zijn gemodelleerd om aan die verwachtingen te voldoen.

### Objecten versus vrije-formuliervelden {#objects-v-freeform}

Bij het ontwerpen van uw schema&#39;s moet u rekening houden met een aantal belangrijke factoren wanneer u objecten kiest op vrije-formuliervelden:

| Objecten | Velden met vrije vorm |
| --- | --- |
| Meer nesten | Minder of geen nesten |
| Hiermee maakt u logische veldgroepen | Velden worden op ad-hoclocaties geplaatst |

#### Objecten

Hieronder ziet u de voor- en nadelen van het gebruik van objecten op vrije velden.

**Pros**:

* Objecten kunt u het beste gebruiken als u een logische groepering van bepaalde velden wilt maken.
* Objecten ordenen het schema op een meer gestructureerde manier.
* Objecten helpen indirect bij het maken van een goede menustructuur in de gebruikersinterface van Segment Builder. De gegroepeerde velden in het schema worden direct weerspiegeld in de mappenstructuur die is opgegeven in de gebruikersinterface van Segment Builder.

**Cons**:

* Velden worden meer genest.
* Wanneer u [Adobe Experience Platform Query Service](../../query-service/home.md) gebruikt, moeten langere verwijzingstekenreeksen worden opgegeven voor queryvelden die in objecten zijn genest.

#### Velden met vrije vorm

De voor- en nadelen van het gebruik van vrije-formuliervelden op objecten worden hieronder weergegeven.

**Pros**:

* Velden met vrije vorm worden direct onder het basisobject van het schema (`_tenantId`) gemaakt, waardoor de zichtbaarheid toeneemt.
* De koorden van de verwijzing voor vrije-vormgebieden zijn gewoonlijk korter wanneer het gebruiken van de Dienst van de Vraag.

**Cons**:

* De locatie van vrije-formuliervelden in het schema is ad hoc. Dit betekent dat deze velden in alfabetische volgorde worden weergegeven in de Schema-editor. Hierdoor kunnen schema&#39;s minder gestructureerd worden, en vergelijkbare vrije-vormgebieden kunnen uiteindelijk ver worden gescheiden afhankelijk van hun namen.