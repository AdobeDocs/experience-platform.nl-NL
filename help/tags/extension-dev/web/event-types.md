---
title: Gebeurtenistypen voor webextensies
description: Leer hoe u een bibliotheekmodule voor het type gebeurtenis definieert voor een webextensie in Adobe Experience Platform.
exl-id: dbdd1c88-5c54-46be-9824-2f15cce3d160
source-git-commit: 0c2ee3bbb4d85bd755b4847a509fc7bd50ba67bc
workflow-type: tm+mt
source-wordcount: '1048'
ht-degree: 0%

---

# Gebeurtenistypen voor webextensies

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

In een labelregel is een gebeurtenis een activiteit die moet plaatsvinden voordat een regel kan worden geactiveerd. Een webextensie kan bijvoorbeeld een &#39;gebaargebeurtenis&#39; leveren die controleert of een bepaalde muis- of aanraakbeweging plaatsvindt. Zodra de beweging voorkomt, zou de gebeurtenislogica de regel in brand steken.

Een module van de gebeurtenistype bibliotheek wordt ontworpen om te ontdekken wanneer een activiteit gebeurt en dan een functie te roepen om een bijbehorende regel in brand te steken. De gebeurtenis die wordt gedetecteerd, kan worden aangepast. Bijvoorbeeld, kon ontdekken wanneer een gebruiker een bepaalde beweging maakt, snel scrolt, of met iets in wisselwerking staat.

In dit document wordt beschreven hoe u gebeurtenistypen voor een webextensie in Adobe Experience Platform definieert.

>[!NOTE]
>
>In dit document wordt ervan uitgegaan dat u bekend bent met bibliotheekmodules en hoe deze zijn geïntegreerd in webextensies. Zie het overzicht op [Opmaak van de module Bibliotheek](./format.md) een inleiding tot de uitvoering ervan voordat wordt teruggekomen op deze handleiding.

Gebeurtenistypen worden gedefinieerd door extensies en bestaan doorgaans uit de volgende kenmerken:

1. A [weergave](./views.md) weergegeven in de gebruikersinterface voor gegevensverzameling waarin gebruikers instellingen voor de gebeurtenis kunnen wijzigen.
2. Een bibliotheekmodule die wordt uitgegeven in de tagruntime-bibliotheek om de instellingen te interpreteren en te controleren of een bepaalde activiteit plaatsvindt.

`module.exports` beide `settings` en `trigger` parameters. Dit maakt het aanpassen van het gebeurtenistype mogelijk.

```js
module.exports = function(settings, trigger) { … };
```

| Parameter | Beschrijving |
| --- | --- |
| `settings` | Een object dat de instellingen bevat die de gebruiker in de weergave van het gebeurtenistype heeft geconfigureerd. U hebt de uiteindelijke controle over wat er in dit object gebeurt. |
| `trigger` | Een functie die de module moet aanroepen wanneer de regel moet worden geactiveerd. Er bestaat een één-op-één relatie tussen een `settings` object, een `trigger` en een regel. Dit betekent dat de trekkerfunctie u voor één regel ontving niet kan worden gebruikt om een verschillende regel in werking te stellen. |

>[!NOTE]
>
>De geëxporteerde functie wordt één keer aangeroepen voor elke regel die is geconfigureerd om uw gebeurtenistype te gebruiken.

Gebruikend de activiteit van vijf seconden die als voorbeeld overgaan, na vijf seconden overgaat, heeft de activiteit plaatsgevonden en de regel zal in brand steken. De module zal gelijkaardig aan dit voorbeeld kijken.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, 5000);
};
```

Als u de duur configureerbaar wilt maken voor de Adobe Experience Platform-gebruiker, is de optie voor het invoeren en opslaan van een duur in het instellingsobject vereist. Het object kan er ongeveer als volgt uitzien:

```js
{
  "duration": 25000
}
```

Om op de user-defined duur te werken, zou de module moeten worden bijgewerkt om dit te omvatten.

```js
module.exports = function(settings, trigger) {
  setTimeout(trigger, settings.duration);
};
```

## Contextafhankelijke gebeurtenisgegevens doorgeven

Wanneer een regel wordt teweeggebracht, is het vaak nuttig om extra detail over de gebeurtenis te verstrekken die voorkwam. Gebruikers die regels maken, kunnen deze informatie nuttig vinden om een bepaald gedrag te bereiken. Bijvoorbeeld, als een teller een regel wil tot stand brengen waar een analytische baken wordt verzonden telkens als de gebruiker het scherm veegt. De uitbreiding zou een `swipe` gebeurtenistype zodat de markeerteken dit gebeurtenistype kan gebruiken om de juiste regel te activeren. Ervan uitgaande dat de markeerteken ook de hoek zou willen aangeven waarop de veegbeweging op het baken heeft plaatsgevonden, is dit moeilijk zonder aanvullende informatie. Als u aanvullende informatie wilt geven over de gebeurtenis die heeft plaatsgevonden, geeft u een object door wanneer u de `trigger` functie. Bijvoorbeeld:

```js
trigger({
  swipeAngle: 90 // the value would be the detected angle
});
```

De teller kon deze waarde op een analytisch baken dan gebruiken door de waarde te specificeren `%event.swipeAngle%` in een tekstveld. Zij kunnen ook `event.swipeAngle` ook vanuit andere contexten (zoals een aangepaste code-actie). Het is mogelijk andere typen optionele gebeurtenisinformatie op te nemen die op dezelfde manier voor een markeerteken nuttig kunnen zijn.

### [!DNL nativeEvent]

Als uw gebeurtenistype op een inheemse gebeurtenis gebaseerd is (bijvoorbeeld als uw uitbreiding verstrekte een `click` gebeurtenistype), wordt aangeraden het `nativeEvent` eigenschap als volgt.

```js
trigger({
  nativeEvent: nativeEvent // the value would be the underlying native event
});
```

Dit kan handig zijn voor marketers die toegang proberen te krijgen tot informatie uit de native gebeurtenis, zoals cursorcoördinaten.

### [!DNL element]

Als er een sterke relatie is tussen een element en de gebeurtenis die is opgetreden, wordt aanbevolen om de instelling `element` eigenschap aan het DOM-knooppunt van het element. Als uw extensie bijvoorbeeld een `click` gebeurtenistype en u staat marketers toe het te vormen zodat zou de regel slechts in brand steken als een element met identiteitskaart van `herobanner` is geselecteerd. Als de gebruiker in dit geval de hoofdbanner selecteert, wordt aangeraden `trigger` en instellen `element` op het DOM-knooppunt van de hoofdbanner.

```js
trigger({
  element: element // the value would be the DOM node
});
```

## Regelvolgorde respecteren

Met labels kunnen gebruikers regels bestellen. Een gebruiker kan bijvoorbeeld twee regels maken die zowel het gebeurtenistype oriëntatie wijzigen als de volgorde waarin de regels worden doorlopen. Ervan uitgaande dat de Adobe Experience Platform-gebruiker een orderwaarde opgeeft van `2` voor de gebeurtenis oriëntatiewijziging in regel A en een orderwaarde van `1` voor de gebeurtenis die de oriëntatiewijziging in regel B veroorzaakt. Dit geeft aan dat wanneer de oriëntatie op een mobiel apparaat verandert, regel B vóór regel A moet worden geactiveerd (regels met waarden in een lagere volgorde worden eerst geactiveerd).

Zoals eerder vermeld, zal de uitgevoerde functie in onze gebeurtenismodule eens voor elke regel worden geroepen die om ons gebeurtenistype is gevormd te gebruiken. Elke keer dat de geëxporteerde functie wordt aangeroepen, wordt deze een unieke functie doorgegeven `trigger` functie die aan een specifieke regel is gebonden. In het zojuist beschreven scenario wordt onze geëxporteerde functie één keer aangeroepen met een `trigger` functie gekoppeld aan regel B en vervolgens opnieuw met een `trigger` functie die aan regel A is gekoppeld. Regel B komt eerst omdat de gebruiker het een lager-ordewaarde dan Regel A heeft gegeven. Wanneer in onze bibliotheekmodule een wijziging in de oriëntatie wordt gedetecteerd, is het belangrijk dat u de `trigger` functies in dezelfde volgorde als de bibliotheekmodule.

In de voorbeeldcode hieronder, merk op dat wanneer een oriëntatieverandering wordt ontdekt, de trekkerfuncties in de zelfde orde worden geroepen zij aan onze uitgevoerde functie werden verstrekt:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  triggers.forEach(function(trigger) {
    trigger();
  });
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Dit zorgt ervoor dat de user-specified orde wordt gehandhaafd.

Een onjuiste implementatie zou een toepassing zijn die de triggerfuncties in een andere volgorde aanroept:

```js
var triggers = [];

window.addEventListener('orientationchange', function() {
  for (var i = triggers.length - 1; i >= 0; i--) {
    triggers[i]();
  }
});

module.exports = function(settings, trigger) {
  triggers.push(trigger);
};
```

Natuurlijke programmeringspraktijken handhaven doorgaans de goede orde, maar het is belangrijk om bewust te zijn van de implicaties en dienovereenkomstig te ontwikkelen.
