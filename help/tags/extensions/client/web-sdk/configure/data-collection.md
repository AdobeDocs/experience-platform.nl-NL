---
title: Instellingen voor gegevensverzameling
description: Configureer instellingen voor gegevensverzameling in de SDK-tagextensie voor het web.
exl-id: 88c34545-9a58-4d49-a939-36edaa9a46be
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 0%

---

# Instellingen voor gegevensverzameling {#data-collection}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datacollection"
>title="Dataverzameling"
>abstract="Bepaal welke gegevens moeten worden verzameld en hoe die gegevens worden verzameld over de tagextensie."

Deze configuratiesectie staat u toe om te bepalen hoe de gegevens over de uitbreiding worden verzameld.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Data collection]** .

![&#x200B; Beeld dat de montages van de gegevensinzameling van de de markeringsuitbreiding van SDK van het Web in de Markeringen UI toont.](../assets/web-sdk-ext-collection.png)

De volgende opties zijn beschikbaar:

## [!UICONTROL On before event send callback]

Een callback functie om de lading te evalueren en te wijzigen die naar Adobe wordt verzonden. In de code-editor hebt u toegang tot de volgende variabelen:

* **`content.xdm`**: De XDM-lading voor de gebeurtenis.
* **`content.data`**: De payload van het gegevensobject voor de gebeurtenis.
* **`return true`**: Sluit de callback onmiddellijk af en verzend gegevens naar Adobe met de huidige waarden in het `content` -object.
* **`return false`**: Sluit de callback onmiddellijk af en abort het verzenden van gegevens naar Adobe af.

Variabelen die buiten `content` worden gedefinieerd, kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar Adobe wordt verzonden.

>[!WARNING]
>
>Deze callback staat het gebruik van douanecode toe. Als een code die u in de callback opneemt, een niet-afgevangen uitzondering genereert, wordt de verwerking voor de gebeurtenis gestopt. **Gegevens worden niet verzonden naar Adobe.**

```js
// Use nullish coalescing assignments to add objects if they don't yet exist
content.xdm.commerce ??= {};
content.xdm.commerce.order ??= {};

// Then add the purchase ID
content.xdm.commerce.order.purchaseID = "12345";

// Use optional chaining to prevent undefined errors when setting tracking code to lower case
if(content.xdm.marketing?.trackingCode) content.xdm.marketing.trackingCode = content.xdm.marketing.trackingCode.toLowerCase();

// Delete operating system version
if(content.xdm.environment) delete content.xdm.environment.operatingSystemVersion;

// Immediately end onBeforeEventSend logic and send the data to Adobe for this event type
if (content.xdm.eventType === "web.webInteraction.linkClicks") {
  return true;
}

// Cancel sending data if it is a known bot
if (myBotDetector.isABot()) {
  return false;
}
```

>[!TIP]
>Retourneer `false` niet op de eerste gebeurtenis op een pagina. Het retourneren van `false` op de eerste gebeurtenis kan een negatieve invloed hebben op de personalisatie.

Deze callback is gelijk aan de tag [`onBeforeEventSend`](/help/collection/js/commands/configure/onbeforeeventsend.md) in de JavaScript-bibliotheek.

## [!UICONTROL Collect internal link clicks]

Een checkbox die de inzameling van verbinding het volgen gegevens intern aan uw plaats of bezit toelaat. Dit selectievakje is gelijk aan de tag [`clickCollection.internalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) in de JavaScript-bibliotheek. Wanneer u dit selectievakje inschakelt, worden opties voor gebeurtenisgroepering weergegeven:

* **[!UICONTROL No event grouping]**: Gegevens voor het bijhouden van koppelingen worden in afzonderlijke gebeurtenissen naar Adobe verzonden. Koppelingsklikken die in afzonderlijke gebeurtenissen worden verzonden, kunnen het contractuele gebruik van gegevens die naar Adobe Experience Platform worden verzonden verhogen.
* **[!UICONTROL Event grouping using session storage]**: Sla koppelingsvolggegevens op in de sessieopslag tot de volgende &quot;paginaweergave&quot;-gebeurtenis. Bij de volgende gebeurtenis die als een &quot;paginaweergave&quot; wordt beschouwd, worden de opgeslagen gegevens voor het bijhouden van koppelingen samengevoegd met de payload van de gebeurtenis &quot;paginaweergave&quot;. Adobe raadt u aan deze instelling in te schakelen bij het bijhouden van interne koppelingen.
* **[!UICONTROL Event grouping using local object]**: Sla koppelingsvolggegevens in een lokaal object op tot de volgende gebeurtenis &quot;paginaweergave&quot;. Als een bezoeker naar een nieuwe browserpagina navigeert, gaan de gegevens voor het bijhouden van koppelingen verloren. Deze instelling is het meest geschikt voor toepassingen van één pagina.

De tagbibliotheek beschouwt een bepaalde gebeurtenis als een &quot;paginaweergave&quot; wanneer de volgende elementen in de payload zijn opgenomen:

* `xdm.web.webPageDetails.name` bevat een tekenreekswaarde
* `xdm.web.webPageDetails.pageViews.value` is groter dan `0`

## [!UICONTROL Collect external link clicks]

Een selectievakje waarmee externe koppelingen kunnen worden verzameld. Dit selectievakje is gelijk aan de tag [`clickCollection.externalLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) in de JavaScript-bibliotheek.

## [!UICONTROL Collect download link clicks]

Een selectievakje waarmee downloadkoppelingen kunnen worden verzameld. Dit selectievakje is gelijk aan de tag [`clickCollection.downloadLinkEnabled`](/help/collection/js/commands/configure/clickcollection.md) in de JavaScript-bibliotheek.

## [!UICONTROL Download link qualifier]

Een reguliere expressie die een link-URL kwalificeert als een downloadkoppeling. Deze tekenreeks komt overeen met de tag [`downloadLinkQualifier`](/help/collection/js/commands/configure/downloadlinkqualifier.md) in de JavaScript-bibliotheek.

## [!UICONTROL Filter click properties]

Een callback functie om op klik betrekking hebbende eigenschappen vóór inzameling te evalueren en te wijzigen. Deze functie wordt uitgevoerd vóór de [!UICONTROL On before event send callback] en is gelijk aan de tag [`clickCollection.filterClickDetails`](/help/collection/js/commands/configure/clickcollection.md) in de JavaScript-bibliotheek. In de code-editor hebt u toegang tot de volgende variabelen:

* **`content.clickedElement`**: Het DOM-element waarop is geklikt.
* **`content.pageName`**: De paginanaam wanneer de klik voorkwam.
* **`content.linkName`**: De naam van de aangeklikte koppeling.
* **`content.linkRegion`**: Het gebied van de aangeklikte koppeling.
* **`content.linkType`**: Het type koppeling (afsluiten, downloaden of andere).
* **`content.linkURL`**: De doel-URL van de aangeklikte koppeling.
* **`return true`**: Sluit de callback onmiddellijk af met de huidige variabelewaarden.
* **`return false`**: Sluit de callback onmiddellijk af en sluit het verzamelen van gegevens af.
* Variabelen die buiten `content` worden gedefinieerd, kunnen worden gebruikt, maar worden niet opgenomen in de lading die naar Adobe wordt verzonden.

>[!TIP]
>
>Het veld **[!UICONTROL On before link click send]** is een afgekeurde callback die alleen zichtbaar is voor eigenschappen waarvoor deze al is geconfigureerd. De tag komt overeen met [`onBeforeLinkClickSend`](/help/collection/js/commands/configure/onbeforelinkclicksend.md) in de JavaScript-bibliotheek. Gebruik de callback van **[!UICONTROL Filter click properties]** om klikgegevens te filteren of aan te passen, of **[!UICONTROL On before event send callback]** te gebruiken om de algemene lading te filtreren of aan te passen die naar Adobe wordt verzonden. Wanneer zowel de callback als de callback **[!UICONTROL Filter click properties]** zijn ingesteld, wordt alleen de callback **[!UICONTROL On before link click send]** uitgevoerd.**[!UICONTROL Filter click properties]**

## Contextinstellingen

Verzamel automatisch bezoekersinformatie, die specifieke XDM gebieden voor u bevolkt. U kunt **[!UICONTROL All default context information]** of **[!UICONTROL Specific context information]** kiezen. De tag komt overeen met [`context`](/help/collection/js/commands/configure/context.md) in de JavaScript-bibliotheek.

* **[!UICONTROL Web]**: verzamelt informatie over de huidige pagina.
* **[!UICONTROL Device]**: verzamelt informatie over het apparaat van de gebruiker.
* **[!UICONTROL Environment]**: verzamelt informatie over de browser van de gebruiker.
* **[!UICONTROL Place context]**: verzamelt informatie over de locatie van de gebruiker.
* **[!UICONTROL High entropy user-agent hints]**: verzamelt meer gedetailleerde informatie over het apparaat van de gebruiker.
* **[!UICONTROL Send referrer to Adobe Analytics only once per page view]**: voorkom dat dubbele verwijzingsgegevens naar Adobe Analytics worden verzonden.
