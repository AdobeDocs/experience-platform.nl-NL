---
keywords: Experience Platform;home;popular topics;schema;Schema;enum;mixin;Mixin;Mixins;mixins;data type;data types;Data types;Data type;primary identity;primary idenity;XDM individual profile;XDM fields;enum datatype;Experience event;XDM Experience Event;XDM ExperienceEvent;experienceEvent;experienceevent;XDM Experienceevenet;schema design;class;Class;classes;Classes;datatype;Datatype;data type;Data type;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Basisbeginselen van de schemacompositie
topic: overview
description: Dit document verstrekt een inleiding aan de schema's van het Gegevensmodel van de Ervaring (XDM) en de bouwstenen, de beginselen, en beste praktijken voor het samenstellen van schema's die in Adobe Experience Platform moeten worden gebruikt.
translation-type: tm+mt
source-git-commit: b7b57c0b70b1af3a833f0386bc809bb92c9b50f8
workflow-type: tm+mt
source-wordcount: '2834'
ht-degree: 0%

---


# Basisbeginselen van de schemacompositie

Dit document verstrekt een inleiding aan [!DNL Experience Data Model] (XDM) schema&#39;s en de bouwstenen, principes, en beste praktijken voor het samenstellen van schema&#39;s die in Adobe Experience Platform moeten worden gebruikt. Voor algemene informatie over XDM en hoe het binnen wordt gebruikt, zie het [!DNL Platform]XDM systeemoverzicht [](../home.md).

## Schema&#39;s begrijpen

Een schema is een set regels die de structuur en indeling van gegevens vertegenwoordigen en valideren. Op een hoog niveau, verstrekken de schema&#39;s een abstracte definitie van een real-world voorwerp (zoals een persoon) en schetsen welke gegevens in elke instantie van dat voorwerp (zoals voornaam, achternaam, verjaardag, etc.) zouden moeten worden omvat.

Naast het beschrijven van de structuur van gegevens, passen de schema&#39;s beperkingen en verwachtingen op gegevens toe zodat het kan worden bevestigd aangezien het zich tussen systemen beweegt. Deze standaarddefinities maken het mogelijk dat gegevens consistent worden geïnterpreteerd, ongeacht de oorsprong, en verwijderen de noodzaak van vertaling in verschillende toepassingen.

[!DNL Experience Platform] handhaaft deze semantische normalisatie door het gebruik van schema&#39;s. Schema&#39;s zijn de standaardmanier om gegevens in te beschrijven [!DNL Experience Platform], zodat alle gegevens die aan schema&#39;s voldoen, opnieuw kunnen worden gebruikt zonder conflicten in een organisatie en zelfs tussen meerdere organisaties kunnen worden gedeeld.

### Relatieve tabellen versus ingesloten objecten

Wanneer het werken met relationele gegevensbestanden, impliceren de beste praktijken het normaliseren van gegevens, of het nemen van een entiteit en het verdelen van het in discrete stukken die dan over veelvoudige lijsten worden getoond. Om de gegevens als geheel te lezen of de entiteit bij te werken, lees en schrijf verrichtingen over vele individuele lijsten moeten worden gemaakt gebruikend JOIN.

Door het gebruik van ingebedde voorwerpen, kunnen de schema&#39;s XDM complexe gegevens direct vertegenwoordigen en het opslaan in op zichzelf staande documenten met hiërarchische structuur. Één van de belangrijkste voordelen aan deze structuur is dat het u toestaat om de gegevens te vragen zonder het moeten de entiteit door dure verbindingen aan veelvoudige gedenormaliseerde lijsten reconstrueren.

### Schema&#39;s en grote gegevens

Moderne digitale systemen genereren enorme hoeveelheden gedragssignalen (transactiegegevens, weblogbestanden, internet van dingen, weergave, enzovoort). Deze grote gegevens bieden buitengewone mogelijkheden om ervaringen te optimaliseren, maar zijn lastig te gebruiken vanwege de schaal en de verscheidenheid van de gegevens. Om waarde te kunnen halen uit de gegevens, moeten de structuur, de indeling en de definities ervan worden gestandaardiseerd, zodat ze consistent en efficiënt kunnen worden verwerkt.

De schema&#39;s lossen dit probleem op door gegevens toe te laten om uit veelvoudige bronnen worden geïntegreerd, door gemeenschappelijke structuren en definities worden gestandaardiseerd, en over oplossingen worden gedeeld. Op die manier kunnen verdere processen en services elk type vraag van de gegevens beantwoorden, waarbij van de traditionele benadering naar gegevensmodellering wordt overgeschakeld, waarbij alle vragen die van de gegevens worden gesteld van tevoren bekend zijn en de gegevens zijn gemodelleerd om aan die verwachtingen te voldoen.

### Workflows op basis van schema&#39;s in [!DNL Experience Platform]

Standaardisering is een essentieel concept achter [!DNL Experience Platform]. XDM, die door Adobe wordt gedreven, is een inspanning om de gegevens van de klantenervaring te standaardiseren en standaardschema&#39;s voor het beheer van de klantenervaring te bepalen.

De infrastructuur waarop [!DNL Experience Platform] wordt gebouwd, die als [!DNL XDM System], op schema-gebaseerde werkschema&#39;s wordt bekend en omvat de [!DNL Schema Registry], [!DNL Schema Editor], schemameta-gegevens, en de patronen van het de dienstconsumptie. Zie het [XDM-systeemoverzicht](../home.md) voor meer informatie.

## Uw schema plannen

De eerste stap in het bouwen van een schema is het concept, of real-world voorwerp, te bepalen dat u binnen het schema probeert te vangen. Zodra u het concept identificeert u probeert te beschrijven, kunt u beginnen uw schema te plannen door over dingen zoals het type van gegevens, potentiële identiteitsgebieden, en te denken hoe het schema in de toekomst kan evolueren.

### Gedrag van gegevens in [!DNL Experience Platform]

Gegevens die bestemd zijn voor gebruik in [!DNL Experience Platform] worden gegroepeerd in twee gedragstypen:

* **Opnamegegevens**: Verstrekt informatie over de attributen van een onderwerp. Een onderwerp kan een organisatie of een individu zijn.
* **Gegevens** tijdreeks: Biedt een momentopname van het systeem op het moment dat een handeling direct of indirect door een recordonderwerp is uitgevoerd.

Alle XDM schema&#39;s beschrijven gegevens die als verslag of tijdreeks kunnen worden gecategoriseerd. Het gegevensgedrag van een schema wordt bepaald door de klasse van het schema, die aan een schema wordt toegewezen wanneer het eerst wordt gecreeerd. XDM-klassen worden later in dit document nader beschreven.

Zowel de verslagen als de tijdreeksschema&#39;s bevatten een kaart van identiteiten (`xdm:identityMap`). Dit veld bevat de identiteitsrepresentatie van een onderwerp, getekend vanuit velden die zijn gemarkeerd als Identiteit zoals beschreven in de volgende sectie.

### [!UICONTROL Identiteit] {#identity}

Schema&#39;s worden gebruikt om gegevens in te voeren [!DNL Experience Platform]. Deze gegevens kunnen over de veelvoudige diensten worden gebruikt om één enkele, verenigde mening van een individuele entiteit tot stand te brengen. Daarom is het belangrijk wanneer het denken over schema&#39;s om over klantenidentiteiten te denken en welke gebieden kunnen worden gebruikt om een onderwerp te identificeren ongeacht waar de gegevens uit kunnen komen.

Om dit proces te helpen, kunnen de belangrijkste gebieden binnen uw schema&#39;s als identiteiten worden gemerkt. Bij gegevensinvoer worden de gegevens in die velden ingevoegd in de &quot;[!UICONTROL Identiteitsgrafiek]&quot; voor die persoon. De grafiekgegevens kunnen dan door [[!DNL Real-time Customer Profile]](../../profile/home.md) en andere [!DNL Experience Platform] diensten worden betreden om een geneutraliseerde mening van elke individuele klant te verstrekken.

Velden die algemeen als &quot;[!UICONTROL Identiteit]&quot;worden gemerkt omvatten: e-mailadres, telefoonnummer, [[!DNL Experience Cloud ID (ECID)]](https://docs.adobe.com/content/help/nl-NL/id-service/using/home.html)CRM-id of andere unieke id-velden. U zou ook om het even welke unieke herkenningstekens moeten overwegen specifiek voor uw organisatie, aangezien zij ook goede &quot;[!UICONTROL Identiteit]&quot;gebieden kunnen zijn.

Het is belangrijk om over klantenidentiteiten tijdens de schema planningsfase te denken helpen ervoor zorgen de gegevens worden samengebracht om het meest robuuste profiel mogelijk te bouwen. Zie het overzicht over [Adobe Experience Platform Identity Service](../../identity-service/home.md) voor meer informatie over hoe identiteitsgegevens u kunnen helpen uw klanten digitale ervaringen te bieden.

#### xdm:identityMap {#identityMap}

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

Zoals in het bovenstaande voorbeeld wordt getoond, vertegenwoordigt elke sleutel in het `identityMap` object een naamruimte voor identiteit. De waarde voor elke sleutel is een array van objecten die de identiteitswaarden (`id`) voor de respectievelijke naamruimte vertegenwoordigt. Raadpleeg de [!DNL Identity Service] documentatie voor een [lijst met standaardnaamruimten](../../identity-service/troubleshooting-guide.md#standard-namespaces) die door Adobe-toepassingen worden herkend.

>[!NOTE]
>
>Voor elke identiteitswaarde kan ook een booleaanse waarde worden opgegeven, of de waarde een primaire identiteit (`primary`) is. De primaire identiteiten hoeven alleen te worden vastgesteld voor schema&#39;s die bestemd zijn om te worden gebruikt in [!DNL Real-time Customer Profile]. Zie de sectie over [samenvoegingsschema&#39;s](#union) voor meer informatie.

### Beginselen voor de ontwikkeling van schema&#39;s {#evolution}

Naarmate de aard van de digitale ervaringen zich blijft ontwikkelen, moeten de schema&#39;s die gebruikt worden om ze te vertegenwoordigen ook worden gebruikt. Een goed ontworpen schema kan daarom aanpassen en evolueren zoals nodig, zonder destructieve veranderingen in vorige versies van het schema te veroorzaken.

Aangezien het handhaven van achterwaartse verenigbaarheid essentieel voor schemaevolutie is, [!DNL Experience Platform] handhaaft een zuiver additief versieringsbeginsel om ervoor te zorgen dat om het even welke herzieningen aan het schema slechts in niet-destructieve updates en veranderingen resulteren. Met andere woorden, **afbrekende wijzigingen worden niet ondersteund.**

| Ondersteunde wijzigingen | Wijzigingen doorlopen (niet ondersteund) |
|------------------------------------|---------------------------------|
| <ul><li>Nieuwe velden toevoegen aan een bestaand schema</li><li>Een verplicht veld optioneel maken</li></ul> | <ul><li>Eerder gedefinieerde velden verwijderen</li><li>Nieuwe verplichte velden invoegen</li><li>Bestaande velden hernoemen of opnieuw definiëren</li><li>Eerder ondersteunde veldwaarden verwijderen of beperken</li><li>Kenmerken verplaatsen naar een andere locatie in de structuur</li></ul> |

>[!NOTE]
>
>Als een schema nog niet is gebruikt om gegevens in op te nemen in [!DNL Experience Platform], kunt u een het breken verandering in dat schema introduceren. Nochtans, zodra het schema binnen is gebruikt [!DNL Platform], moet het aan het additieve versieringsbeleid houden.

### Schema&#39;s en gegevensinvoer

Om gegevens in te voeren in [!DNL Experience Platform], moet een dataset eerst worden gecreeerd. Datasets zijn de bouwstenen voor gegevenstransformatie en -tracking voor [[!DNL Catalog Service]](../../catalog/home.md), en vertegenwoordigen over het algemeen tabellen of bestanden die ingesloten gegevens bevatten. Alle datasets zijn gebaseerd op bestaande schema&#39;s XDM, die beperkingen voor wat verstrekken de ingebedde gegevens zouden moeten bevatten en hoe het zou moeten worden gestructureerd. Zie het overzicht over [Adobe Experience Platform Data Ingestie](../../ingestion/home.md) voor meer informatie.

## Bouwstenen van een schema

[!DNL Experience Platform] gebruikt een compositiebenadering waarin de standaard bouwstenen worden gecombineerd om schema&#39;s tot stand te brengen. Deze benadering bevordert de herbruikbaarheid van bestaande componenten en drijft standaardisatie over de industrie om verkopersschema&#39;s en componenten in [!DNL Platform]te steunen.

De schema&#39;s worden samengesteld gebruikend de volgende formule:

**Klasse + Mixin&amp;ast; = XDM-schema**

&amp;ast;Een schema bestaat uit een klasse en nul of meer mixins. Dit betekent dat u een datasetschema kon samenstellen zonder mixins bij allen te gebruiken.

### Klasse

Het samenstellen van een schema begint door een klasse toe te wijzen. De klassen bepalen de gedragsaspecten van de gegevens het schema (verslag of tijdreeks) zal bevatten. Bovendien beschrijven de klassen het kleinste aantal gemeenschappelijke eigenschappen die alle die schema&#39;s op die klasse worden gebaseerd zouden moeten omvatten en een manier verstrekken om veelvoudige compatibele datasets worden samengevoegd.

Een klasse bepaalt ook welke mengen voor gebruik in het schema in aanmerking komen. Dit wordt meer in detail besproken in de [mixinsectie](#mixin) die volgt.

Er zijn standaardklassen voorzien van elke integratie van [!DNL Experience Platform], die als &quot;Industrie&quot;klassen wordt bekend. Industrieklassen zijn algemeen aanvaarde industriestandaarden die van toepassing zijn op een breed scala van gebruiksgevallen. De voorbeelden van de klassen van de Industrie omvatten de [!DNL XDM Individual Profile] en [!DNL XDM ExperienceEvent] klassen door Adobe worden verstrekt die.

[!DNL Experience Platform] staat ook voor klassen &quot;van de Leverancier&quot;toe, die klassen door [!DNL Experience Platform] partners worden bepaald en ter beschikking gesteld aan alle klanten die die verkopersdienst of toepassing binnen gebruiken [!DNL Platform].

Er zijn ook klassen die worden gebruikt om specifiekere gebruiksgevallen voor individuele organisaties binnen te beschrijven [!DNL Platform], de &quot;Klant&quot;klassen. Klantklassen worden gedefinieerd door een organisatie wanneer er geen branche- of leveranciersklassen beschikbaar zijn om een uniek geval van gebruik te beschrijven.

Een schema dat bijvoorbeeld leden van een Loyalty-programma vertegenwoordigt, beschrijft recordgegevens over een individu en kan daarom op de [!DNL XDM Individual Profile] klasse worden gebaseerd, een standaardklasse van de Industrie die door Adobe wordt bepaald.

### Mixin {#mixin}

Een mix is een herbruikbare component die een of meer velden definieert die bepaalde functies implementeren, zoals persoonlijke gegevens, hotelvoorkeuren of adres. Mixins zijn bedoeld om te worden opgenomen als onderdeel van een schema dat een compatibele klasse implementeert.

Mixins definiëren met welke klasse(n) ze compatibel zijn op basis van het gedrag van de gegevens die ze vertegenwoordigen (record- of tijdreeks). Dit betekent dat niet alle mengsels beschikbaar zijn voor gebruik met alle klassen.

Mixinen hebben hetzelfde bereik en dezelfde definitie als klassen: Er zijn industriemengsels, leveranciersmixen, en de mixins van de Klant die door individuele organisaties worden bepaald gebruikend [!DNL Platform]. [!DNL Experience Platform] omvat vele standaardMengsels van de Industrie terwijl ook het toestaan van verkopers om mengsels voor hun gebruikers te bepalen, en individuele gebruikers om mengsels voor hun eigen specifieke concepten te bepalen.

Bijvoorbeeld, om details zoals &quot;[!UICONTROL Voornaam]&quot;en &quot;Adres[!UICONTROL van het]Huis&quot;voor uw schema van &quot;[!UICONTROL Loyalty Leden]&quot;te vangen, zou u standaardmengingen kunnen gebruiken die die gemeenschappelijke concepten bepalen. Concepten die specifiek zijn voor minder gangbare gebruiksgevallen (zoals &quot;[!UICONTROL Loyalty Program Level]&quot;) hebben echter vaak geen vooraf gedefinieerde mix. In dit geval moet u uw eigen mix definiëren om deze informatie vast te leggen.

Herinner dat de schema&#39;s uit &quot;nul of meer&quot;mengen bestaan, zodat betekent dit dat u een geldig schema kon samenstellen zonder enige mengen bij allen te gebruiken.

### Data type {#data-type}

Gegevenstypen worden op dezelfde manier als letterlijke basisvelden gebruikt als referentieveldtypen in klassen of schema&#39;s. Het belangrijkste verschil is dat gegevenstypen meerdere subvelden kunnen definiëren. Vergelijkbaar met een mixin, staat een gegevenstype voor het verenigbare gebruik van een multi-gebiedstructuur toe, maar heeft meer flexibiliteit dan een mixin omdat een gegevenstype overal in een schema kan worden omvat door het als &quot;gegevenstype&quot;van een gebied toe te voegen.

[!DNL Experience Platform] bevat een aantal gangbare gegevenstypen als onderdeel van het programma [!DNL Schema Registry] ter ondersteuning van het gebruik van standaardpatronen voor het beschrijven van gemeenschappelijke gegevensstructuren. Dit wordt meer in detail uitgelegd in de [!DNL Schema Registry] zelfstudies, waar het duidelijker zal worden aangezien u door de stappen loopt om gegevenstypes te bepalen.

### Veld

Een veld is de eenvoudigste bouwsteen van een schema. Velden bieden beperkingen met betrekking tot het type gegevens dat ze kunnen bevatten door een specifiek gegevenstype te definiëren. Deze basistypen definiëren één veld, terwijl u met de eerder vermelde [gegevenstypen](#data-type) meerdere subvelden kunt definiëren en dezelfde structuur voor meerdere velden kunt gebruiken in verschillende schema&#39;s. Zo, naast het bepalen van het &quot;gegevenstype&quot;van een gebied als één van de gegevenstypes die in de registratie worden bepaald, [!DNL Experience Platform] steunt fundamentele scalaire types zoals:

* Tekenreeks
* Geheel
* Dubbel
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

>[!NOTE]
>
>Het &quot;kaart&quot;gebiedstype staat voor sleutel-waarde paargegevens, met inbegrip van veelvoudige waarden voor één enkele sleutel toe. Kaarten kunnen alleen op systeemniveau worden gedefinieerd. Dit betekent dat u een kaart in een door de industrie of leverancier gedefinieerd schema tegenkomt, maar dat deze kaart niet beschikbaar is voor gebruik in velden die u definieert. De ontwikkelaarsgids voor [de](../api/getting-started.md) schemaregistratie-API bevat meer informatie over het definiëren van veldtypen.

Sommige gegevensverrichtingen die door stroomafwaartse diensten en toepassingen worden gebruikt dwingen beperkingen op specifieke gebiedstypes af. De betrokken diensten omvatten, maar zijn niet beperkt tot:

* [[!DNL Real-time Customer Profile]](../../profile/home.md)
* [[!DNL Identity Service]](../../identity-service/home.md)
* [[!DNL Segmentation]](../../segmentation/home.md)
* [[!DNL Query Service]](../../query-service/home.md)
* [[!DNL Data Science Workspace]](../../data-science-workspace/home.md)

Alvorens een schema voor gebruik in de stroomafwaartse diensten te creëren, te herzien gelieve de aangewezen documentatie voor die diensten om de gebiedsvereisten en de beperkingen voor de gegevensverrichtingen beter te begrijpen het schema voor bedoeld is.

### XDM-velden

Naast basisgebieden en de capaciteit om uw eigen gegevenstypes te bepalen, verstrekt XDM een standaardreeks gebieden en gegevenstypes die impliciet door de [!DNL Experience Platform] diensten worden begrepen en grotere consistentie wanneer gebruikt over [!DNL Platform] componenten verstrekken.

Deze velden, zoals &quot;Voornaam&quot; en &quot;E-mailadres&quot;, bevatten toegevoegde aantekeningen die verder gaan dan elementaire scalaire veldtypen en die aangeven [!DNL Platform] dat velden met hetzelfde XDM-gegevenstype zich op dezelfde manier gedragen. Dit gedrag kan worden vertrouwd om verenigbaar te zijn ongeacht waar de gegevens uit komen, of waarin de [!DNL Platform] dienst de gegevens wordt gebruikt.

Zie het [XDM-veldwoordenboek](field-dictionary.md) voor een volledige lijst met beschikbare XDM-velden. Het wordt aanbevolen om XDM-velden en gegevenstypen waar mogelijk te gebruiken ter ondersteuning van consistentie en standaardisering in de gehele [!DNL Experience Platform]regio.

## Compositievoorbeeld

De schema&#39;s vertegenwoordigen het formaat en de structuur van gegevens die in zullen worden opgenomen [!DNL Platform], en gebruikend een samenstellingsmodel worden gebouwd. Zoals eerder vermeld, zijn deze schema&#39;s samengesteld uit een klasse en nul of meer mengsels die met die klasse compatibel zijn.

Bijvoorbeeld, zou een schema beschrijvend aankopen die bij een detailhandel worden gemaakt &quot;Transacties van de[!UICONTROL Opslag]&quot;kunnen worden genoemd. Het schema implementeert de [!DNL XDM ExperienceEvent] klasse die wordt gecombineerd met de standaardmixin [!UICONTROL Handel] en een door de gebruiker gedefinieerde mix [!UICONTROL van Productinformatie] .

Een ander schema dat websiteverkeer volgt zou &quot;[!UICONTROL Webbezoeken]&quot;kunnen worden genoemd. Het voert ook de [!DNL XDM ExperienceEvent] klasse uit, maar deze keer combineert de standaardmixin van het [!UICONTROL Web] .

In het onderstaande diagram ziet u deze schema&#39;s en de velden die door elke mix worden ingebracht. Het bevat ook twee schema&#39;s die op de [!DNL XDM Individual Profile] klasse worden gebaseerd, met inbegrip van het schema &quot;[!UICONTROL Loyalty Leden]&quot;die eerder in deze gids wordt vermeld.

![](../images/schema-composition/composition.png)

### Samenvoegen {#union}

Terwijl [!DNL Experience Platform] u schema&#39;s voor bepaalde gebruiksgevallen kunt samenstellen, staat het u ook toe om een &quot;unie&quot;van schema&#39;s voor een specifiek klassentype te zien. Het vorige diagram toont twee schema&#39;s die op de klasse XDM ExperienceEvent en twee schema&#39;s worden gebaseerd die op [!DNL XDM Individual Profile] klasse worden gebaseerd. De samenvoeging, die hieronder wordt weergegeven, aggregeert de velden van alle schema&#39;s die dezelfde klasse ([!DNL XDM ExperienceEvent] respectievelijk [!DNL XDM Individual Profile]) delen.

![](../images/schema-composition/union.png)

Als u een schema inschakelt voor gebruik met [!DNL Real-time Customer Profile], wordt dit opgenomen in de union voor dat klassetype. [!DNL Profile] levert robuuste, gecentraliseerde profielen van klantenattributen evenals een timestamped rekening van elke gebeurtenis die de klant over om het even welk systeem heeft gehad dat met [!DNL Platform]wordt geïntegreerd. [!DNL Profile] gebruikt de verenigingsmening om deze gegevens te vertegenwoordigen en een holistische mening van elke individuele klant te verstrekken.

Voor meer informatie over het werken met [!DNL Profile], zie het [overzicht](../../profile/home.md)van het Profiel van de Klant In real time.

## Gegevensbestanden toewijzen aan XDM-schema&#39;s

Alle gegevensbestanden die in worden opgenomen [!DNL Experience Platform] moeten de structuur van een XDM-schema in acht nemen. Zie het document over [voorbeeld-ETL-transformaties](../../etl/transformations.md)voor meer informatie over hoe u gegevensbestanden kunt opmaken om te voldoen aan XDM-hiërarchieën (inclusief voorbeeldbestanden). Voor algemene informatie over het opnemen van gegevensbestanden in [!DNL Experience Platform], zie het [batch ingestion overzicht](../../ingestion/batch-ingestion/overview.md).

## Volgende stappen

Nu u de grondbeginselen van schemacompositie begrijpt, bent u bereid beginnen het onderzoeken en het bouwen van schema&#39;s gebruikend [!DNL Schema Registry].

Zie de volgende referentiedocumentatie voor een overzicht van de structuur van de twee belangrijkste XDM-klassen en hun algemeen gebruikte compatibele mixen:

* [[!DNL XDM Individual Profile]](../classes/individual-profile.md)
* [[!DNL XDM ExperienceEvent]](../classes/experienceevent.md)

Het [!DNL Schema Registry] wordt gebruikt om toegang te krijgen tot het [!DNL Schema Library] binnen Adobe Experience Platform en biedt een gebruikersinterface en RESTful-API die toegang bieden tot alle beschikbare bibliotheekbronnen. Het [!DNL Schema Library] bevat de middelen van de Industrie die door Adobe worden bepaald, de middelen van de Leverancier door [!DNL Experience Platform] partners, en klassen, mengen, gegevenstypes, en schema&#39;s worden bepaald die door leden van uw organisatie zijn samengesteld die.

Als u wilt beginnen met het samenstellen van een schema met behulp van de UI, volgt u de zelfstudie [van de](../tutorials/create-schema-ui.md) Schema-editor om het schema &quot;Loyalty-leden&quot; te bouwen dat in dit document wordt vermeld.

Als u de [!DNL Schema Registry] API wilt gaan gebruiken, begint u met het lezen van de ontwikkelaarsgids [van de](../api/getting-started.md)schemaregistratie-API. Na het lezen van de ontwikkelaarsgids, volg de stappen die in het leerprogramma worden geschetst over het [creëren van een schema gebruikend de Registratie API](../tutorials/create-schema-api.md)van het Schema.