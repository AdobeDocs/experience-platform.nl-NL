---
title: 'Adobe Target en The Adobe Experience Platform Web SDK. '
seo-title: Adobe Experience Platform Web SDK en Adobe Target gebruiken
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Target
seo-description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Target
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 1%

---


# [!DNL Target] Overzicht

Het Adobe Experience Platform [!DNL Web SDK] kan persoonlijke ervaringen die in Adobe Target worden beheerd, aanbieden en weergeven op het webkanaal. U kunt een redacteur WYSIWYG, genoemd de [Visuele Composer](https://docs.adobe.com/content/help/en/target/using/experiences/vec/visual-experience-composer.html) van de Ervaring (VEC), of een niet-visuele interface, de op [vorm-gebaseerde Composer](https://docs.adobe.com/content/help/en/target/using/experiences/form-experience-composer.html)van de Ervaring gebruiken, om, uw activiteiten en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

## Adobe Target inschakelen

U moet het volgende doen om in te schakelen [!DNL Target]:

1. Schakel activity.id- en experience.id-reponsettokens in de [!DNL Target] gebruikersinterface in.

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

`decisionScopes` Hiermee definieert u secties, locaties of delen van uw pagina&#39;s waar u een persoonlijke ervaring wilt weergeven. Deze `decisionScopes` zijn aanpasbaar en door de gebruiker gedefinieerd. Voor huidige [!DNL Target] klanten, `decisionScopes` zijn ook gekend als &quot;dozen.&quot; In de [!DNL Target] UI, `decisionScopes` verschijnen als &quot;plaatsen.&quot;

## __weergavebereik__

AEP [!DNL Web SDK] verstrekt een functionaliteit waar u acties kunt terugwinnen VEC zonder het steunen van AEP [!DNL Web SDK] om de acties VEC voor u terug te geven. Verzend een gebeurtenis met `__view__` als een `decisionScopes`gedefinieerd item.

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

Bij het definiëren van Soorten publiek voor uw Target-activiteiten die via de AEP Web SDK worden geleverd, moet [XDM](https://docs.adobe.com/content/help/en/experience-platform/xdm/home.html) worden gedefinieerd en gebruikt. Nadat u XDM schema&#39;s, klassen, en mengen bepaalt, kunt u een het publieksregel van Target tot stand brengen die door XDM gegevens voor het richten wordt bepaald. Binnen Target worden XDM-gegevens in de Audience Builder weergegeven als een aangepaste parameter. XDM wordt geserialiseerd gebruikend puntaantekening (bijvoorbeeld, `web.webPageDetails.name`).

Als u Target-activiteiten hebt met vooraf gedefinieerd publiek dat aangepaste parameters of een gebruikersprofiel gebruikt, moet u er rekening mee houden dat deze niet correct worden geleverd via de AEP Web SDK. In plaats van aangepaste parameters of het gebruikersprofiel te gebruiken, moet u in plaats daarvan XDM gebruiken. Er is echter een out-of-the-box-publiek dat zich richt op velden die worden ondersteund via de AEP Web SDK en die geen XDM vereisen. Dit zijn de velden die beschikbaar zijn in de gebruikersinterface van Target waarvoor geen XDM vereist is:

* Target Library
* Geo
* Netwerk
* Besturingssysteem
* Sitepagina&#39;s
* Browser
* Verkeersbronnen
* Tijdschema

## Terminologie

__Beslissingen__ - In [!DNL Target]verband hiermee hebben deze betrekking op de ervaring die is gekozen uit een activiteit.

__Toepassingsgebied__ - Het toepassingsgebied van de beschikking. In [!DNL Target], dit is de mBox. Het algemene mBox is het `__view__` bereik.

__Schema__ - Het schema van een besluit is het soort aanbod in [!DNL Target].

__XDM__ - XDM wordt in series vervaardigd in puntaantekening en dan gezet in [!DNL Target] als parameters mBox.
