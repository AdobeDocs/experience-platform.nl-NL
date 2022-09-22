---
title: Overzicht Adobe Target-extensie
description: Meer informatie over de tagextensie voor Adobe Target in Adobe Experience Platform.
exl-id: b1c5e25b-42ea-4835-b2d4-913fa2536e77
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 0%

---

# Overzicht Adobe Target-extensie

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## De Adobe Target-extensie configureren

>[!IMPORTANT]
>
> De Adobe Target-extensie vereist at.js. mbox.js wordt niet ondersteund.

Als de extensie Adobe Target nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensions > Catalog]**, plaatst u de cursor boven de doelextensie en selecteert u **[!UICONTROL Install]**.

Als u de extensie wilt configureren, opent u de [!UICONTROL Extensions] , plaatst u de cursor boven de extensie en selecteert u vervolgens **[!UICONTROL Configure]**.

![](../../../images/ext-target-config.png)

### at.js Settings

Al uw montages at.js, met uitzondering van de Onderbreking worden automatisch teruggewonnen van uw configuratie at.js in het gebruikersinterface van het Doel. De uitbreiding wint slechts montages van het Doel gebruikersinterface terug wanneer het eerst wordt toegevoegd, zodat zouden alle montages in de UI van de Inzameling van Gegevens moeten worden beheerd als de extra updates nodig zijn.

De volgende configuratieopties zijn beschikbaar:

#### Clientcode

De clientcode is de account-id van Target. Dit zou bijna altijd als standaardwaarde moeten worden verlaten.

Kan worden gewijzigd met gegevenselementen.

#### Organisatie-id

Deze id koppelt uw implementatie aan uw Adobe Experience Cloud-account. Dit zou bijna altijd als standaardwaarde moeten worden verlaten.

Kan worden gewijzigd met gegevenselementen.

#### Algemene naam van box

Toont de naam van uw globale verzoek van het Doel. Deze naam is standaard target-global-mbox, tenzij u de naam in de gebruikersinterface van het Doel hebt gewijzigd voordat u de extensie toevoegt.

Kan worden gewijzigd met gegevenselementen.

#### Serverdomein

Het domein waar de verzoeken van het Doel worden verzonden. Dit zou bijna altijd als standaardwaarde moeten worden verlaten.

#### Domein overschrijden

Bepaalt waar Doel cookies instelt in de browsers.

* **Uitgeschakeld:** Stelt de cookies alleen in op het domein van de eerste fabrikant. Dit is de standaardinstelling.
* **Ingeschakeld:** Stelt cookies in op zowel het eerste domein als het externe doeldomein (het &#39;serverdomein&#39;).

#### Time-out (ms)

Als de reactie van Doel niet binnen de bepaalde periode wordt ontvangen, de vraagtijden uit en de standaardinhoud wordt getoond. Tijdens de bezoekerssessie wordt nog steeds geprobeerd om aanvullende verzoeken in te dienen. Het gebrek is 3000ms, die van de Onderbreking verschillend zou kunnen zijn die in het gebruikersinterface van het Doel wordt gevormd.

Raadpleeg voor meer informatie over de werking van de instelling Time-out de optie [Adobe Target Help](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/deploy-at-js/implementing-target-without-a-tag-manager.html).

#### Andere at.js-instellingen beschikbaar in de gebruikersinterface van Doel

Verschillende instellingen die beschikbaar zijn op de [!UICONTROL Edit at.js settings] De pagina van Doel UI maakt geen deel uit van de uitbreiding van het Doel. Hier volgen enkele suggesties voor het uitvoeren van taken:

* Automatisch globale mbox maken Deze instelling wordt vervangen door de actie Globale mbox branden in de extensie Doel.
* Bibliotheekkop Deze instelling maakt geen deel uit van de doelextensie. Plaats code die voor at.js in een actie van de Uitbreiding van de Kern > van de Code van de Douane moet worden geladen alvorens de actie van het Doel van de Lading te gebruiken.
* Bibliotheekvoettekst Deze instelling maakt geen deel uit van de extensie Doel. Plaats code die na at.js in een actie van de Uitbreiding van de Kern > van de Code van de Douane na het gebruiken van de Actie van het Doel van de Lading moet worden geladen.

## Handelingstypen voor doelextensie

In deze sectie worden de actietypen beschreven die beschikbaar zijn in de extensie Doel.

De uitbreiding van het Doel verstrekt de volgende acties in Dan gedeelte van een regel:

### Doel laden

Voeg deze actie aan uw markeringsregel toe waar het zinvol is om Doel in de context van uw regel te laden. Hiermee wordt de bibliotheek at.js in de pagina geladen. In de meeste implementaties moet Doel op elke pagina van uw site worden geladen.

Er is geen configuratie nodig.

### Mbox-parameters toevoegen

Voeg parameters toe aan alle mbox-aanvragen. De handeling Doel laden moet eerder worden gebruikt.

1. Geef de naam en waarde op van de parameters die u wilt toevoegen.
1. Selecteer **plus (+)** om meer parameters toe te voegen.

### Globale Mbox-parameters toevoegen

Voeg alleen parameters toe aan uw algemene mbox-aanvragen. De handeling Doel laden moet eerder worden gebruikt.

1. Geef de naam en waarde op van de parameters die u wilt toevoegen.
1. Selecteer **plus (+)** om meer parameters toe te voegen.

### Globale standaardmap

Vuur het globale vakje op uw pagina. De handeling Doel laden moet eerder worden gebruikt.

Geef op of het verbergen van het lichaam moet worden ingeschakeld om flikkering te voorkomen en welke stijl wordt gebruikt wanneer het element van het lichaam wordt verborgen.

De volgende opties zijn beschikbaar:

* **Bodyhiding:** U kunt deze instelling in- of uitschakelen. De standaardwaarde is Enabled, wat betekent HTML BODY verborgen is.
* **Verborgen stijl hoofdtekst:** De standaardwaarde is `body{opacity:0}`. Deze waarde kan worden gewijzigd in iets anders, zoals `body{display:none}`.

Raadpleeg voor meer informatie de [Online Help-documentatie van Target](https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/mbox-implement/advanced-mboxjs-settings.html).

## Basisimplementatie van Adobe Target

Zodra de Uitbreiding van het Doel wordt geïnstalleerd, zult u minstens één regel moeten tot stand brengen om het behoorlijk op te stellen. U moet eerst de bibliotheek van het Doel (at.js) laden, de parameters specificeren u met globale mbox wilt gebruiken, en globale mbox in brand steken.

Een doelregel met deze basisimplementatie ziet er als volgt uit:

![](../../../images/basic_target_implementation.png)

Nadat u deze regel hebt opgeslagen, moet u deze toevoegen aan een bibliotheek en samenstellen/implementeren zodat u het gedrag kunt testen.

## Adobe Target-extensie met asynchrone implementatie

Tags kunnen asynchroon worden geïmplementeerd. Als u de tagbibliotheek asynchroon laadt met Doel erin, wordt Doel ook asynchroon geladen. Dit is een volledig gesteund scenario, maar er is één extra overweging die moet worden behandeld.

Bij asynchrone implementaties kan de pagina de standaardinhoud volledig renderen voordat de doelbibliotheek volledig is geladen en de inhoudsomwisseling heeft uitgevoerd. Dit kan leiden tot wat &quot;flikkering&quot;wordt genoemd waar de standaardinhoud kort verschijnt alvorens door de gepersonaliseerde inhoud wordt vervangen die door Doel wordt gespecificeerd. Als u deze flikkering wilt voorkomen, raden we u aan een voorverborgen fragment te gebruiken en de tagbundel asynchroon te laden om te voorkomen dat de inhoud gaat flikkeren.

Houd rekening met het volgende wanneer u het voorverborgen fragment gebruikt:

* Het fragment moet worden toegevoegd voordat de code voor de ingesloten koptekst van de tag wordt geladen.
* Deze code kan niet door markeringen worden beheerd, zodat moet het aan de pagina direct worden toegevoegd.
* De pagina wordt weergegeven wanneer de vroegste van de volgende gebeurtenissen plaatsvindt:
   * Wanneer de globale mbox-reactie is ontvangen
   * Wanneer de globale mbox-aanvraag uitvalt
   * Wanneer het fragment zelf een keer uitvalt
* De actie &quot;Globale box van de Vuur&quot;zou op alle pagina&#39;s moeten worden gebruikt die het pre-verbergende fragment gebruiken om de duur van het pre-verbergen te minimaliseren.

Het codefragment dat u vooraf verbergt, ziet er als volgt uit en kan worden geminificeerd. De configureerbare opties zijn aan het eind:

```javascript
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

Standaard wordt in het fragment het hele HTML-BODY verborgen. In sommige gevallen wilt u mogelijk alleen bepaalde HTML-elementen vooraf verbergen, en niet de hele pagina. U kunt dit bereiken door de stijlparameter aan te passen. Vervang de pagina door iets dat alleen bepaalde gebieden op de pagina vooraf verbergt.

Als u bijvoorbeeld twee gebieden hebt die worden aangeduid met ID&#39;s container-1 en container-2, kan de stijl worden vervangen door:

```css
#container-1, #container-2 {opacity: 0 !important}
```

In plaats van de standaardinstelling:

```css
body {opacity: 0 !important}
```

Het fragment wordt standaard uitgezet bij 3000 ms of 3 seconden. Deze waarde kan worden aangepast.
