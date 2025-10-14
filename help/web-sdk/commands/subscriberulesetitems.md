---
title: subscribeRulesetItems
description: Abonneren op inhoudskaarten voor een specifieke oppervlakte gebruikend het subscribeRulesetItems bevel.
source-git-commit: 01cba985e22e4673fb60721c810ac9cbee287386
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 1%

---


# `subscribeRulesetItems`

Met de opdracht `subscribeRulesetItems` kunt u zich abonneren op voorstellingen die het resultaat zijn van bevredigende linialen. U kunt dit doen door te specificeren op welke oppervlakken en schema&#39;s moet worden gefilterd, en een callback functie te verstrekken.

Wanneer tijdlinialen worden geëvalueerd, ontvangt de callback-functie een `result` -object met daarin een array van voorstellingen.

>[!IMPORTANT]
>
>De opdracht `subscribeRulesetItems` is de enige manier om voorstellen op te halen die afkomstig zijn van regels, aangezien deze niet worden geretourneerd naast de resultaten van [`sendEvent`](sendevent/overview.md) .

## Opdrachten {#command-options}

Deze opdracht heeft een `options` -object met de volgende eigenschappen:

| Eigenschap | Type | Beschrijving |
| --- | --- | --- |
| `surfaces` | Tekenreeksarray | Een lijst met oppervlakken. De callback functie zal slechts voorstellen ontvangen als zij één van de hier verstrekte oppervlakten aanpassen. |
| `schemas` | Tekenreeksarray | Een lijst met schema&#39;s. De voorstellen zullen slechts door de callback functie worden ontvangen als zij één van de hier verstrekte schema&#39;s aanpassen. |
| `callback` | Functie | Een callback-functie die wordt aangeroepen wanneer voorstellingen het resultaat zijn van bevredigende regels. De callback-functie ontvangt twee parameters wanneer deze wordt aangeroepen: `result` en `collectEvent` . Zie [&#x200B; callback parameters &#x200B;](#callback-parameters) voor details. |

### Callback-parameters {#callback-parameters}

De callback functie ontvangt de twee parameters die in de lijst hieronder worden beschreven wanneer aangehaald.

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| `result` | Object | Dit object bevat een array `propositions` .  Deze voorstellen zijn het directe resultaat van tevreden regels. Het `result` voorwerp is gestructureerd het zelfde als het [&#x200B; resultaatvoorwerp &#x200B;](command-responses.md) dat door `sendEvent` gebruikend een `then` clausule is teruggekeerd. |
| `collectEvent` | Functie | Een gebruiksvriendelijke functie die u kunt gebruiken om gebeurtenissen van de Edge Network naar spoorinteractie, vertoningen en andere gebeurtenissen te verzenden. |

### `collectEvent` functie {#collectevent-function}

De functie `collectEvent` is een handige functie die u kunt gebruiken om gebeurtenissen van de Edge Network naar spoorinteractie, vertoningen en andere gebeurtenissen te verzenden. De twee parameters die in de onderstaande tabel worden beschreven, worden geaccepteerd.

| Parameter | Type | Beschrijving |
| --- | --- | --- |
| Het type Event | String | Een tekenreeks die aangeeft welk type propositiegebeurtenis moet worden verzonden. Ondersteunde gebeurtenistypen zijn `display` , `interact` of `dismiss` . |
| `propositions` | Array | Een array met voorstellen die overeenkomen met de gebeurtenis. |

## Abonneren op inhoudskaarten met de Web SDK-tagextensie {#tag-extension}

Voer de onderstaande stappen uit om u via de gebruikersinterface Codes aan te melden voor inhoudskaarten.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Events] een bestaande gebeurtenis of maak een nieuwe gebeurtenis.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde **[!UICONTROL Event Type]** in op **[!UICONTROL Subscribe ruleset items]** .
1. Selecteer aan de rechterkant van het scherm de schema&#39;s en oppervlakken waarvoor u zich wilt abonneren op inhoudskaarten.
1. Selecteer **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

## Abonneren op inhoudskaarten met de Web SDK JavaScript-bibliotheek {#library}

De volgende voorbeeldcode abonneert zich op het oppervlak van `web://mywebsite.com/#welcome` voor inhoudskaarten en gebruikt de methode `collectEvent` uit `display` om gebeurtenissen voor alle proposities uit te zenden.

```js
alloy("subscribeRulesetItems", {
  surfaces: ["web://mywebsite.com/#welcome"],
  schemas: ["https://ns.adobe.com/personalization/message/content-card"],
  callback: (result, collectEvent) => {
    const { propositions = [] } = result;
    renderMyPropositions(propositions);
    collectEvent("display", propositions);    
  },
});
```
