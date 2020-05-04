---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Basisbeginselen van de schemacompositie
topic: overview
translation-type: tm+mt
source-git-commit: 14cd3d17c7d9ba602d02925abddec9e0b246a8c8

---


# Basisbeginselen van de schemacompositie

Dit document biedt een inleiding tot de schema&#39;s van het Gegevensmodel van de Ervaring (XDM) en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die in het Platform van de Ervaring van Adobe moeten worden gebruikt. Voor algemene informatie over XDM en hoe het binnen Platform wordt gebruikt, zie het [XDM systeemoverzicht](../home.md).

## Schema&#39;s begrijpen

Een schema is een set regels die de structuur en indeling van gegevens vertegenwoordigen en valideren. Op een hoog niveau, verstrekken de schema&#39;s een abstracte definitie van een real-world voorwerp (zoals een persoon) en schetsen welke gegevens in elke instantie van dat voorwerp (zoals voornaam, achternaam, verjaardag, etc.) zouden moeten worden omvat.

Naast het beschrijven van de structuur van gegevens, passen de schema&#39;s beperkingen en verwachtingen op gegevens toe zodat het kan worden bevestigd aangezien het zich tussen systemen beweegt. Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen.

Het Platform van de ervaring handhaaft deze semantische normalisatie door het gebruik van schema&#39;s. De schema&#39;s zijn de standaardmanier om gegevens in het Platform van de Ervaring te beschrijven, toestaand alle gegevens die aan schema&#39;s in overeenstemming zijn herbruikbaar zonder conflicten over een organisatie en zelfs om tussen veelvoudige organisaties te kunnen delen.

### Relatieve tabellen versus ingesloten objecten

Wanneer het werken met relationele gegevensbestanden, impliceren de beste praktijken het normaliseren van gegevens, of het nemen van een entiteit en het verdelen van het in discrete stukken die dan over veelvoudige lijsten worden getoond. Om de gegevens als geheel te lezen of de entiteit bij te werken, lees en schrijf verrichtingen over vele individuele lijsten moeten worden gemaakt gebruikend JOIN.

Door het gebruik van ingebedde voorwerpen, kunnen de schema&#39;s XDM complexe gegevens direct vertegenwoordigen en het opslaan in op zichzelf staande documenten met hiërarchische structuur. Één van de belangrijkste voordelen aan deze structuur is dat het u toestaat om de gegevens te vragen zonder het moeten de entiteit door dure verbindingen aan veelvoudige gedenormaliseerde lijsten reconstrueren.

### Schema&#39;s en grote gegevens

Moderne digitale systemen genereren enorme hoeveelheden gedragssignalen (transactiegegevens, weblogbestanden, internet van dingen, weergave, enzovoort). Deze grote gegevens bieden buitengewone mogelijkheden om ervaringen te optimaliseren, maar zijn lastig te gebruiken vanwege de schaal en de verscheidenheid van de gegevens. Om waarde te kunnen halen uit de gegevens, moeten de structuur, de indeling en de definities ervan worden gestandaardiseerd, zodat ze consistent en efficiënt kunnen worden verwerkt.

De schema&#39;s lossen dit probleem op door gegevens toe te laten om uit veelvoudige bronnen worden geïntegreerd, door gemeenschappelijke structuren en definities worden gestandaardiseerd, en over oplossingen worden gedeeld. Op die manier kunnen verdere processen en services elk type vraag van de gegevens beantwoorden, waarbij van de traditionele benadering naar gegevensmodellering wordt overgeschakeld, waarbij alle vragen die van de gegevens worden gesteld van tevoren bekend zijn en de gegevens zijn gemodelleerd om aan die verwachtingen te voldoen.

### Workflows op basis van schema&#39;s in Experience Platform

Standaardisering is een essentieel concept achter het ervaringsplatform. XDM, aangedreven door Adobe, is een inspanning om de gegevens van de klantenervaring te standaardiseren en standaardschema&#39;s voor het beheer van de klantenervaring te bepalen.

De infrastructuur waarop het Platform van de Ervaring wordt gebouwd, die als Systeem XDM wordt bekend, vergemakkelijkt op schema-gebaseerde werkschema&#39;s en omvat de Registratie van het Schema, de Redacteur van het Schema, schemameta-gegevens, en de patronen van het de dienstconsumptie. Zie het [XDM-systeemoverzicht](../home.md) voor meer informatie.

## Uw schema plannen

De eerste stap in het bouwen van een schema is het concept, of real-world voorwerp, te bepalen dat u binnen het schema probeert te vangen. Zodra u het concept identificeert u probeert te beschrijven, kunt u beginnen uw schema te plannen door over dingen zoals het type van gegevens, potentiële identiteitsgebieden, en te denken hoe het schema in de toekomst kan evolueren.

### Gedrag van gegevens in Experience Platform

Gegevens die bestemd zijn voor gebruik in Experience Platform, worden gegroepeerd in twee gedragstypen:

* **Opnamegegevens**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **Gegevens** tijdreeks: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de **klasse** van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. XDM-klassen worden later in dit document nader beschreven.

Zowel de verslagen als de tijdreeksschema&#39;s bevatten een kaart van identiteiten (`xdm:identityMap`). Dit veld bevat de identiteitsrepresentatie van een onderwerp, getekend vanuit velden die zijn gemarkeerd als Identiteit zoals beschreven in de volgende sectie.

### Identiteit

De schema&#39;s worden gebruikt voor het opnemen van gegevens in het Platform van de Ervaring. Deze gegevens kunnen over de veelvoudige diensten worden gebruikt om één enkele, verenigde mening van een individuele entiteit tot stand te brengen. Daarom is het belangrijk bij het denken over schema&#39;s om over &quot;Identiteit&quot;te denken en welke gebieden kunnen worden gebruikt om een onderwerp te identificeren ongeacht waar de gegevens uit kunnen komen.

Om dit proces te helpen, kunnen de zeer belangrijke gebieden als &quot;Identiteit&quot;worden gemerkt. Bij gegevensinvoer worden de gegevens in die velden ingevoegd in de &quot;Identiteitsgrafiek&quot; voor die persoon. De grafiekgegevens kunnen dan door het Profiel [van de Klant in](../../profile/home.md) real time en de andere diensten van het Platform van de Ervaring worden betreden om een geneutraliseerde mening van elke individuele klant te verstrekken.

Velden die algemeen als &quot;Identiteit&quot;worden gemerkt omvatten: e-mailadres, telefoonnummer, [Experience Cloud ID (ECID)](https://docs.adobe.com/content/help/en/id-service/using/home.html), CRM-id of andere unieke id-velden. U moet ook rekening houden met eventuele unieke id&#39;s die specifiek zijn voor uw organisatie, omdat deze ook goede velden voor &#39;Identiteit&#39; kunnen zijn.

Het is belangrijk om over klantenidentiteiten tijdens de schema planningsfase te denken helpen ervoor zorgen de gegevens worden samengebracht om het meest robuuste profiel mogelijk te bouwen. Zie het overzicht [van de](../../identity-service/home.md) Identiteitsdienst voor meer informatie over hoe de identiteitsinformatie u kan helpen digitale ervaringen aan uw klanten leveren.

### Beginselen voor de ontwikkeling van schema&#39;s {#evolution}

Naarmate de aard van de digitale ervaringen zich blijft ontwikkelen, moeten de schema&#39;s die gebruikt worden om ze te vertegenwoordigen ook worden gebruikt. Een goed ontworpen schema kan daarom aanpassen en evolueren zoals nodig, zonder destructieve veranderingen in vorige versies van het schema te veroorzaken.

Aangezien het handhaven van achterwaartse verenigbaarheid essentieel voor schemaevolutie is, handhaaft het Platform van de Ervaring een zuiver additief versieringsbeginsel om ervoor te zorgen dat om het even welke herzieningen van het schema slechts in niet destructieve updates en veranderingen resulteren. Met andere woorden, **afbrekende wijzigingen worden niet ondersteund.**

| Ondersteunde wijzigingen | Wijzigingen doorlopen (niet ondersteund) |
|------------------------------------|---------------------------------|
| <ul><li>Nieuwe velden toevoegen aan een bestaand schema</li><li>Een verplicht veld optioneel maken</li></ul> | <ul><li>Eerder gedefinieerde velden verwijderen</li><li>Nieuwe verplichte velden invoegen</li><li>Bestaande velden hernoemen of opnieuw definiëren</li><li>Eerder ondersteunde veldwaarden verwijderen of beperken</li><li>Kenmerken verplaatsen naar een andere locatie in de structuur</li></ul> |

>[!NOTE] Als een schema nog niet is gebruikt om gegevens in het Platform van de Ervaring op te nemen, kunt u een breekverandering in dat schema introduceren. Nochtans, zodra het schema in Platform is gebruikt, moet het aan het additieve versieringsbeleid houden.

### Schema&#39;s en gegevensinvoer

Om gegevens in het Platform van de Ervaring op te nemen, moet een dataset eerst worden gecreeerd. Datasets zijn de bouwstenen voor gegevenstransformatie en het volgen voor de Dienst [van de](../../catalog/home.md)Catalogus, en vertegenwoordigen over het algemeen lijsten of dossiers die ingebedde gegevens bevatten. Alle datasets zijn gebaseerd op bestaande schema&#39;s XDM, die beperkingen voor wat verstrekken de ingebedde gegevens zouden moeten bevatten en hoe het zou moeten worden gestructureerd. Zie het overzicht op het [Adobe Experience Platform - Gegevensverwerking](../../ingestion/home.md) voor meer informatie.

## Bouwstenen van een schema

Het Platform van de ervaring gebruikt een samenstellingsbenadering waarin de standaard bouwstenen worden gecombineerd om schema&#39;s tot stand te brengen. Deze benadering bevordert de herbruikbaarheid van bestaande componenten en drijft standaardisatie over de industrie om verkopersschema&#39;s en componenten in Platform te steunen.

De schema&#39;s worden samengesteld gebruikend de volgende formule:

**Klasse + Mixin&amp;ast; = XDM-schema**

&amp;ast;Een schema bestaat uit een klasse en _nul of meer_ mixins. Dit betekent dat u een datasetschema kon samenstellen zonder mixins bij allen te gebruiken.

### Klasse

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

Een klasse bepaalt ook welke mengen voor gebruik in het schema in aanmerking komen. Dit wordt meer in detail besproken in de [mixinsectie](#mixin) die volgt.

Er zijn standaardklassen voorzien van elke integratie van het Platform van de Ervaring, die als &quot;Industrie&quot;klassen wordt bekend. Industrieklassen zijn algemeen aanvaarde industriestandaarden die van toepassing zijn op een breed scala van gebruiksgevallen. Voorbeelden van industrieklassen zijn de klassen XDM Individual Profile en XDM ExperienceEvent die door Adobe worden verstrekt.

Het Platform van de ervaring staat ook voor &quot;Verkoper&quot;klassen toe, die klassen door de partners van het Platform van de Ervaring worden bepaald en ter beschikking gesteld aan alle klanten die die verkopersdienst of toepassing binnen Platform gebruiken.

Er zijn ook klassen die worden gebruikt om specifiekere gebruiksgevallen voor individuele organisaties binnen Platform te beschrijven, de &quot;Klant&quot;klassen genoemd. Klantklassen worden gedefinieerd door een organisatie wanneer er geen branche- of leveranciersklassen beschikbaar zijn om een uniek geval van gebruik te beschrijven.

Een schema dat bijvoorbeeld leden van een Loyalty-programma vertegenwoordigt, beschrijft recordgegevens over een individu en kan daarom worden gebaseerd op de klasse Individual Profile van XDM, een standaardklasse van de Industrie die door Adobe wordt bepaald.

### Mixin {#mixin}

Een mix is een herbruikbare component die een of meer velden definieert die bepaalde functies implementeren, zoals persoonlijke gegevens, hotelvoorkeuren of adres. Mixins zijn bedoeld om te worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Mixins definiëren met welke klasse(n) ze compatibel zijn op basis van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Dit betekent dat niet alle mengsels beschikbaar zijn voor gebruik met alle klassen.

Mixinen hebben hetzelfde bereik en dezelfde definitie als klassen: Er zijn industriemengsels, leveranciersmixen, en de mixins van de Klant die door individuele organisaties gebruikend Platform worden bepaald. Het Platform van de ervaring omvat vele standaardmengen van de Industrie terwijl ook het toestaan van verkopers om mengsels voor hun gebruikers te bepalen, en individuele gebruikers om mengins voor hun eigen specifieke concepten te bepalen.

Bijvoorbeeld, om details zoals &quot;Voornaam&quot;en &quot;Adres van het Huis&quot;voor uw schema van &quot;Loyalty Leden&quot;te vangen, zou u standaardmengen kunnen gebruiken die die gemeenschappelijke concepten bepalen. Concepten die specifiek zijn voor minder gangbare gebruiksgevallen (zoals &quot;Loyalty Program Level&quot;) hebben echter vaak geen vooraf gedefinieerde mix. In dit geval moet u uw eigen mix definiëren om deze informatie vast te leggen.

Herinner dat de schema&#39;s uit &quot;nul of meer&quot;mengen bestaan, zodat betekent dit dat u een geldig schema kon samenstellen zonder enige mengen bij allen te gebruiken.

### Gegevenstype {#data-type}

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als referentieveldtypen in klassen of schema&#39;s. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Vergelijkbaar met een mixin, staat een gegevenstype voor het verenigbare gebruik van een multi-gebiedstructuur toe, maar heeft meer flexibiliteit dan een mixin omdat een gegevenstype overal in een schema kan worden omvat door het als &quot;gegevenstype&quot;van een gebied toe te voegen.

Het Platform van de ervaring verstrekt een aantal gemeenschappelijke gegevenstypes als deel van het Registratie van het Schema om het gebruik van standaardpatronen voor het beschrijven van gemeenschappelijke gegevensstructuren te steunen. Dit wordt meer in detail uitgelegd in de leerprogramma&#39;s van de Registratie van het Schema, waar het duidelijker zal worden aangezien u door de stappen loopt om gegevenstypes te bepalen.

### Veld

Een veld is de eenvoudigste bouwsteen van een schema. Velden bieden beperkingen met betrekking tot het type gegevens dat ze kunnen bevatten door een specifiek gegevenstype te definiëren. Deze basistypen definiëren één veld, terwijl u met de eerder vermelde [gegevenstypen](#data-type) meerdere subvelden kunt definiëren en dezelfde structuur voor meerdere velden kunt gebruiken in verschillende schema&#39;s. Zo, naast het bepalen van het &quot;gegevenstype&quot;van een gebied als één van de gegevenstypes die in de registratie worden bepaald, steunt het Platform van de Ervaring fundamentele scalaire types zoals:

* String
* Geheel
* Getal
* Boolean
* Array
* Object

De geldige waaiers van deze scalaire types kunnen verder tot bepaalde patronen, formaten, minimum/maximum, of vooraf bepaalde waarden worden beperkt. Gebruikend deze beperkingen, kan een brede waaier van specifiekere gebiedstypes worden vertegenwoordigd, die omvatten:

* Enum
* Lang
* Kort
* Byte
* Datum
* Datum/tijd
* Kaart

>[!NOTE] Het &quot;kaart&quot;gebiedstype staat voor sleutel-waarde paargegevens, met inbegrip van veelvoudige waarden voor één enkele sleutel toe. Kaarten kunnen alleen op systeemniveau worden gedefinieerd. Dit betekent dat u een kaart in een door de industrie of leverancier gedefinieerd schema tegenkomt, maar dat deze kaart niet beschikbaar is voor gebruik in velden die u definieert. De ontwikkelaarsgids voor [de](../api/getting-started.md) schemaregistratie-API bevat meer informatie over het definiëren van veldtypen.

Sommige gegevensverrichtingen die door stroomafwaartse diensten en toepassingen worden gebruikt dwingen beperkingen op specifieke gebiedstypes af. De betrokken diensten omvatten, maar zijn niet beperkt tot:

* [Klantprofiel in realtime](../../profile/home.md)
* [Identiteitsservice](../../identity-service/home.md)
* [Segmentering](../../segmentation/home.md)
* [Query-service](../../query-service/home.md)
* [Werkruimte voor gegevenswetenschap](../../data-science-workspace/home.md)

Alvorens een schema voor gebruik in de stroomafwaartse diensten te creëren, te herzien gelieve de aangewezen documentatie voor die diensten om de gebiedsvereisten en de beperkingen voor de gegevensverrichtingen beter te begrijpen het schema voor bedoeld is.

### XDM-velden

Naast basisgebieden en de capaciteit om uw eigen gegevenstypes te bepalen, verstrekt XDM een standaardreeks gebieden en gegevenstypes die impliciet door de diensten van het Platform van de Ervaring worden begrepen en grotere consistentie wanneer gebruikt over de componenten van het Platform verstrekken.

Deze velden, zoals &quot;Voornaam&quot; en &quot;E-mailadres&quot;, bevatten toegevoegde verbindingen die verder gaan dan elementaire scalaire veldtypen en het Platform laten weten dat velden die hetzelfde XDM-gegevenstype delen, zich op dezelfde manier gedragen. Dit gedrag kan worden vertrouwd om verenigbaar te zijn ongeacht waar de gegevens uit komen, of waarin de dienst van het Platform de gegevens wordt gebruikt.

Zie het [XDM-veldwoordenboek](field-dictionary.md) voor een volledige lijst met beschikbare XDM-velden. U wordt aangeraden XDM-velden en gegevenstypen waar mogelijk te gebruiken ter ondersteuning van consistentie en standaardisering in het ervaringsplatform.

## Compositievoorbeeld

De schema&#39;s vertegenwoordigen het formaat en de structuur van gegevens die in Platform zullen worden opgenomen, en gebruikend een samenstellingsmodel gebouwd. Zoals eerder vermeld, zijn deze schema&#39;s samengesteld uit een klasse en nul of meer mengsels die met die klasse compatibel zijn.

Bijvoorbeeld, zou een schema beschrijvend aankopen die bij een detailhandel worden gemaakt &quot;Transacties van de Opslag&quot;kunnen worden genoemd. Het schema implementeert de klasse XDM ExperienceEvent gecombineerd met de standaardmix van Handel en een door de gebruiker gedefinieerde mix van Productinformatie.

Een ander schema dat websiteverkeer volgt zou &quot;Webbezoeken&quot;kunnen worden genoemd. Het voert ook de klasse XDM ExperienceEvent uit, maar deze keer combineert de standaardmixin van het Web.

In het onderstaande diagram ziet u deze schema&#39;s en de velden die door elke mix worden ingebracht. Het bevat ook twee schema&#39;s die op de individuele klasse van het Profiel XDM worden gebaseerd, met inbegrip van het schema van de &quot;Leden van de Loyalty&quot;die eerder in deze gids wordt vermeld.

![](../images/schema-composition/composition.png)

### Unie {#union}

Terwijl het Platform van de Ervaring u toestaat om schema&#39;s voor bepaalde gebruiksgevallen samen te stellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s voor een specifiek klassentype te zien. Het vorige diagram toont twee schema&#39;s die op de klasse XDM ExperienceEvent en twee schema&#39;s worden gebaseerd die op de Individuele klasse van het Profiel XDM worden gebaseerd. De samenvoeging, die hieronder wordt weergegeven, aggregeert de velden van alle schema&#39;s die dezelfde klasse delen (respectievelijk XDM ExperienceEvent en XDM Individual Profile).

![](../images/schema-composition/union.png)

Door een schema voor gebruik met het Profiel van de Klant in real time toe te laten, zal het in de unie voor dat klassentype worden omvat. Profiel biedt robuuste, gecentraliseerde profielen van klantkenmerken en een tijdstempelaccount voor elke gebeurtenis die de klant heeft gehad in een systeem dat is geïntegreerd met Platform. Het profiel gebruikt de verenigingsmening om deze gegevens te vertegenwoordigen en een holistische mening van elke individuele klant te verstrekken.

Voor meer informatie over het werken met Profiel, zie het [overzicht](../../profile/home.md)van het Profiel van de Klant In real time.

## Gegevensbestanden toewijzen aan XDM-schema&#39;s

Alle gegevensbestanden die in het Platform van de Ervaring worden opgenomen moeten met de structuur van een XDM- schema in overeenstemming zijn. Zie het document over [voorbeeld-ETL-transformaties](../../etl/transformations.md)voor meer informatie over hoe u gegevensbestanden kunt opmaken om te voldoen aan XDM-hiërarchieën (inclusief voorbeeldbestanden). Voor algemene informatie over het opnemen van gegevensbestanden in het Platform van de Ervaring, zie het overzicht [van](../../ingestion/batch-ingestion/overview.md)partijingestie.

## Volgende stappen

Nu u de grondbeginselen van schemacompositie begrijpt, bent u bereid beginnen bouwend schema&#39;s gebruikend de Registratie van het Schema.

Het Schemaregister wordt gebruikt om toegang te krijgen tot de Schemabibliotheek binnen het Adobe Experience Platform en biedt een gebruikersinterface en RESTful-API waaruit alle beschikbare bibliotheekbronnen toegankelijk zijn. De Schemabibliotheek bevat de middelen van de Industrie die door Adobe worden bepaald, de middelen van de Leverancier door de partners van het Platform van de Ervaring worden bepaald, en klassen, mengen, gegevenstypes, en schema&#39;s die door leden van uw organisatie zijn samengesteld.

Als u wilt beginnen met het samenstellen van een schema met behulp van de UI, volgt u de zelfstudie [van de](../tutorials/create-schema-ui.md) Schema-editor om het schema &quot;Loyalty-leden&quot; te bouwen dat in dit document wordt vermeld.

Om te beginnen met het gebruiken van de Registratie API van het Schema, begin door de de ontwikkelaarsgids [van de Registratie van het](../api/getting-started.md)Schema te lezen. Na het lezen van de ontwikkelaarsgids, volg de stappen die in het leerprogramma worden geschetst over het [creëren van een schema gebruikend de Registratie API](../tutorials/create-schema-api.md)van het Schema.
