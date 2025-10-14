---
title: clickCollectionEnabled
description: Leer hoe te om Web SDK te vormen om te bepalen als de verbindingsklikgegevens automatisch worden verzameld.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: fdb809ea86e91a98b45877c99c3e64d7c49d1cd5
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# `clickCollectionEnabled`

De eigenschap `clickCollectionEnabled` is een Booleaanse waarde die bepaalt of de Web SDK automatisch koppelingsgegevens verzamelt. Als u deze variabele niet instelt, is de standaardwaarde `true` . Dit houdt in dat de gegevens voor het bijhouden van koppelingen standaard automatisch worden verzameld. Het instellen van deze eigenschap op `false` is nuttig wanneer u koppelingsgegevens handmatig wilt bijhouden.

Wanneer `clickCollectionEnabled` is ingeschakeld, vullen de volgende XDM-elementen automatisch met gegevens:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne koppelingen, downloadkoppelingen en afsluitkoppelingen worden standaard automatisch bijgehouden wanneer deze Boolean is ingeschakeld. Adobe raadt u aan het [`clickCollection`](clickcollection.md) -object te gebruiken als u meer controle wilt hebben over het automatisch bijhouden van koppelingen.

## Ondersteuning voor open [!DNL Shadow DOM] -elementen

SDK van het Web steunt automatische klik het volgen voor verbindingen binnen **open DOM van de Schaduw** elementen.

Vele moderne websites gebruiken {de Componenten van 0} Web [&#128279;](https://developer.mozilla.org/en-US/docs/Web/Web_Components) om herbruikbare en ingekapselde gebruikersinterfaceelementen te bouwen.  Deze componenten gebruiken vaak een technologie genoemd [**DOM van de Schaduw** &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) om hun interne structuur en stijlen gescheiden van de rest van de pagina te houden.

Er zijn twee soorten schaduw-DOM:

* **Open DOM van de Schaduw:** de interne structuur is toegankelijk voor JavaScript die op de pagina loopt. Dit betekent dat andere scripts de inhoud van de component kunnen beïnvloeden of inspecteren.
* **Gesloten DOM van de Schaduw:** de interne structuur wordt verborgen van JavaScript buiten de component, die het ontoegankelijk maken voor het volgen of manipulatie.

Het Web SDK houdt automatisch kliks op `<a>` en `<area>` elementen binnen **open DOMs van de Schaduw**, enkel zoals het voor verbindingen in het belangrijkste document doet. Zo zorgt u ervoor dat koppelingsklikken binnen webcomponenten die open [!DNL Shadow DOM] gebruiken, worden opgenomen in de analysegegevens. De klikken binnen **gesloten Schaduw DOMs** worden niet gevolgd, aangezien hun interne structuur van de code van JavaScript die buiten de component werken verborgen is.

## Logica voor automatisch bijhouden van koppelingen

De Web SDK houdt bij alle klikken op `<a>` en `<area>` HTML-elementen als het geen `onClick` -kenmerk heeft. De klikken worden gevangen met a [&#x200B; vangt &#x200B;](https://www.w3.org/TR/uievents/#capture-phase) klik gebeurtenisluisteraar die aan het document in bijlage is. Wanneer op een geldige koppeling wordt geklikt, wordt de volgende logica in de juiste volgorde uitgevoerd:

1. Als de koppeling overeenkomt met criteria op basis van waarden in [`downloadLinkQualifier`](downloadlinkqualifier.md) of als de koppeling een `download` HTML-kenmerk bevat, wordt `xdm.web.webInteraction.type` ingesteld op `"download"` (als `clickCollection.downloadLinkEnabled` is ingeschakeld).
1. Als het koppelingsdoeldomein verschilt van het huidige `window.location.hostname` , wordt `xdm.web.webInteraction.type` ingesteld op `"exit"` (als `clickCollection.exitLinkEnabled` is ingeschakeld).
1. Als de koppeling niet in aanmerking komt voor `"download"` of `"exit"` , wordt `xdm.web.webInteraction.type` ingesteld op `"other"` .

In alle gevallen wordt `xdm.web.webInteraction.name` ingesteld op het label van de koppelingstekst en wordt `xdm.web.webInteraction.URL` ingesteld op de URL van het doel van de koppeling. Als u ook de naam van de koppeling wilt instellen op de URL, kunt u dit XDM-veld overschrijven met de callback `filterClickDetails` in het `clickCollection` -object.

## Automatisch koppelingen bijhouden inschakelen met de webtagextensie SDK {#tag-extension}

Deze variabele wordt automatisch beheerd door de tagextensie. U hoeft deze niet expliciet in te stellen. Als om het even welk van het volgende wordt geselecteerd wanneer [&#x200B; het vormen van de markeringsuitbreiding &#x200B;](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md), wordt de toepasselijke verbinding volgende gegevens verzameld:

* [!UICONTROL Collect internal link clicks]
* [!UICONTROL Collect external link clicks]
* [!UICONTROL Collect download link clicks]

Zie [`clickCollection`](clickcollection.md) voor meer informatie.

## Automatisch koppelingen bijhouden inschakelen met de Web SDK JavaScript-bibliotheek {#library}

Stel de Booleaanse waarde `clickCollectionEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze waarde in op `false` als u `xdm.web.webInteraction.type` en `xdm.web.webInteraction.value` handmatig wilt instellen.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```
