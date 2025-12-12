---
title: Overzicht van Core Event Forwarding Extension
description: Leer over de gebeurtenis van de Kern door:sturen uitbreiding in Adobe Experience Platform.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 0%

---

# Overzicht van door:sturen van kerngebeurtenis

De de gebeurtenis-door:sturen uitbreiding van de Kern verstrekt de standaardgebeurtenissen, de voorwaarden, en de gegevenstypes voor gebeurtenis door:sturen in Adobe Experience Platform.

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## Voorkeurstypen van kernextensie

In deze sectie worden de voorwaardetypen beschreven die beschikbaar zijn in de extensie Core.  Deze voorwaardetypes kunnen met of het regelmatige of type van uitzonderingslogica worden gebruikt.

### Aangepaste code

Geef aangepaste code op die als voorwaarde voor de gebeurtenis moet bestaan. Gebruik de ingebouwde code-editor om de aangepaste code in te voeren. Het door:sturen van gebeurtenissen in Adobe Experience Platform steunt ES13.

1. Selecteer **[!UICONTROL Open Editor]**.
1. Typ de aangepaste code.
1. Selecteer **[!UICONTROL Save]**.

Met de methode `getDataElementValue` hebt u toegang tot de waarde van een gegevenselement in aangepaste code. Als u bijvoorbeeld de waarde van een gegevenselement met de naam `productName` wilt ophalen, schrijft u het volgende: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash, object

In uw aangepaste code kunt u ook het object `ruleStash` gebruiken.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` is een object dat elk resultaat van actiemodules verzamelt.

Elke extensie heeft een eigen naamruimte. Als uw extensie bijvoorbeeld de naam `send-beacon` heeft, worden alle resultaten van de `send-beacon` -handelingen opgeslagen in de naamruimte `ruleStash['send-beacon']` .

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

De naamruimte is uniek voor elke extensie en heeft de waarde `undefined` aan het begin.

De naamruimte wordt overschreven door het geretourneerde resultaat van elke actie. Er gebeurt geen naamruimtemagie. Als u bijvoorbeeld een extensie `transform` hebt met twee handelingen: `generate-fullname` en `generate-fulladdress` , voegt u de twee handelingen toe aan een regel.

Als het resultaat van de `generate-fullname` actie `Firstname Lastname` is, verschijnt de regelstreepje als volgt nadat de actie is voltooid:

```js
{
  transform: 'Firstname Lastname`
}
```

Als het resultaat van de `generate-address` actie `3900 Adobe Way` is, verschijnt de regelstreepje als volgt nadat de actie is voltooid:

```js
{
  transform: '3900 Adobe Way`
}
```

`Firstname Lastname` bestaat niet meer binnen de regelstreepje. Dit komt doordat de handeling `generate-address` deze heeft overschreven door het adres.

Als u de resultaten van beide handelingen wilt opslaan in de naamruimte `transform` in `ruleStash` , kunt u de actiemodule schrijven, vergelijkbaar met het volgende voorbeeld:

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

De eerste keer dat deze handeling wordt uitgevoerd, is `ruleStash` `undefined` en wordt deze geïnitialiseerd met een leeg object. De volgende keer dat de handeling wordt uitgevoerd, wordt `ruleStash` geretourneerd door de handeling toen deze eerder werd aangeroepen. Als u een object gebruikt als `ruleStash` , kunt u nieuwe gegevens toevoegen zonder gegevens te verliezen die eerder zijn ingesteld door andere handelingen van de extensie.

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

**Gelijk:** de voorwaarde keert waar terug als de twee waarden gelijk gebruikend een niet-strikte vergelijking (in JavaScript, == exploitant) zijn. De waarden kunnen van elk type zijn. Wanneer het typen van een woord als _waar_, _vals_, _ongeldig_, of _niet gedefiniëerd_ in een waardegebied, wordt het woord vergeleken als koord en niet in zijn equivalent van JavaScript omgezet.

**GEEFT niet Gelijk:** de voorwaarde keert waar terug als de twee waarden niet gelijk het gebruiken van een niet-strikte vergelijking (in JavaScript, != operator). De waarden kunnen van elk type zijn. Wanneer het typen van een woord als _waar_, _vals_, _ongeldig_, of _niet gedefiniëerd_ in een waardegebied, wordt het woord vergeleken als koord en niet in zijn equivalent van JavaScript omgezet.

**bevat:** de voorwaarde keert waar terug als de eerste waarde de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**bevat niet:** de voorwaarde keert waar terug als de eerste waarde niet de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**begint met:** de voorwaarde keert waar terug als de eerste waarde met de tweede waarde begint. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**begint niet met:** de voorwaarde keert waar terug als de eerste waarde niet met de tweede waarde begint. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**eindigt met:** de voorwaarde keert waar terug als de eerste waarde met de tweede waarde beëindigt. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**beëindigt niet met:** de voorwaarde keert waar terug als de eerste waarde niet met de tweede waarde beëindigt. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**past Regex aan:** de voorwaarde keert waar terug als de eerste waarde de regelmatige uitdrukking aanpast. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**komt niet Regex overeen:** de voorwaarde keert waar terug als de eerste waarde niet de regelmatige uitdrukking aanpast. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**is minder dan:** de voorwaarde keert waar terug als de eerste waarde minder dan de tweede waarde is. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**is minder dan of gelijk aan:** de voorwaarde keert waar terug als de eerste waarde minder dan of gelijk aan de tweede waarde is. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**is Groter dan:** de voorwaarde keert waar terug als de eerste waarde groter is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**is groter dan of gelijk aan:** de voorwaarde keert waar terug als de eerste waarde groter dan of gelijk aan de tweede waarde is. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**is Waar:** de voorwaarde keert waar terug als de waarde boolean met de waarde waar is. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde true resulteert in de voorwaarde die false retourneert.

**is Waarheid:** de voorwaarde keert waar terug als de waarde na wordt omgezet in boolean waar is. Zie [&#x200B; van de Vertrouwelijke documentatie van 0&rbrace; MDN voor voorbeelden van waarheidswaarden.](https://developer.mozilla.org/en-US/docs/Glossary/Truthy)

**is Vals:** de voorwaarde keert waar terug als de waarde boolean met de waarde van vals is. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde false resulteert in de voorwaarde die false retourneert.

**is vals:** de voorwaarde keert waar terug als de waarde na wordt omgezet in boolean vals is. Zie {de documentatie van het Falsy van 0} MDN [&#x200B; voor voorbeelden van valse waarden.](https://developer.mozilla.org/en-US/docs/Glossary/Falsy)



## Typen handelingen voor kernextensies

Deze sectie beschrijft de actietypes beschikbaar in de uitbreiding van de Kern.

### Aangepaste code

Geef de code op die wordt uitgevoerd nadat de gebeurtenis is geactiveerd en de voorwaarden zijn geëvalueerd. Het door:sturen van gebeurtenissen in Adobe Experience Platform steunt ES13.

1. Geef de actiecode een naam.
1. Selecteer **[!UICONTROL Open Editor]**.
1. Bewerk de code en selecteer vervolgens **[!UICONTROL Save]** .

Met de methode `getDataElementValue` hebt u toegang tot de waarde van een gegevenselement in aangepaste code. Als u bijvoorbeeld de waarde van een gegevenselement met de naam `productName` wilt ophalen, schrijft u het volgende: 

```javascript
getDataElementValue('productName') 
```

Gebeurtenis die acties door:sturen voert opeenvolgend uit. Het is ook mogelijk dat aangepaste code in één actie een waarde retourneert die in een volgende actie kan worden gebruikt. De teruggekeerde waarde kan uit code binnen die actie, of van het reactielichaam van een vraag komen die aan een externe bron wordt gemaakt. Als u wilt verwijzen naar gegevens van een eerder uitgevoerde actie binnen één regel waarin de Core-extensie wordt gebruikt, maakt u een gegevenselement van het type `Path` en gebruikt u het volgende pad om te verwijzen naar de waarde van een variabele met de naam `productCategory` die is gedefinieerd in aangepaste code binnen de Core-extensie:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Gegevenstelelementtypen van de kernextensie

Gegevenselementen worden bepaald door de extensie. Er is geen limiet aan de typen die kunnen worden gemaakt.

De volgende secties beschrijven de types van gegevenselementen beschikbaar in de uitbreiding van de Kern. Andere extensies gebruiken andere typen gegevenselementen.

### Aangepaste code

Aangepaste JavaScript kan in de gebruikersinterface worden ingevoerd door **[!UICONTROL Open Editor]** te selecteren en code in het editorvenster in te voegen.

Een terugkeerverklaring is noodzakelijk in het redacteursvenster om erop te wijzen welke waarde als waarde van het gegevenselement zou moeten worden gebruikt. Als een retourinstructie niet wordt opgenomen of als de waarde `null` of `undefined` wordt geretourneerd, geeft de standaardwaarde van het gegevenselement `null` of `undefined` aan.

Met de methode `getDataElementValue` hebt u toegang tot de waarde van een gegevenselement in aangepaste code. Als u bijvoorbeeld de waarde van een gegevenselement met de naam `productName` wilt ophalen, schrijft u het volgende: 

```javascript
getDataElementValue('productName') 
```

**Voorbeeld:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Pad

Er kan naar een pad naar een sleutelwaardepaar bij een gebeurtenis die naar Adobe Experience Platform Edge Network wordt verzonden, worden verwezen met het gegevenstype Path.

Als u naar het volledige object van een gebeurtenis wilt verwijzen, voert u `arc` in als het pad. Het acroniem `arc` staat voor Adobe Resource Context en is het pad op hoofdniveau voor een gebeurtenis die naar Adobe Experience Platform Edge Network wordt verzonden.

Als de `interact` -aanroep van de client naar Edge Network bijvoorbeeld de volgende aanvraag bevat, zoals u kunt zien in de browserconsole:

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
>De `interact` oproep van de client heeft `events` , maar voor het doorsturen van gebeurtenissen hebt u `event` nodig. Dit is omdat gebeurtenis door:sturen elke gebeurtenis individueel inspecteert, en niet als partij van veelvoudige gebeurtenissen zoals aangetoond op de cliënt.
