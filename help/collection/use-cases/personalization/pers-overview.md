---
title: Overzicht van Personalization-gebruikskwesties
description: Leer hoe u gebruiksgevallen voor personalisatie implementeert met de Adobe Experience Platform Web SDK, waaronder patronen voor het renderen van inhoud en het bijhouden van weergave.
keywords: personalization;sendEvent;renderDecisions;applyProposities;DecisionScopes;display events;flicker;
exl-id: 6beccbfd-fddb-4e19-8a56-caba276e1643
source-git-commit: caaf5cad7276d6429fbbf35585fd4845de6ff60c
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Overzicht van Personalization-gebruikskwesties

De Adobe Experience Platform Web SDK biedt een groot aantal verschillende gebruiksscenario&#39;s voor personalisatie voor wegeigenschappen. Het steunt flexibele architecturen (cliënt-kant, server-kant, en hybride) zodat kunt u besluiten verzoeken en inhoud teruggeven op manieren die aan de behoeften van uw plaats aanpassen.

## Aangepaste inhoud renderen

SDK van het Web kan verpersoonlijkingsbesluiten (die ook als _worden bekend voorstellingen_) terugwinnen en u helpen hen op de pagina teruggeven. Renderen is asynchroon, dus gebruik geen specifieke timing voor wanneer de inhoud wordt toegepast.

Kies het patroon dat overeenkomt met de pro-positieitems die u ontvangt:

1. **geeft automatisch DOM actievoorstellen** terug: Gebruik wanneer de voorstellen `dom-action` punten met selecteurs en actietypes omvatten die SDK van het Web automatisch kan toepassen. Zie [ automatisch DOM actievoorstellen ](render-auto-pers-content.md) teruggeven.
1. **geeft de aanbiedingen van HTML zonder selecteurs terug gebruikend applyProposities**: Gebruik wanneer u de inhoud van HTML ontvangt, maar u moet verstrekken waar en hoe te om het (selecteur + actietype) via meta-gegevens toe te passen. Zie [ HTML aanbiedingen zonder selecteurs teruggeven ](render-html-offers.md).
1. **geeft manueel voorstellingen** terug: Gebruik wanneer u volledige controle over het teruggeven logica (bijvoorbeeld, het samenstellen UI van JSON of het toepassen van douanebedrijfsregels) nodig hebt. Zie [ manueel proposities ](render-manual-propositions.md) teruggeven.

>[!TIP]
>
>Deze patronen kunnen worden gecombineerd. U kunt bijvoorbeeld automatische rendering van DOM-handelingen inschakelen, terwijl u ook handmatig inhoud rendert vanuit een bepaald beslissingsbereik.

## Algemene onderwerpen

De meeste verpersoonlijkingsimplementaties impliceren deze gemeenschappelijke onderwerpen:

* **Prevent flikkering** (facultatief): Verberg en verberg containers tijdens verpersoonlijking. Zie [ flikkering beheren ](manage-flicker.md).
* **Spoor wat werd getoond**: De vertoningsgebeurtenissen van het verslag voor teruggegeven inhoud. Zie [ vertoningsgebeurtenissen ](display-events.md) beheren.
* **Top-van-pagina halen/bodem-van-pagina metriek**: De besluiten van het verzoek vroeg, dan omvatten meting later. Zie [ boven en bodem van paginagebeurtenissen ](top-bottom-page-events.md) vormen.

## Web SDK-voorbeelden

Naast de documentpagina&#39;s in deze map houdt Adobe een opslagplaats bij van voorbeeldtoepassingen waarnaar u kunt verwijzen. Zie {de steekproeven van SDK van 0} Web [ op GitHub voor extra verpersoonlijkingsscenario&#39;s, die omvatten:](https://github.com/adobe/alloy-samples/)

* Aanpassing aan clientzijde
* Aanpassing aan server
* Hybride personalisatie
* Personalization in toepassingen van één pagina
