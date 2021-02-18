---
title: Adobe Target gebruiken met de SDK van het Web van het Platform
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Target
keywords: doel;adobe target;activity.id;experience.id;renderDecisions;DecisionScopes;prehide snippet;vec;Form-Based Experience Composer;xdm;publiek;decisions;scope;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 2%

---


# Adobe Target gebruiken met de SDK van het Web van het Platform

Adobe Experience Platform [!DNL Web SDK] kan persoonlijke ervaringen die in Adobe Target worden beheerd, aanbieden en weergeven op het webkanaal. U kunt een redacteur WYSIWYG, genoemd [Visual Experience Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) (VEC), of een niet-visuele interface, [Op vorm-gebaseerde Composer van de Ervaring](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html), gebruiken om, uw activiteiten en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

## Adobe Target inschakelen

Als u [!DNL Target] wilt inschakelen, moet u het volgende doen:

1. Doel inschakelen in uw [randconfiguratie](../../fundamentals/edge-configuration.md) met de juiste clientcode.
1. Voeg de optie `renderDecisions` toe aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook:

* Voeg `decisionScopes` aan uw gebeurtenissen toe om specifieke activiteiten (nuttig voor activiteiten terug te winnen die met op vorm-gebaseerde composer worden gecreeerd).
* Voeg het [voorverborgen fragment](../manage-flicker.md) toe om alleen bepaalde delen van de pagina te verbergen.

## Adobe Target VEC gebruiken

Als u de VEC wilt gebruiken met een Platform Web SDK-implementatie, moet u de [Firefox](https://addons.mozilla.org/en-US/firefox/addon/adobe-target-vec-helper/) of [Chrome](https://chrome.google.com/webstore/detail/adobe-target-vec-helper/ggjpideecfnbipkacplkhhaflkdjagak) VEC Helper Extension installeren en activeren.

## VEC-activiteiten automatisch renderen

Adobe Experience Platform Web SDK heeft de mogelijkheid om uw ervaringen die via de VEC van Adobe Target op het web zijn gedefinieerd, automatisch te renderen voor uw gebruikers. Als u aan Adobe Experience Platform Web SDK wilt aangeven dat VEC-activiteiten automatisch moeten worden gerenderd, verzendt u een gebeurtenis met `renderDecisions = true`:

```javascript
alloy
("sendEvent", 
  { 
  "renderDecisions": true, 
  "xdm": {
    "commerce": { 
      "order": {
        "purchaseID": "a8g784hjq1mnp3", 
         "purchaseOrderNumber": "VAU3123", 
         "currencyCode": "USD", 
         "priceTotal": 999.98 
         } 
      } 
    }
  }
);
```

## De op formulieren gebaseerde composer gebruiken

De Form-Based Experience Composer is een niet-visuele interface die handig is voor het configureren van A/B Tests, [!DNL Experience Targeting], Automated Personalization en Recommendations-activiteiten met verschillende soorten reacties, zoals JSON, HTML, Image, enz. Afhankelijk van het type reactie of de beslissing die Adobe Target heeft gegeven, kan uw kernbedrijfslogica worden uitgevoerd. Om besluiten voor uw op vorm-Gebaseerde Composer activiteiten terug te winnen, verzend een gebeurtenis met alle &quot;DecisionScopes&quot;u een besluit voor wilt terugwinnen.

```javascript
alloy
  ("sendEvent", { 
    decisionScopes: [
      "foo", "bar"], 
      "xdm": {
        "commerce": { 
          "order": { 
            "purchaseID": "a8g784hjq1mnp3", 
            "purchaseOrderNumber": "VAU3123", 
            "currencyCode": "USD", 
            "priceTotal": 999.98 
          } 
        } 
      } 
    }
  );
```

## Beslissingsgebieden

`decisionScopes` Hiermee definieert u secties, locaties of delen van uw pagina&#39;s waar u een persoonlijke ervaring wilt weergeven. Deze `decisionScopes` zijn aanpasbaar en user-defined. Voor huidige [!DNL Target]-klanten wordt `decisionScopes` ook wel ‘mboxes’ genoemd. In [!DNL Target] UI, `decisionScopes` verschijnen als &quot;plaatsen.&quot;

## Het `__view__`-bereik

Adobe Experience Platform Web SDK verstrekt functionaliteit waar u acties kunt terugwinnen VEC zonder zich op SDK te verlaten om de acties VEC voor u terug te geven. Verzend een gebeurtenis met `__view__` die als `decisionScopes` wordt gedefinieerd.

```javascript
alloy("sendEvent", {
      "decisionScopes": ["__view__", "foo", "bar"], 
      "xdm": { 
        "web": { 
          "webPageDetails": { 
            "name": "Home Page"
          }
        } 
      }
    }
  ).then(function(results) {
    for (decision of results.decisions) {
      if (decision.decisionScope === "__view__") {
        console.log(decision.content)
      }
    }
  });
```

## Soorten publiek in XDM

Wanneer het bepalen van Publiek voor uw activiteiten van het Doel die via het Web SDK van Adobe Experience Platform zullen worden geleverd, [XDM](https://docs.adobe.com/content/help/nl-NL/experience-platform/xdm/home.html) moet worden bepaald en worden gebruikt. Nadat u schema&#39;s XDM, klassen, en mengen bepaalt, kunt u een het publieksregel van het Doel tot stand brengen die door XDM gegevens voor het richten wordt bepaald. Binnen Doel, XDM- gegevensvertoningen in de Bouwer van de Publiek als douaneparameter. XDM wordt geserialiseerd gebruikend puntaantekening (bijvoorbeeld, `web.webPageDetails.name`).

Als u doelactiviteiten hebt met vooraf gedefinieerde doelgroepen die aangepaste parameters of een gebruikersprofiel gebruiken, moet u er rekening mee houden dat deze niet correct worden geleverd via de SDK. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box publiek dat zich richt op velden die worden ondersteund via Adobe Experience Platform Web SDK en waarvoor geen XDM vereist is. Dit zijn de gebieden beschikbaar in het Doel UI die geen XDM vereisen:

* Doelbibliotheek
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* Verkeersbronnen
* Tijdschema

## Terminologie

__Beslissingen:__ In  [!DNL Target]verband houden deze met de ervaring die uit een activiteit wordt geselecteerd.

__Schema:__ Het schema van een besluit is het soort aanbod in  [!DNL Target].

__Toepassingsgebied:__ het toepassingsgebied van de beschikking. In [!DNL Target] is dit de mBox. Het globale mBox is het `__view__` werkingsgebied.

__XDM:__ XDM wordt geserialiseerd in puntnotatie en dan gezet in  [!DNL Target] als parameters mBox.
