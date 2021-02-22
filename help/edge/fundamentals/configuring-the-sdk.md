---
title: De SDK van Adobe Experience Platform Web configureren
description: Leer hoe u de SDK van Adobe Experience Platform Web configureert.
seo-description: Leer hoe te om het Web SDK van het Experience Platform te vormen
keywords: configureren;configuratie;SDK;edge;Web SDK;configure;edgeConfigId;context;web;apparaat;omgeving;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk montages;prehideStyle;opacity;cookieDestinationEnabled;urlMigrationEnabled;idID Enabled;thirdPartyCookiesEnabled;
translation-type: tm+mt
source-git-commit: 85bb984231a3069aad0c63707f5024612181798c
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 4%

---


# Vorm de SDK van het Web van het Platform

De configuratie voor SDK wordt gedaan met `configure` bevel.

>[!IMPORTANT]
>
>`configure` zou  ** altijd het eerste geroepen bevel moeten zijn.

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
| Tekenreeks | Ja | none |

Uw toegewezen configuratie-id, die de SDK koppelt aan de juiste accounts en configuratie.  Wanneer het vormen van veelvoudige instanties binnen één enkele pagina, moet u verschillende `edgeConfigId` voor elke instantie vormen.

### `context`

| **Type** | **Vereist** | **Standaardwaarde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array van tekenreeksen | Nee | `["web", "device", "environment", "placeContext"]` |

Geeft aan welke contextcategorieën automatisch moeten worden verzameld, zoals beschreven in [Automatische informatie](../data-collection/automatic-information.md).  Als deze configuratie niet wordt gespecificeerd, worden alle categorieën gebruikt door gebrek.

### `debugEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `false` |

Geeft aan of foutopsporing moet worden ingeschakeld. Als u deze configuratie instelt op `true`, worden de volgende functies ingeschakeld:

| **Functie** | **-functie** |
| ---------------------- | ------------------ |
| Synchrone validatie | Valideert de gegevens die worden verzameld op basis van het schema en retourneert een fout in de reactie onder het volgende label: `collect:error OR success` |
| Logboek van console | Laat het zuiveren berichten toe om in de console van JavaScript van browser worden getoond |

### `edgeDomain` {#edge-domain}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ------------------ |
| Tekenreeks | Nee | `beta.adobedc.net` |
| Tekenreeks | Nee | `omtrdc.net` |

Het domein dat wordt gebruikt om met de diensten van Adobe in wisselwerking te staan. Dit wordt slechts gebruikt als u een eerste partijdomein (CNAME) hebt dat volmachten verzoeken aan de de randinfrastructuur van de Adobe.

### `orgId`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | none |

Uw toegewezen [!DNL Experience Cloud] organisatie-id.  Wanneer het vormen van veelvoudige instanties binnen een pagina, moet u verschillende `orgId` voor elke instantie vormen.

## Gegevensverzameling

### `clickCollectionEnabled` {#clickCollectionEnabled}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Geeft aan of gegevens die aan koppelingsklikken zijn gekoppeld, automatisch moeten worden verzameld. Zie [Automatische koppeling bijhouden](../data-collection/track-links.md#automaticLinkTracking) voor meer informatie.

### `onBeforeEventSend`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| -functie | Nee | () => undefined |

Plaats dit om callback te vormen die voor elke gebeurtenis vlak alvorens het wordt verzonden wordt geroepen.  Een object met het veld `xdm` wordt naar de callback verzonden.  Wijzig het `xdm` voorwerp om te veranderen wat wordt verzonden.  Binnen callback, zal het `xdm` voorwerp reeds de gegevens hebben die in het gebeurtenisbevel worden overgegaan, en de automatisch verzamelde informatie. Zie [Gebeurtenissen globaal wijzigen](tracking-events.md#modifying-events-globally) voor meer informatie over de timing van deze callback en een voorbeeld.

## Privacyopties

### `defaultConsent` {#default-consent}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Object | Nee | `"in"` |

Hiermee stelt u de standaardtoestemming van de gebruiker in. Dit wordt gebruikt wanneer er geen voorkeur voor toestemming reeds voor de gebruiker wordt bewaard. De andere geldige waarde is `"pending"`. Wanneer deze is ingesteld, wordt het werk in de wachtrij geplaatst totdat de gebruiker voorkeuren voor toestemming heeft ingesteld. Nadat de voorkeuren van de gebruiker zijn opgegeven, gaat het werk door of wordt het afgebroken op basis van de voorkeuren van de gebruiker. Zie [Ondersteunende toestemming](../consent/supporting-consent.md) voor meer informatie.

## Persoonlijke opties

### `prehidingStyle`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Tekenreeks | Nee | none |

Wordt gebruikt om een CSS-stijldefinitie te maken die inhoudsgebieden van uw webpagina verbergt terwijl gepersonaliseerde inhoud van de server wordt geladen. Als deze optie niet wordt opgegeven, probeert de SDK geen inhoudsgebieden te verbergen terwijl gepersonaliseerde inhoud wordt geladen, wat mogelijk resulteert in &quot;flikkering&quot;.

Als u bijvoorbeeld een element op uw webpagina met een id van `container` hebt waarvan u de standaardinhoud wilt verbergen terwijl gepersonaliseerde inhoud wordt geladen van de server, ziet een voorbeeld van een vooraf verborgen stijl er als volgt uit:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opties voor soorten publiek

### `cookieDestinationsEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Hiermee schakelt u cookie-doelen [!DNL Audience Manager] in, zodat cookies kunnen worden ingesteld op basis van segmentkwalificatie.

### `urlDestinationsEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Laat [!DNL Audience Manager] bestemmingen URL toe, die het vuren van URLs toestaat die op segmentkwalificatie wordt gebaseerd.

## Identiteitsopties

### `idMigrationEnabled` {#id-migration-enabled}

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | true |

Indien waar (true), leest de SDK oude AMCV-cookies en stelt deze in. Dit helpt bij de overgang naar het gebruik van Adobe Experience Platform Web SDK, terwijl sommige delen van de site wellicht nog steeds Visitor.js gebruiken. Als de API voor bezoekers op de pagina is gedefinieerd, vraagt de SDK bovendien naar de API voor bezoekers voor de ECID. Op deze manier kunt u pagina&#39;s met twee tags plaatsen met de AEP Web SDK en toch dezelfde ECID hebben.

### `thirdPartyCookiesEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | true |

Hiermee schakelt u het instellen van cookies van derden voor Adobe in. De SDK kan de bezoekersidentiteitskaart in een derdecontext handhaven om de zelfde bezoekersidentiteitskaart toe te laten om over plaatsen worden gebruikt. Dit is nuttig als u veelvoudige plaatsen hebt of u gegevens met partners wilt delen; soms is dit echter om privacyredenen niet gewenst .
