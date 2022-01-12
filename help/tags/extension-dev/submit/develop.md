---
title: Een extensie ontwikkelen
description: Dit document biedt een algemeen overzicht van het ontwikkelingsproces van de tagextensie met koppelingen naar verdere documentatie voor meer gedetailleerde processen.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# Een extensie ontwikkelen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een uitbreiding van een tag moet worden beschouwd als een (klein) product met eigen vereisten. Bepalen hoe een Adobe Experience Platform-gebruiker de extensie wil gebruiken, kan u helpen de functionaliteit te sorteren op welke gebeurtenistypen, gebeurtenistypen, actietypen en gegevenselementen uw extensie moet bieden.

Met die kennis, kunt u plannen welke componenten in uw uitbreiding zouden moeten worden verstrekt.

## Hulplijnen

Met een plan op zijn plaats, kunnen deze gidsen u het proces van de uitbreidingsontwikkeling begrijpen:

* De [gids Aan de slag](../getting-started.md) en andere onder **Uitbreiding** in de linkernavigatie is groot referentiemateriaal voor het begrijpen van extensies. Deze bevatten informatie over wat extensies kunnen doen, hoe gebruikersgegevens worden opgeslagen en doorgegeven tussen uw extensie en Adobe Experience Platform, hoe uw code in bibliotheken wordt opgenomen en hoe uw extensiecode wordt geïnterpreteerd en gebruikt tijdens runtime in de browser.
* De [videozelfstudie extensie](https://youtu.be/rxjtC9o4rl0) is een goede startplaats.
* De [Inleiding tot extensies](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) De afspeellijst van YouTube doorloopt het proces om uitbreidingspakketten tot stand te brengen.
* [JSON-schema](https://spacetelescope.github.io/understanding-json-schema/index.html#) artikel.
* [JSON Lint/Validator](https://jsonlint.com/).
* [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) Chrome-extensie voor het markeren en afdrukken van JSON en JSONP.
* [jsonschema.net](https://jsonschema.net/#/editor) om te helpen bij het maken van JSON-schema&#39;s van uw object.
* [JSON-schema-validatie](https://www.jsonschemavalidator.net) Een online, interactieve JSON-schemavalidator.

## Tools

Er zijn ook een aantal npm hulpmiddelen om u met uw uitbreidingspakketontwikkeling te helpen:

* [Tagextensie, gestippeld](https://www.npmjs.com/package/@adobe/reactor-scaffold) kunt u gemakkelijk een startproject op uw lokale computer maken.
* [Tagextensie-sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox) helpt u bij het valideren van de extensieweergaven en -modules op uw lokale computer.
* [Tag Extension Packager](https://www.npmjs.com/package/@adobe/reactor-packager) is een opdrachtregelprogramma voor het verpakken van een tagextensie in een ZIP-bestand.
* [Uploader voor extensie van tag](https://www.npmjs.com/package/@adobe/reactor-uploader) is een interactief opdrachtregelprogramma waarmee u de gegevens van uw technische account kunt invoeren en het extensiepakket kunt uploaden naar codes.
* [Tagextensie-release](https://www.npmjs.com/package/@adobe/reactor-releaser) is een interactief opdrachtregelprogramma waarmee u uw extensie kunt vrijgeven voor persoonlijke beschikbaarheid.

## Voorbeelden van extensies

Er zijn voorbeelduitbreidingen op GitHub u kunt herzien of als starterprojecten gebruiken:

* [Hello World, voorbeeldextensie](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook-voorbeeldextensie](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit-voorbeeldextensie](https://github.com/jeffchasin/extension-typekit)
* [Pinterest-voorbeeldextensie](https://github.com/jeffchasin/extension-pinterest)

## Slack-werkruimte

U kunt toegang aanvragen tot de werkruimte van de gemeenschap Slack waar auteurs van extensies elkaar kunnen ondersteunen met behulp van deze [aanvraagformulier](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**Let op**: hoewel er leden van Adobe in deze werkruimte van Slack zijn , is het een communautaire hulpbron die niet door Adobe wordt gesponsord of gemodereerd .
