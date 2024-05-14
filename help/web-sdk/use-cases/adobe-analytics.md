---
title: Gegevens naar Adobe Analytics verzenden met de Web SDK
description: Leer hoe u gegevens naar Adobe Analytics verzendt met de Adobe Experience Platform Web SDK.
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---


# Gegevens naar Adobe Analytics verzenden met de Web SDK

De SDK van het Web van het Experience Platform kan gegevens naar Adobe Analytics door de Edge Network van het Experience Platform verzenden. Adobe biedt verschillende opties voor het verzenden van gegevens naar Adobe Analytics met de SDK van Web:

* Voeg de [**[!UICONTROL Adobe Analytics ExperienceEvent field group]**](../../xdm/field-groups/event/analytics-full-extension.md) aan uw schema, dan gebruik [`XDM` object](../commands/sendevent/xdm.md).
* Gebruik de [`data` object](../commands/sendevent/data.md) gegevens naar Adobe Analytics verzenden zonder XDM-schema.
* Automatisch gegenereerd gebruiken [contextgegevensvariabelen](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) en [verwerkingsvoorschriften](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Gebruik de `XDM` object {#use-xdm-object}

Als u een vooraf gedefinieerd schema wilt gebruiken dat specifiek is voor Adobe Analytics, kunt u de opdracht [Adobe Analytics ExperienceEvent-schemaveldgroep](../../xdm/field-groups/event/analytics-full-extension.md) op uw schema. Nadat u het schema hebt toegevoegd, kunt u het met het `xdm` voorwerp in het Web SDK om gegevens naar een rapportreeks te verzenden. Wanneer de gegevens bij de Edge Network aankomen, zet het het voorwerp XDM in een formaat om dat Adobe Analytics begrijpt.

U kunt gegevens op twee manieren via Web SDK naar Adobe Analytics verzenden:

* [Gegevens naar Adobe Analytics verzenden met de Web SDK-tagextensie](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [Gegevens naar Adobe Analytics verzenden met de Web SDK JavaScript-bibliotheek](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Zie [XML-objectvariabele toewijzen aan Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping) in de Adobe Analytics-implementatiegids voor een volledige referentie van XDM-velden en hoe deze worden toegewezen aan analytische variabelen.

## Gebruik de `data` object {#use-data-object}

Als alternatief voor het gebruik van het XDM-object kunt u in plaats daarvan het gegevensobject gebruiken. Het gegevensvoorwerp wordt gericht op implementaties die momenteel AppMeasurement gebruiken, die de verbetering aan het Web SDK veel gemakkelijker maken.

Afhankelijk van of u AppMeasurement of de de markeringsuitbreiding van de Analyse gebruikt, zie de volgende gidsen voor details op hoe te om aan Web SDK te migreren:

* [Migreren van de Adobe Analytics-tagextensie naar de Web SDK-tagextensie](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [Migreren van AppMeasurement naar de Web SDK](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Zie de documentatie op [gegevensobjectvariabele toewijzen aan Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) in de Adobe Analytics-implementatiegids voor een volledige referentie van gegevensobjectvelden en hoe deze worden toegewezen aan analytische variabelen.

## Contextgegevensvariabelen gebruiken {#use-context-data-variables}

Variabelen die niet automatisch worden toegewezen, zijn beschikbaar als [contextgegevensvariabelen](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata). U kunt vervolgens [verwerkingsvoorschriften](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) om contextgegevensvariabelen toe te wijzen aan analytische variabelen. Stel dat u een aangepast XDM-schema had dat er als volgt uitziet:

```json
{
  "xdm": {
    "key":"value",
    "animal": {
      "species": "Raven",
      "size": "13 inches"
    },
    "array": [
      "v0",
      "v1",
      "v2"
    ],
    "objectArray":[{
      "ad1": "300x200",
      "ad2": "60x240",
      "ad3": "600x50"
    }]
  }
}
```

Dan zouden deze gebieden de sleutels van contextgegevens beschikbaar aan u in de interface van de Regels van de Verwerking zijn:

```javascript
a.x.key //value
a.x.animal.species //Raven
a.x.animal.size //13 inches
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.objectarray.0.ad1 //300x200
a.x.objectarray.1.ad2 //60x240
a.x.objectarray.2.ad3 //600x50
```

## Veelgestelde vragen

+++Hoe maak ik onderscheid tussen vraag van de paginamening van verbinding het volgen vraag in het Web SDK?

AppMeasurement in Adobe Analytics gebruikt aparte methodeaanroepen voor paginaweergaven ([`t()` methode](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)) en koppelings volgende vraag ([`tl()` methode](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)). De SDK van het Web biedt in plaats daarvan alleen de [`sendEvent`](../commands/sendevent/overview.md) gebruiken voor het verzenden van paginaweergaven en het bijhouden van koppelingen. De gegevens die u in een gebeurtenis opneemt, bepalen of het een [paginaweergave](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views) of [page, gebeurtenis](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events) in Adobe Analytics.

Standaard worden alle gebeurtenissen beschouwd als paginaweergaven in Adobe Analytics. Als u een Web SDK-gebeurtenis wilt instellen op een Adobe Analytics-aanroep voor het bijhouden van koppelingen, stelt u de volgende velden in:

* **XDM-object**: `xdm.web.webInteraction.name`, `web.webInteraction.type`, en `web.webInteraction.URL`
* **Data, object**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType`, en `data.__adobe.analytics.linkURL`
* **Contextgegevens**: Niet ondersteund

Zie de [`tl()` methode](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method) in de Adobe Analytics-implementatiegids voor meer informatie.

Als u [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) in de `configure` , worden deze velden voor u gevuld.

+++

+++Hoe onderscheidt een gegevensstroom gegevens van andere diensten met gegevens die voor Adobe Analytics worden bedoeld?

Alle gebeurtenissen die naar een gegevensstroom worden verzonden worden overgegaan tot alle gevormde diensten. Bijvoorbeeld, als u afzonderlijke vraag naar verpersoonlijking en Analytics maakt, worden beide gebeurtenissen verzonden naar Analytics en Doel. Deze gebeurtenissen worden opgenomen in Analytics-rapporten en kunnen van invloed zijn op metriek zoals de stuiteringsfrequentie.

Als u SDK van het Web gebruikt, worden deze vraag typisch gecombineerd in [`sendEvent`](../commands/sendevent/overview.md) gebruiken.

+++
