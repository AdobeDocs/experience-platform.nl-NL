---
title: Overzicht van Core Event Forwarding Extension
description: Leer over de gebeurtenis van de Kern door:sturen uitbreiding in Adobe Experience Platform.
feature: Event Forwarding
exl-id: b5ee4ccf-6fa5-4472-be04-782930f07e20
source-git-commit: c7344d0ac5b65c6abae6a040304f27dc7cd77cbb
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

Als u toegang wilt krijgen tot de waarde van een gegevenselement in aangepaste code, gebruikt u de opdracht `getDataElementValue` methode. Bijvoorbeeld, om de waarde van een gegevenselement terug te winnen genoemd `productName`, schrijft het volgende: 

```javascript
getDataElementValue('productName') 
```

#### ruleStash, object

In uw aangepaste code kunt u ook de opdracht `ruleStash` object.

```javascript
utils.logger.log(context.arc.ruleStash);
```

`ruleStash` is een object dat elk resultaat van actiemodules verzamelt.

Elke extensie heeft een eigen naamruimte. Als uw extensie bijvoorbeeld de naam heeft `send-beacon`alle resultaten van de `send-beacon` acties worden opgeslagen op de `ruleStash['send-beacon']` naamruimte.

```javascript
utils.logger.log(context.arc.ruleStash['adobe-cloud-connector']);
```

De naamruimte is uniek voor elke extensie en heeft de waarde `undefined` aan het begin.

De naamruimte wordt overschreven door het geretourneerde resultaat van elke actie. Er gebeurt geen naamruimtemagie. Als u bijvoorbeeld een `transform` extensie met twee acties: `generate-fullname` en `generate-fulladdress`Voeg vervolgens de twee handelingen aan een regel toe.

Indien het resultaat van de `generate-fullname` handeling is `Firstname Lastname`Vervolgens ziet u de regelstash als volgt nadat de handeling is voltooid:

```js
{
  transform: 'Firstname Lastname`
}
```

Indien het resultaat van de `generate-address` handeling is `3900 Adobe Way`Vervolgens ziet u de regelstash als volgt nadat de handeling is voltooid:

```js
{
  transform: '3900 Adobe Way`
}
```

Let op: `Firstname Lastname` bestaat niet meer binnen de regelstreepje. Dit komt omdat de `generate-address` de actie overtrok het met het adres.

Als u de resultaten van beide handelingen wilt opslaan in het dialoogvenster `transform` naamruimte in het dialoogvenster `ruleStash`U kunt uw actiemodule schrijven, vergelijkbaar met het volgende voorbeeld:

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

De eerste keer dat deze handeling wordt uitgevoerd, wordt `ruleStash` is `undefined` en wordt geïnitialiseerd met een leeg object. De volgende keer dat de handeling wordt uitgevoerd, `ruleStash` wordt geretourneerd door de handeling toen deze eerder werd aangeroepen. Een object gebruiken als `ruleStash` Hiermee kunt u nieuwe gegevens toevoegen zonder dat gegevens verloren gaan die eerder zijn ingesteld door andere handelingen uit de extensie.

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

**Gelijk:** De voorwaarde retourneert true als de twee waarden gelijk zijn via een niet-strikte vergelijking (in JavaScript, de == operator). De waarden kunnen van elk type zijn. Als u een woord typt als _true_, _false_, _null_, of _ongedefinieerd_ in een waardeveld wordt het woord vergeleken als een tekenreeks en wordt het niet omgezet in het JavaScript-equivalent ervan.

**Niet gelijk:** De voorwaarde retourneert true als de twee waarden niet gelijk zijn aan een niet-strikte vergelijking (in JavaScript, de != operator). De waarden kunnen van elk type zijn. Als u een woord typt als _true_, _false_, _null_, of _ongedefinieerd_ in een waardeveld wordt het woord vergeleken als een tekenreeks en wordt het niet omgezet in het JavaScript-equivalent ervan.

**Bevat:** De voorwaarde retourneert true als de eerste waarde de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Bevat niet:** De voorwaarde retourneert true als de eerste waarde niet de tweede waarde bevat. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Begint met:** De voorwaarde retourneert true als de eerste waarde begint met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Begint niet met:** De voorwaarde retourneert true als de eerste waarde niet begint met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Eindigt met:** De voorwaarde retourneert true als de eerste waarde eindigt met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Eindigt niet met:** De voorwaarde retourneert true als de eerste waarde niet eindigt met de tweede waarde. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**Komt overeen met Regex:** De voorwaarde retourneert true als de eerste waarde overeenkomt met de reguliere expressie. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die false retourneert.

**Komt niet overeen met Regex:** De voorwaarde retourneert true als de eerste waarde niet overeenkomt met de reguliere expressie. Getallen worden omgezet in tekenreeksen. Elke andere waarde dan een getal of tekenreeks resulteert in de voorwaarde die true retourneert.

**is kleiner dan:** De voorwaarde retourneert true als de eerste waarde kleiner is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**is kleiner dan of gelijk aan:** De voorwaarde retourneert true als de eerste waarde kleiner dan of gelijk is aan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is groter dan:** De voorwaarde retourneert true als de eerste waarde groter is dan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**groter dan of gelijk aan:** De voorwaarde retourneert true als de eerste waarde groter dan of gelijk is aan de tweede waarde. Tekenreeksen die getallen vertegenwoordigen, worden omgezet in getallen. Een andere waarde dan een getal of een convertibele tekenreeks resulteert in de voorwaarde die false retourneert.

**Is waar:** De voorwaarde retourneert true als de waarde een booleaanse waarde is met de waarde true. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde true resulteert in de voorwaarde die false retourneert.

**Is waar:** De voorwaarde retourneert true als de waarde waar is nadat deze is omgezet in een Booleaanse waarde. Zie [Truthy-documentatie van MDN](https://developer.mozilla.org/en-US/docs/Glossary/Truthy) voor voorbeelden van waarheidswaarden.

**Is onwaar:** De voorwaarde retourneert true als de waarde een booleaanse waarde is met de waarde false. De waarde die u opgeeft, wordt niet omgezet in een Booleaanse waarde als het een ander type betreft. Elke andere waarde dan een booleaanse waarde met de waarde false resulteert in de voorwaarde die false retourneert.

**Is false:** De voorwaarde retourneert true als de waarde false is na de conversie naar een Booleaanse waarde. Zie [Falsy-documentatie van MDN](https://developer.mozilla.org/en-US/docs/Glossary/Falsy) voor voorbeelden van ongeldige waarden.



## Typen handelingen voor kernextensies

Deze sectie beschrijft de actietypes beschikbaar in de uitbreiding van de Kern.

### Aangepaste code

Geef de code op die wordt uitgevoerd nadat de gebeurtenis is geactiveerd en de voorwaarden zijn geëvalueerd. Het doorsturen van gebeurtenissen in Adobe Experience Platform ondersteunt ES6.

1. Geef de actiecode een naam.
1. Selecteer **[!UICONTROL Open Editor]**.
1. Bewerk de code en selecteer vervolgens **[!UICONTROL Save]**.

Als u toegang wilt krijgen tot de waarde van een gegevenselement in aangepaste code, gebruikt u de opdracht `getDataElementValue` methode. Bijvoorbeeld, om de waarde van een gegevenselement terug te winnen genoemd `productName`, schrijft het volgende: 

```javascript
getDataElementValue('productName') 
```

Gebeurtenis die acties door:sturen voert opeenvolgend uit. Het is ook mogelijk dat aangepaste code in één actie een waarde retourneert die in een volgende actie kan worden gebruikt. De teruggekeerde waarde kan uit code binnen die actie, of van het reactielichaam van een vraag komen die aan een externe bron wordt gemaakt. Om gegevens van een eerder uitgevoerde actie binnen één enkele regel van verwijzingen te voorzien waar de uitbreiding van de Kern wordt gebruikt, creeer een gegevenselement van type `Path` en gebruik het volgende pad om naar de waarde van een variabele te verwijzen die `productCategory` gedefinieerd in aangepaste code binnen de Core-extensie:

```javascript
arc.ruleStash.[Extension-Name].[key-as-defined-by-action] 

arc.ruleStash.core.productCategory  
```

## Gegevenstelelementtypen van de kernextensie

Gegevenselementen worden bepaald door de extensie. Er is geen limiet aan de typen die kunnen worden gemaakt.

De volgende secties beschrijven de types van gegevenselementen beschikbaar in de uitbreiding van de Kern. Andere extensies gebruiken andere typen gegevenselementen.

### Aangepaste code

U kunt aangepaste JavaScript invoeren in de gebruikersinterface door  **[!UICONTROL Open Editor]** en code invoegen in het editorvenster.

Een terugkeerverklaring is noodzakelijk in het redacteursvenster om erop te wijzen welke waarde als waarde van het gegevenselement zou moeten worden gebruikt. Als een instructie return niet is opgenomen of als de waarde `null` of `undefined` wordt geretourneerd, geeft de standaardwaarde van het gegevenselement aan `null` of `undefined`.

Als u toegang wilt krijgen tot de waarde van een gegevenselement in aangepaste code, gebruikt u de opdracht `getDataElementValue` methode. Bijvoorbeeld, om de waarde van een gegevenselement terug te winnen genoemd `productName`, schrijft het volgende: 

```javascript
getDataElementValue('productName') 
```

**Voorbeeld:**

```javascript
return getDataElementValue('section').concat(getDataElementValue('pName')); 
```

#### Pad

Er kan naar een pad naar een sleutelwaardepaar op een gebeurtenis die naar Adobe Experience Platform Edge Network wordt verzonden, worden verwezen met het gegevenstype Path.

Als u naar het volledige object van een gebeurtenis wilt verwijzen, voert u `arc` als het pad. Het acroniem `arc` staat voor de Context van het Middel van Adobe en is de top-level weg voor een gebeurtenis die naar Adobe Experience Platform Edge Network wordt verzonden.

Als u bijvoorbeeld de `interact` De vraag van de cliënt aan het Netwerk van Edge heeft het volgende verzoek zoals die van de browser console wordt gezien:

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

Een pad invoeren dat verwijst naar `pageName`voert u in het veld Pad het volgende in:

```javascript
arc.event.xdm.page.pageName 
```

>[!NOTE]
>
>De `interact` de vraag van de cliënt heeft `events`, maar voor het doorsturen van gebeurtenissen hebt u `event`. Dit is omdat gebeurtenis door:sturen elke gebeurtenis individueel inspecteert, en niet als partij van veelvoudige gebeurtenissen zoals aangetoond op de cliënt.
