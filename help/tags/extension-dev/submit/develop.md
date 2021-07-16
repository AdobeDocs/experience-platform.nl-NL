---
title: Een extensie ontwikkelen
description: Dit document biedt een algemeen overzicht van het ontwikkelingsproces van de tagextensie met koppelingen naar verdere documentatie voor meer gedetailleerde processen.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Een extensie ontwikkelen

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een uitbreiding van een tag moet worden beschouwd als een (klein) product met eigen vereisten. Bepalen hoe een Adobe Experience Platform-gebruiker de extensie wil gebruiken, kan u helpen de functionaliteit te sorteren op welke gebeurtenistypen, gebeurtenistypen, actietypen en gegevenselementen uw extensie moet bieden.

Met die kennis, kunt u plannen welke componenten in uw uitbreiding zouden moeten worden verstrekt.

## Hulplijnen

Met een plan op zijn plaats, kunnen deze gidsen u het proces van de uitbreidingsontwikkeling begrijpen:

* De [gids Aan de slag](../getting-started.md) en andere documenten onder **Extensieontwikkeling** in de linkernavigatie zijn groot referentiemateriaal voor het begrijpen van extensies. Deze bevatten informatie over wat extensies kunnen doen, hoe gebruikersgegevens worden opgeslagen en doorgegeven tussen uw extensie en Adobe Experience Platform, hoe uw code in bibliotheken wordt opgenomen en hoe uw extensiecode wordt geïnterpreteerd en gebruikt tijdens runtime in de browser.
* De [zelfstudievideo](https://youtu.be/rxjtC9o4rl0) is een ideale plaats om te beginnen.
* De [Inleiding tot Uitbreidingen](https://www.youtube.com/playlist?list=PLOdw8u2F8CIgynzKrPEwCPuDxzHW1WP5m) afspeellijst van YouTube doorloopt het proces om uitbreidingspakketten tot stand te brengen.
* [Een goed begrip van JSON ](https://spacetelescope.github.io/understanding-json-schema/index.html#) Schemarticle.
* [JSON Lint/Validator](http://jsonlint.com/).
* [JSON ](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) ViewerChrome-extensie voor het markeren en afdrukken van JSON en JSONP.
* [jsonschema.](https://jsonschema.net/#/editor) neteditor om JSON-schema&#39;s te maken van uw object.
* [JSON-schema ](http://www.jsonschemavalidator.net/) ValidatorAn online, interactieve JSON-schema-validator.

## Tools

Er zijn ook een aantal npm hulpmiddelen om u met uw uitbreidingspakketontwikkeling te helpen:

* [Met de ](https://www.npmjs.com/package/@adobe/reactor-scaffold) werkbalk Tagextensies verpakken kunt u eenvoudig een startproject maken op uw lokale computer.
* [Met de ](https://www.npmjs.com/package/@adobe/reactor-sandbox) sandbox van de tagextensie kunt u de extensieweergaven en -modules op uw lokale computer valideren.
* [De Uitbreiding van de markering ](https://www.npmjs.com/package/@adobe/reactor-packager) Packageris een bevel-lijn nut voor het verpakken van een markeringsuitbreiding in een ZIP dossier.
* [De Uitbreiding van de markering ](https://www.npmjs.com/package/@adobe/reactor-uploader) Uploader is een interactief bevellijnhulpmiddel om u te helpen uw technische accountgeloofsbrieven invoeren en uw uitbreidingspakket uploaden aan markeringen.
* [De ](https://www.npmjs.com/package/@adobe/reactor-releaser) Verspreiding van de Uitbreiding van de markering is een interactief bevellijnhulpmiddel om u te helpen uw uitbreiding aan privé beschikbaarheid vrijgeven.

## Voorbeelden van extensies

Er zijn voorbeelduitbreidingen op GitHub u kunt herzien of als starterprojecten gebruiken:

* [Hello World, voorbeeldextensie](https://github.com/adobe/reactor-helloworld-extension)
* [Facebook-voorbeeldextensie](https://github.com/Adobe-Marketing-Cloud-Activation/extension-facebookpixel)
* [Typekit-voorbeeldextensie](https://github.com/jeffchasin/extension-typekit)
* [Pinterest-voorbeeldextensie](https://github.com/jeffchasin/extension-pinterest)

## Slack-werkruimte

U kunt toegang tot de werkruimte van de gemeenschap van de Slack verzoeken waar de uitbreidingsauteurs elkaar kunnen steunen gebruikend dit [aanvraagformulier](http://join.launchdevelopers.chat).

**Opmerking**: hoewel er leden van Adobe in deze werkruimte van Slack zijn , is het een communautaire hulpbron die niet door Adobe wordt gesponsord of gemodereerd .
