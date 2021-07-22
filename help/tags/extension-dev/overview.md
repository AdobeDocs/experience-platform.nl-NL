---
title: Overzicht van extensieontwikkeling
description: In deze video ziet u de belangrijkste componenten van verschillende extensietypen en het ontwikkelingsproces voor extensies in Adobe Experience Platform.
source-git-commit: 421d1d0660c4c9c7280974f8a812a8f0e4f7cbea
workflow-type: tm+mt
source-wordcount: '1888'
ht-degree: 0%

---

# Overzicht van extensieontwikkeling

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een van de belangrijkste doelstellingen van Adobe Experience Platform is het maken van een open ecosysteem waar technici buiten het kerntechnische team extra functionaliteit kunnen blootstellen via tags. Dit wordt gedaan door markeringsuitbreidingen. Nadat een gebruiker een extensie op een eigenschap tag heeft geïnstalleerd, wordt de functionaliteit van die extensie beschikbaar voor gebruik door alle gebruikers van de eigenschap.

In dit document worden de primaire componenten van verschillende extensietypen beschreven en vindt u koppelingen voor verdere documentatie om u te begeleiden bij het ontwikkelingsproces van de extensie.

## Bibliotheekmodules

Bibliotheekmodules zijn stukken herbruikbare code die door een extensie worden geleverd en die worden uitgegeven in de runtimebibliotheek van de tag. Afhankelijk van of u een Webuitbreiding of een randuitbreiding ontwikkelt, zullen de beschikbare moduletypes en hun gebruiksgevallen verschillen. Raadpleeg de volgende subsecties voor een overzicht van de modules voor elk extensietype:

* [Modules voor webextensies](#web-modules)
* [Modules voor randextensies](#edge-modules)

### Modules voor webextensies {#web-modules}

In webextensies worden regels geactiveerd via gebeurtenissen, die vervolgens specifieke acties kunnen uitvoeren als aan een bepaalde set voorwaarden wordt voldaan. Zie het overzicht op [modulestroom in Webuitbreidingen](./web/flow.md) voor meer informatie.

Naast de [kernmodules](./web/core.md) die door Adobe worden verstrekt, kunt u de volgende types van bibliotheekmodule in uw Webuitbreidingen bepalen:

* [Gebeurtenistypen](#web-event)
* [Type voorwaarde](#web-condition)
* [Typen handelingen](#web-action)
* [Gegevenstelelementtypen](#web-data-element)
* [Gedeelde modules](#shared)

>[!NOTE]
>
>Zie [module format overview](./web/format.md) voor meer informatie over de vereiste indeling voor het implementeren van bibliotheekmodules in webextensies.

#### Gebeurtenistypen {#web-event}

Een regelgebeurtenis is een activiteit die moet optreden voordat een regel wordt geactiveerd.

Een extensie kan bijvoorbeeld een &quot;beweging&quot;-gebeurtenistype zijn dat controleert of een bepaalde muis- of aanraakbeweging plaatsvindt. Zodra de beweging voorkomt, zou de gebeurtenislogica de regel in brand steken.

Gebeurtenistypen bestaan doorgaans uit (1) een weergave die wordt weergegeven in de gebruikersinterface voor gegevensverzameling, waarmee gebruikers instellingen voor de gebeurtenis kunnen wijzigen en (2) een bibliotheekmodule die wordt uitgegeven in de tagruntime-bibliotheek om de instellingen te interpreteren en te controleren of een bepaalde activiteit plaatsvindt.

[Meer informatie](./web/event-types.md)

#### Type voorwaarde {#web-condition}

Een regelvoorwaarde wordt geëvalueerd nadat een regelgebeurtenis is opgetreden. Alle voorwaarden moeten waar terugkeren opdat de regel verder verwerkt. De uitzondering is wanneer de gebruikers uitdrukkelijk voorwaarden in een &quot;uitzondering&quot;emmer plaatsen in welk geval alle voorwaarden binnen het emmertje vals voor de regel moeten terugkeren om verwerking voort te zetten.

Een extensie kan bijvoorbeeld een voorwaardetype &#39;viewport contains&#39; weergeven waarin de gebruiker een CSS-kiezer kan opgeven. Wanneer de voorwaarde op de website van de cliënt wordt geëvalueerd, zou de uitbreiding elementen kunnen vinden die de CSS selecteur aanpassen en terugkeren of om het even welk van hen binnen viewport van de gebruiker bevat.

Voorwaardetypen bestaan doorgaans uit (1) een weergave die wordt weergegeven in de gebruikersinterface voor gegevensverzameling, waarmee gebruikers instellingen voor de voorwaarde kunnen wijzigen en (2) een bibliotheekmodule die wordt uitgegeven in de tagruntime-bibliotheek om de instellingen te interpreteren en een voorwaarde te evalueren.

[Meer informatie](./web/condition-types.md)

#### Typen handelingen {#web-action}

Een regelactie is iets dat wordt uitgevoerd nadat de regelgebeurtenis is voorgekomen en de voorwaarden evaluatie zijn overgegaan.

Een extensie kan bijvoorbeeld een actietype &#39;showsupport chat&#39; weergeven, dat een dialoogvenster voor supportchatten kan weergeven om gebruikers te helpen die problemen kunnen ondervinden bij het uitchecken.

Handelingstypen bestaan doorgaans uit (1) een weergave die wordt weergegeven in de gebruikersinterface voor gegevensverzameling, waarmee gebruikers instellingen voor de handeling kunnen wijzigen en (2) een bibliotheekmodule die wordt uitgegeven in de tagruntime-bibliotheek om de instellingen te interpreteren en een handeling uit te voeren.

[Meer informatie](./web/action-types.md)

#### Gegevenstelelementtypen {#web-data-element}

De elementen van gegevens zijn hoofdzakelijk aliassen aan stukken gegevens op een pagina ongeacht of die gegevens in de parameters van het vraagkoord, koekjes, DOM elementen, of één of andere andere andere plaats worden gevonden. Een gegevenselement kan door regels worden van verwijzingen voorzien en als abstractie voor de toegang tot van deze stukken van gegevens dienst doen. Wanneer de locatie van de gegevens in de toekomst verandert (bijvoorbeeld van de waarde `innerHTML` van een DOM-element in de waarde van een JavaScript-variabele), kan één gegevenselement opnieuw worden geconfigureerd, terwijl alle regels die naar dat gegevenselement verwijzen ongewijzigd kunnen blijven.

Een gegevenstype van het gegevenselement laat gebruikers toe om gegevenselementen te vormen om tot een stuk van gegevens op een bepaalde manier toegang te hebben. Een extensie kan bijvoorbeeld een gegevenstype ‘lokaal opslagitem’ leveren waarin de gebruiker een naam voor een lokaal opslagitem kan opgeven. Wanneer het gegevenselement door een regel van verwijzingen wordt voorzien, zou de uitbreiding de waarde van het lokale opslagpunt kunnen omhoog kijken door de lokale naam van het opslagpunt te gebruiken die de gebruiker had verstrekt toen het vormen van het gegevenselement.

De types van gegevenselement bestaan typisch uit (1) een mening die binnen UI van de Inzameling van Gegevens wordt getoond die gebruikers toestaat om montages voor het gegevenselement te wijzigen en (2) een bibliotheekmodule die binnen de markering runtime bibliotheek wordt uitgegeven om de montages te interpreteren en stukken van gegevens terug te winnen.

[Meer informatie](./web/data-element-types.md)

#### Gedeelde modules {#shared}

Een gedeelde module is een module die door één uitbreiding wordt blootgesteld die door een andere moet worden betreden. Dit kan een zeer nuttig mechanisme voor communicatie tussen uitbreidingen zijn. Zo kan Extension A bijvoorbeeld een stukje gegevens asynchroon laden en beschikbaar maken voor Extension B via een [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise).

Gedeelde modules worden opgenomen in de bibliotheek, zelfs wanneer ze nooit worden aangeroepen vanuit andere extensies. Als u de bibliotheekgrootte niet onnodig wilt vergroten, moet u voorzichtig zijn met wat u als gedeelde module beschikbaar maakt.

De gedeelde modules hebben geen meningscomponent.

[Meer informatie](./web/shared.md)

### Modules voor randextensies {#edge-modules}

In randuitbreidingen worden de regels geactiveerd door voorwaardencontroles, die vervolgens specifieke acties uitvoeren als die controles slagen. Zie het overzicht op [modulestroom in randuitbreidingen](./edge/flow.md) voor meer informatie.

U kunt uw eigen bibliotheekmodules definiëren in uw Edge-extensies. Deze kunnen in de volgende types worden gecategoriseerd:

* [Type voorwaarde](#condition)
* [Typen handelingen](#action)
* [Gegevenstelelementtypen](#data-element)

>[!NOTE]
>
>Voor details op het vereiste formaat voor het uitvoeren van bibliotheekmodules in randuitbreidingen, zie [moduleformaat overzicht](./edge/format.md).

#### Type voorwaarde {#condition}

Een regelvoorwaarde wordt geëvalueerd nadat een regelgebeurtenis is opgetreden. Alle voorwaarden moeten waar terugkeren opdat de regel verder verwerkt. De uitzondering is wanneer de gebruikers uitdrukkelijk voorwaarden in een &quot;uitzondering&quot;emmer plaatsen in welk geval alle voorwaarden binnen het emmertje vals voor de regel moeten terugkeren om verwerking voort te zetten.

Een extensie kan bijvoorbeeld een voorwaardetype &#39;viewport contains&#39; weergeven waarin de gebruiker een CSS-kiezer kan opgeven. Wanneer de voorwaarde op de website van de cliënt wordt geëvalueerd, zou de uitbreiding elementen kunnen vinden die de CSS selecteur aanpassen en terugkeren of om het even welk van hen binnen viewport van de gebruiker bevat.

Voorwaardetypen bestaan doorgaans uit (1) een weergave die wordt weergegeven in de gebruikersinterface voor gegevensverzameling, waarmee gebruikers instellingen voor de voorwaarde kunnen wijzigen en (2) een bibliotheekmodule die wordt uitgegeven in de tagruntime-bibliotheek om de instellingen te interpreteren en een voorwaarde te evalueren.

[Meer informatie](./web/condition-types.md)

#### Typen handelingen {#action}

Een regelactie is iets dat wordt uitgevoerd nadat de regelvoorwaarden de evaluatie hebben goedgekeurd.

Een extensie kan bijvoorbeeld een actietype &#39;showsupport chat&#39; weergeven, dat een dialoogvenster voor supportchatten kan weergeven om gebruikers te helpen die problemen kunnen ondervinden bij het uitchecken.

Handelingstypen bestaan doorgaans uit (1) een weergave die wordt weergegeven in de gebruikersinterface voor gegevensverzameling, waarmee gebruikers instellingen voor de handeling kunnen wijzigen en (2) een bibliotheekmodule die wordt uitgegeven in de tagruntime-bibliotheek om de instellingen te interpreteren en een handeling uit te voeren.

[Meer informatie](./web/action-types.md)

#### Gegevenstelelementtypen {#data-element}

De elementen van gegevens zijn hoofdzakelijk aliassen aan stukken gegevens op een pagina ongeacht waar dat gegeven binnen de gebeurtenis wordt gevonden die door de server wordt ontvangen. Een gegevenselement kan door regels worden van verwijzingen voorzien en als abstractie voor de toegang tot van deze stukken van gegevens dienst doen. Wanneer de locatie van de gegevens in de toekomst verandert (bijvoorbeeld de gebeurtenissleutel die de waarde bevat, wordt gewijzigd), kan één gegevenselement opnieuw worden geconfigureerd, terwijl alle regels die naar dat gegevenselement verwijzen, ongewijzigd kunnen blijven.

De types van gegevenselement bestaan typisch uit (1) een mening die binnen UI van de Inzameling van Gegevens wordt getoond die gebruikers toestaat om montages voor het gegevenselement te wijzigen en (2) een bibliotheekmodule die binnen de markering runtime bibliotheek wordt uitgegeven om de montages te interpreteren en stukken van gegevens terug te winnen.

[Meer informatie](./web/data-element-types.md)

## Extensieconfiguratie

De configuratie van een extensie verwijst naar de manier waarop algemene instellingen van een gebruiker worden verzameld. Bijvoorbeeld, overweeg een uitbreiding die de gebruiker toestaat om een baken te verzenden gebruikend een Send actie van het Baken en het baken moet altijd een rekeningsidentiteitskaart bevatten. We willen gebruikers niet lastig maken door hen elke keer om de account-id te vragen wanneer ze een handeling Send Beacon configureren. In plaats daarvan moet de extensie eenmaal om de account-id vragen vanuit de configuratieweergave van de extensie. Telkens wanneer een baken moet worden verzonden, kan de Send module van de de actielobiebibliotheek van het Baken rekeningsidentiteitskaart van de uitbreidingsconfiguratie trekken en het toevoegen aan het baken.

Wanneer gebruikers een extensie op een eigenschap tag installeren, wordt de weergave voor de extensieconfiguratie weergegeven. Ze kunnen de installatie van de extensie niet voltooien zonder de extensieconfiguratie te voltooien.

De extensieconfiguratie bestaat uit een weergavecomponent die instellingen exporteert die vervolgens als onbewerkte object worden uitgestraald in de runtimebibliotheek van de tag.

[Meer informatie](./configuration.md)

## Extensiestructuur

Een extensie bestaat uit een map met bestanden. Hieronder volgt een overzicht van de structuur van deze bestanden. Details over de bestandsinhoud vindt u in andere secties.

Een [`extension.json`](./manifest.md) dossier moet bij de wortel van de folder bestaan. In dit bestand wordt onder andere de samenstelling van de extensie beschreven en wordt aangegeven waar bepaalde bestanden zich in de map bevinden. Dit heeft sommige gelijkenissen met een [`package.json`](https://docs.npmjs.com/files/package.json) dossier in [npm](https://www.npmjs.com/).

Elke bibliotheekmodule (de logica die binnen de runtimebibliotheek van de tag moet worden uitgegeven) moet zijn eigen bestand zijn waarvan de inhoud voldoet aan de [CommonJS module standard](http://wiki.commonjs.org/wiki/Modules/1.1.1). Bijvoorbeeld, als wij een &quot;send baken&quot;actietype bouwen, moeten wij een dossier hebben dat de logica bevat die het baken verzendt. De inhoud van dit bestand wordt weergegeven in de runtimebibliotheek van de tag. U zou het `sendBeacon.js` kunnen roepen. De locatie van het bestand in de map is niet belangrijk, omdat `extension.json` de locatie van het bestand aangeeft.

Elke weergave moet een HTML-bestand zijn dat in een iframe in de tagtoepassing kan worden geladen. De weergave moet een script bevatten dat wordt geleverd door tags en moet voldoen aan een kleine API om te kunnen communiceren met de toepassing. Er gelden geen beperkingen ten aanzien van de bibliotheken die in uw weergaven worden gebruikt. Met andere woorden, u kunt jQuery-, onderstrepingsteken-, React-, Angular-, Bootstrap- of andere bibliotheken gebruiken. We hopen echter dat u uw extensie even opvallend zult maken voor de toepassing.

U wordt aangeraden alle weergavegerelateerde bestanden (HTML, CSS, JavaScript) in één submap te plaatsen die is gescheiden van de bibliotheekmodulebestanden. In `extension.json` zult u beschrijven waar deze meningssubdirectory wordt gevestigd. Platform zal deze subdirectory (en slechts deze subdirectory) van zijn Webservers dan dienen.
