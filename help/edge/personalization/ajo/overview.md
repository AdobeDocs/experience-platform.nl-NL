---
title: Adobe Journey Optimizer gebruiken met de SDK van het Web van het Platform
description: Leer hoe te om gepersonaliseerde inhoud met het Web SDK van het Experience Platform terug te geven gebruikend Adobe Journey Optimizer
keywords: ajo;ajo web;adobe road optimizer;renderDecisions;surfaces;decisions;proposities;scope;schema
exl-id: 3f28e2bc-2c4b-4400-8f69-c7316449ff4f
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---

# Gebruiken [!DNL Adobe Journey Optimizer] met de [!DNL Platform Web SDK]

[!DNL Adobe Experience Platform] [!DNL Web SDK] kan persoonlijke ervaringen leveren en weergeven die worden beheerd in [!DNL Adobe Journey Optimizer] naar het webkanaal. U kunt een redacteur gebruiken WYSIWYG, [!DNL Adobe Journey Optimizer] [Gebruikersinterface webcampagne](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), om uw [!DNL Journey Optimizer Web] campagnes en personalisatie ervaringen.

>[!IMPORTANT]
>
>Lees de [Adobe Journey Optimizer Web Channel-documentatie](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/get-started-web.html) voor informatie over hoe u aan de slag gaat met [!DNL Journey Optimizer Web] het schrijven en rapporteren van ervaringen.

## Terminologie {#terminology}

**[!UICONTROL Surface]**: Een weboppervlak is een webeigenschap die wordt geïdentificeerd door een URL waarbij [!DNL Adobe Journey Optimizer] ervaringsinhoud wordt geleverd.

**[!UICONTROL Propositions]**: In [!DNL Adobe Journey Optimizer], correleren voorstellen met de ervaring die is gekozen op basis van een [!DNL Journey Optimizer Campaign].

## Inschakelen [!DNL Adobe Journey Optimizer] {#enable-ajo}

Als u wilt beginnen met [!DNL Adobe Journey Optimizer]volgt u de onderstaande stappen.

1. Ga door de [voorwaarden](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#prerequesites) van de [!DNL Adobe Journey Optimizer] [Web Experience Guide](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html), met name:
   * Instellen [!DNL Adobe Experience Cloud Visual Editing Helper].
   * Inschakelen [!DNL Adobe Journey Optimizer] in uw [datastream](../../datastreams/overview.md).
   * De optie [!UICONTROL Active-On-Edge Merge Policy] optie.

2. Voeg de `renderDecisions` aan uw gebeurtenissen. Set `renderDecisions` tot `true` voor automatische weergave van geleverde Journey Optimizer-inhoudsprofielen op de oppervlakken van uw webpagina.

   ```javascript
   alloy("sendEvent", {
       ...,
       "renderDecisions": true
   })
   ```

3. Geef desgewenst extra oppervlakken op in uw gebeurtenissen. Door gebrek, zal SDK van het Web automatisch de Weboppervlakte voor de huidige Web-pagina produceren en zal het in het verzoek aan het Netwerk van de Rand omvatten. Indien nodig kunnen aanvullende oppervlakken in het verzoek worden opgenomen door deze op te geven in het dialoogvenster `personalization.surfaces` de `sendEvent` of in het corresponderende **[!UICONTROL Surfaces]** [[!UICONTROL Send event] action](../../extension/action-types.md#send-event) configuratie van de extensie van Web SDK.

   ```javascript
   alloy("sendEvent", {
       ...
       "personalization": {
       "surfaces": [ "web://my.site.com/about.html", "web://my.site.com/contact.html" ]
       }
   })
   ```

   ![extensie-add-surface](./assets/extension-add-surface.png)

   Gebeurtenisoppervlakken worden opgenomen in het dialoogvenster `query.personalization.surfaces` aanvraagveld:

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

4. Net als andere personalisatiefuncties kunt u een **[fragment vooraf verbergen](../manage-flicker.md)** om alleen bepaalde delen van de pagina te verbergen terwijl u ervaringen ophaalt.

## Adobe Journey Optimizer Web-ervaringen maken {#create-ajo-web-experiences}

Volg de [webcampagne ontwerpen](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html#create-web-campaign) instructies van de [!DNL Adobe Journey Optimizer] [Web Experience Guide](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) om [!DNL Journey Optimizer Web] campagnes en ervaringen.

## Aangepaste inhoud renderen {#rendering-personalized-content}

Zie de documentatie op [weergave van personalisatie-inhoud](../rendering-personalization-content.md) voor meer informatie .

Adobe Journey Optimizer-voorstellingen voor weblaten worden op vergelijkbare wijze verwerkt als de `__view__` voorstellen voor het toepassingsgebied van de beslissing. Wanneer `renderDecisions` optie is ingesteld op `true` in de `sendEvent` bevel zullen deze automatisch door het Web SDK worden teruggegeven.

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

Voor foutopsporing in Adobe Journey Optimizer-implementaties kunt u [[!DNL Web SDK] foutopsporing](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/debugging.html). [!DNL Adobe Journey Optimizer] foutopsporingssporen zijn beschikbaar bij het oplossen van problemen met [[!DNL Adobe Experience Platform Assurance]](https://developer.adobe.com/client-sdks/documentation/platform-assurance/). Controleren op gebeurtenissen met de opdracht `AJO:` voorvoegsel.

![assurance-ajo-trace](./assets/assurance-ajo-trace.png)
