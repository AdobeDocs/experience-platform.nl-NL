---
title: Overzicht van Adobe Target v2-extensie
description: Meer informatie over de Adobe Target v2-tagextensie in Adobe Experience Platform.
exl-id: 8f491d67-86da-4e27-92bf-909cd6854be1
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1298'
ht-degree: 0%

---

# Overzicht van Adobe Target v2-extensie

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## De Adobe Target v2-extensie configureren

>[!IMPORTANT]
>
>De Adobe Target-extensie vereist At.js 2.x.

Als de Adobe Target-extensie nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]** , plaatst u de cursor boven de Target-extensie en selecteert u **[!UICONTROL Install]** .

Als u de extensie wilt configureren, opent u het tabblad Extensies, plaatst u de muisaanwijzer op de extensie en selecteert u **[!UICONTROL Configure]** .

![](../../../images/targetv2config.png)

### at.js-instellingen

Al uw montages at.js, met uitzondering van de Onderbreking, worden automatisch teruggewonnen van uw configuratie at.js in het Doel UI. De uitbreiding wint slechts montages van het Doel UI terug wanneer het eerst wordt toegevoegd, zodat zouden alle montages in UI moeten worden beheerd als de extra updates nodig zijn.

De volgende configuratieopties zijn beschikbaar:

#### Clientcode

De clientcode is de account-id van Target. Dit zou bijna altijd als standaardwaarde moeten worden verlaten. Deze kan worden gewijzigd met behulp van gegevenselementen.

#### Organisatie-ID

Deze id koppelt uw implementatie aan uw Adobe Experience Cloud-account. Dit zou bijna altijd als standaardwaarde moeten worden verlaten. Deze kan worden gewijzigd met behulp van gegevenselementen.

#### Serverdomein

Het serverdomein verwijst naar het domein waar de verzoeken van het Doel worden verzonden. Dit zou bijna altijd als standaardwaarde moeten worden verlaten.

#### GDPR Opt-In

Als deze optie is ingeschakeld, biedt Adobe Target aanmeldingsfunctionaliteit waarmee u uw strategie voor het beheer van uw toestemming kunt ondersteunen. Met de functie Inschakelen kunnen klanten bepalen hoe en wanneer de tag Doel wordt geactiveerd.  Voor meer informatie over Adobe Opt-binnen, zie [&#x200B; Privacy en Algemene Verordening van de Bescherming van Gegevens (GDPR) &#x200B;](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=nl-NL).

#### Time-out (ms)

Als de reactie van Doel niet binnen de bepaalde periode wordt ontvangen, de vraagtijden uit en de standaardinhoud wordt getoond. Tijdens de bezoekerssessie wordt nog steeds geprobeerd om aanvullende verzoeken in te dienen. Het gebrek is 3000ms, die van de Onderbreking verschillend zou kunnen zijn die in het gebruikersinterface van het Doel wordt gevormd.

Voor meer informatie over hoe de Onderbreking het plaatsen van de Onderbreking werkt, verwijs naar de [&#x200B; hulp van Adobe Target &#x200B;](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html?lang=nl-NL).

## Handelingstypen voor doelextensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Doel.

De uitbreiding van het Doel verstrekt de volgende acties in Dan gedeelte van een regel:

### Doel laden

Voeg deze actie aan uw markeringsregel toe waar het zinvol is om Doel in de context van uw regel te laden. Hiermee wordt de bibliotheek at.js in de pagina geladen. In de meeste implementaties moet Doel op elke pagina van uw site worden geladen. Adobe raadt aan de handeling Doel laden alleen te gebruiken als deze wordt voorafgegaan door een doelaanroep. Anders, zou u op kwesties zoals de vraag van Analytics kunnen lopen die wordt vertraagd.

Er is geen configuratie nodig.

### Doel laden met apparaatbeslissingen

Voeg deze actie aan uw markeringsregel toe waar het zinvol is om Doel met [&#x200B; op-apparatenbeslissing &#x200B;](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/on-device-decisioning/on-device-decisioning.html?lang=nl-NL) te laden die in de context van uw regel wordt toegelaten. Hierdoor wordt de bibliotheek at.js geladen met apparaatbesluitvorming ingeschakeld op de pagina. In de meeste implementaties moet Doel op elke pagina van uw site worden geladen. Adobe adviseert gebruikend het Doel van de Lading met op-apparaat beslissingsactie slechts als het door een vraag van het Doel wordt voorafgegaan. Anders, zou u op kwesties zoals de vraag van Analytics kunnen lopen die wordt vertraagd.

>[!IMPORTANT]
>
>Gebruik alleen een verzoek om pagina te laden met een beslissing op het apparaat als dit al is geconfigureerd. Als u deze handeling aan uw regel toevoegt, wordt de definitieve opstarthakkel groter omdat deze de engine voor de beslissingsregels voor apparaten bevat.

### Params toevoegen aan alle aanvragen

Dit handelingstype staat parameters toe om aan alle verzoeken van het Doel worden toegevoegd. De handeling Doel laden moet eerder worden gebruikt.

1. Geef de naam en waarde op van de parameters die u wilt toevoegen.
1. Selecteer het pictogram Toevoegen om meer parameters toe te voegen.

### Params toevoegen aan verzoek om pagina te laden

Met dit actietype kunnen parameters specifiek aan de laadaanvragen van de pagina worden toegevoegd. De handeling Doel laden moet eerder worden gebruikt.

1. Geef de naam en waarde op van de parameters die u wilt toevoegen.
1. Selecteer het pictogram Toevoegen om meer parameters toe te voegen.

### Aanvraag voor laden van brandbluspagina

Met dit actietype kan Target een aanvraag uitvoeren wanneer de pagina wordt geladen. De handeling Doel laden moet eerder worden gebruikt.

U moet opgeven of het verbergen van het lichaam moet worden ingeschakeld om flikkering te voorkomen en welke stijl wordt gebruikt wanneer het element van het lichaam wordt verborgen. De volgende opties zijn beschikbaar:

* **Bodyverbergen:** u kunt dit het plaatsen toelaten of onbruikbaar maken. De standaardwaarde is Enabled, wat betekent dat de HTML BODY verborgen is.
* **Verborgen Stijl van het Lichaam:** de standaardwaarde is lichaam {opacity:0}. Deze waarde kan in iets verschillend, zoals lichaam {display:none} worden veranderd.

Voor meer informatie, verwijs naar de [&#x200B; online hulpdocumentatie van het Doel &#x200B;](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html?lang=nl-NL).

### Triggerweergave

De actie Weergave activeren kan worden aangeroepen wanneer een nieuwe pagina wordt geladen of wanneer een component op een pagina opnieuw wordt weergegeven. De triggerweergave moet worden geïmplementeerd voor toepassingen van één pagina.

1. Geef de weergavenaam op die moet worden geactiveerd.
1. Geef aan of de weergave moet worden geactiveerd door het selectievakje Pagina in te schakelen. Als de weergave is gecorreleerd aan een component die opnieuw wordt weergegeven en niet aan een indruk voor rapportage wordt toegewezen, schakelt u het selectievakje Pagina niet in.

Raadpleeg de [`triggerView()` Help-documentatie &#x200B;](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/functions-overview/adobe-target-triggerview-atjs-2.html?lang=nl-NL) voor meer informatie over het activeren van een weergave.

## Basisimplementatie van Adobe Target

Nadat de doelextensie is geïnstalleerd, maakt u ten minste één regel om deze correct te implementeren. Eerst moet u de doelbibliotheek (at.js) laden, de parameters opgeven die u wilt gebruiken met de aanvraag voor het laden van de pagina en de aanvraag voor het laden van de pagina uitvoeren.

Een doelregel met deze basisimplementatie ziet er als volgt uit:

![](../../../images/targetv2deploy.png)

Nadat u deze regel hebt opgeslagen, zult u het aan een Bibliotheek moeten toevoegen en bouwt/opstelt het zodat u het gedrag kunt testen.

## Adobe Target-extensie met asynchrone implementatie

Tags kunnen asynchroon worden geïmplementeerd. Als u de tagbibliotheek asynchroon laadt met Doel erin, wordt Doel ook asynchroon geladen. Dit is een volledig gesteund scenario, maar er is één extra overweging die moet worden behandeld.

Bij asynchrone implementaties is het mogelijk dat de pagina de rendering van de standaardinhoud voltooit voordat de doelbibliotheek volledig is geladen en de inhoudswisseling heeft uitgevoerd. Dit kan leiden tot wat &quot;flikkering&quot;wordt genoemd waar de standaardinhoud kort verschijnt alvorens door de gepersonaliseerde inhoud wordt vervangen die door Doel wordt gespecificeerd. Als u deze flikkering wilt voorkomen, raden we u aan een voorverborgen fragment te gebruiken en de tagbundel asynchroon te laden om te voorkomen dat de inhoud gaat flikkeren.

Houd rekening met het volgende wanneer u het voorverborgen fragment gebruikt:

* Het fragment moet worden toegevoegd voordat de code voor de ingesloten koptekst van de tag wordt geladen.
* Deze code kan niet door markeringen worden beheerd, zodat moet het aan de pagina direct worden toegevoegd.
* De pagina wordt weergegeven wanneer de vroegste van de volgende gebeurtenissen plaatsvindt:
   * Wanneer de pagina is geladen
   * Wanneer de pagina de aanvraagtijden uit laadt
   * Wanneer het fragment zelf een keer uitvalt
* De actie &quot;Vuurpagina laden&quot; moet op alle pagina&#39;s worden gebruikt met het voorverborgen fragment om de duur van het voorverbergen te minimaliseren.
* Het verbergen van de hoofdtekst moet ook worden ingeschakeld in de handeling Aanvraag voor laden pagina in de regel voor het laden van de pagina die u voor Doel gebruikt. Als dit niet het geval is, blijven alle paginalading verborgen gedurende de time-outperiode.

Het codefragment dat u vooraf verbergt, ziet er als volgt uit en kan worden geminificeerd. De configureerbare opties zijn aan het eind:

```js
;(function(win, doc, style, timeout) {
  var STYLE_ID = 'at-body-style';

  function getParent() {
    return doc.getElementsByTagName('head')[0];
  }

  function addStyle(parent, id, def) {
    if (!parent) {
      return;
    }

    var style = doc.createElement('style');
    style.id = id;
    style.innerHTML = def;
    parent.appendChild(style);
  }

  function removeStyle(parent, id) {
    if (!parent) {
      return;
    }

    var style = doc.getElementById(id);

    if (!style) {
      return;
    }

    parent.removeChild(style);
  }

  addStyle(getParent(), STYLE_ID, style);
  setTimeout(function() {
    removeStyle(getParent(), STYLE_ID);
  }, timeout);
}(window, document, "body {opacity: 0 !important}", 3000));
```

Standaard wordt in het fragment de hele HTML-instantie vooraf verborgen. In sommige gevallen wilt u mogelijk alleen bepaalde HTML-elementen vooraf verbergen, en niet de hele pagina. U kunt dit bereiken door de stijlparameter aan te passen. Vervang de pagina door iets dat alleen bepaalde gebieden op de pagina vooraf verbergt.

Als u bijvoorbeeld twee gebieden hebt die worden aangeduid met ID&#39;s container-1 en container-2, kan de stijl worden vervangen door:

```css
#container-1, #container-2 {opacity: 0 !important}
```

In plaats van de standaardinstelling:

```css
body {opacity: 0 !important}
```

Het fragment wordt standaard uitgezet bij 3000 ms of 3 seconden. Deze waarde kan worden aangepast.
