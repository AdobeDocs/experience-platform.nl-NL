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

* Voeg [**[!UICONTROL Adobe Analytics ExperienceEvent field group]**](../../xdm/field-groups/event/analytics-full-extension.md) aan uw schema toe, dan gebruik [`XDM` voorwerp ](../commands/sendevent/xdm.md).
* Gebruik het [`data` voorwerp ](../commands/sendevent/data.md) om gegevens naar Adobe Analytics zonder een schema te verzenden XDM.
* Het gebruik automatisch geproduceerde [ variabelen van contextgegevens ](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata) en [ verwerkingsregels ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about).

## Het object `XDM` gebruiken {#use-xdm-object}

Als u een vooraf bepaald schema specifiek voor Adobe Analytics wilt gebruiken, kunt u de [ groep van het het schemagebied van de ErvaringEvent van Adobe Analytics ](../../xdm/field-groups/event/analytics-full-extension.md) aan uw schema toevoegen. Zodra toegevoegd, kunt u dit schema bevolken gebruikend het `xdm` voorwerp in het Web SDK om gegevens naar een rapportreeks te verzenden. Wanneer de gegevens bij de Edge Network aankomen, zet het het voorwerp XDM in een formaat om dat Adobe Analytics begrijpt.

U kunt gegevens op twee manieren via Web SDK naar Adobe Analytics verzenden:

* [ verzendt gegevens naar Adobe Analytics gebruikend de de markeringsuitbreiding van SDK van het Web ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-tag-extension)
* [ verzendt gegevens naar Adobe Analytics gebruikend de bibliotheek van JavaScript van SDK van het Web ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/web-sdk-javascript-library)

Zie [ XDM objecten veranderlijke afbeelding aan Adobe Analytics ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/xdm-var-mapping) in de de implementatiegids van Adobe Analytics voor een volledige verwijzing van XDM gebieden en hoe zij aan de variabelen van Analytics in kaart brengen.

## Het object `data` gebruiken {#use-data-object}

Als alternatief voor het gebruik van het XDM-object kunt u in plaats daarvan het gegevensobject gebruiken. Het gegevensvoorwerp wordt gericht op implementaties die momenteel AppMeasurement gebruiken, die de verbetering aan het Web SDK veel gemakkelijker maken.

Afhankelijk van of u AppMeasurement of de de markeringsuitbreiding van de Analyse gebruikt, zie de volgende gidsen voor details op hoe te om aan Web SDK te migreren:

* [ Migreer van de de markeringsuitbreiding van Adobe Analytics aan de de markeringsuitbreiding van SDK van het Web ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/analytics-extension-to-web-sdk)
* [ Migreer van AppMeasurement aan het Web SDK ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/web-sdk/appmeasurement-to-web-sdk)

Zie de documentatie over [ veranderlijke afbeelding van gegevensobjecten aan Adobe Analytics ](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) in de de implementatiegids van Adobe Analytics voor een volledige verwijzing van gegevensobjecten gebieden en hoe zij aan de variabelen van Analytics in kaart brengen.

## Contextgegevensvariabelen gebruiken {#use-context-data-variables}

Om het even welke variabelen die niet automatisch in kaart worden gebracht zijn beschikbaar als [ variabelen van contextgegevens ](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/page-vars/contextdata). U kunt [ verwerkingsregels ](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about) dan gebruiken om de variabelen van contextgegevens aan de variabelen van de Analyse in kaart te brengen. Stel dat u een aangepast XDM-schema had dat er als volgt uitziet:

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

Het AppMeasurement in Adobe Analytics gebruikt afzonderlijke methodevraag voor paginameningen ([`t()` methode ](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/t-method)) en verbinding het volgen vraag ([`tl()` methode ](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method)). De SDK van het Web verstrekt in plaats daarvan slechts het [`sendEvent`](../commands/sendevent/overview.md) bevel voor het verzenden van zowel paginameningen als verbinding het volgen. De gegevens die u in een gebeurtenis omvat bepalen als het a [ paginamening ](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-views) of a [ paginagebeurtenis ](https://experienceleague.adobe.com/en/docs/analytics/components/metrics/page-events) in Adobe Analytics is.

Standaard worden alle gebeurtenissen beschouwd als paginaweergaven in Adobe Analytics. Als u een Web SDK-gebeurtenis wilt instellen op een Adobe Analytics-aanroep voor het bijhouden van koppelingen, stelt u de volgende velden in:

* **voorwerp XDM**: `xdm.web.webInteraction.name`, `web.webInteraction.type`, en `web.webInteraction.URL`
* **voorwerp van Gegevens**: `data.__adobe.analytics.linkName`, `data.__adobe.analytics.linkType`, en `data.__adobe.analytics.linkURL`
* **Contextgegevens**: Niet gesteund

Zie de [`tl()` methode ](https://experienceleague.adobe.com/en/docs/analytics/implementation/vars/functions/tl-method) in de de implementatiegids van Adobe Analytics voor meer informatie.

Als u [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) inschakelt in de opdracht `configure` , worden deze velden voor u gevuld.

+++

+++Hoe onderscheidt een gegevensstroom gegevens van andere diensten met gegevens die voor Adobe Analytics worden bedoeld?

Alle gebeurtenissen die naar een gegevensstroom worden verzonden worden overgegaan tot alle gevormde diensten. Bijvoorbeeld, als u afzonderlijke vraag naar verpersoonlijking en Analytics maakt, worden beide gebeurtenissen verzonden naar Analytics en Doel. Deze gebeurtenissen worden opgenomen in Analytics-rapporten en kunnen van invloed zijn op metriek zoals de stuiteringsfrequentie.

Als u SDK van het Web gebruikt, worden deze vraag typisch gecombineerd in het [`sendEvent`](../commands/sendevent/overview.md) bevel.

+++
