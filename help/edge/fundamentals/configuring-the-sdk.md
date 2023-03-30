---
title: De SDK van Adobe Experience Platform Web configureren
description: Leer hoe u de SDK van Adobe Experience Platform Web configureert.
seo-description: Learn how to configure the Experience Platform Web SDK
keywords: configureren;configuratie;SDK;edge;Web SDK;configure;edgeConfigId;context;web;apparaat;omgeving;placeContext;debugEnabled;edgeDomain;orgId;clickCollectionEnabled;onBeforeEventSend;defaultConsent;web sdk montages;prehideStyle;opacity;cookieDestinationEnabled;urlMigrationEnabled;idID Enabled;thirdPartyCookiesEnabled;
exl-id: d1e95afc-0b8a-49c0-a20e-e2ab3d657e45
source-git-commit: a192a746fa227b658fcdb8caa07ea6fb4ac1a944
workflow-type: tm+mt
source-wordcount: '1128'
ht-degree: 3%

---

# Vorm de SDK van het Web van het Platform

De configuratie voor de SDK wordt uitgevoerd met de `configure` gebruiken.

>[!IMPORTANT]
>
>`configure` is *altijd* het eerste geroepen bevel.

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Er zijn vele opties die tijdens configuratie kunnen worden geplaatst. Alle opties vindt u hieronder, gegroepeerd op categorie.

## Algemene opties

### `edgeConfigId`

>[!NOTE]
>
>**Edge Configurations zijn omgedoopt tot gegevensstreams. Een gegevensstroom-id is hetzelfde als een configuratie-id.**

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | Geen |

{style="table-layout:auto"}

Uw toegewezen configuratie-id, die de SDK koppelt aan de juiste accounts en configuratie. Wanneer het vormen van veelvoudige instanties binnen één enkele pagina, moet u verschillende vormen `edgeConfigId` voor elke instantie.

### `context` {#context}

| **Type** | Vereist | **Standaardwaarde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array van tekenreeksen | Nee | `["web", "device", "environment", "placeContext", "highEntropyUserAgentHints"]` |

{style="table-layout:auto"}

Geeft aan welke contextcategorieën automatisch moeten worden verzameld, zoals beschreven in [Automatische informatie](../data-collection/automatic-information.md). Als deze configuratie niet wordt gespecificeerd, worden alle categorieën gebruikt door gebrek.

>[!IMPORTANT]
>
>Alle contexteigenschappen, met uitzondering van `highEntropyUserAgentHints`, zijn standaard ingeschakeld. Als u contexteigenschappen manueel in uw configuratie van SDK van het Web specificeerde, moet u alle contexteigenschappen toelaten om de noodzakelijke informatie te blijven verzamelen.

Inschakelen [hoge entropieclienthints](user-agent-client-hints.md#enabling-high-entropy-client-hints) op uw plaatsing van SDK van het Web, moet u extra omvatten `highEntropyUserAgentHints` naast uw bestaande configuratie.

Als u bijvoorbeeld hoge entropientroy-clienthints wilt ophalen van westeigenschappen, ziet uw configuratie er als volgt uit:

`context: ["highEntropyUserAgentHints", "web"]`


### `debugEnabled`

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `false` |

{style="table-layout:auto"}

Geeft aan of foutopsporing is ingeschakeld. Deze configuratie instellen op `true` schakelt de volgende functies in:

| **Functie** | **-functie** |
| ---------------------- | ------------------ |
| Logboek van console | Laat het zuiveren berichten toe om in de console van JavaScript van browser worden getoond |

{style="table-layout:auto"}

### `edgeDomain` {#edge-domain}

Vul dit veld met uw domein van de eerste partij. Zie voor meer informatie de [documentatie](https://experienceleague.adobe.com/docs/core-services/interface/ec-cookies/cookies-first-party.html).

Het domein is vergelijkbaar met `data.{customerdomain.com}` voor een website op www.{customerdomain.com}.

### `edgeBasePath` {#edge-base-path}

Pad na het edgeDomain dat wordt gebruikt voor communicatie en interactie met Adobe-services.  Vaak zou dit alleen veranderen wanneer de standaardproductieomgeving niet wordt gebruikt.

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Tekenreeks | Nee | ee |

{style="table-layout:auto"}

### `orgId`

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Tekenreeks | Ja | Geen |

{style="table-layout:auto"}

Uw toegewezen [!DNL Experience Cloud] organisatie-id. Wanneer het vormen van veelvoudige instanties binnen een pagina, moet u verschillende vormen `orgId` voor elke instantie.

## Gegevensverzameling

### `clickCollectionEnabled` {#clickCollectionEnabled}

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style="table-layout:auto"}

Geeft aan of gegevens die aan koppelingsklikken zijn gekoppeld, automatisch worden verzameld. Zie [Automatisch koppelen bijhouden](../data-collection/track-links.md#automaticLinkTracking) voor meer informatie . Koppelingen worden ook gelabeld als downloadkoppelingen als deze een downloadkenmerk bevatten of als de koppeling eindigt met een bestandsextensie. De de verbindingsbepalers van de download kunnen met een regelmatige uitdrukking worden gevormd. De standaardwaarde is `"\\.(exe|zip|wav|mp3|mov|mpg|avi|wmv|pdf|doc|docx|xls|xlsx|ppt|pptx)$"`

### `onBeforeEventSend`

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| -functie | Nee | () => undefined |

{style="table-layout:auto"}

Vorm callback die voor elke gebeurtenis vlak alvorens het wordt verzonden wordt geroepen. Een object met het veld `xdm` wordt verzonden binnen naar callback. Om te wijzigen wat wordt verzonden, wijzigt u de `xdm` object. Binnen de callback, `xdm` heeft de gegevens al doorgegeven in de gebeurtenisopdracht en de automatisch verzamelde informatie. Voor meer informatie over de timing van deze callback en een voorbeeld, zie [Gebeurtenissen globaal wijzigen](tracking-events.md#modifying-events-globally).

### `onBeforeLinkClickSend` {#onBeforeLinkClickSend}

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| -functie | Nee | () => undefined |

{style="table-layout:auto"}

Vorm callback die voor elke verbinding wordt geroepen klikt volgende gebeurtenis vlak alvorens het wordt verzonden. De callback verzendt een voorwerp met `xdm`, `clickedElement`, en `data` velden.

Wanneer het filtreren van de verbinding het volgen door de DOM elementenstructuur te gebruiken, kunt u gebruiken `clickElement` gebruiken. `clickedElement` is de DOM elementenknoop die werd geklikt en de boom van ouderknopen heeft ingekapseld.

Als u wilt wijzigen welke gegevens worden verzonden, wijzigt u de `xdm` en/of `data` objecten. Binnen de callback, `xdm` heeft de gegevens al doorgegeven in de gebeurtenisopdracht en de automatisch verzamelde informatie.

* Elke andere waarde dan `false` De gebeurtenis kan worden verwerkt en de callback kan worden verzonden.
* Als de callback het `false` waarde, gebeurtenisverwerking wordt gestopt, zonder fout, en de gebeurtenis wordt niet verzonden. Met dit mechanisme kunnen bepaalde gebeurtenissen worden gefilterd door de gebeurtenisgegevens te bekijken en te retourneren `false` als de gebeurtenis niet moet worden verzonden.
* Als callback een uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt en wordt de gebeurtenis niet verzonden.


## Privacyopties

### `defaultConsent` {#default-consent}

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Object | Nee | `"in"` |

{style="table-layout:auto"}

Hiermee stelt u de standaardtoestemming van de gebruiker in. Gebruik deze instelling als er nog geen voorkeur voor toestemming is opgeslagen voor de gebruiker. De andere geldige waarden zijn `"pending"` en `"out"`. Deze standaardwaarde wordt niet doorgevoerd in het profiel van de gebruiker. Het gebruikersprofiel wordt alleen bijgewerkt wanneer `setConsent` wordt aangeroepen.
* `"in"`: Wanneer deze instelling is ingesteld of geen waarde is opgegeven, gaat het werk verder zonder voorkeuren voor gebruikerstoestemming.
* `"pending"`: Wanneer deze instelling is ingesteld, wordt het werk in de wachtrij geplaatst totdat de gebruiker voorkeuren voor toestemming geeft.
* `"out"`: Wanneer deze instelling is ingesteld, worden de werkzaamheden verwijderd totdat de gebruiker voorkeuren voor toestemming heeft ingesteld.
Nadat de voorkeuren van de gebruiker zijn opgegeven, gaat het werk door of wordt het afgebroken op basis van de voorkeuren van de gebruiker. Zie [Ondersteunende toestemming](../consent/supporting-consent.md) voor meer informatie .

## Persoonlijke opties {#personalization}

### `prehidingStyle` {#prehidingStyle}

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Tekenreeks | Nee | Geen |

{style="table-layout:auto"}

Wordt gebruikt om een CSS-stijldefinitie te maken die inhoudsgebieden van uw webpagina verbergt terwijl gepersonaliseerde inhoud van de server wordt geladen. Als deze optie niet wordt opgegeven, probeert de SDK geen inhoudsgebieden te verbergen terwijl gepersonaliseerde inhoud wordt geladen, wat mogelijk resulteert in &quot;flikkering&quot;.

Als een element op uw webpagina bijvoorbeeld een id heeft van `container`, waarvan u de standaardinhoud wilt verbergen terwijl gepersonaliseerde inhoud van de server wordt geladen, gebruikt u de volgende voorverbergingsstijl:

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

### `targetMigrationEnabled` {#targetMigrationEnabled}

Deze optie moet worden gebruikt bij het migreren van afzonderlijke pagina&#39;s van [!DNL at.js] naar Web SDK.

Gebruik deze optie om de SDK van het Web toe te laten om de erfenis te lezen en te schrijven `mbox` en `mboxEdgeCluster` cookies die worden gebruikt door [!DNL at.js]. Zo kunt u het bezoekersprofiel behouden terwijl u overschakelt van een pagina die de SDK van Web gebruikt naar een pagina die de [!DNL at.js] bibliotheek en omgekeerd.

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `false` |

## Opties voor soorten publiek

### `cookieDestinationsEnabled`

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style="table-layout:auto"}

Inschakelen [!DNL Audience Manager] koekjesbestemmingen, die het plaatsen van koekjes toestaat die op segmentkwalificatie worden gebaseerd.

### `urlDestinationsEnabled`

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style="table-layout:auto"}

Inschakelen [!DNL Audience Manager] URL-doelen, waarmee URL&#39;s kunnen worden geactiveerd op basis van segmentkwalificatie.

## Identiteitsopties

### `idMigrationEnabled` {#id-migration-enabled}

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style="table-layout:auto"}

Indien waar (true), leest de SDK oude AMCV-cookies en stelt deze in. Deze optie helpt bij het overstappen naar het gebruik van Adobe Experience Platform Web SDK, terwijl sommige delen van de site wellicht nog steeds Visitor.js gebruiken.

Als de Bezoeker-API op de pagina is gedefinieerd, vraagt de SDK de Bezoeker-API voor de ECID. Met deze optie kunt u pagina&#39;s met twee tags toevoegen met de Adobe Experience Platform Web SDK en toch dezelfde ECID hebben.

### `thirdPartyCookiesEnabled`

| Type | Vereist | Standaardwaarde |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

{style="table-layout:auto"}

Hiermee schakelt u het instellen van cookies van derden voor Adobe in. De SDK kan de bezoekersidentiteitskaart in een derdecontext voortzetten om de zelfde bezoekersidentiteitskaart toe te laten om over plaatsen worden gebruikt. Gebruik deze optie als u veelvoudige plaatsen hebt of u gegevens met partners wilt delen; soms is deze optie echter om privacyredenen niet gewenst .
