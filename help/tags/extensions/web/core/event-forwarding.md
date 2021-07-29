---
title: Overzicht van Core Event Forwarding Extension
description: Leer over de gebeurtenis van de Kern door:sturen uitbreiding in Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1716'
ht-degree: 0%

---

# Overzicht van door:sturen van kerngebeurtenis

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De de gebeurtenis-door:sturen uitbreiding van de Kern verstrekt de standaardgebeurtenissen, de voorwaarden, en de gegevenstypes voor gebeurtenis door:sturen in Adobe Experience Platform.

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## Type voorwaarde voor kernextensie

In deze sectie worden de voorwaardetypen beschreven die beschikbaar zijn in de extensie Core.  Deze voorwaardetypes kunnen met of het regelmatige of type van uitzonderingslogica worden gebruikt.

### Aangepaste code

Geef aangepaste code op die als voorwaarde voor de gebeurtenis moet bestaan. Gebruik de ingebouwde code-editor om de aangepaste code in te voeren. Het doorsturen van gebeurtenissen in Adobe Experience Platform ondersteunt ES6.

1. Selecteer **[!UICONTROL Open Editor]**.
1. Typ de aangepaste code.
1. Selecteer **[!UICONTROL Save]**.

Als u toegang wilt krijgen tot de waarde van een gegevenselement in aangepaste code, gebruikt u de methode `getDataElementValue`. Als u bijvoorbeeld de waarde van een gegevenselement met de naam `productName` wilt ophalen, schrijft u het volgende: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash, object

In uw douanecode, zou u het `ruleStash` voorwerp ook kunnen gebruiken.

```javascript
arc.ruleStash: Object<string, *>`
```

```javascript
logger.log(context.arc.ruleStash);
```

`ruleStash` is een object dat elk resultaat van actiemodules verzamelt.

Elke extensie heeft een eigen naamruimte. Als uw extensie bijvoorbeeld de naam `send-beacon` heeft, worden alle resultaten van de acties `send-beacon` opgeslagen in de naamruimte `ruleStash['send-beacon']`.

De naamruimte is uniek voor elke extensie en heeft aan het begin de waarde `undefined`.

De naamruimte wordt overschreven door het geretourneerde resultaat van elke actie. Er gebeurt geen naamruimtemagie. Als u bijvoorbeeld een extensie `transform` hebt met twee handelingen: `generate-fullname` en `generate-fulladdress`, dan voeg de twee acties aan een regel toe.

Als het resultaat van de `generate-fullname` actie `Firstname Lastname` is, dan verschijnt de regelstash als volgt nadat de actie wordt voltooid:

```js
{
  transform: 'Firstname Lastname`
}
```

Als het resultaat van de `generate-address` actie `3900 Adobe Way` is, dan verschijnt de regelstash als volgt nadat de actie wordt voltooid:

```js
{
  transform: '3900 Adobe Way`
}
```

Merk op dat `Firstname Lastname` niet meer binnen de regelstreepje bestaat. Dit is omdat de `generate-address` actie het met het adres overtrok.

Als u de resultaten van beide acties binnen `transform` namespace in `ruleStash` wilt opslaan, kunt u uw actiemodule gelijkend op het volgende voorbeeld schrijven:

```javascript
module.exports = (context) => {
  let transformRuleStash = context.arc.ruleStash.transform;
  if (!transformRuleStash) {
    transformRuleStash = {};
  }
  transformRuleStash.fullName = 'Firstname Lastname';
  return transformRuleStash;
}
```

De eerste keer dat deze handeling wordt uitgevoerd, is `ruleStash` `undefined` en wordt geïnitialiseerd met een leeg object. De volgende keer dat de handeling wordt uitgevoerd, wordt `ruleStash` geretourneerd door de handeling toen deze eerder werd aangeroepen. Door een object als `ruleStash` te gebruiken, kunt u nieuwe gegevens toevoegen zonder dat gegevens verloren gaan die eerder zijn ingesteld door andere handelingen van de extensie.

U moet voorzichtig zijn om altijd de volledige stash van de uitbreidingsregel te retourneren in dit geval. Als u slechts een waarde (bijvoorbeeld, 5) moest terugkeren, dan zou de regelstash als:

```js
{
  transform: 5
}
```

### Waardevergelijking {#value-comparison}

Vergelijkt twee waarden om te bepalen of deze voorwaarde waar terugkeert.

Als u een regel met veelvoudige voorwaarden hebt, is het mogelijk dat deze voorwaarde waar zal terugkeren, maar de regel zal nog niet in brand steken omdat de andere voorwaarden als vals evalueren of één van de uitzonderingen als waar evalueert.

1. Geef een waarde op.
1. Selecteer de operator. Raadpleeg de lijst met vergelijkingsoperatoren voor waarden hieronder voor meer informatie.
1. Geef een andere waarde op voor de vergelijking.

De volgende vergelijkingsoperatoren voor waarden zijn beschikbaar:

**Gelijk:** de voorwaarde keert waar terug als de twee waarden gelijk zijn gebruikend een niet-strikte vergelijking (in JavaScript, == exploitant). De waarden kunnen van elk type zijn. Wanneer u een woord als _true_, _false_, _null_ of _undefined_ in een waardeveld typt, wordt het woord vergeleken als een tekenreeks en wordt het niet omgezet in het JavaScript-equivalent ervan.

**Niet gelijk:** de voorwaarde retourneert true als de twee waarden niet gelijk zijn met een niet-strikte vergelijking (in JavaScript, de != operator). De waarden kunnen van elk type zijn. Wanneer u een woord als _true_, _false_, _null_ of _undefined_ in een waardeveld typt, wordt het woord vergeleken als een tekenreeks en wordt het niet omgezet in het JavaScript-equivalent ervan.

**Bevat:** de voorwaarde retourneert true als de eerste waarde de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Bevat niet:** de voorwaarde retourneert true als de eerste waarde niet de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Begint met:** de voorwaarde retourneert true als de eerste waarde met de tweede waarde begint. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Begint niet met:** de voorwaarde retourneert true als de eerste waarde niet begint met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Eindigt met:** de voorwaarde retourneert true als de eerste waarde eindigt met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Niet eindigen met:** de voorwaarde retourneert true als de eerste waarde niet eindigt met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Komt overeen met Regex:** De voorwaarde retourneert true als de eerste waarde overeenkomt met de reguliere expressie. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Komt niet overeen met Regex:** de voorwaarde retourneert true als de eerste waarde niet overeenkomt met de reguliere expressie. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Is minder dan:** De voorwaarde retourneert true als de eerste waarde kleiner is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is kleiner dan of gelijk aan:** de voorwaarde retourneert true als de eerste waarde kleiner dan of gelijk is aan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is groter dan:** de voorwaarde keert waar terug als de eerste waarde groter is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is groter dan of gelijk aan:** de voorwaarde keert waar terug als de eerste waarde groter dan of gelijk aan de tweede waarde is. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is Waar:** de voorwaarde keert waar terug als de waarde een booleaanse waarde met de waarde waar is. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde true resulteert in de voorwaarde die false retourneert.

**Is Truthy:** De voorwaarde retourneert true als de waarde waar is na de conversie naar een booleaanse waarde. Zie [Truthy-documentatie van MDN](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) voor voorbeelden van waarheidswaarden.

**Is Onwaar:** de voorwaarde retourneert true als de waarde een booleaanse waarde is met de waarde false. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde false resulteert in de voorwaarde die false retourneert.

**Is Falsy:** de voorwaarde retourneert true als de waarde false is nadat deze is omgezet in een Booleaanse waarde. Zie [Falsy documentation](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) voor voorbeelden van valse waarden.



## Typen handelingen voor kernextensies

Deze sectie beschrijft de actietypes beschikbaar in de uitbreiding van de Kern.

### Aangepaste code

Geef de code op die wordt uitgevoerd nadat de gebeurtenis is geactiveerd en de voorwaarden zijn geëvalueerd. Het doorsturen van gebeurtenissen in Adobe Experience Platform ondersteunt ES6.

1. Geef de actiecode een naam.
1. Selecteer **[!UICONTROL Open Editor]**.
1. Bewerk de code en selecteer **[!UICONTROL Save]**.

Als u toegang wilt krijgen tot de waarde van een gegevenselement in aangepaste code, gebruikt u de methode `getDataElementValue`. Als u bijvoorbeeld de waarde van een gegevenselement met de naam `productName` wilt ophalen, schrijft u het volgende: 

```javascript
getDataElementValue('productName') 
```

Gebeurtenis die acties door:sturen voert opeenvolgend uit. Het is ook mogelijk dat aangepaste code in één actie een waarde retourneert die in een volgende actie kan worden gebruikt. De teruggekeerde waarde kan uit code binnen die actie, of van het reactielichaam van een vraag komen die aan een externe bron wordt gemaakt. Als u wilt verwijzen naar gegevens van een eerder uitgevoerde handeling binnen één regel waarin de Core-extensie wordt gebruikt, maakt u een gegevenselement van het type `Path` en gebruikt u het volgende pad om te verwijzen naar de waarde van een variabele met de naam `productCategory` die is gedefinieerd in aangepaste code binnen de Core-extensie:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Gegevenstelelementtypen van de kernextensie

Gegevenselementen worden bepaald door de extensie. Er is geen limiet aan de typen die kunnen worden gemaakt.

De volgende secties beschrijven de types van gegevenselementen beschikbaar in de uitbreiding van de Kern. Andere extensies gebruiken andere typen gegevenselementen.

### Aangepaste code

U kunt aangepaste JavaScript invoeren in de gebruikersinterface door **[!UICONTROL Open Editor]** te selecteren en code in het editorvenster in te voegen.

Een terugkeerverklaring is noodzakelijk in het redacteursvenster om erop te wijzen welke waarde als waarde van het gegevenselement zou moeten worden gebruikt. Als een retourinstructie niet is opgenomen of als de waarde `null` of `undefined` wordt geretourneerd, geeft de standaardwaarde van het gegevenselement `null` of `undefined` weer.

Als u toegang wilt krijgen tot de waarde van een gegevenselement in aangepaste code, gebruikt u de methode `getDataElementValue`. Als u bijvoorbeeld de waarde van een gegevenselement met de naam `productName` wilt ophalen, schrijft u het volgende: 

```javascript
getDataElementValue('productName') 
```

**Voorbeeld:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Pad

Er kan naar een pad naar een sleutelwaardepaar op een gebeurtenis die naar Adobe Experience Platform Edge Network wordt verzonden, worden verwezen met het gegevenstype Path.

Als u wilt verwijzen naar het volledige object van een gebeurtenis, voert u `arc` in als het pad. Het acroniem `arc` staat voor de Context van het Middel van Adobe en is de top-level weg voor een gebeurtenis die naar het Netwerk van de Rand van Adobe Experience Platform wordt verzonden.

Met de `interact`-oproep van de client naar Edge Network hebt u bijvoorbeeld de volgende aanvraag, zoals u kunt zien op de browserconsole:

```javascript
"events": [ 
        { 
             "xdm": { 
                    "page": { 
                            "btnHover": false, 
                            "pageName": "We Travel Home Page", 
                            "siteSection": "Landing Page" 
                     }] 
```

Als u een pad wilt invoeren dat naar `pageName` verwijst, voert u het volgende in het padveld in:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>De `interact` vraag van de cliënt heeft `events`, maar voor gebeurtenis door:sturen hebt u `event` nodig. Dit is omdat gebeurtenis door:sturen elke gebeurtenis individueel inspecteert, en niet als partij van veelvoudige gebeurtenissen zoals aangetoond op de cliënt.
