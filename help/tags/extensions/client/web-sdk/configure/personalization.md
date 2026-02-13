---
title: Personalization-configuratie-instellingen
description: Vorm verpersoonlijkingsmontages in de de markeringsuitbreiding van SDK van het Web.
exl-id: 24009a40-92ad-49d6-b768-49d64dccf4e0
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Personalization-configuratie-instellingen {#personalization}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_personalization"
>title="Personalisatie"
>abstract="Hiermee bepaalt u hoe de bestandsextensie van de tag persoonlijke inhoud behandelt."

In deze configuratiesectie kunt u bepalen hoe u bepaalde delen van de pagina wilt verbergen terwijl gepersonaliseerde inhoud wordt geladen. Wanneer correct gevormd, zorgen deze montages ervoor dat uw bezoekers de juiste gepersonaliseerde inhoud zien.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Personalization]** .

![&#x200B; Beeld dat de verpersoonlijkingsmontages van de de markeringsuitbreiding van SDK van het Web in de Markeringen UI toont &#x200B;](../assets/web-sdk-ext-personalization.png)

De volgende opties zijn beschikbaar:

## [!UICONTROL Migrate Target from at.js to the Web SDK]**

Met deze optie stelt u de Web SDK in staat de verouderde `mbox` - en `mboxEdgeCluster` -cookies te lezen en te schrijven die door de `at.js` 1.x- of 2.x-bibliotheken worden gebruikt. Deze instelling helpt bezoekersprofielen intact te houden terwijl er wordt geschakeld tussen pagina&#39;s met de Web SDK of `at.js` op dezelfde website. Als u `at.js` niet ergens op uw site hebt geïmplementeerd, hoeft u dit selectievakje niet in te schakelen. Het JavaScript-bibliotheekequivalent aan dit selectievakje is [`targetMigrationEnabled`](/help/collection/js/commands/configure/targetmigrationenabled.md) .

Wanneer u deze optie inschakelt, moet u ook [`overrideMboxEdgeServer` &#x200B;](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/at-js-implementation/functions-overview/targetglobalsettings#overridemboxedgeserver) in `targetGlobalSettings()` inschakelen.

## [!UICONTROL Prehiding style] {#prehiding-style}

Met de preHide style editor kunt u aangepaste CSS-regels definiëren om specifieke secties van een pagina te verbergen. Wanneer de pagina wordt geladen, gebruikt SDK van het Web deze stijl om de secties te verbergen die moeten worden gepersonaliseerd, wint de verpersoonlijking terug, dan unhides de gepersonaliseerde paginagedeelten. Met deze workflow kunnen bezoekers persoonlijke inhoud zien zonder dat het ophaalproces voor personalisatie wordt geladen in of geflikkerd. Het JavaScript-bibliotheekequivalent voor deze code-editor is [`prehidingStyle`](/help/collection/js/commands/configure/prehidingstyle.md) .

## [!UICONTROL Prehiding snippet] {#prehiding-snippet}

Deze sectie is geen directe configuratie het plaatsen, maar eerder een geschikte plaats waar u implementatiecode kunt verkrijgen. Implementeer dit voorverborgen fragment binnen de tag `<head>` op uw site om de gewenste inhoud te verbergen terwijl de Web SDK-bibliotheek wordt geladen.

>[!IMPORTANT]
>
>Bij het gebruik van het voorverborgen fragment raadt Adobe aan dezelfde CSS-regel te gebruiken tussen het voorverborgen fragment en de voorverborgen stijl.

## [!UICONTROL Enable personalization storage]

Een checkbox die het Web SDK toestaat om verpersoonlijkingsgebeurtenissen op te slaan. in de lokale opslag van de browser. Het is handig wanneer u wilt bijhouden welke ervaringen de bezoeker op de pagina heeft gezien.

## [!UICONTROL Auto click collection for Adobe Journey Optimizer]

Een vervolgkeuzemenu dat bepaalt wanneer het Web SDK automatisch klikt op inhoud die door Adobe Journey Optimizer is geretourneerd.

* **[!UICONTROL Always]**: verzamel alle interacties met voorstellingen.
* **[!UICONTROL Decorated elements only]**: verzamel alleen interacties op elementen met `data-aep-click-label` - of `data-aep-click-token` HTML-kenmerken.
* **[!UICONTROL Never]**: verzamel geen interacties met voorstellingen.

De JavaScript-bibliotheek die equivalent is aan deze vervolgkeuzelijst, is [`autoCollectPropositionInteractions.AJO`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md) . De standaardwaarde is [!UICONTROL Always] .

## [!UICONTROL Auto click collection for Adobe Target]

Een vervolgkeuzemenu dat bepaalt wanneer het Web SDK automatisch klikt op inhoud die door Adobe Target is geretourneerd.

* **[!UICONTROL Always]**: verzamel alle interacties met voorstellingen.
* **[!UICONTROL Decorated elements only]**: verzamel alleen interacties op elementen met `data-aep-click-label` - of `data-aep-click-token` HTML-kenmerken.
* **[!UICONTROL Never]**: verzamel geen interacties met voorstellingen.

De JavaScript-bibliotheek die equivalent is aan deze vervolgkeuzelijst, is [`autoCollectPropositionInteractions.TGT`](/help/collection/js/commands/configure/autocollectpropositioninteractions.md) . De standaardwaarde is [!UICONTROL Never] .
