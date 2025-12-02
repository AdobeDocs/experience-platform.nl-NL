---
title: milieu
description: De ontwikkelomgeving die momenteel door de eigenschap tag wordt gebruikt.
source-git-commit: 434d6913ea391b127b4b52c8494730c496bbcfe2
workflow-type: tm+mt
source-wordcount: '61'
ht-degree: 4%

---

# `environment`

De `_satellite.environment` -objectstatussen die een omgeving bouwen die de tag-eigenschap momenteel gebruikt.

```js
readonly _satellite.environment: Environment
```

## Beschikbare velden

De volgende velden zijn beschikbaar wanneer u dit object aanroept.

```json
{
  "id": "EN6b2...d6ff2",
  "stage": "production"
}
```

| Naam | Type | Beschrijving |
|---|---|---|
| **`id`** | `string` | De unieke id voor de omgeving. U kunt de milieu-id zoeken door het pictogram **[!UICONTROL Install]** onder [[!UICONTROL Environments]](/help/tags/ui/publishing/environments.md) te selecteren in de interface voor tags. |
| **`stage`** | `development \| staging \| production` | Het omgevingstype. |
