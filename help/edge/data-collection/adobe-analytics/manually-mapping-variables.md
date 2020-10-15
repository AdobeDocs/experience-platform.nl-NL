---
title: Variabelen handmatig toewijzen in Adobe Analytics
seo-title: Variabelen handmatig toewijzen in Adobe Analytics met Web SDK
description: Hoe kan ik variabelen handmatig toewijzen aan Adobe Analytics met behulp van verwerkingsregels
seo-description: manueel kaart variabelen in Adobe Analytics gebruikend verwerkingsregels met Web SDK
keywords: adobe analytics;analytics;variables;mapping variables;map variables;contextData;context Data;Processing rules;rules;xdm;schema;
translation-type: tm+mt
source-git-commit: 5ef902ef7f7717121744f7f0074c0aa17e5a9e9a
workflow-type: tm+mt
source-wordcount: '377'
ht-degree: 0%

---


# Variabelen handmatig toewijzen in Adobe Analytics

In de Adobe Experience Platform (AEP) [!DNL Web SDK] kunnen bepaalde variabelen automatisch worden toegewezen, maar aangepaste variabelen moeten handmatig worden toegewezen.

Voor XDM-gegevens die niet automatisch worden toegewezen aan [!DNL Analytics], kunt u [contextgegevens](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/contextdata.html) gebruiken om uw [schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)aan te passen. Vervolgens kan het worden toegewezen aan het [!DNL Analytics] gebruik van [verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) om [!DNL Analytics] variabelen te vullen.

U kunt ook een standaardset handelingen en productlijsten gebruiken om gegevens te verzenden of op te halen met de AEP [!DNL Web SDK]. Zie [Producten](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html)om dit te doen.

## Contextgegevens

Om door te worden gebruikt, worden de gegevens XDM afgevlakt gebruikend puntnotatie en ter beschikking gesteld zoals [!DNL Analytics]`contextData`. In de volgende lijst met waardeparen ziet u een voorbeeld van `context data`:

```javascript
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

Alle gegevens die door het randnetwerk worden verzameld, zijn toegankelijk via [verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In kunt [!DNL Analytics]u verwerkingsregels gebruiken om contextgegevens op te nemen in [!DNL Analytics] variabelen.

In de volgende regel is Adobe Analytics bijvoorbeeld ingesteld op het vullen van **interne zoektermen (eVar2)** met de gegevens die zijn gekoppeld aan **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM-schema

[!DNL Experience Platform] gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens. [!DNL Analytics] contextgegevens werken met de structuur die door het schema wordt bepaald.

In het volgende voorbeeld wordt getoond hoe de [`event` opdracht](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) kan worden gebruikt met de `xdm` optie om gegevens te verzenden en op te halen met de AEP [!DNL Web SDK]. In dit voorbeeld, past het `event` bevel het Schema [van de Details van de Handel van](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent aan zodat productListItems `name` en de `SKU` waarden worden gevolgd:


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

Zie Gebeurtenissen [!DNL Web SDK]bijhouden voor meer informatie over het bijhouden van gebeurtenissen met de AEP [](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
