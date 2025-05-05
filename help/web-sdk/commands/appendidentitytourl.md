---
title: appendIdentityToUrl
description: Lever persoonlijke ervaringen nauwkeuriger tussen apps, het Web, en over domeinen.
exl-id: 09dd03bd-66d8-4d53-bda8-84fc4caadea6
source-git-commit: 7c262e5819f8e3488c5ddd5a0221d1c52c28c029
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 1%

---

# `appendIdentityToUrl`

Met de opdracht `appendIdentityToUrl` kunt u een gebruiker-id aan de URL toevoegen als een queryreeks. Met deze actie kunt u de identiteit van een bezoeker tussen domeinen dragen, waardoor dubbele bezoekersaantallen voor datasets met zowel domeinen als kanalen worden voorkomen. Het is beschikbaar op het Web SDK versie 2.11.0 of later.

De querytekenreeks die wordt gegenereerd en aan de URL wordt toegevoegd, is `adobe_mc` . Als het Web SDK geen ECID kan vinden, roept het het `/acquire` eindpunt om te produceren.

>[!NOTE]
>
>Als er geen toestemming is gegeven, wordt de URL van deze methode ongewijzigd geretourneerd. Deze opdracht wordt onmiddellijk uitgevoerd; er wordt niet gewacht op een toestemmingsupdate.

## Identiteit toevoegen aan URL met de extensie Web SDK {#extension}

Het toevoegen van een identiteit aan een URL wordt uitgevoerd als een actie binnen een regel in de interface van de markeringen van de Inzameling van Gegevens van Adobe Experience Platform.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Redirect with identity]** .
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

Dit bevel wordt typisch gebruikt met een specifieke regel die op kliks en controles gewenste domeinen let.

+++Gebeurteniscriteria van de regel

Triggers wanneer op een ankertag met een eigenschap `href` wordt geklikt.

* **[!UICONTROL Extension]**: Kern
* **[!UICONTROL Event type]**: klikken
* **[!UICONTROL When the user clicks on]**: specifieke elementen
* **[!UICONTROL Elements matching the CSS selector]**: `a[href]`

![ gebeurtenis van de Regel ](../assets/id-sharing-event-configuration.png)

+++

+++voorwaarde van de regel

Triggers worden alleen op de gewenste domeinen geactiveerd.

* **[!UICONTROL Logic type]**: Standaard
* **[!UICONTROL Extension]**: Kern
* **[!UICONTROL Condition Type]**: vergelijking van waarden
* **[!UICONTROL Left Operand]**: `%this.hostname%`
* **[!UICONTROL Operator]**: Komt overeen met Regex
* **[!UICONTROL Right Operand]**: Een reguliere expressie die overeenkomt met de gewenste domeinen. Bijvoorbeeld: `adobe.com$|behance.com$`

![ voorwaarde van de Regel ](../assets/id-sharing-condition-configuration.png)

+++

+++Handeling Rule

Voeg de identiteit toe aan de URL.

* **[!UICONTROL Extension]**: Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**: Omleiden met identiteit

![ actie van de Regel ](../assets/id-sharing-action-configuration.png)

+++

## Identiteit toevoegen aan URL met de Web SDK JavaScript-bibliotheek

Voer de opdracht `appendIdentityToUrl` uit met een URL als parameter. De methode retourneert een URL waarvan de id als queryreeks is toegevoegd.

```js
alloy("appendIdentityToUrl",
  {
    url: document.location.href
  }
);
```

U kunt een gebeurtenislistener toevoegen voor alle klikken die op de pagina worden ontvangen en controleren of de URL overeenkomt met de gewenste domeinen. Als dit het geval is, voegt u de identiteit toe aan de URL en leidt u de gebruiker om.

```js
document.addEventListener("click", event => {
  // Check if the click was a link
  const anchor = event.target.closest("a");
  if (!anchor || !anchor.href) return;

  // Check if the link points to the desired domain
  const url = new URL(anchor.href);
  if (!url.hostname.endsWith(".adobe.com") && !url.hostname.endsWith(".behance.com")) return;

  // Append the identity to the URL, then direct the user to the URL
  event.preventDefault();
  alloy("appendIdentityToUrl", {url: anchor.href}).then(result => {document.location = result.url;});
});
```

## Object Response

Als u besluit om reacties [&#128279;](command-responses.md) met dit bevel  te behandelen, bevat het reactievoorwerp **`url`**, nieuwe URL met identiteitsinformatie die als parameter van het vraagkoord wordt toegevoegd.
