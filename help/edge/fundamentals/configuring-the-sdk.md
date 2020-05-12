---
title: De SDK configureren
seo-title: De Adobe Experience Platform Web SDK configureren
description: Leer hoe te om het Platform van de Ervaring te vormen SDK van het Web
seo-description: Leer hoe te om het Platform van de Ervaring te vormen SDK van het Web
translation-type: tm+mt
source-git-commit: 767f0e1bfdfcc898313b546c804ba1287f2aec50
workflow-type: tm+mt
source-wordcount: '765'
ht-degree: 0%

---


# (Beta) Het vormen SDK

>[!IMPORTANT]
>
>De Adobe Experience Platform Web SDK is momenteel in bèta en is niet beschikbaar voor alle gebruikers. De documentatie en de functionaliteit kunnen worden gewijzigd.

De configuratie voor SDK wordt gedaan met het `configure` bevel.

>[!Ibelangrijk]
>`configure` zou _altijd_ het eerste geroepen bevel moeten zijn.

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId":"ADB3LETTERSANDNUMBERS@AdobeOrg"
});
```

Er zijn vele opties die tijdens configuratie kunnen worden geplaatst. Alle opties vindt u hieronder, gegroepeerd op categorie.

## Algemene opties

### `configId`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| String | Ja | none |

Uw toegewezen configuratie-id, die de SDK koppelt aan de juiste accounts en configuratie.  Wanneer het vormen van veelvoudige instanties binnen één enkele pagina, moet u een verschillende `configId` voor elke instantie vormen.

### `context`

| **Type** | **Vereist** | **Standaardwaarde** |
| ---------------- | ------------ | -------------------------------------------------- |
| Array van tekenreeksen | Nee | `["web", "device", "environment", "placeContext"]` |

Geeft aan welke contextcategorieën automatisch worden verzameld, zoals wordt beschreven in [Automatische informatie](../reference/automatic-information.md).  Als deze configuratie niet wordt gespecificeerd, worden alle categorieën gebruikt door gebrek.

### `debugEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `false` |

Geeft aan of foutopsporing moet worden ingeschakeld. Het plaatsen van dit config om de volgende eigenschappen toe te `true` laten:

| **Functie** |  |  |
| ---------------------- | ------------------ |
| Synchrone validatie | Valideert de gegevens die worden verzameld op basis van het schema en retourneert een fout in de reactie onder het volgende label: `collect:error OR success` |
| Logboek van console | Laat het zuiveren berichten toe om in de console van JavaScript van browser worden getoond |

### `edgeDomain`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ------------------ |
| String | Nee | `beta.adobedc.net` |

Het domein dat wordt gebruikt voor interactie met Adobe Services. Dit wordt alleen gebruikt als u een domein van de eerste partij (CNAME) hebt dat proxy&#39;s aanvragen bij de Adobe Edge-infrastructuur.

### `orgId`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| String | Ja | none |

Uw toegewezen Experience Cloud-organisatie-id.  Wanneer het vormen van veelvoudige instanties binnen een pagina, moet u een verschillende `orgId` voor elke instantie vormen.

## Gegevensverzameling

### `clickCollectionEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Geeft aan of gegevens die aan koppelingsklikken zijn gekoppeld, automatisch moeten worden verzameld. Voor kliks die als verbinding kwalificeren klikt, worden de volgende gegevens van de Interactie [van het](https://github.com/adobe/xdm/blob/master/docs/reference/context/webinteraction.schema.md) Web verzameld:

| **Eigenschap** |  |
| ------------ | ----------------------------------- |
| Koppelingsnaam | Naam die wordt bepaald door de context van de koppeling |
| Koppelings-URL | Genormaliseerde URL |
| Koppelingstype | Instellen op downloaden, afsluiten of andere |

### `onBeforeEventSend`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| -functie | Nee | () => undefined |

Plaats dit om callback te vormen die voor elke gebeurtenis vlak alvorens het wordt verzonden wordt geroepen.  Een object met het veld `xdm` wordt naar de callback verzonden.  Wijzig het xdm-object om te wijzigen wat wordt verzonden.  Binnen callback, zal het `xdm` voorwerp reeds de gegevens hebben die in het gebeurtenisbevel worden overgegaan, en de automatisch verzamelde informatie.  Zie Gebeurtenissen globaal [wijzigen voor meer informatie over de timing van deze callback en een voorbeeld](tracking-events.md#modifying-events-globally).

## Privacyopties

### `defaultConsent`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Object | Nee | `{"general": "in"}` |

Hiermee stelt u de standaardtoestemming van de gebruiker in. Dit wordt gebruikt wanneer er geen voorkeur voor toestemming reeds voor de gebruiker wordt bewaard. De andere geldige waarde is `{"general": "pending"}`. Wanneer deze is ingesteld, wordt het werk in de wachtrij geplaatst totdat de gebruiker voorkeuren voor toestemming heeft ingesteld. Nadat de voorkeuren van de gebruiker zijn opgegeven, gaat het werk door of wordt het afgebroken op basis van de voorkeuren van de gebruiker. Zie [Ondersteunende toestemming](supporting-consent.md) voor meer informatie.

## Persoonlijke opties

### `prehidingStyle`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| String | Nee | none |

Wordt gebruikt om een CSS-stijldefinitie te maken die inhoudsgebieden van uw webpagina verbergt terwijl gepersonaliseerde inhoud van de server wordt geladen. Als deze optie niet wordt opgegeven, probeert de SDK geen inhoudsgebieden te verbergen terwijl gepersonaliseerde inhoud wordt geladen, wat mogelijk resulteert in &quot;flikkering&quot;.

Als u bijvoorbeeld een element op uw webpagina had met een id waarvan u de standaardinhoud wilt verbergen terwijl gepersonaliseerde inhoud wordt geladen van de server, ziet een voorbeeld van een vooraf verborgen stijl er als volgt uit: `container`

```javascript
  prehidingStyle: "#container { opacity: 0 !important }"
```

## Opties voor soorten publiek

### `cookieDestinationsEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Laat koekjesbestemmingen toe, die het plaatsen van koekjes toestaat die op segmentkwalificatie worden gebaseerd.

### `urlDestinationsEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Laat bestemmingen URL toe, die het vuren van URLs toestaat die op segmentkwalificatie wordt gebaseerd.

## Identiteitsopties

### `idSyncContainerId`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Getal | Nee | none |

De container-id die aangeeft welke ID-syncs worden geactiveerd. Dit is een niet-negatief geheel getal dat u kunt verkrijgen van uw consultant.

### `idSyncEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | `true` |

Hiermee schakelt u de functie voor het synchroniseren van id&#39;s in. Hiermee kunnen URL&#39;s worden geactiveerd om de unieke gebruikers-id van Adobe te synchroniseren met de unieke gebruikers-id van een gegevensbron van derden.

### `thirdPartyCookiesEnabled`

| **Type** | **Vereist** | **Standaardwaarde** |
| -------- | ------------ | ----------------- |
| Boolean | Nee | true |

Hiermee schakelt u het instellen van cookies van derden van Adobe in. De SDK kan de bezoekersidentiteitskaart in een derdecontext handhaven om de zelfde bezoekersidentiteitskaart toe te laten om over plaats te gebruiken. Dit is nuttig als u veelvoudige plaatsen hebt of u gegevens met partners wilt delen; soms is dit echter om privacyredenen niet gewenst .
