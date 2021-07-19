---
title: Verwijzing naar satellietobject
description: Leer meer over het client-side _satelliet object en de verschillende functies die u ermee kunt uitvoeren in Adobe Experience Platform.
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 1%

---

# Adobe Experience Platform-tags Satellite, objectverwijzing

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document dient als referentie voor het client-side `_satellite`-object en de verschillende functies die u ermee kunt uitvoeren.

## `track`

**Code**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Voorbeeld**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` brandt alle regels gebruikend het Directe gebeurtenistype van de Vraag dat met het bepaalde herkenningsteken van de de markeringsuitbreiding van de Kern is gevormd. Het bovenstaande voorbeeld brengt alle regels teweeg gebruikend een Directe gebeurtenistype van de Vraag waar het gevormde herkenningsteken `contact_submit` is. Er wordt ook een optioneel object met gerelateerde informatie doorgegeven. Het detailobject kan worden benaderd door `%event.detail%` in een tekstveld in te voeren in een voorwaarde of handeling of `event.detail` in de code-editor in een aangepaste codevoorwaarde of handeling.

## `getVar`

**Code**

```javascript
_satellite.getVar(name: string) => *
```

**Voorbeeld**

```javascript
var product = _satellite.getVar('product');
```

In het gegeven voorbeeld, als een gegevenselement met een passende naam bestaat, zal de waarde van het gegevenselement zijn teruggekeerd. Als er geen overeenkomend gegevenselement bestaat, wordt gecontroleerd of een aangepaste variabele met een overeenkomende naam eerder is ingesteld met `_satellite.setVar()`. Als een aangepaste variabele wordt gevonden, wordt de waarde ervan geretourneerd.

Merk op dat in vele vormgebieden in het gebruikersinterface van de Inzameling van Gegevens, u de `%%` syntaxis kunt gebruiken om variabelen van verwijzingen te voorzien, die de behoefte om `_satellite.getVar()` verminderen te roepen. Als u bijvoorbeeld %product% gebruikt, krijgt u toegang tot de waarde van het element met productgegevens of de aangepaste variabele.

## `setVar`

**Code**

```javascript
_satellite.setVar(name: string, value: *)
```

**Voorbeeld**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` Hiermee stelt u een aangepaste variabele in met een bepaalde naam en waarde. De waarde van de variabele kan later worden betreden gebruikend `_satellite.getVar()`.

U kunt optioneel meerdere variabelen tegelijk instellen door een object door te geven waarin de sleutels variabelenamen zijn en de waarden de respectievelijke variabelewaarden zijn.

```javascript
_satellite.setVar({ 'product': 'Circuit Pro', 'category': 'hobby' });
```

## `getVisitorId`

**Code**

```javascript
_satellite.getVisitorId() => Object
```

**Voorbeeld**

```javascript
var visitorIdInstance = _satellite.getVisitorId();
```

Als de [!DNL Adobe Experience Cloud ID] uitbreiding op het bezit wordt geïnstalleerd, keert deze methode de instantie van identiteitskaart van de Bezoeker terug. Raadpleeg de [Experience Cloud ID Service documentation](https://experienceleague.adobe.com/docs/id-service/using/home.html) voor meer informatie.

## `logger`

**Code**

```javascript
_satellite.logger.log(message: string)
```

```javascript
_satellite.logger.info(message: string)
```

```javascript
_satellite.logger.warn(message: string)
```

```javascript
_satellite.logger.error(message: string)
```

**Voorbeeld**

```javascript
_satellite.logger.error('No product ID found.');
```

Met het `logger`-object kan een bericht worden aangemeld bij de browserconsole. Het bericht wordt alleen weergegeven als foutopsporing van tags is ingeschakeld door de gebruiker (door `_satellite.setDebug(true)` aan te roepen of een geschikte browserextensie te gebruiken).

### Waarschuwingen bij deponering van registratie

```javascript
_satellite.logger.deprecation(message: string)
```

**Voorbeeld**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Dit registreert een waarschuwing aan de browser console. Het bericht wordt weergegeven of foutopsporing van tags is ingeschakeld door de gebruiker.

## `cookie`

**Code**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

```javascript
_satellite.cookie.get(name: string) => string
```

```javascript
_satellite.cookie.remove(name: string)
```

**Voorbeeld**

```javascript
// Writing a cookie that expires in one week.
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

```javascript
// Reading a previously set cookie.
var product = _satellite.cookie.get('product');
```

```javascript
// Removing a previously set cookie.
_satellite.cookie.remove('product');
```

Dit is een hulpprogramma voor het lezen en schrijven van cookies. Het is een belichte kopie van de externe bibliotheek js-cookie. Voor geavanceerder gebruik raadpleegt u de [js-cookie gebruiksdocumentatie](https://www.npmjs.com/package/js-cookie#basic-usage) (externe koppeling).

## `buildInfo`

**Code**

```javascript
_satellite.buildInfo
```

Dit object bevat informatie over de build van de huidige tagruntimebibliotheek. Het object bevat de volgende eigenschappen:

### `turbineVersion`

Dit verstrekt [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) versie die binnen de huidige bibliotheek wordt gebruikt.

### `turbineBuildDate`

De ISO 8601-datum waarop de in de container gebruikte versie van [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) is gemaakt.

### `buildDate`

De ISO 8601-datum waarop de huidige bibliotheek is gemaakt.

### `environment`

De omgeving waarvoor deze bibliotheek is gemaakt. De mogelijke waarden zijn:

* ontwikkeling
* fasering
* productie

In dit voorbeeld worden de objectwaarden getoond:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z",
  environment: "development"
}
```

## `notify`

>[!NOTE]
>
>Deze methode is vervangen. Gebruik in plaats hiervan `_satellite.logger.log()`.

**Code**

```javascript
_satellite.notify(message: string[, level: number])
```

**Voorbeeld**

```javascript
_satellite.notify('Hello world!');
```

`notify` logt een bericht aan de browser console. Het bericht wordt alleen weergegeven als foutopsporing van tags is ingeschakeld door de gebruiker (door `_satellite.setDebug(true)` aan te roepen of een geschikte browserextensie te gebruiken).

Een facultatief registrerenniveau kan worden overgegaan dat het stileren en het filtreren van het bericht zal beïnvloeden dat wordt geregistreerd. De ondersteunde niveaus zijn als volgt:

3 - Informatieberichten.

4 - Waarschuwingsberichten.

5 - Foutberichten.

Als u geen registrerenniveau verstrekt of geen andere niveauwaarde overgaat, zal het bericht als regelmatig bericht worden geregistreerd.

## `setCookie`

>[!NOTE]
>
>Deze methode is vervangen. Gebruik in plaats hiervan `_satellite.cookie.set()`.

**Code**

```javascript
_satellite.setCookie(name: string, value: string, days: number)
```

**Voorbeeld**

```javascript
_satellite.setCookie('product', 'Circuit Pro', 3);
```

Hiermee wordt een cookie ingesteld in de browser van de gebruiker. Het cookie blijft gedurende het opgegeven aantal dagen aanwezig.

## `readCookie`

>[!NOTE]
>
>Deze methode is vervangen. Gebruik in plaats hiervan `_satellite.cookie.get()`.

**Code**

```javascript
_satellite.readCookie(name: string) => string
```

**Voorbeeld**

```javascript
var product = _satellite.readCookie('product');
```

Dit leest een koekje van browser van de gebruiker.

## `removeCookie`

>[!NOTE]
>
>Deze methode is vervangen. Gebruik in plaats hiervan `_satellite.cookie.remove()`.

**Code**

```javascript
_satellite.removeCookie(name: string)
```

**Voorbeeld**

```javascript
_satellite.removeCookie('product');
```

Hierdoor wordt een cookie verwijderd uit de browser van de gebruiker.

## Foutopsporingsfuncties

De volgende functies zijn niet toegankelijk via de productiecode. Ze zijn alleen bedoeld voor foutopsporingsdoeleinden en worden na verloop van tijd aangepast.

### `container`

**Code**

```javascript
_satellite._container
```

**Voorbeeld**

>[!IMPORTANT]
>
>Deze functie moet niet worden benaderd vanuit de productiecode. Het is bedoeld slechts voor het zuiveren doeleinden en zal in tijd veranderen zoals nodig.

### `monitor`

**Code**

```javascript
_satellite._monitors
```

**Voorbeeld**

>[!IMPORTANT]
>
>Deze functie moet niet worden benaderd vanuit de productiecode. Het is bedoeld slechts voor het zuiveren doeleinden en zal in tijd veranderen zoals nodig.

**Monster**

Voeg op uw webpagina met een tagbibliotheek een codefragment toe aan uw HTML. Doorgaans wordt de code ingevoegd in het element `<head>` vóór het element `<script>` waarmee de tagbibliotheek wordt geladen. Hierdoor kan de monitor de vroegste systeemgebeurtenissen afvangen die in de tagbibliotheek voorkomen. Bijvoorbeeld:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Title</title>
  <script>
    window._satellite = window._satellite || {};
    window._satellite._monitors = window._satellite._monitors || [];
    window._satellite._monitors.push({
      ruleTriggered: function (event) {
        console.log(
          'rule triggered',
          event.rule
        );
      },
      ruleCompleted: function (event) {
        console.log(
          'rule completed',
          event.rule
        );
      },
      ruleConditionFailed: function (event) {
        console.log(
          'rule condition failed',
          event.rule,
          event.condition
        );
      }
    });
  </script>
  <script src="//assets.adobedtm.com/launch-EN5bfa516febde4b22b3e7c6f96f6b439f.min.js"
          async></script>
</head>
<body>
  <h1>Click me!</h1>
</body>
</html>
```

In het eerste scriptelement wordt, omdat de tagbibliotheek nog niet is geladen, het eerste `_satellite`-object gemaakt en wordt een array op `_satellite._monitors` geïnitialiseerd. Het script voegt vervolgens een monitorobject aan die array toe. Het monitorobject kan de volgende methoden opgeven, die later door de tagbibliotheek worden aangeroepen:

### `ruleTriggered`

Deze functie wordt aangeroepen nadat een gebeurtenis een regel activeert, maar voordat de voorwaarden en handelingen van de regel zijn verwerkt. Het gebeurtenisobject dat aan `ruleTriggered` is doorgegeven, bevat informatie over de regel die is geactiveerd.

### `ruleCompleted`

Deze functie wordt aangeroepen nadat een regel volledig is verwerkt. Met andere woorden, de gebeurtenis heeft plaatsgevonden, alle voorwaarden zijn vervuld en alle handelingen zijn uitgevoerd. Het gebeurtenisobject dat aan `ruleCompleted` is doorgegeven, bevat informatie over de regel die is voltooid.

### `ruleConditionFailed`

Deze functie wordt aangeroepen nadat een regel is geactiveerd en een van de voorwaarden ervan is mislukt. Het gebeurtenisobject dat aan `ruleConditionFailed` is doorgegeven, bevat informatie over de regel die is geactiveerd en de voorwaarde die is mislukt.

Als `ruleTriggered` wordt geroepen, of `ruleCompleted` of `ruleConditionFailed` zal kort daarna worden geroepen.

>[!NOTE]
>
>Een monitor hoeft niet alle drie methoden op te geven (`ruleTriggered`, `ruleCompleted` en `ruleConditionFailed`). Tags in Adobe Experience Platform werken met alle ondersteunde methoden die door de monitor zijn geleverd.

### De monitor testen

In het bovenstaande voorbeeld worden alle drie methoden in de monitor opgegeven. Wanneer ze worden opgeroepen, meldt de monitor relevante informatie. Als u dit wilt testen, stelt u twee regels in de tagbibliotheek in:

1. Een regel die een klikgebeurtenis en een browser voorwaarde heeft die slechts overgaat als browser [!DNL Chrome] is.
1. Een regel die een klikgebeurtenis en een browser voorwaarde heeft die slechts overgaat als browser [!DNL Firefox] is.

Als u de pagina opent in [!DNL Chrome], open de browser console, en selecteer de pagina, verschijnt het volgende in de console:

![](../../images/debug.png)

Indien nodig kunnen extra haken of aanvullende informatie aan deze handlers worden toegevoegd.
