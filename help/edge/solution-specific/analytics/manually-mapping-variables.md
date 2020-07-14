---
title: Variabelen handmatig toewijzen in Analytics
seo-title: Variabelen handmatig toewijzen in Analytics met Web SDK
description: Hoe kan ik variabelen handmatig toewijzen aan Analytics met behulp van verwerkingsregels
seo-description: manueel kaart variabelen in Analytics gebruikend verwerkingsregels met Web SDK
translation-type: tm+mt
source-git-commit: 71193ad346c3976f80b14ee0d6e5b12055a17473
workflow-type: tm+mt
source-wordcount: '388'
ht-degree: 0%

---


# Variabelen handmatig toewijzen in Analytics

De Adobe Experience Platform (AEP) Web SDK kan bepaalde variabelen automatisch in kaart brengen maar de douanevariabelen moeten manueel in kaart worden gebracht.

Voor XDM-gegevens die niet automatisch aan Analytics worden toegewezen, kunt u [contextgegevens](https://docs.adobe.com/content/help/en/analytics/implementation/vars/page-vars/contextdata.html) gebruiken om aan uw [schema](https://docs.adobe.com/content/help/en/experience-platform/xdm/schema/composition.html)te voldoen. Vervolgens kan het in Analytics worden toegewezen met behulp van [verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html) om Analytics-variabelen te vullen.

Ook, kunt u een standaardreeks acties en productlijsten gebruiken om gegevens met het Web SDK van AEP te verzenden of terug te winnen. Zie [Producten](https://docs.adobe.com/content/help/en/experience-platform/edge/implement/commerce.html)om dit te doen.

## Contextgegevens

Voor gebruik door Analytics worden XDM-gegevens afgevlakt met puntnotatie en beschikbaar gemaakt als `contextData`. In de volgende lijst met waardeparen ziet u een voorbeeld van `context data`:

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

Alle gegevens die door het randnetwerk worden verzameld, zijn toegankelijk via [verwerkingsregels](https://docs.adobe.com/content/help/en/analytics/admin/admin-tools/processing-rules/processing-rules-configuration/t-processing-rules.html). In Analytics kunt u verwerkingsregels gebruiken om contextgegevens op te nemen in Analytics-variabelen.

In de volgende regel is Analytics bijvoorbeeld ingesteld op het vullen van **interne zoektermen (eVar2)** met de gegevens die zijn gekoppeld aan **a.x_atag.search.term(Context Data)**.

![](assets/examplerule.png)


## XDM-schema

Het Experience Platform gebruikt schema&#39;s om de structuur van gegevens op een verenigbare en herbruikbare manier te beschrijven. Door gegevens consistent in verschillende systemen te definiëren, wordt het eenvoudiger om betekenis te behouden en dus waarde te verkrijgen van gegevens. Analytics-contextgegevens werken met de structuur die door het schema wordt gedefinieerd.

Het volgende voorbeeld toont hoe het [`event` bevel](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html) met de `xdm` optie kan worden gebruikt om gegevens met het Web SDK van AEP te verzenden en terug te winnen. In dit voorbeeld, past het `event` bevel het Schema [van de Details van de Handel van](https://github.com/adobe/xdm/blob/1c22180490558e3c13352fe3e0540cb7e93c69ca/docs/reference/context/experienceevent-commerce.schema.md) ExperienceEvent aan zodat productListItems `name` en de `SKU` waarden worden gevolgd:


```
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

Voor meer informatie bij het volgen van gebeurtenissen met het Web SDK van AEP, zie het [Volgen gebeurtenissen](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/tracking-events.html).
