---
title: Adobe Journey Optimizer gebruiken met de Experience Platform Web SDK
description: Leer hoe u persoonlijke inhoud kunt renderen met de Experience Platform Web SDK met Adobe Journey Optimizer
keywords: ajo;ajo web;adobe road optimizer;renderDecisions;surfaces;decisions;proposities;scope;schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# [!DNL Adobe Journey Optimizer] gebruiken met de [!DNL Experience Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan persoonlijke ervaringen die in [!DNL Adobe Journey Optimizer] worden beheerd, leveren en renderen naar het webkanaal. U kunt een redacteur van WYSIWYG, [!DNL Adobe Journey Optimizer] [ Kanaal van het Web ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), of een niet-visuele interface, het [ op code-Gebaseerde Kanaal van de Ervaring ](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/code-based-experience/get-started-code-based) gebruiken om, uw [!DNL Journey Optimizer Web] campagnes en verpersoonlijkingservaringen tot stand te brengen te activeren en te leveren.

>[!IMPORTANT]
>
>Lees de [ documentatie van het Kanaal van het Web van Adobe Journey Optimizer ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) voor informatie bij het worden begonnen met [!DNL Journey Optimizer Web] ervaring creatie en rapportering.

## Terminologie {#terminology}

**[!UICONTROL Surface]**: Een weboppervlak is een webpagina of locatie op een pagina die wordt aangeduid met een URI waar de [!DNL Adobe Journey Optimizer] -ervaringsinhoud wordt geleverd.

**[!UICONTROL Propositions]**: In [!DNL Adobe Journey Optimizer] hebben de voorstellingen betrekking op de ervaring die u hebt geselecteerd in een [!DNL Journey Optimizer Campaign] .

## [!DNL Adobe Journey Optimizer] inschakelen {#enable-ajo}

Voer de onderstaande stappen uit om [!DNL Adobe Journey Optimizer] te gaan gebruiken.

1. Ga door de [ eerste vereisten ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) van de [!DNL Adobe Journey Optimizer] [ Gids van de Ervaringen van het Web ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), specifiek:
   * Instellen [!DNL Adobe Experience Cloud Visual Editing Helper] .
   * Laat [!DNL Adobe Journey Optimizer] in uw [ datastream ](../../../datastreams/overview.md) toe.
   * Schakel de optie [!UICONTROL Active-On-Edge Merge Policy] in.

2. Voeg de optie `renderDecisions` toe aan uw gebeurtenissen. Stel `renderDecisions` in op `true` voor automatische weergave van geleverde Journey Optimizer-inhoudsprofielen op de oppervlakken van uw webpagina.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Geef desgewenst extra oppervlakken op in uw gebeurtenissen. Standaard genereert de Web SDK automatisch het weboppervlak voor de huidige webpagina en neemt deze op in de aanvraag naar de Edge Network. Indien nodig, kunnen extra oppervlakten in het verzoek worden omvat door deze in de `personalization.surfaces` optie van het `sendEvent` bevel, of in de overeenkomstige **[!UICONTROL Surfaces]** [[!UICONTROL Send event] actie ](../../../tags/extensions/client/web-sdk/action-types.md#send-event) configuratie van de Uitbreiding van SDK van het Web te specificeren.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
           "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![ uitbreiding-toe:voegen-oppervlakte ](./assets/extension-add-surface.png)

   Gebeurtenisoppervlakken worden opgenomen in het aanvraagveld `query.personalization.surfaces` :

   ```json
   {
   "events": [
       {
           "query": {
               "personalization": {
               "schemas": [
                   ...
               ],
               "decisionScopes": [
                   "__view__"
               ],
               "surfaces": [
                   "web://ajostage.weebly.com/"
               ]
               }
           },
           ...
       }
   ]
   }
   ```

4. Gelijkaardig aan andere verpersoonlijkingseigenschappen, kunt u a **[toevoegen prehide fragment](../manage-flicker.md)** om slechts bepaalde gedeelten van de pagina te verbergen terwijl het halen van ervaringen.

## Adobe Journey Optimizer Web-ervaringen maken {#create-ajo-web-experiences}

Volg de [&#128279;](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) instructies van de [!DNL Adobe Journey Optimizer] [ Gids van de Ervaringen van het Web ](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html)  campagne authoring &lbrace;om [!DNL Journey Optimizer Web] campagnes en ervaringen tot stand te brengen.

## Aangepaste inhoud renderen {#rendering-personalized-content}

Zie de documentatie bij [ teruggevende verpersoonlijkingsinhoud ](../rendering-personalization-content.md) voor meer informatie.

Adobe Journey Optimizer-voorstellingen voor weblaten worden op vergelijkbare wijze verwerkt als de `__view__` -voorstellingen voor het beslissingsbereik. Als de optie `renderDecisions` is ingesteld op `true` in de opdracht `sendEvent` , worden deze automatisch gerenderd door de SDK Web.

Voorbeeld Journey Optimizer-inhoudsvoorstel:

```json
{
    "scope": "web://ajostage.weebly.com/",
    "scopeDetails": {
        "correlationID": "ccfaf19c-6360-4aea-b464-0cf924db5da7",
        "characteristics": {
            "eventToken": "eyJtZXNzYWdlRXhlY3V0aW9uIjp7Im1lc3NhZ2VFeGVjdXRpb25JRCI6ImEzNDYxYTMzLTc5MjktNGQyNS1hNmMxLTVkYzM2YWY1NzRmMyIsIm1lc3NhZ2VJRCI6ImNjZmFmMTljLTYzNjAtNGFlYS1iNDY0LTBjZjkyNGRiNWRhNyIsIm1lc3NhZ2VUeXBlIjoibWFya2V0aW5nIiwiY2FtcGFpZ25JRCI6IjEzN2JmMzllLWM1ODgtNGI1My1iODQxLTJiMWZiZDYxM2JkYiIsImNhbXBhaWduVmVyc2lvbklEIjoiMTA1NzY1MmEtZWYwNS00YjE3LWExMmUtY2FlOTQyOTFhMWFjIiwiY2FtcGFpZ25BY3Rpb25JRCI6ImViNTlmODQ4LTk5ZDYtNGE1OC05YmU4LTk4MjIxODU0NmYzNiIsIm1lc3NhZ2VQdWJsaWNhdGlvbklEIjoiYzg2NzFjZmItNDdjYS00YTVjLTg4Y2YtNzYwZDFlZjU1MzQyIn0sIm1lc3NhZ2VQcm9maWxlIjp7ImNoYW5uZWwiOnsiX2lkIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWxzL3dlYiIsIl90eXBlIjoiaHR0cHM6Ly9ucy5hZG9iZS5jb20veGRtL2NoYW5uZWwtdHlwZXMvd2ViIn0sIm1lc3NhZ2VQcm9maWxlSUQiOiI2YTViY2I3ZC02MmYxLTQ5NDItODRkMC02MzE5ZjM5Zjk1ZGUifX0="
        },
        "decisionProvider": "AJO",
        "activity": {
            "id": "137bf39e-c588-4b53-b841-2b1fbd613bdb#eb59f848-99d6-4a58-9be8-982218546f36"
        }
    },
    "id": "002321c0-dff5-4153-b171-a9dfb70b9750",
    "items": [
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": "Welcome AJO!",
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setHtml",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "0a522f66-9e6a-4ded-b1d0-e9167f103290"
        },
        {
            "schema": "https://ns.adobe.com/personalization/dom-action",
            "data": {
                "uiData": {
                    "tagType": "Text",
                    "actionType": "changed"
                },
                "content": {
                    "font-weight": "bold"
                },
                "prehidingSelector": "#wsite-content > DIV:nth-of-type(2) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(1) > DIV:nth-of-type(3) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)",
                "type": "setStyle",
                "selector": "#wsite-content > DIV.wsite-section-wrap:eq(1) > DIV.wsite-section:eq(0) > DIV.wsite-section-content:eq(0) > DIV.container:eq(0) > DIV.wsite-section-elements:eq(0) > DIV.paragraph:eq(0) > FONT:nth-of-type(1) > SPAN:nth-of-type(1)"
            },
            "id": "66216ca5-5d0f-4239-a8c8-6bc4a5a7cbdb"
        }
    ]
}
```

## Foutopsporing {#debugging}

Om de implementaties van de verpersoonlijking van Adobe Journey Optimizer te zuiveren, gebruik [ het zuiveren van SDK van het Web ](/help/web-sdk/use-cases/debugging.md). [!DNL Adobe Journey Optimizer] zuivert sporen zijn beschikbaar wanneer het oplossen van problemen gebruikend [[!DNL Adobe Experience Platform Assurance] ](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Controleer op gebeurtenissen met het voorvoegsel `AJO:` .

![ verzekering-ajo-spoor ](./assets/assurance-ajo-trace.png)
