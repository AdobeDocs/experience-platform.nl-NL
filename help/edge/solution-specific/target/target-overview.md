---
title: 'Adobe Target en de Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK en Adobe Target gebruiken
description: Leer hoe u persoonlijke inhoud kunt renderen met Experience Platform Web SDK met Adobe Target
seo-description: Leer hoe u persoonlijke inhoud kunt renderen met Experience Platform Web SDK met Adobe Target
translation-type: tm+mt
source-git-commit: 4bff4b20ccc1913151aa1783d5123ffbb141a7d0
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---


# Doeloverzicht

De Adobe Experience Platform Web SDK kan persoonlijke ervaringen die in Adobe Target worden beheerd, aan het webkanaal leveren en weergeven. U kunt een redacteur WYSIWYG, genoemd de [Visuele Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) van de Ervaring (VEC), of een niet-visuele interface, de op [vorm-gebaseerde Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)van de Ervaring gebruiken, om, uw activiteiten en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

## Adobe-doel inschakelen

Als u Doel wilt inschakelen, moet u het volgende doen:

1. Schakel activity.id- en experience.id-responstokens in de doelinterface.

![target_reponse_token](../../solution-specific/target/assets/target_response_token.png)

1. Laat doel in uw [randconfiguratie](../../fundamentals/edge-configuration.md) met de aangewezen cliëntcode toe.
1. Voeg de `renderDecisions` optie toe aan uw gebeurtenissen.

Vervolgens kunt u desgewenst ook:

* Voeg toe `decisionScopes` aan uw gebeurtenissen om specifieke activiteiten (nuttig voor activiteiten terug te winnen die met op vorm-gebaseerde composer worden gecreeerd).
* Voeg het [voorverborgen fragment](../../solution-specific/target/flicker-management.md) toe om alleen bepaalde delen van de pagina te verbergen.

## Adobe Target VEC gebruiken

Met SDK, kunt u VEC normaal met één uitzondering gebruiken: u hebt de [doelVEC helperuitbreiding](https://docs.adobe.com/content/help/en/target/using/experiences/vec/troubleshoot-composer/vec-helper-browser-extension.html) geïnstalleerd en actief nodig.

## VEC-activiteiten automatisch renderen

De AEP Web SDK heeft de macht om uw ervaringen automatisch terug te geven die via VEC van Adobe Target op het Web voor uw gebruikers worden bepaald. Om aan het Web SDK van AEP aan auto-render VEC activiteiten te wijzen, verzend een gebeurtenis met `renderDecisions = true`:

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

De Form-Based Experience Composer is een niet-visuele interface die nuttig is voor het configureren van A/B Tests, Experience Targeting, Automated Personalization en Recommendations activiteiten met verschillende soorten reacties, zoals JSON, HTML, Image, enz. Afhankelijk van het type reactie of de beslissing die door Adobe Target is geretourneerd, kan uw kernbedrijfslogica worden uitgevoerd. Om besluiten voor uw op vorm-Gebaseerde Composer activiteiten terug te winnen, verzend een gebeurtenis met alle &quot;DecisionScopes&quot;u een besluit voor wilt terugwinnen.

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

`decisionScopes` Hiermee definieert u secties, locaties of delen van uw pagina&#39;s waar u een persoonlijke ervaring wilt weergeven. Deze `decisionScopes` zijn aanpasbaar en door de gebruiker gedefinieerd. Voor huidige klanten van het Doel, `decisionScopes` zijn ook gekend als &quot;dozen.&quot; Ga naar de doelinterface en `decisionScopes` kies Locaties.

## __weergavebereik__

AEP Web SDK verstrekt een functionaliteit waar u acties kunt terugwinnen VEC zonder zich het verlaten van het Web SDK van AEP om de acties VEC voor u terug te geven. Verzend een gebeurtenis met `__view__` als een `decisionScopes`gedefinieerd item.

```javascript
alloy("sendEvent", {
  decisionScopes: [“__view__”,"foo", "bar"], 
  "xdm": { 
    "web": { 
      "webPageDetails": { 
        "name": "Home Page"
       }
      } 
     }
    }
   ).then(results){
  for (decision of results.decisions){
     if(decision.decisionScope == "__view__")
       console.log(decision.content)
}
};
```

## Soorten publiek in XDM

Wanneer het bepalen van Publiek voor uw activiteiten van het Doel die via het Web SDK van AEP zullen worden geleverd, moet [XDM](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html) worden bepaald en worden gebruikt. Nadat u schema&#39;s XDM, klassen, en mengen bepaalt, kunt u een het publieksregel van het Doel tot stand brengen die door XDM gegevens voor het richten wordt bepaald. Binnen Doel, XDM- gegevensvertoningen in de Bouwer van de Publiek als douaneparameter. XDM wordt geserialiseerd gebruikend puntaantekening (bijvoorbeeld, `web.webPageDetails.name`).

Als u doelactiviteiten hebt met vooraf gedefinieerde doelgroepen die aangepaste parameters of een gebruikersprofiel gebruiken, moet u er rekening mee houden dat deze niet correct worden geleverd via de AEP Web SDK. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box-publiek dat zich richt op velden die worden ondersteund via de AEP Web SDK en die geen XDM vereisen. Dit zijn de gebieden beschikbaar in het Doel UI die geen XDM vereisen:

* Doelbibliotheek
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* Verkeersbronnen
* Tijdschema

## Terminologie

__Beslissingen__ - In doel hebben deze betrekking op de ervaring die is gekozen uit een activiteit.

__Toepassingsgebied__ - Het toepassingsgebied van de beschikking. In Doel is dit de mBox. Het algemene mBox is het `__view__` bereik.

__Schema__ - Het schema van een besluit is het type aanbod in Target.

__XDM__ - XDM wordt geserialiseerd in puntnotatie en dan gezet in Doel als mBox parameters.
