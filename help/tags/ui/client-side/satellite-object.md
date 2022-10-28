---
title: Verwijzing naar satellietobject
description: Leer meer over het client-side _satelliet object en de verschillende functies die u ermee kunt uitvoeren in tags.
exl-id: f8b31c23-409b-471e-bbbc-b8f24d254761
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1290'
ht-degree: 1%

---

# Verwijzing naar satellietobject

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Dit document fungeert als referentie voor de client `_satellite` -object en de verschillende functies die u ermee kunt uitvoeren.

## `track`

**Code**

```javascript
_satellite.track(identifier: string [, detail: *] )
```

**Voorbeeld**

```javascript
_satellite.track('contact_submit', { name: 'John Doe' });
```

`track` brandt alle regels gebruikend het Directe gebeurtenistype van de Vraag dat met het bepaalde herkenningsteken van de de markeringsuitbreiding van de Kern is gevormd. Het bovenstaande voorbeeld brengt alle regels teweeg gebruikend een Directe gebeurtenistype van de Vraag waar het gevormde herkenningsteken is `contact_submit`. Er wordt ook een optioneel object met gerelateerde informatie doorgegeven. U kunt het detailobject openen door `%event.detail%` in een tekstveld in een voorwaarde of handeling of `event.detail` in de code-editor in een aangepaste codevoorwaarde of -handeling.

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

>[!NOTE]
>
>U kunt percentages gebruiken (`%`) syntaxis gebruiken om te verwijzen naar variabelen voor vele formuliervelden in uw tagimplementatie, waardoor de noodzaak om te bellen afneemt `_satellite.getVar()`. Als u bijvoorbeeld `%product%` heeft toegang tot de waarde van het element met productgegevens of de aangepaste variabele.

Wanneer een gebeurtenis een regel teweegbrengt, kunt u het overeenkomstige regeltype overgaan `event` object in `_satellite.getVar()` zoals:

```javascript
// event refers to the calling rule's event
var rule = _satellite.getVar('return event rule', event);
```

## `setVar`

**Code**

```javascript
_satellite.setVar(name: string, value: *)
```

**Voorbeeld**

```javascript
_satellite.setVar('product', 'Circuit Pro');
```

`setVar()` Hiermee stelt u een aangepaste variabele in met een bepaalde naam en waarde. De waarde van de variabele kan later worden benaderd met `_satellite.getVar()`.

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

Als de [!DNL Adobe Experience Cloud ID] Als de extensie op de eigenschap is geïnstalleerd, retourneert deze methode de instantie van de bezoeker-id. Zie de [Documentatie Experience Cloud ID-service](https://experienceleague.adobe.com/docs/id-service/using/home.html) voor meer informatie .

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

De `logger` Met dit object kan een bericht worden aangemeld bij de browserconsole. Het bericht wordt alleen weergegeven als foutopsporing van tags is ingeschakeld door de gebruiker (door `_satellite.setDebug(true)` of met een geschikte browserextensie).

### Waarschuwingen bij deponering van registratie

```javascript
_satellite.logger.deprecation(message: string)
```

**Voorbeeld**

```javascript
_satellite.logger.deprecation('This method is no longer supported, please use [new example] instead.');
```

Dit registreert een waarschuwing aan de browser console. Het bericht wordt weergegeven of foutopsporing van tags is ingeschakeld door de gebruiker.

## `cookie` {#cookie}

`_satellite.cookie` bevat functies voor het lezen en schrijven van cookies. Het is een belichte kopie van de externe bibliotheek js-cookie. Voor meer informatie over geavanceerd gebruik van deze bibliotheek raadpleegt u de [js-cookie documentatie](https://www.npmjs.com/package/js-cookie#basic-usage).

### Een cookie instellen {#cookie-set}

Als u een cookie wilt instellen, gebruikt u `_satellite.cookie.set()`.

**Code**

```javascript
_satellite.cookie.set(name: string, value: string[, attributes: Object])
```

>[!NOTE]
>
>In het oude [`setCookie`](#setCookie) Bij het instellen van cookies was het derde (optionele) argument voor deze functieaanroep een geheel getal dat de vervaltijd van het cookie in dagen aangeeft. In deze nieuwe methode wordt een object &quot;attributes&quot; geaccepteerd als een derde argument. Als u een vervaldatum voor een cookie wilt instellen met de nieuwe methode, moet u een `expires` in het object attributes en stel dit in op de gewenste waarde. Dit wordt in het onderstaande voorbeeld getoond.

**Voorbeeld**

Met de volgende functieaanroep wordt een cookie geschreven die in een week verloopt.

```javascript
_satellite.cookie.set('product', 'Circuit Pro', { expires: 7 });
```

### Een cookie ophalen {#cookie-get}

Als u een cookie wilt ophalen, gebruikt u `_satellite.cookie.get()`.

**Code**

```javascript
_satellite.cookie.get(name: string) => string
```

**Voorbeeld**

De volgende functieaanroep leest een eerder ingesteld cookie.

```javascript
var product = _satellite.cookie.get('product');
```

### Een cookie verwijderen {#cookie-remove}

Als u een cookie wilt verwijderen, gebruikt u `_satellite.cookie.remove()`.

**Code**

```javascript
_satellite.cookie.remove(name: string)
```

**Voorbeeld**

De volgende functieaanroep verwijdert een eerder ingestelde cookie.

```javascript
_satellite.cookie.remove('product');
```

## `buildInfo`

**Code**

```javascript
_satellite.buildInfo
```

Dit object bevat informatie over de build van de huidige tagruntimebibliotheek. Het object bevat de volgende eigenschappen:

### `turbineVersion`

Dit biedt de [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) in de huidige bibliotheek wordt gebruikt.

### `turbineBuildDate`

De ISO 8601-datum waarop de versie van [Turbine](https://www.npmjs.com/package/@adobe/reactor-turbine) in de container is gebruikt.

### `buildDate`

De ISO 8601-datum waarop de huidige bibliotheek is gemaakt.

In dit voorbeeld worden de objectwaarden getoond:

```javascript
{
  turbineVersion: "14.0.0",
  turbineBuildDate: "2016-07-01T18:10:34Z",
  buildDate: "2016-03-30T16:27:10Z"
}
```

## `environment`

Dit object bevat informatie over de omgeving waarin de huidige tagruntime-bibliotheek wordt geïmplementeerd.

**Code**

```javascript
_satellite.environment
```

Het object bevat de volgende eigenschappen:

```javascript
{
  id: "ENbe322acb4fc64dfdb603254ffe98b5d3",
  stage: "development"
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `id` | De id van het milieu. |
| `stage` | De omgeving waarvoor deze bibliotheek is gemaakt. De mogelijke waarden zijn: `development`, `staging`, en `production`. |

## `notify`

>[!NOTE]
>
>Deze methode is vervangen. Gebruik `_satellite.logger.log()` in plaats daarvan.

**Code**

```javascript
_satellite.notify(message: string[, level: number])
```

**Voorbeeld**

```javascript
_satellite.notify('Hello world!');
```

`notify` logt een bericht aan de browser console. Het bericht wordt alleen weergegeven als foutopsporing van tags is ingeschakeld door de gebruiker (door `_satellite.setDebug(true)` of met een geschikte browserextensie).

Een facultatief registrerenniveau kan worden overgegaan dat het stileren en het filtreren van het bericht zal beïnvloeden dat wordt geregistreerd. De ondersteunde niveaus zijn als volgt:

3 - Informatieberichten.

4 - Waarschuwingsberichten.

5 - Foutberichten.

Als u geen registrerenniveau verstrekt of geen andere niveauwaarde overgaat, zal het bericht als regelmatig bericht worden geregistreerd.

## `setCookie` {#setCookie}

>[!IMPORTANT]
>
>Deze methode is vervangen. Gebruik [`_satellite.cookie.set()`](#cookie-set) in plaats daarvan.

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

>[!IMPORTANT]
>
>Deze methode is vervangen. Gebruik [`_satellite.cookie.get()`](#cookie-get) in plaats daarvan.

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
>Deze methode is vervangen. Gebruik [`_satellite.cookie.remove()`](#cookie-remove) in plaats daarvan.

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

Voeg op uw webpagina met een tagbibliotheek een codefragment toe aan de HTML. Doorgaans wordt de code ingevoegd in de `<head>` element voor het `<script>` element dat de tagbibliotheek laadt. Hierdoor kan de monitor de vroegste systeemgebeurtenissen afvangen die in de tagbibliotheek voorkomen. Bijvoorbeeld:

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

In het eerste scriptelement, omdat de tagbibliotheek nog niet is geladen, wordt het eerste `_satellite` object wordt gemaakt en er wordt een array op `_satellite._monitors` is geïnitialiseerd. Het script voegt vervolgens een monitorobject aan die array toe. Het monitorobject kan de volgende methoden opgeven, die later door de tagbibliotheek worden aangeroepen:

### `ruleTriggered`

Deze functie wordt aangeroepen nadat een gebeurtenis een regel activeert, maar voordat de voorwaarden en handelingen van de regel zijn verwerkt. Het gebeurtenisobject dat wordt doorgegeven aan `ruleTriggered` bevat informatie over de regel die is geactiveerd.

### `ruleCompleted`

Deze functie wordt aangeroepen nadat een regel volledig is verwerkt. Met andere woorden, de gebeurtenis heeft plaatsgevonden, alle voorwaarden zijn vervuld en alle handelingen zijn uitgevoerd. Het gebeurtenisobject dat wordt doorgegeven aan `ruleCompleted` bevat informatie over de regel die is voltooid.

### `ruleConditionFailed`

Deze functie wordt aangeroepen nadat een regel is geactiveerd en een van de voorwaarden ervan is mislukt. Het gebeurtenisobject dat wordt doorgegeven aan `ruleConditionFailed` bevat informatie over de regel die is geactiveerd en de voorwaarde die is mislukt.

Indien `ruleTriggered` wordt aangeroepen, ofwel `ruleCompleted` of `ruleConditionFailed` zal kort daarna worden geroepen.

>[!NOTE]
>
>Een monitor hoeft niet alle drie de methoden op te geven (`ruleTriggered`, `ruleCompleted`, en `ruleConditionFailed`). Tags in Adobe Experience Platform werken met alle ondersteunde methoden die door de monitor zijn geleverd.

### De monitor testen

In het bovenstaande voorbeeld worden alle drie methoden in de monitor opgegeven. Wanneer ze worden opgeroepen, meldt de monitor relevante informatie. Als u dit wilt testen, stelt u twee regels in de tagbibliotheek in:

1. Een regel die een klikgebeurtenis en een browser voorwaarde heeft die slechts overgaat als browser is [!DNL Chrome].
1. Een regel die een klikgebeurtenis en een browser voorwaarde heeft die slechts overgaat als browser is [!DNL Firefox].

Als u de pagina opent in [!DNL Chrome], opent u de browserconsole en selecteert u de pagina. In de console wordt het volgende weergegeven:

![](../../images/debug.png)

Indien nodig kunnen extra haken of aanvullende informatie aan deze handlers worden toegevoegd.
