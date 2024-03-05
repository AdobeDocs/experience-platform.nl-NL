---
title: Gegevens naar Adobe Analytics verzenden met de Web SDK
description: Leer hoe u gegevens naar Adobe Analytics verzendt met de Adobe Experience Platform Web SDK.
keywords: adobe analytics;analytics;mapped data;mapped vars;
exl-id: b18d1163-9edf-4a9c-b247-cd1aa7dfca50
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---

# Gegevens naar Adobe Analytics verzenden met de Web SDK

De Adobe Experience Platform Web SDK kan gegevens naar Adobe Analytics verzenden via het Adobe Experience Platform Edge Network. Wanneer de gegevens bij het Netwerk van de Rand aankomen, zet het het voorwerp XDM in een formaat om dat Adobe Analytics begrijpt.

## XDM-veldgroep

Om het gemakkelijker te maken om de gemeenschappelijkste metriek van Adobe Analytics te vangen, verstrekt de Adobe een gebiedsgroep die op Adobe Analytics wordt gericht dat u kunt gebruiken. Voor meer informatie over dit schema raadpleegt u [Adobe Analytics ExperienceEvent Volledige extensieschema, veldgroep](/help/xdm/field-groups/event/analytics-full-extension.md).

## Variabele toewijzen

Het netwerk van de Rand brengt automatisch vele variabelen XDM in kaart. Zie [Analyses variable mapping in het Edge Network](https://experienceleague.adobe.com/docs/analytics/implementation/aep-edge/variable-mapping.html) in de Adobe Analytics-implementatiegids voor een uitgebreide lijst met variabelen die automatisch worden toegewezen.

Variabelen die niet automatisch worden toegewezen, zijn beschikbaar als [Contextgegevensvariabelen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/contextdata.html?lang=nl). U kunt vervolgens [Verwerkingsregels](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/c-processing-rules/c-processing-rules-configuration/processing-rules-about.html) om contextgegevensvariabelen toe te wijzen aan analytische variabelen. Stel dat u een aangepast XDM-schema had dat er als volgt uitziet:

```js
{
  key:value,
  object:{
    key1:value1,
    key2:value2
  },
  array:[
    "v0",
    "v1",
    "v2"
  ],
  arrayofobjects:[
    {
      obj1key:objval0
    },
    {
      obj2key:objval1
    }
  ]
}
```

Dan zouden deze de sleutels van contextgegevens beschikbaar aan u in de interface van de Regels van de Verwerking zijn:

```javascript
a.x.key //value
a.x.object.key1 //value1
a.x.object.key2 //value2
a.x.array.0 //v0
a.x.array.1 //v1
a.x.array.2 //v2
a.x.arrayofobjects.0.obj1key //objval0
a.x.arrayofobjects.1.obj2key //objval1
```

>[!NOTE]
>
>Met de inzameling van het Netwerk van de Rand, worden alle gebeurtenissen verzonden naar Analytics en andere diensten die u voor uw gegevensstroom hebt gevormd. Bijvoorbeeld, als u zowel Analytics als Doel hebt die als diensten wordt gevormd en u afzonderlijke vraag naar verpersoonlijking en voor Analytics maakt, worden beide gebeurtenissen verzonden naar Analytics en Doel. Deze gebeurtenissen worden opgenomen in Analytics-rapporten en kunnen van invloed zijn op metriek zoals de stuiteringsfrequentie.

## De meningen van de pagina en verbinding het volgen vraag

AppMeasurement in Adobe Analytics gebruikt aparte methodeaanroepen voor paginaweergaven ([`t()` methode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/t-method.html)) en koppelings volgende vraag ([`tl()` methode](https://experienceleague.adobe.com/docs/analytics/implementation/vars/functions/tl-method.html)). De SDK van het Web biedt in plaats daarvan alleen de [`sendEvent`](../commands/sendevent/overview.md) gebruiken voor het verzenden van paginaweergaven en het bijhouden van koppelingen. De gegevens die u in een gebeurtenis opneemt, bepalen of het een [paginaweergave](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-views.html) of [page, gebeurtenis](https://experienceleague.adobe.com/docs/analytics/components/metrics/page-events.html) in Adobe Analytics.

Standaard worden alle gebeurtenissen beschouwd als paginaweergaven in Adobe Analytics. Als u een Web SDK-gebeurtenis wilt instellen op een Adobe Analytics-aanroep voor het bijhouden van koppelingen, stelt u de volgende XDM-velden in:

* **`web.webInteraction.URL`**: De URL van de koppeling.
* **`web.webInteraction.name`**: De naam van de aangepaste koppeling, de koppeling Downloaden of de afmeting Afsluiten, afhankelijk van de waarde in `web.webInteraction.type`
* **`web.webInteraction.type`**: Hiermee bepaalt u het type koppeling waarop wordt geklikt. Geldige waarden zijn `other` (Aangepaste koppelingen), `download` (Koppelingen downloaden) en `exit` (Koppelingen afsluiten).

Als u [`clickCollectionEnabled`](../commands/configure/clickcollectionenabled.md) in de `configure` , worden deze XDM-velden voor u gevuld.
