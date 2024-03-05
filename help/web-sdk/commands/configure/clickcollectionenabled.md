---
title: clickCollectionEnabled
description: Bepaal of de gegevens van de verbindingsklik automatisch worden verzameld.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '276'
ht-degree: 0%

---


# `clickCollectionEnabled`

De `clickCollectionEnabled` bezit is een booleaanse waarde die bepaalt als het Web SDK automatisch verbindingsgegevens verzamelt. Deze eigenschap is nuttig wanneer u koppelingsgegevens liever handmatig bijhoudt.

Als deze optie niet is uitgeschakeld, worden de volgende XDM-elementen automatisch gevuld met gegevens:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

## Logica voor automatisch bijhouden van koppelingen

De SDK van het Web volgt allen klikken op `<a>` en `<area>` HTML-elementen als deze geen `onClick` kenmerk. Klikken worden vastgelegd met een [vastleggen](https://www.w3.org/TR/uievents/#capture-phase) Klik op de gebeurtenislistener die aan het document is gekoppeld. Wanneer op een geldige koppeling wordt geklikt, wordt de volgende logica in de juiste volgorde uitgevoerd:

1. Als de koppeling overeenkomt met criteria op basis van waarden in [`downloadLinkQualifier`](downloadlinkqualifier.md)of als de koppeling een `download` HTML, kenmerk, `xdm.web.webInteraction.type` is ingesteld op `"download"`.
1. Als het koppelingsdoeldomein afwijkt van het huidige `window.location.hostname`, `xdm.web.webInteraction.type` is ingesteld op `"exit"`.
1. Als de koppeling niet in aanmerking komt voor `"download"` of `"exit"`, `xdm.web.webInteraction.type` is ingesteld op `"other"`.

In alle gevallen `xdm.web.webInteraction.name` is ingesteld op het label van de koppelingstekst en `xdm.web.webInteraction.URL` wordt ingesteld op de URL van het koppelingsdoel. Als u ook de naam van de koppeling wilt instellen op de URL, kunt u dit XDM-veld overschrijven met [`onBeforeLinkClickSend`](onbeforelinkclicksend.md).

## Automatisch koppelingen bijhouden inschakelen met de webSDK-tagextensie

Selecteer de **[!UICONTROL Enable click data collection]** selectievakje wanneer [configureren van de tagextensie](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] kaart.
1. Omlaag schuiven naar de [!UICONTROL Data Collection] en selecteert u vervolgens het selectievakje **[!UICONTROL Enable click data collection]**.
1. Klikken **[!UICONTROL Save]** publiceert u vervolgens uw wijzigingen.

## Automatisch koppelingen bijhouden inschakelen met de Web SDK JavaScript-bibliotheek

Stel de `clickCollectionEnabled` boolean wanneer de `configure` gebruiken. Als u dit bezit weglaat wanneer het vormen van het Web SDK, blijft het in gebreke aan `true`. Deze waarde instellen op `false` als u handmatig wilt instellen `xdm.web.webInteraction.type` en `xdm.web.webInteraction.value`.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "clickCollectionEnabled": false
});
```
