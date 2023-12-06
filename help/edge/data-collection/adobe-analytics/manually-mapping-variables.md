---
title: Adobe Analytics-variabelen handmatig toewijzen in de Adobe Experience Platform Web SDK
description: Leer hoe te om variabelen in Adobe Analytics manueel in kaart te brengen gebruikend verwerkingsregels in het Web SDK van het Experience Platform.
seo-description: Manually map variables into Adobe Analytics using processing rules with Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;xdm;schema;
exl-id: 395050c1-8d39-4da8-acea-6e618ed662dd
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---

# Variabelen handmatig toewijzen in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kan bepaalde variabelen automatisch toewijzen, maar aangepaste variabelen moeten handmatig worden toegewezen.

Voor XDM-gegevens die niet automatisch worden toegewezen aan [!DNL Analytics]kunt u [contextgegevens](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=nl) om overeen te komen met [schema](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html). Vervolgens kan het worden toegewezen aan [!DNL Analytics] gebruiken [verwerkingsvoorschriften](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) vullen [!DNL Analytics] variabelen.

U kunt ook een standaardset handelingen en productlijsten gebruiken om gegevens te verzenden of op te halen met Adobe Experience Platform Web SDK. Ga hiervoor naar [Verzamelen van handel en productinformatie](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/collect-commerce-data.html).

## Contextgegevens

Te gebruiken door [!DNL Analytics], XDM-gegevens worden afgevlakt met puntnotatie en beschikbaar gemaakt als `contextData`. In de volgende lijst met waardeparen ziet u een voorbeeld van wat de `context data` ziet er als volgt uit:

```json
{
  "bh": "900",
  "bw": "1680",
  "c": "24",
  "c.a.d.key.[0]": "value1",
  "c.a.d.key.[1]": "value2",
  "c.a.d.object.key1": "value1",
  "c.a.d.object.key2.[0]": "value2",
  "c.a.x.environment.browserdetails.javascriptenabled": "true",
  "c.a.x.environment.type": "browser",
  "cust_hit_time_gmt": "1579781427",
  "g": "http://example.com/home",
  "gn": "home",
  "j": "1.8.5",
  "k": "Y",
  "s": "1680x1050",
  "tnta": "218287:1:0|0,218287:1:0|2,218287:1:0|1,218287:1:0|32767,218287:1:0|1,218287:1:0|0,218287:1:0|1,218287:1:0|0,218287:1:0|1",
  "user_agent": "Mozilla/5.0 AppleWebKit/537.36 Safari/537.36",
  "v": "Y"
}
```

## Verwerkingsregels

Alle gegevens die door het Edge-netwerk worden verzameld, zijn toegankelijk via [verwerkingsvoorschriften](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics]kunt u verwerkingsregels gebruiken om contextgegevens in te voegen [!DNL Analytics] variabelen.

In de volgende regel is Adobe Analytics bijvoorbeeld ingesteld op vullen **Interne zoektermen (eVar2)** met de gegevens die aan **a.x._atag.search.term(Context Data)**.

![Een voorbeeld van een regel wordt weergegeven in een UI-afbeelding voor analyse.](assets/examplerule.png)

## XDM-schema

Adobe Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens. [!DNL Analytics] contextgegevens werken met de structuur die door het schema wordt bepaald.

In het volgende voorbeeld wordt getoond hoe het [`event` command](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html) kan worden gebruikt met de `xdm` om gegevens te verzenden en op te halen met Adobe Experience Platform Web SDK. In dit voorbeeld wordt `event` de opdracht komt overeen met de [ExperienceEvent Commerce — Details Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) zodat de productListItems `name` en `SKU` waarden worden bijgehouden:


```javascript
alloy("event",{
  "xdm":{
    "commerce":{
      "productViews":{
        "value":1
      }
    },
    "productListItems":[
      {
        "SKU":"HT105",
        "name":"Large Field Hat",
      },
      {
        "SKU":"HT104",
        "name":"Small Field Hat",
      }
    ]
  }
});
```

Voor meer informatie over het bijhouden van gebeurtenissen met Adobe Experience Platform [!DNL Web SDK], zie [Gebeurtenissen bijhouden](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html).
