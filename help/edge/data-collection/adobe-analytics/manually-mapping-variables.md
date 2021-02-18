---
title: Adobe Analytics-variabelen handmatig toewijzen in de Adobe Experience Platform Web SDK
description: Leer hoe te om variabelen in Adobe Analytics manueel in kaart te brengen gebruikend verwerkingsregels in het Web SDK van het Experience Platform.
seo-description: Wijs manueel variabelen in Adobe Analytics toe gebruikend verwerkingsregels met Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---


# Variabelen handmatig toewijzen in Adobe Analytics

Adobe Experience Platform [!DNL Web SDK] kan bepaalde variabelen automatisch toewijzen, maar aangepaste variabelen moeten handmatig worden toegewezen.

Voor XDM-gegevens die niet automatisch worden toegewezen aan [!DNL Analytics], kunt u [contextgegevens](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/contextdata.html) gebruiken om uw [schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html) aan te passen. Vervolgens kan het worden toegewezen aan [!DNL Analytics] met behulp van [verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) om [!DNL Analytics] variabelen te vullen.

U kunt ook een standaardset handelingen en productlijsten gebruiken om gegevens te verzenden of op te halen met Adobe Experience Platform Web SDK. Zie [Producten](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html) om dit te doen.

## Contextgegevens

Te gebruiken door [!DNL Analytics], worden de gegevens XDM afgevlakt gebruikend puntaantekening en ter beschikking gesteld als `contextData`. In de volgende lijst met waardeparen ziet u een voorbeeld van `context data`:

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

Alle gegevens die door het randnetwerk worden verzameld, zijn toegankelijk via [verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In [!DNL Analytics], kunt u verwerkingsregels gebruiken om contextgegevens in [!DNL Analytics] variabelen op te nemen.

In de volgende regel is Adobe Analytics bijvoorbeeld ingesteld op het vullen van **Interne zoektermen (eVar2)** met de gegevens die zijn gekoppeld aan **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM-schema

Adobe Experience Platform gebruikt schema&#39;s om de gegevensstructuur op een consistente en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens. [!DNL Analytics] contextgegevens werken met de structuur die door het schema wordt bepaald.

In het volgende voorbeeld wordt getoond hoe de opdracht [`event`](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) kan worden gebruikt met de optie `xdm` om gegevens te verzenden en op te halen met Adobe Experience Platform Web SDK. In dit voorbeeld komt de opdracht `event` overeen met het [ExperienceEvent Commerce Details Schema](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md), zodat de waarden productListItems `name` en `SKU` worden bijgehouden:


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

Zie [Gebeurtenissen bijhouden](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) voor meer informatie over het bijhouden van gebeurtenissen met Adobe Experience Platform.[!DNL Web SDK]
