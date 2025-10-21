---
title: Een extensie ontwikkelen
description: Dit document biedt een algemeen overzicht van het ontwikkelingsproces van de tagextensie met koppelingen naar verdere documentatie voor meer gedetailleerde processen.
exl-id: fb2f7275-a5da-4a41-b915-822c71c02e5c
source-git-commit: 36870fa5359b5382cb9f1e9a5220ce8311f0c45c
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 10%

---

# Een extensie ontwikkelen

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor dataverzameling in Adobe Experience Platform.  Als gevolg hiervan zijn er verschillende terminologiewijzigingen in de productdocumentatie doorgevoerd. Raadpleeg het volgende [&#x200B; document &#x200B;](../../term-updates.md) voor een geconsolideerde referentie van de terminologiewijzigingen.

Een uitbreiding van een tag moet worden beschouwd als een (klein) product met eigen vereisten. Bepalen hoe een Adobe Experience Platform-gebruiker de extensie wil gebruiken, kan u helpen de functionaliteit te sorteren op welke gebeurtenistypen, gebeurtenistypen, actietypen en gegevenselementen uw extensie moet bieden.

Met die kennis, kunt u plannen welke componenten in uw uitbreiding zouden moeten worden verstrekt.

## Handleidingen

Met een plan op zijn plaats, kunnen deze gidsen u het proces van de uitbreidingsontwikkeling begrijpen:

* De [&#x200B; begonnen gids &#x200B;](../getting-started.md) en andere documenten onder **ontwikkeling van de Uitbreiding** in de linkernavigatie zijn groot verwijzingsmateriaal voor het begrip van uitbreidingen. Deze bevatten informatie over wat extensies kunnen doen, hoe gebruikersgegevens worden opgeslagen en doorgegeven tussen uw extensie en Adobe Experience Platform, hoe uw code in bibliotheken wordt opgenomen en hoe uw extensiecode wordt geïnterpreteerd en gebruikt tijdens runtime in de browser.
* [&#x200B; Begrijpend JSON Schema &#x200B;](https://spacetelescope.github.io/understanding-json-schema/index.html#) artikel.
* [&#x200B; JSON Lint/Validator &#x200B;](https://jsonlint.com/).
* [&#x200B; JSON Viewer &#x200B;](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) de uitbreiding van Chrome om JSON &amp; JSONP te benadrukken en te drukken.
* [&#x200B; jsonschema.net &#x200B;](https://jsonschema.net/#/editor) redacteur helpen tot schema JSON van uw voorwerp tot stand brengen.
* [&#x200B; Validator van het Schema JSON &#x200B;](https://www.jsonschemavalidator.net) een online, interactieve JSON- Schema validator.

## Tools

Er zijn ook een aantal npm hulpmiddelen om u met uw uitbreidingspakketontwikkeling te helpen:

* [&#x200B; het Hulpmiddel van het Kader van de Uitbreiding van de Markering &#x200B;](https://www.npmjs.com/package/@adobe/reactor-scaffold) helpt u gemakkelijk een starter project op uw lokale machine tot stand brengen.
* [&#x200B; Sandbox van de Uitbreiding van de Markering &#x200B;](https://www.npmjs.com/package/@adobe/reactor-sandbox) helpt u uw uitbreidingsmeningen en modules op uw lokale machine bevestigen.
* [&#x200B; Packager van de Uitbreiding van de Markering &#x200B;](https://www.npmjs.com/package/@adobe/reactor-packager) is een bevel-lijn nut voor het verpakken van een markeringsuitbreiding in een ZIP dossier.
* [&#x200B; Uploader van de Uitbreiding van de Markering &#x200B;](https://www.npmjs.com/package/@adobe/reactor-uploader) is een interactief hulpmiddel van de bevellijn om u te helpen uw technische rekeningsgeloofsbrieven invoeren en uw uitbreidingspakket aan markeringen uploaden.
* [&#x200B; Verlosser van de Uitbreiding van de Markering &#x200B;](https://www.npmjs.com/package/@adobe/reactor-releaser) is een interactief hulpmiddel van de bevellijn om u te helpen uw uitbreiding aan privé beschikbaarheid vrijgeven.

## Voorbeelden van extensies

Er zijn voorbeelduitbreidingen op GitHub u kunt herzien of als starterprojecten gebruiken:

* [&#x200B; de voorbeelduitbreiding van de Wereld van Hello &#x200B;](https://github.com/adobe/reactor-helloworld-extension)
* [&#x200B; Typekit voorbeelduitbreiding &#x200B;](https://github.com/jeffchasin/extension-typekit)
* [&#x200B; de voorbeelduitbreiding van Pinterest &#x200B;](https://github.com/jeffchasin/extension-pinterest)

## Slack-werkruimte

U kunt toegang tot de de communautaire werkruimte van Slack verzoeken waar de uitbreidingsauteurs elkaar kunnen steunen gebruikend dit [&#x200B; verzoekvorm &#x200B;](https://docs.google.com/forms/d/e/1FAIpQLScq1m63YkDrRpvPLhzUqtfoleWiDDTTXZsSivIXRfFdlSMzpQ/viewform).

**gelieve nota te nemen van**: terwijl er leden van Adobe in deze werkruimte van Slack zijn, is het een communautaire middel niet gesponsord door of gemodereerd door Adobe.
