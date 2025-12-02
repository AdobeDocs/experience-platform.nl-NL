---
title: registreerapparaat
description: Uitvoergegevens naar de browserconsole tijdens foutopsporing.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# `logger`

Het `_satellite.logger` voorwerp bevat methodes die u toestaan om kenmerkende of informatieberichten aan de browser console uit te voeren wanneer [&#x200B; het Zuiveren &#x200B;](../use-cases/debugging.md) wordt toegelaten. Als foutopsporing niet is ingeschakeld, doen alle aanroepen van de methode `logger` niets.

Met deze methoden kunnen ontwikkelaars, technische marketers en testers eenvoudig zien wat er wordt geactiveerd binnen een tag-eigenschap en wanneer. Aangezien deze consoleberichten slechts verschijnen wanneer het zuiveren wordt toegelaten, kunt u `logger` berichten in plaatsingen aan productie verlaten zonder de browser console van bezoekers aan uw plaats te beïnvloeden.

```ts
readonly _satellite.logger: {
  debug(...args: unknown[]): void;
  log(...args: unknown[]): void;
  info(...args: unknown[]): void;
  warn(...args: unknown[]): void;
  error(...args: unknown[]): void;
}
```

>[!TIP]
>
>Eerdere versies van het gebruikte tagobject `_satellite.notify()` . De functie `notify()` is vervangen door `_satellite.logger` .

## Methoden

Alle `_satellite.logger` -methoden geven de bijbehorende JavaScript `console.*` -methode door wanneer foutopsporing is ingeschakeld. De meeste `console` argumenten of objecten worden ondersteund met `_satellite.logger` :

| Methode | Doorsturen naar | Aanbevolen gebruik |
|---|---|---|
| `_satellite.logger.debug()` | `console.debug()` | Verbose diagnostiek; sommige browsers zouden uitgebreide logboekregistratie kunnen vereisen om het te zien. |
| `_satellite.logger.log()` | `console.log()` | Algemene berichten. |
| `_satellite.logger.info()` | `console.info()` | Informatieevenementen op hoog niveau. |
| `_satellite.logger.warn()` | `console.warn()` | Herstelbare problemen. De consoleingang wordt benadrukt geel. |
| `_satellite.logger.error()` | `console.error()` | Mislukt. De consoleingang wordt benadrukt rood. Adobe raadt u aan `error` -objecten te gebruiken voor stapels. |

```js
// First enable debugging mode
_satellite.setDebug(true);

// Logs a debug message
_satellite.logger.debug('Verbose diagnostic event');

// Logs a generic message
_satellite.logger.log('Example');

// Logs an informational message with mixed arguments
_satellite.logger.info('Rule triggered', 42, { ruleId: 'R123' }, ['a', 'b']);

// Logs a warning message
_satellite.logger.warn('Data element does not contain a value');

// Logs an error message with stack
_satellite.logger.error(new Error('Required extension not found'));
```

## Uitvoer van console

De bibliotheek voegt het volgende aan alle berichten van de consoleoutput voor:

* **🚀**: Hiermee kunt u gemakkelijk detecteren welke consoleberichten afkomstig zijn van de implementatie van uw tag.
* **\ [Oorsprong \]**: De regel, de actie, de uitbreiding, of naam van het gegevenselement waar het logboek van oorsprong was. Als u een logboekmethode buiten uw implementatie (zoals door de browser console) roept, wordt `[Custom Script]` gebruikt.
* **output van het Bericht**: De berichtoutput inbegrepen wanneer het aanhalen van de methode.

>[!NOTE]
>
>Browseropmaaktokens zoals `%c` , `%s` en `%d` worden niet toegepast vanwege het logger dat het voorvoegsel `🚀 [Origin]` toepast.
