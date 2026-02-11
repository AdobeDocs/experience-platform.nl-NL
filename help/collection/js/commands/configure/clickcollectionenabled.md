---
title: clickCollectionEnabled
description: Leer hoe te om Web SDK te vormen om te bepalen als de verbindingsklikgegevens automatisch worden verzameld.
exl-id: e91b5bc6-8880-4884-87f9-60ec8787027e
source-git-commit: 4d251ff7323e83ac5c47b5817f81e8fde64cb7d9
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `clickCollectionEnabled`

De eigenschap `clickCollectionEnabled` is een Booleaanse waarde die bepaalt of de Web SDK automatisch koppelingsgegevens verzamelt. Als u deze variabele niet instelt, is de standaardwaarde `true` . Dit houdt in dat de gegevens voor het bijhouden van koppelingen standaard automatisch worden verzameld. Het instellen van deze eigenschap op `false` is nuttig wanneer u koppelingsgegevens handmatig wilt bijhouden.

Wanneer `clickCollectionEnabled` is ingeschakeld, vullen de volgende XDM-elementen automatisch met gegevens:

* `xdm.web.webInteraction.name`
* `xdm.web.webInteraction.type`
* `xdm.web.webInteraction.URL`

Interne koppelingen, downloadkoppelingen en afsluitkoppelingen worden standaard automatisch bijgehouden wanneer deze Boolean is ingeschakeld. Adobe raadt u aan het [`clickCollection`](clickcollection.md) -object te gebruiken als u meer controle wilt hebben over het automatisch bijhouden van koppelingen.

## Logica voor automatisch bijhouden van koppelingen

De Web SDK houdt bij alle klikken op `<a>` en `<area>` HTML-elementen als het geen `onClick` -kenmerk heeft. De klikken worden gevangen met a [ vangt ](https://www.w3.org/TR/uievents/#capture-phase) klik gebeurtenisluisteraar die aan het document in bijlage is. Wanneer op een geldige koppeling wordt geklikt, wordt de volgende logica in de juiste volgorde uitgevoerd:

1. Als de koppeling overeenkomt met criteria op basis van waarden in [`downloadLinkQualifier`](downloadlinkqualifier.md) of als de koppeling een `download` HTML-kenmerk bevat, wordt `xdm.web.webInteraction.type` ingesteld op `"download"` (als `clickCollection.downloadLinkEnabled` is ingeschakeld).
1. Als het koppelingsdoeldomein verschilt van het huidige `window.location.hostname` , wordt `xdm.web.webInteraction.type` ingesteld op `"exit"` (als `clickCollection.exitLinkEnabled` is ingeschakeld).
1. Als de koppeling niet in aanmerking komt voor `"download"` of `"exit"` , wordt `xdm.web.webInteraction.type` ingesteld op `"other"` .

In alle gevallen controleert `xdm.web.webInteraction.name` het aangeklikte element en de onderliggende elementen ervan op de eerste niet-lege waarde in de volgende volgorde:

1. `innerText` (valt terug naar `textContent`)
1. Samengevoegd `nodeValue` van ondersteunde afstammende tekstknooppunten
1. `alt` -kenmerk
1. `title` -kenmerk
1. `<input value="...">` -kenmerk
1. `<img src="...">` -kenmerk
1. `aria-label` -kenmerk
1. `name` -kenmerk
1. Lege tekenreeks

Het veld `xdm.web.webInteraction.URL` wordt ingesteld op de doel-URL van de koppeling. Als u ook de naam van de koppeling wilt instellen op de URL, kunt u dit XDM-veld overschrijven met de callback `filterClickDetails` in het `clickCollection` -object.

## Implementatie

Stel de Booleaanse waarde `clickCollectionEnabled` in wanneer u de opdracht `configure` uitvoert. Als u deze eigenschap weglaat bij het configureren van de Web SDK, wordt standaard `true` gebruikt. Stel deze waarde in op `false` als u `xdm.web.webInteraction.type` en `xdm.web.webInteraction.value` handmatig wilt instellen.

```js
alloy(configure, {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  clickCollectionEnabled: false
});
```

## Ondersteuning voor open [!DNL Shadow DOM] -elementen

SDK van het Web steunt automatische klik het volgen voor verbindingen binnen **open DOM van de Schaduw** elementen.

Vele moderne websites gebruiken {de Componenten van 0} Web [ om herbruikbare en ingekapselde gebruikersinterfaceelementen te bouwen. ](https://developer.mozilla.org/en-US/docs/Web/Web_Components) Deze componenten gebruiken vaak een technologie genoemd [**DOM van de Schaduw** ](https://developer.mozilla.org/en-US/docs/Web/API/Web_components/Using_shadow_DOM) om hun interne structuur en stijlen gescheiden van de rest van de pagina te houden.

Er zijn twee soorten schaduw-DOM:

* **Open DOM van de Schaduw:** de interne structuur is toegankelijk voor JavaScript die op de pagina loopt. Andere scripts kunnen de inhoud van de component beïnvloeden of inspecteren.
* **Gesloten DOM van de Schaduw:** de interne structuur wordt verborgen van JavaScript buiten de component, die het ontoegankelijk maken voor het volgen of manipulatie.

Het Web SDK houdt automatisch kliks op `<a>` en `<area>` elementen binnen **open DOMs van de Schaduw**, enkel zoals het voor verbindingen in het belangrijkste document doet. Deze controle zorgt ervoor dat de verbinding binnen Webcomponenten gebruikend open [!DNL Shadow DOM] wordt geklikt inbegrepen in uw analysegegevens. De klikken binnen **gesloten Schaduw DOMs** worden niet gevolgd, aangezien hun interne structuur van de code van JavaScript die buiten de component werken verborgen is.

## Klikverzameling voor de Web SDK-tagextensie in- of uitschakelen

Zie [ de montages van de inzamelingsconfiguratie van Gegevens ](/help/tags/extensions/client/web-sdk/configure/data-collection.md) in de de uitbreidingsdocumentatie van SDK van het Web leren hoe te om deze acties uit te voeren gebruikend markeringen.
