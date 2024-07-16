---
title: clickCollectionEnabled
description: Leer hoe te om Web SDK te vormen om te bepalen als de verbinding gegevens klikt automatisch wordt verzameld.
source-git-commit: 660d4e72bd93ca65001092520539a249eae23bfc
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---


# `clickCollectionEnabled`

De eigenschap `clickCollectionEnabled` is een Booleaanse waarde die bepaalt of de SDK van het Web automatisch koppelingsgegevens verzamelt. Als u deze variabele niet instelt, is de standaardwaarde `true` . Dit houdt in dat de gegevens voor het bijhouden van koppelingen standaard automatisch worden verzameld. Het instellen van deze eigenschap op `false` is nuttig wanneer u koppelingsgegevens handmatig wilt bijhouden.

Wanneer `clickCollectionEnabled` is ingeschakeld, vullen de volgende XDM-elementen automatisch met gegevens:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne koppelingen, downloadkoppelingen en afsluitkoppelingen worden standaard automatisch bijgehouden wanneer deze Boolean is ingeschakeld. Als u meer controle wilt hebben over het automatisch bijhouden van koppelingen, raadt Adobe u aan het object [`clickCollection`](clickcollection.md) te gebruiken.

## Logica voor automatisch bijhouden van koppelingen

De SDK van het Web volgt alle klikken op `<a>` en `<area>` HTML elementen als het geen `onClick` attribuut heeft. De klikken worden gevangen met a [ vangt ](https://www.w3.org/TR/uievents/#capture-phase) klik gebeurtenisluisteraar die aan het document in bijlage is. Wanneer op een geldige koppeling wordt geklikt, wordt de volgende logica in de juiste volgorde uitgevoerd:

1. Als de koppeling overeenkomt met criteria op basis van waarden in [`downloadLinkQualifier`](downloadlinkqualifier.md) of als de koppeling een `download` HTML-kenmerk bevat, wordt `xdm.web.webInteraction.type` ingesteld op `"download"` (als `clickCollection.downloadLinkEnabled` is ingeschakeld).
1. Als het koppelingsdoeldomein verschilt van het huidige `window.location.hostname` , wordt `xdm.web.webInteraction.type` ingesteld op `"exit"` (als `clickCollection.exitLinkEnabled` is ingeschakeld).
1. Als de koppeling niet in aanmerking komt voor `"download"` of `"exit"` , wordt `xdm.web.webInteraction.type` ingesteld op `"other"` .

In alle gevallen wordt `xdm.web.webInteraction.name` ingesteld op het label van de koppelingstekst en wordt `xdm.web.webInteraction.URL` ingesteld op de URL van het doel van de koppeling. Als u ook de naam van de koppeling wilt instellen op de URL, kunt u dit XDM-veld overschrijven met de callback `filterClickDetails` in het `clickCollection` -object.

## Automatisch koppelingen bijhouden inschakelen met de webSDK-tagextensie {#tag-extension}

Selecteer **[!UICONTROL Enable click data collection]** checkbox wanneer [ het vormen van de markeringsuitbreiding ](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie [!UICONTROL Data Collection] en schakel vervolgens het selectievakje **[!UICONTROL Enable click data collection]** in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

## Automatisch koppelingen bijhouden inschakelen met de Web SDK JavaScript-bibliotheek {#library}

Stel de Booleaanse waarde `clickCollectionEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze waarde in op `false` als u `xdm.web.webInteraction.type` en `xdm.web.webInteraction.value` handmatig wilt instellen.

```js
alloy(configure, {
  edgeConfigId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
