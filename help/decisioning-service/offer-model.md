---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Het domeinmodel van de Beslissing van de aanbieding
topic: overview
translation-type: tm+mt
source-git-commit: fdaef24a23c1c1da064ca33e8bed522e506fead5

---


# Overzicht van het besluitvormingsdomeinmodel van de aanbieding

Het besluit van de aanbieding is een gebruiksgeval van de Dienst van Beslissing waarin u de regels en de voorspellingen formaliseert en centraal beheert die voor het in dienst nemen van klanten met aanbiedingen worden gebruikt. Beslissing van aanbiedingen wordt beschouwd als een type _**inhoudbeslissing**_. In dit geval worden de _**beslissingsopties**_ aangeduid als _**aanbiedingen**_ en worden zij als zodanig gekenmerkt door de inhoud die eraan is gehecht. Voor een inleiding van het objecten model dat door de Beslissende Dienst wordt gebruikt, gelieve te verwijzen naar het Model [van het Domein van de Dienst van de](experience-model.md)Beslissing.

Het doel is de eindgebruiker een &quot;beste voorstel&quot; te bieden in elk kanaal op basis van doelcriteria, kosten en frequentievereisten, alsmede eerdere interacties tussen kanalen, waaronder eerder voorgestelde aanbiedingen.

Net als bij alle gevallen waarin beslissingen worden genomen, worden de beslissingsopties (aanbiedingen) beheerd in een register dat door een willekeurig aantal toepassingen wordt gedeeld. De aanbiedingen zouden door verschillende afdelingen van uw organisatie of door partners kunnen worden gecreeerd, en die aanbiedingen zouden kunnen worden toegevoegd en worden verwijderd dagelijks.

Aanbiedingen worden visueel geplaatst in grotere ervaringen door de toepassing die de ervaring levert. _**Plaatsen**_, ook wel &#39;spts&#39; of &#39;slots&#39; genoemd, zijn belangrijke onderdelen voor het maken van een strategie. Het ontwerpen van een aanbiedingsstrategie begint vaak met de definitie van die stages. Een aanbieding heeft doorgaans meerdere _**inhoudrepresentaties**_ , zodat deze correct kan worden geïntegreerd in een groot aantal verschillende ervaringen, waarbij elke aanbieding een verschillende afmeting of andere beperkingen heeft en verschillende media-indelingen vereist.

Aanbiedingen houden vaak verband met fysieke goederen of diensten en er is een kostenberekening mee gemoeid. Een organisatie moet de middelen kunnen beperken die door aanbiedingen worden verbruikt en moet daarom het totale aantal _**keren dat een aanbod kan worden voorgesteld, kunnen beperken**_ .

De voorspelde waarde van een geaccepteerde aanbieding aan de organisatie is de optimalisatiecriteria en staat tegenover de kosten van een aanbieding. De kosten, de waarschijnlijkheid van aanvaarding en de voorspelde waarde worden gebruikt om de aanbiedingen te rangschikken. Het beste voorstel is het voorstel met de hoogst voorspelde positieve impact op de doelstellingen van je aanbiedingsactiviteiten.

Het Beslissen van de aanbieding overweegt de interactie een eindgebruiker, _**over vele kanalen**_ en toepassingen had, het hefboomwerkingen het profiel van een eindgebruiker en ervaringsgebeurtenisgegevens. Een callcentertoepassing kan bijvoorbeeld de Beslissing van de Aanbieding gebruiken om een aanbieding toe te laten of te onderdrukken die op aankopen wordt gebaseerd en revisies die door de eindgebruiker worden geplaatst; Of een e-mailbeheertoepassing kan afhankelijk zijn van de beslissing van de aanbieding om de volgende beste aanbieding te selecteren in een wekelijkse nieuwsbrief op basis van de browsergeschiedenis op een website.

Aanbiedingen hebben andere interessante eigenschappen. Vaak is er een bepaald _**schema**_ of een bepaald datum- en tijdbereik wanneer de aanbieding geldig is en wanneer de aanbieding ongeldig moet worden verklaard.

Tot slot wordt de aantrekkingskracht van een bod steeds verder verslechterd met de frequentie waarmee het wordt ingediend. Een voorstel dat na herhaalde indiening niet wordt aanvaard, is een gemiste kans omdat er een ander aanbod had kunnen worden gedaan. Daarom moet de _**vermoeidheid**_ van de eindgebruiker worden beheerd.

## Beslissingsstrategie in één oogopslag aanbieden

De algemene benadering is de selectie van Aanbiedingen te beperken tot alle beperkingen worden voldaan, dan het Rangschikkende model op de resterende Opties toe te passen, en dan over veelvoudige activiteiten te optimaliseren gebruikend Afdekkende Beperkingen (deduplicatie &amp; vermijding van fallback keuzen).

| Strategische component | Gerealiseerd als |
| --- | --- |
| Beslissingsactiviteiten | Aanbiedingsactiviteiten |
| Beslissingsopties | Aanbieden met weergaven van inhoud |
| Opties voor alternatieven | Fallback-aanbieding met weergave van inhoud |
| Voltooide set beslissingsopties | Overzicht van aanbiedingen (ook bekend als aanbiedingsbibliotheek) |
| Topcategorieën | Het filter van de aanbieding die op markeringen en aanbiedingsidentificateurs wordt gebaseerd |
| Uitvoer van besluiten | Voorstel voor één aanbieding per activiteit, voor meerdere activiteiten tegelijk |
| Beslissingsresultaten | Verwachte ervaringsgebeurtenis met betrekking tot de aanbieding, bv. `eventType='opened'` |
| Beslissingsalgoritme | Interne servicelogica, parameters |
| Restricties | Plaatsingsbeperkingen, kalenderbeperkingen, beperkingen van het globale en per gebruiker maximum, de beperkingen van de deduplicatie |
| Besluitvormingsregels | Subsidiabiliteitsregels |
| Model voor *verwacht hulpprogramma* | Offerte of prioriteit |

Het totale aantal aanbiedingen in de inventaris van opties is doorgaans vrij groot (in de orde van 10.000) en elke aanbiedingsactiviteit kan worden geconcentreerd op aanbiedingen die in een verschillende categorie (onderwerp) vallen. Met de strategie voor het nemen van voorstellen kunt u een aanbiedingsfilter toevoegen aan een aanbiedingsactiviteit. Extra beperkingen zullen worden geëvalueerd op het moment dat het besluit wordt gevraagd.
De volgende secties verklaren de componenten voor het domein van de Beslissing van de Aanbieding in detail.

## Algemene aanbiedingen

Algemene aanbiedingen, ook wel gepersonaliseerde aanbiedingen genoemd, zijn de opties die centraal staan bij de besluitvorming over aanbiedingen. Ze hebben kenmerken zoals naam en status. Het kenmerk status geeft aan of de entiteit gereed is om te worden opgenomen in de lijst met actieve goedgekeurde aanbiedingen. Aan algemene aanbiedingen worden verschillende beperkingen toegevoegd. Meer over dit in sectie ‎ Beperkingen [hieronder](#offer-constraints).

## Inhoud in voorstellen

### Plaatsingen voorstellen

Plaatsen definiëren inhoudsbeperkingen en worden gebruikt met een activiteit om de plaats te bepalen waar de volgende beste ervaring wordt geleverd. Dit vermindert verder het aantal opties dat in overweging kan worden genomen en is een andere beperking die door de activiteit wordt opgelegd. Dit wordt de plaatsingsbeperking genoemd. Alleen opties met inhoud die voldoet aan een plaatsingsbeperking, zoals aanbiedingen, worden in overweging genomen. Dit wordt geëvalueerd in de beginstadia van de besluitvormingsstrategie. Wanneer optieobjecten de plaatsingsbeperkingen van elke activiteit wijzigen, worden deze opnieuw geëvalueerd en kan de optie voor een of meer activiteiten in aanmerking worden genomen of eruit vallen.

Het is niet de verantwoordelijkheid van de beslissingsdienst om de complexe details van inhoudsafhankelijkheden te formaliseren. In plaats daarvan identificeert elke client de lijst met plaatsingen op alle kanalen en geeft deze plaatsingen unieke id&#39;s en namen. Door naar een bepaalde plaatsing te verwijzen, beweert de ontwerper dat de bepaalde inhoud in de plaatsing zal passen.

Wanneer de inhoud wordt ontwikkeld zal de aanbiedingsteller en de inhoudsontwerper eenvoudig (moeten) overeenkomen over een &quot;impliciet contract&quot;dat achter de naam &quot;het Beeld van de Hero van de Homepage&quot;of &quot;het Openende Manuscript van de Vraag van de Dienst&quot;plaatst. Het eerste object kan worden overeengekomen als een afbeelding met een breedte van 600 px en een hoogte van 350 px. In het laatste geval kan de inhoud worden beperkt tot tekst in twee taalvarianten die niet meer dan 50 woorden in drie of vier zinnen met een semantische structuur zijn. Plaatsing om niet alle betekenis van het verborgen contract op te slaan.

### Voorstelling

Om ervoor te zorgen dat een aanbieding correct in de variërende parameters van de plaatsing in uw kanalen kan worden voorgesteld, moeten verschillende vertegenwoordiging van dat aanbod worden gecreeerd. De inhoud die wordt gekoppeld aan aanbiedingen, wordt gegroepeerd per plaatsing. Elk aanbod kan een of meer representaties hebben waarbij elk van deze vertegenwoordigingen verwijst naar een van de gedefinieerde plaatsingen. Elke vertegenwoordiging in een aanbieding moet een verschillende plaatsing gebruiken. Hoe meer vertegenwoordigingen een aanbieding heeft, des te meer mogelijkheden er zijn om het aanbod in een andere plaatsingscontext te gebruiken.

Een Plaatsing beperkt het type van inhoudspunten die aan de Vertegenwoordiging kunnen worden toegevoegd.

## Extra aanbiedingen

De aanbiedingen van de reserve zijn besluitvormingsopties die geen extra beperkingen behalve de plaatsingsregels hebben. Voor alternatieven zijn inhoudrepresentaties gekoppeld aan plaatsingen, net als voor andere aanbiedingen.

In activiteiten worden alternatieven gespecificeerd om een bruikbare ervaring met inhoud aan te geven wanneer gecombineerde beperkingen alle vernauwde-downopties uitschakelen. Omdat deze niet afhankelijk is van de runtime-context of het profiel, kan de plaatsingsbeperking vooraf worden gecontroleerd wanneer de activiteit wordt samengesteld. Met behulp van fallback-aanbiedingen is er altijd een antwoord op de vraag: Wat is momenteel de beste aanbieding?

## Restricties voorstel

### Kalenderbeperkingen

In het biedingsbeslissingsdomein hebben de aanbiedingen een geldigheidsperiode. Dit betekent dat de aanbieding niet kan worden voorgesteld vóór de begindatum en het tijdstip ervan en niet langer na de einddatum en -tijd kan worden voorgesteld. De biedende entiteit heeft een eenvoudige structuur die deze kalenderbeperkingen definieert.

Periodiek worden verlopen voorstellen verwijderd uit de lijst met overwogen opties. Het kalenderfilter wordt echter toegepast op het moment dat de beslissing wordt gevraagd, zodat de beperkingen nauwkeurig worden toegepast.

### Beperkingen voor plafonds

Aanbiedingen kunnen een optionele begrenzing hebben. Het bestaat uit twee waarden:

- De algemene waarde voor de limiet bepaalt hoe vaak een aanbieding kan worden voorgesteld voor de gehele profielset (doelgroep).

- De begrenzing per profiel en bepaalt hoe vaak die Aanbieding aan het zelfde profiel kan worden voorgesteld.

### Duplicatiebeperkingen

Wanneer een beslissing wordt gevraagd, kan de cliënt verzoeken om voorstellen voor meerdere activiteiten tegelijk. Dit is een typisch scenario in inhoudsbesluit. Elke activiteit draagt één of meerdere inhoudsopties aan de algemene ervaring bij. Wegens het compositieaspect, moeten de besluiten over activiteiten bemiddelen om dubbel werk te vermijden - tenzij de activiteiten elk een van onsamenhangende ondergroep van de algemene optiecontrole kiezen. Een topoptie zal waarschijnlijk in alle activiteiten hoog op de ranglijst staan en het zou een slechte ervaring zijn als alle activiteiten dezelfde optie zouden voorstellen. Anderzijds, als een leveringssysteem wil weten wat de Volgende Beste Omzetting over alle kanalen is en er geen maximum beperking is, kan het goed zijn om de zelfde optie over verschillende activiteiten voor te stellen.

Er worden momenteel geen dubbele beperkingen naar de opslagplaats voor zakelijke objecten geschreven. In plaats daarvan is deduplicatie de standaardstrategie bij uitvoering. Een verzoekparameter kan het standaardgedrag met voeten treden om de-duplicatiestap te onderdrukken.

### Profielbeperkingen - Subsidiabiliteitsregels

Tot dusverre zijn de hier besproken beperkingen van toepassing, ongeacht voor wie de selectie van de aanbiedingen is bedoeld. Het Beslissen van de ervaring steunt ook een gebruiksgeval waarin het personaliseren van voorstellen op het verslag en de tijdreeksgebeurtenissen van een klant gebaseerd zijn. De regels worden geëvalueerd per profiel, om te beslissen als een aanbieding voor die gebruiker kwalificeert of moet worden onderdrukt. Om dat te doen, kan een toelatingsregel met elke aanbieding worden geassocieerd. Naast het profiel en de ervaringsgebeurtenissen van een eindgebruiker zal de geschiktheidsregel contextgegevens in real time in aanmerking nemen. Deze gegevens worden door de leveringsdienst verstrekt en kunnen de vorm aannemen van gegevens die geen verband houden met een profiel zoals inventarisniveaus, weersomstandigheden en vluchtschema&#39;s.

Het is belangrijk onderscheid te maken tussen richtings- en segmentatieregels en tussen subsidiabiliteits- en prioriteitsregels voor besluitvorming. Voor het opgeven van een reeks profielen wordt de uitvoer (selectie van het publiek) als geschiktheidscategorie gebruikt. Een set opties (toegestane aanbiedingen) is de uitvoer van de evaluatie.

## Verzamelingen voorstellen

De inventarisatie is de totale groep opties die in aanmerking worden genomen voor de besluitvorming. De inventaris kan verder worden onderverdeeld in categorieën of verzamelingen. Een verzameling opties wordt vertegenwoordigd door een gemeenschappelijke tag die deze opties hebben. Filters worden gebruikt om te testen of aanbiedingen tot een bepaalde categorie behoren of, meer specifiek, dezelfde tag of tags delen.

### Tags

Met labels kunt u aangeven dat een groep opties tot een categorie behoort.

Een optie kan uit meerdere tags bestaan en kan daarom in meerdere categorieën tegelijk voorkomen. Categorieën kunnen elkaar ook overlappen of een andere categorie bevatten. Wanneer een categorie &quot;S&quot; wordt gedefinieerd door aanbiedingen met het label &quot;A&quot; en de categorie &quot;R&quot; wordt gedefinieerd door opties met zowel label &quot;A&quot; als &quot;B&quot;, is &quot;S&quot; een superset van &quot;R&quot;.

### Filters

Filters worden gebruikt om de criteria te definiëren voor een set opties die tot een categorie behoren. Filters kunnen worden beschouwd als query&#39;s op de lijst met algemene aanbiedingen. Er zijn twee manieren waarop u een filter kunt maken: door te verklaren dat een aanbieding één of meerdere markeringen heeft en door de reeks aanbiedingen uitdrukkelijk te selecteren. De eerste methode kan worden gevormd om te verklaren dat een aanbieding in die inzameling alle gespecificeerde markeringen moet hebben of dat een optie kwalificeert wanneer het minstens één van de gespecificeerde markeringen heeft.

Wanneer opties expliciet in een verzameling worden geplaatst, wordt de tagset genegeerd voor die verzameling.

## Aanbiedingsactiviteiten

De activiteiten vormen en controleren het besluitvormingsproces. Momenteel is de beslissingsstrategie hoofdzakelijk vooraf bepaald, maar in toekomstige versies van het domeinmodel voor de besluitvorming van het aanbod zal de keuze van modellen, aanvullende regels en beperkingen mogelijk zijn.

Een ervaring kan worden samengesteld gebruikend vele activiteiten gelijktijdig. Op dit moment kunnen maximaal 30 activiteiten in één beslissingsverzoek worden behandeld. Als meer dan 30 activiteiten of slots in een ervaring met inhoud moeten worden gevuld, kunnen meerdere aanvragen voor hetzelfde profiel worden ingediend. Wanneer in hetzelfde verzoek om een besluit activiteiten worden opgenomen, worden de voorstellen tot het aanbieden van een aanbod onder die activiteiten gededupliceerd.

Als activiteiten zodanig worden gedefinieerd dat zij uit een gescheiden reeks aanbiedingen kiezen, maakt het weinig uit of activiteiten in hetzelfde verzoek worden gecombineerd of in afzonderlijke verzoeken worden opgesplitst. Maar, netwerk en reactietijdbeperkingen kunnen vereisen combinerend activiteiten in het zelfde verzoek. Aangezien de verschillende verzoeken aan verschillende de dienstknopen kunnen worden verpletterd, kunnen de zelfde profielgegevens in verschillende knopen moeten worden gehaald. Dit vermindert de efficiënte bandbreedte IO beschikbaar voor andere verzoeken.

Activiteiten worden gebruikt om inhoud in te voegen in een ervaring. Om ervoor te zorgen (niet om ervoor te zorgen) dat de inhoudsitems correct &quot;passen&quot;, verwijst een activiteit naar één plaatsing. Een plaatsing is niet altijd een concrete plaats/sleuf, maar eerder een abstractie van deze plaatsen/slots. Op een webpagina met een raster van tegels kan bijvoorbeeld voor elk element dezelfde plaatsing gelden, mits alle elementen dezelfde vorm en grootte hebben en vergelijkbare inhoud kunnen bevatten. Een afzonderlijke tegel zou echter doorgaans door eigen activiteit worden geleverd.

In de volgende afbeelding ziet u hoe de bedrijfsentiteiten met elkaar verwant zijn:

![](./images/figure-10.png)

Wanneer clients de objectgrafiek voor beslissingen maken en koppelen, zijn er doorgaans drie verschillende werkstromen. Deze zijn als volgt:

- De ondersteunende entiteiten zoals tags en plaatsingen instellen. Deze entiteiten worden gebruikt om andere entiteiten te structureren, filteren en groeperen. Zij worden ook gebruikt om enige coördinatie tussen de tweede en derde werkstroom te verstrekken. Deze workflow vormt een eerste stap, maar op elk gewenst moment kan de installatie worden verfijnd. Tags zijn relatief eenvoudig, maar de plaatsing vereist een beetje meer planning. Een bedrijf moet ten minste een inventarisatie maken van alle plaatsen waar een besluit wordt gepresenteerd.

- Het creëren van aanbiedingen met de diverse vertegenwoordiging en bedrijfsregels (beperkingen). Deze centrale werkstroom biedt de opties waaronder we de beste moeten selecteren. De labels van de eerste workflow worden gebruikt om aanbiedingen te categoriseren en de plaatsingen worden gebruikt om aan te geven welke opties kunnen worden weergegeven en waar.

   - Deze workflow definieert ook absolute beperkingen voor de aanbiedingen. Ze zijn absoluut omdat ze altijd zullen worden afgedwongen en niet alleen van invloed zijn op de rangorde tussen een reeks aanbiedingen. Wanneer bijvoorbeeld een kalenderbeperking wordt ingesteld, wordt afgedwongen dat de aanbieding nooit wordt geselecteerd vóór de ingestelde begindatum/tijd en nooit na de einddatum/tijd. De beperkingen die in deze werkstroom zullen worden geplaatst zijn de [kalenderbeperkingen](#calendar-constraints), [plafondbeperkingen](#capping-constraints) en [geschiktheidsbeperkingen](#profile-constraints---eligibility-rules). Een subwerkstroom hier is de definitie van extra regels die bepalen wie in aanmerking komt om een bepaalde aanbieding te ontvangen.

      - Tegelijk worden de beperkingen gecreeerd voor een aanbieding, worden zijn vertegenwoordiging geselecteerd. In deze workflow wordt ervan uitgegaan dat de inhoud al ergens is gemaakt en eenvoudig wordt geüpload naar en opgehaald uit de opslagplaats voor inhoud. Hier zijn de plaatsingen van de eerste werkstroom in werking gesteld. Een aanbieding kan plaatsingen selecteren en de inhoud onder die [plaatsing](#offer-placements)associëren.

      - Het maken van geschikte fallback-aanbiedingen is de laatste stap in deze workflow. Een fallback-aanbod is erg vergelijkbaar met een algemeen aanbod zonder beperkingen.

- De laatste workflow heeft betrekking op het maken van activiteiten. Deze stap vindt echter niet noodzakelijkerwijs opeenvolgend plaats na de workflow om aanbiedingen te maken. Beide processen zijn aan de gang en gelijktijdig. De activiteiten worden gebruikt om de reikwijdte van de opties per onderwerp en per plaats te beperken waar de besluiten worden voorgesteld. Een activiteit verwijst naar een [verzameling](#offer-collections) en een plaatsing. Het moet ook een [terugvalaanbieding](#fallback-offers) specificeren die wordt gebruikt in gevallen waarin een kwalificerende aanbieding niet kan worden bepaald.

