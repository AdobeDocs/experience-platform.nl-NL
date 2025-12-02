---
title: _container
description: Zie de volledige tagcontainer in één object.
source-git-commit: 6f8bdfd09023ea48962a40a9539afe017bc108cc
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# `_container`

Het `_satellite._container` -object bevat de volledige configuratie en runtime context van de eigenschap tag die op de pagina is geladen. Alle informatie, zoals regels, gegevenselementen, extensies en omgevingen, is beschikbaar in dit object. Zijn primair gebruik moet bij het zuiveren van uw implementatie helpen zodat u precies kunt zien welke logica wordt blootgesteld of gepubliceerd.

```ts
readonly _satellite._container: {
  buildInfo: BuildInfo;
  company: Company;
  dataElements: { [name: string]: DataElement };
  environment: Environment;
  extensions: { [name: string]: Extension };
  property: Property;
  rules: Rule[];
}
```

>[!IMPORTANT]
>
>Dit object is alleen bedoeld voor foutopsporing. Koppel geen productielogica aan dit object, verwijs dit object in de implementatie of bewerk waarden in dit object. De beschikbaarheid van eigenschappen of namen in dit object kan op elk gewenst moment door Adobe worden gewijzigd.

## Beschikbare velden

De volgende objecten zijn ter referentie beschikbaar:

```json
{
  "buildInfo": {
    "minified": true,
    "buildDate": "YYYY-06-13T01:22:12Z"
  },
  "company": {
    "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
    "dynamicCdnEnabled": true,
    "cdnAllowList": [ "assets.adobedtm.com" ]
  },
  "dataElements": { ... },
  "environment": {
    "id": "EN6b2...d6ff2",
    "stage": "production"
  },
  "extensions": {
    "adobe-alloy": { ... },
    "core": { ... },
    "common-web-sdk-plugins": { ... }
  },
  "property": {
    "name": "Example tag property",
    "settings": {
      "domains": [ "example.com" ],
      "undefinedVarsReturnEmpty": false,
      "ruleComponentSequencingEnabled": true
    },
    "id": "PR845...6cf92"
  },
  "rules": [ { ... } ]
}
```

## `buildInfo`

Het `_satellite._container.buildInfo` -object bevat een kopie van [`_satellite.buildInfo`](buildinfo.md) .

```ts
readonly _satellite._container.buildInfo: {
  minified: boolean;
  buildDate: string;
  turbineBuildDate: string;
  turbineVersion: string;
}
```

## `company`

Het `_satellite._container.company` -object bevat een kopie van [`_satellite.company`](company.md) .

```ts
readonly _satellite._container.company: {
  orgId: string;
  dynamicCdnEnabled: boolean;
  cdnAllowList: string[];
}
```

## `dataElements`

Het `_satellite._container.dataElements` -object biedt een verwijzing naar alle gegevenselementen in de eigenschap tag.

```ts
readonly _satellite._container.dataElements: {
  [name: string]: {
    modulePath: string;
    settings: Settings; // Varies by data element type
  }
}
```

Elk gegevenselement bevat de volgende eigenschappen:

| Naam | Type | Beschrijving |
|---|---|---|
| **`modulePath`** | `string` | Het pad van het JavaScript-bestand dat de logica van dat gegevenstype data bepaalt. |
| **`settings`** | `Settings` | De instellingen van het gegevenselement. Eigenschappen in dit object zijn afhankelijk van het type gegevenselement. |

## `environment`

Het `_satellite._container.environment` -object bevat een kopie van [`_satellite.environment`](environment.md) .

```ts
readonly _satellite._container.environment: {
  id: string;
  stage: string;
}
```

## `extensions`

In het `_satellite._container.extensions` -object worden alle extensies weergegeven die naar de eigenschap tag zijn gepubliceerd.

```ts
readonly _satellite._container.extensions: {
  [name: string]: {
    displayName: string;
    hostedLibFilesUrl: string;
    modules: Modules; // Extension-specific module definitions
  }
}
```

Elke extensie bevat de volgende eigenschappen:

| Naam | Type | Beschrijving |
|---|---|---|
| **`displayName`** | `string` | De vriendelijke naam van de extensie. |
| **`hostedLibFilesUrl`** | `string` | De plaats op CDN waar de uitbreiding verblijft. |
| **`modules`** | `Modules` | De JavaScript-logica voor alle gebeurtenissen, handelingen, voorwaarden en gegevenselementen die de extensie gebruikt. De inhoud van dit object verschilt per extensie. |

## `property`

Het `_satellite._container.property` -object biedt informatie over de eigenschap tag zelf.

```ts
readonly _satellite._container.property: {
  id: string;
  name: string;
  settings: {
    domains: string[];
    ruleComponentSequencingEnabled: boolean;
    undefinedVarsReturnEmpty: boolean;
  };
}
```

| Naam | Type | Beschrijving |
|---|---|---|
| **`id`** | `string` | De unieke id voor de eigenschap tag. |
| **`name`** | `string` | De vriendelijke naam voor de eigenschap tag. |
| **`settings`** | `PropertySettings` | Instellingen voor deze eigenschap. Zie de onderstaande tabel. |

| Naam instellen | Type | Beschrijving |
|---|---|---|
| **`domains`** | `string[]` | De gevormde domeinen voor het bezit, zoals geplaatst wanneer [ vormend een markeringsbezit ](/help/tags/ui/administration/companies-and-properties.md). |
| **`ruleComponentSequencingEnabled`** | `boolean` | Hiermee wordt bepaald of het selectievakje **[!UICONTROL Run rule components in sequence]** is ingeschakeld bij het configureren van de eigenschap tag. |
| **`undefinedVarsReturnEmpty`** | `boolean` | Hiermee wordt bepaald of het selectievakje **[!UICONTROL Return an empty string for undefined data elements]** is ingeschakeld bij het configureren van de eigenschap tag. |

## `_container.rules`

De array met objecten `rules` bevat een verwijzing naar alle regels in de eigenschap tag.

```ts
readonly _satellite._container.rules: {
  id: string;
  name: string;
  events: Event[]; // Rule-specific events
  conditions: Condition[]; // Rule-specific conditions
  actions: Action[]; // Rule-specific actions
}[]
```

Elke regel bevat de volgende velden:

| Naam | Type | Beschrijving |
|---|---|---|
| **`id`** | `string` | De unieke id voor de regel. |
| **`name`** | `string` | De vriendelijke naam van de regel. |
| **`events`** | `Event[]` | Een serie van gebeurtenissen die u hebt gevormd om de regel teweeg te brengen. |
| **`conditions`** | `Condition[]` | Een serie van voorwaarden die u hebt gevormd om de regel teweeg te brengen. |
| **`actions`** | `Action[]` | Een serie van acties die u hebt gevormd om uit te voeren wanneer de regel wordt teweeggebracht. |
