---
title: De SDK van Adobe Experience Platform Web configureren
description: Leer hoe u de SDK van Adobe Experience Platform Web configureert.
seo-description: Leer hoe te om het Web SDK van het Experience Platform te vormen
keywords: configureren;configuratie;SDK;edge;Web SDK;configure;edgeConfigId;context;web;apparaat;omgeving;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk montages;prehideStyle;opacity;cookieDestinationEnabled;urlMigrationEnabled;idID Enabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
translation-type: tm+mt
source-git-commit: 2895975b9c103e6afba7db221223b4ef2116caf3
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 4%

---

# Vorm de SDK van het Web van het Platform

De configuratie voor SDK wordt gedaan met `configure` bevel.

>[!IMPORTANT]
>
>`configure` is altijd  ** het eerste geroepen bevel.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Er zijn vele opties die tijdens configuratie kunnen worden geplaatst. Alle opties zijn hieronder te vinden, gegroepeerd op categorie.

## Algemene opties

### `edgeConfigId`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | Geen |

{style=&quot;table-layout:auto&quot;}

Uw toegewezen configuratie-id, die de SDK koppelt aan de juiste accounts en configuratie. Wanneer het vormen van veelvoudige instanties binnen één enkele pagina, moet u verschillende `edgeConfigId` voor elke instantie vormen.

### `context`

| **Type** | **Vereist** | **Standaardwaarde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array van tekenreeksen | Nee | `["web", "device", "environment", "placeContext"]` |

{style=&quot;table-layout:auto&quot;}

Geeft aan welke contextcategorieën automatisch moeten worden verzameld, zoals beschreven in [Automatische informatie](../data-collection/automatic-information.md). Als deze configuratie niet wordt gespecificeerd, worden alle categorieën gebruikt door gebrek.

### `debugEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `false` |

{style=&quot;table-layout:auto&quot;}

Geeft aan of foutopsporing is ingeschakeld. Als u deze configuratie instelt op `true`, worden de volgende functies ingeschakeld:

| **Functie** | **-functie** |
| ---------------------- | ------------------ |
| Synchrone validatie | Valideert de gegevens die worden verzameld op basis van het schema en retourneert een fout in de reactie onder het volgende label: `collect:error OR success` |
| Logboek van console | Laat het zuiveren berichten toe om in de console van JavaScript van browser worden getoond |

{style=&quot;table-layout:auto&quot;}

### `edgeDomain` {#edge-domain}

Vul dit veld met uw domein van de eerste partij. Raadpleeg de [documentatie](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html) voor meer informatie.

Het domein is vergelijkbaar met `data.{customerdomain.com}` voor een website op www.{customerdomain.com}.

### `orgId`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | Geen |

{style=&quot;table-layout:auto&quot;}

Uw toegewezen [!DNL Experience Cloud] organisatie-id. Wanneer het vormen van veelvoudige instanties binnen een pagina, moet u verschillende `orgId` voor elke instantie vormen.

## Gegevensverzameling

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style=&quot;table-layout:auto&quot;}

Geeft aan of gegevens die aan koppelingsklikken zijn gekoppeld, automatisch worden verzameld. Zie [Automatische koppeling bijhouden](../data-collection/track-links.md#automaticLinkTracking) voor meer informatie.

### `onBeforeEventSend`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| -functie | Nee | () => undefined |

{style=&quot;table-layout:auto&quot;}

Vorm callback die voor elke gebeurtenis vlak alvorens het wordt verzonden wordt geroepen. Een object met het veld `xdm` wordt naar de callback verzonden. Als u wilt wijzigen wat wordt verzonden, wijzigt u het object `xdm`. Binnen callback, heeft het `xdm` voorwerp reeds de gegevens die in het gebeurtenisbevel worden overgegaan, en de automatisch verzamelde informatie. Zie [Gebeurtenissen globaal wijzigen](tracking-events.md#modifying-events-globally) voor meer informatie over de timing van deze callback en een voorbeeld.

## Privacyopties

### `defaultConsent` {#default-consent}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Object | Nee | `"in"` |

{style=&quot;table-layout:auto&quot;}

Hiermee stelt u de standaardtoestemming van de gebruiker in. Gebruik deze instelling als er nog geen voorkeur voor toestemming is opgeslagen voor de gebruiker. De andere geldige waarden zijn `"pending"` en `"out"`. Deze standaardwaarde wordt niet doorgevoerd in het profiel van de gebruiker. Het profiel van de gebruiker wordt alleen bijgewerkt wanneer `setConsent` wordt aangeroepen.
* `"in"`: Wanneer deze instelling is ingesteld of geen waarde is opgegeven, gaat het werk verder zonder voorkeuren voor gebruikerstoestemming.
* `"pending"`: Wanneer deze instelling is ingesteld, wordt het werk in de wachtrij geplaatst totdat de gebruiker voorkeuren voor toestemming geeft.
* `"out"`: Wanneer deze instelling is ingesteld, worden de werkzaamheden verwijderd totdat de gebruiker voorkeuren voor toestemming heeft ingesteld.
Nadat de voorkeuren van de gebruiker zijn opgegeven, gaat het werk door of wordt het afgebroken op basis van de voorkeuren van de gebruiker. Zie [Ondersteunende toestemming](../consent/supporting-consent.md) voor meer informatie.

## Persoonlijke opties

### `prehidingStyle`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Nee | Geen |

{style=&quot;table-layout:auto&quot;}

Wordt gebruikt om een CSS-stijldefinitie te maken die inhoudsgebieden van uw webpagina verbergt terwijl gepersonaliseerde inhoud van de server wordt geladen. Als deze optie niet wordt opgegeven, probeert de SDK geen inhoudsgebieden te verbergen terwijl gepersonaliseerde inhoud wordt geladen, wat mogelijk resulteert in &quot;flikkering&quot;.

Als een element op uw webpagina bijvoorbeeld een id heeft van `container`, waarvan u de standaardinhoud wilt verbergen terwijl gepersonaliseerde inhoud van de server wordt geladen, gebruikt u de volgende voorverbergingsstijl:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opties voor soorten publiek

### `cookieDestinationsEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style=&quot;table-layout:auto&quot;}

Hiermee schakelt u cookie-doelen [!DNL Audience Manager] in, zodat cookies kunnen worden ingesteld op basis van segmentkwalificatie.

### `urlDestinationsEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style=&quot;table-layout:auto&quot;}

Laat [!DNL Audience Manager] bestemmingen URL toe, die het vuren van URLs toestaat die op segmentkwalificatie wordt gebaseerd.

## Identiteitsopties

### `idMigrationEnabled` {#id-migration-enabled}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style=&quot;table-layout:auto&quot;}

Indien waar (true), leest de SDK oude AMCV-cookies en stelt deze in. Deze optie helpt bij het overstappen naar het gebruik van Adobe Experience Platform Web SDK, terwijl sommige delen van de site wellicht nog steeds Visitor.js gebruiken. Als de Bezoeker-API op de pagina is gedefinieerd, vraagt de SDK de Bezoeker-API voor de ECID. Met deze optie kunt u pagina&#39;s met twee tags toevoegen met de Adobe Experience Platform Web SDK en toch dezelfde ECID hebben.

### `thirdPartyCookiesEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style=&quot;table-layout:auto&quot;}

Hiermee schakelt u het instellen van cookies van derden voor Adobe in. De SDK kan de bezoekersidentiteitskaart in een derdecontext voortzetten om de zelfde bezoekersidentiteitskaart toe te laten om over plaatsen worden gebruikt. Gebruik deze optie als u veelvoudige plaatsen hebt of u gegevens met partners wilt delen; soms is deze optie echter om privacyredenen niet gewenst .
