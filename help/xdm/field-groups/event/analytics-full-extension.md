---
title: Adobe Analytics ExperienceEvent Full Extension Schema Field Group
description: Dit document biedt een overzicht van de veldgroep met het Adobe Analytics ExperienceEvent-schema voor volledige extensie.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 1%

---

# [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] schemaveldgroep

[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), waarin algemene metriek worden vastgelegd die door Adobe Analytics worden verzameld.

In dit document worden de structuur en het gebruiksscenario van de veldgroep Analytics-extensie beschreven.

>[!NOTE]
>
>Vanwege de grootte en het aantal herhaalde elementen in deze veldgroep zijn veel van de velden in deze handleiding samengevouwen om ruimte te besparen. Als u de volledige structuur van deze veldgroep wilt bekijken, kunt u [omhoog het in Platform UI kijken ](../../ui/explore.md) of bekijk het volledige schema in het [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

## Groepsstructuur van veld

De veldgroep bevat één `_experience` object naar een schema, dat zelf één schema bevat `analytics` object.

![Velden op hoofdniveau voor de veldgroep Analytics](../../images/field-groups/analytics-full-extension/full-schema.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `customDimensions` | Object | Hiermee legt u aangepaste afmetingen vast die worden bijgehouden door Analytics. Zie de [onderafdeling](#custom-dimensions) voor meer informatie over de inhoud van dit object. |
| `endUser` | Object | Hiermee legt u de webinteractiedetails vast voor de eindgebruiker die de gebeurtenis heeft geactiveerd. Zie de [onderafdeling](#end-user) voor meer informatie over de inhoud van dit object. |
| `environment` | Object | Hiermee legt u informatie vast over de browser en het besturingssysteem die de gebeurtenis hebben geactiveerd. Zie de [onderafdeling](#environment) voor meer informatie over de inhoud van dit object. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Object | De veldgroep bevat objectvelden voor het vastleggen van maximaal 1000 aangepaste gebeurtenissen. Zie de [onderafdeling](#events) voor meer informatie over deze velden. |
| `session` | Object | Vangt informatie over de zitting die de gebeurtenis teweegbracht. Zie de [onderafdeling](#session) voor meer informatie over de inhoud van dit object. |

{style=&quot;table-layout:auto&quot;}

## `customDimensions` {#custom-dimensions}

`customDimensions` vastleggen, aangepast [afmetingen](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html) die worden bijgehouden door Analytics.

![customDimensions, veld](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `eVars` | Object | Een object dat maximaal 250 conversievariabelen vastlegt ([eVars](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html)). De eigenschappen van dit object worden scheefgetrokken `eVar1` tot `eVar250` en accepteert alleen tekenreeksen voor hun gegevenstype. |
| `hierarchies` | Object | Een object dat maximaal vijf aangepaste hiërarchievariabelen vastlegt ([huurder](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html)). De eigenschappen van dit object worden scheefgetrokken `hier1` tot `hier5`, die zelf objecten met de volgende subeigenschappen zijn:<ul><li>`delimiter`: Het oorspronkelijke scheidingsteken dat is gebruikt om de lijst te genereren die is opgegeven onder `values`.</li><li>`values`: Een gescheiden lijst met namen op hiërarchisch niveau, weergegeven als een tekenreeks.</li></ul> |
| `listProps` | Object | Een object dat maximaal 75 vastlegt [lijstprofielen](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props). De eigenschappen van dit object worden scheefgetrokken `prop1` tot `prop75`, die zelf objecten met de volgende subeigenschappen zijn:<ul><li>`delimiter`: Het oorspronkelijke scheidingsteken dat is gebruikt om de lijst te genereren die is opgegeven onder `values`.</li><li>`values`: Een gescheiden lijst met waarden voor de eigenschap, weergegeven als een tekenreeks.</li></ul> |
| `lists` | Object | Een object dat maximaal drie vastlegt [lijsten](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html). De eigenschappen van dit object worden scheefgetrokken `list1` tot `list3`. Elk van deze eigenschappen bevat één eigenschap `list` array van [[!UICONTROL Key Value Pair]](../../data-types/key-value-pair.md) gegevenstypen. |
| `props` | Object | Een object dat maximaal 75 vastlegt [props](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html). De eigenschappen van dit object worden scheefgetrokken `prop1` tot `prop75` en accepteert alleen tekenreeksen voor hun gegevenstype. |
| `postalCode` | Tekenreeks | Een door de klant opgegeven postcode. |
| `stateProvince` | Tekenreeks | Een door de klant opgegeven staat of provincie. |

{style=&quot;table-layout:auto&quot;}

## `endUser` {#end-user}

`endUser` legt de webinteractiedetails vast voor de eindgebruiker die de gebeurtenis heeft geactiveerd.

![endUser, veld](../../images/field-groups/analytics-full-extension/endUser.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | De informatie met betrekking tot webpagina, koppeling en referentie van de eerste Experience Event voor deze eindgebruiker. |
| `firstTimestamp` | Geheel | Een Unix-tijdstempel voor de eerste ExperienceEvent voor deze eindgebruiker. |

## `environment` {#environment}

`environment` legt informatie vast over de browser en het besturingssysteem die de gebeurtenis hebben geactiveerd.

![milieu](../../images/field-groups/analytics-full-extension/environment.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `browserIDStr` | Tekenreeks | De Adobe Analytics-id van de gebruikte browser (ook wel de [afmetingen browsertype](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | Tekenreeks | De Adobe Analytics-id van het gebruikte besturingssysteem (ook wel bekend als de [dimensie van besturingssysteemtype](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Aangepaste gebeurtenisvelden {#events}

De de uitbreidingsgebiedgroep van de Analyse verstrekt tien objecten gebieden die tot 100 vangen [maateenheden voor aangepaste gebeurtenissen](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) elk, voor een totaal van 1000 voor de veldgroep.

Elk gebeurtenisobject op hoofdniveau bevat de afzonderlijke gebeurtenisobjecten voor het desbetreffende bereik. Bijvoorbeeld: `event101to200` bevat de gebeurtenissen die zijn uitgevoerd vanaf `event101` tot `event200`.

Elk even object gebruikt de [[!UICONTROL Measure]](../../data-types/measure.md) gegevenstype, met een unieke identificatiecode en een kwantificeerbare waarde.

![Aangepast gebeurtenisveld](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` legt informatie vast over de sessie die de gebeurtenis heeft geactiveerd.

![sessieveld](../../images/field-groups/analytics-full-extension/session.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `search` | [[!UICONTROL Search]](../../data-types/search.md) | Hiermee legt u informatie over het web of de mobiele zoekfunctie voor het sessieitem vast. |
| `web` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | Hiermee legt u informatie vast over het klikken op koppelingen, webpaginadetails, informatie over de referenties en browserdetails voor de sessie. |
| `depth` | Geheel | De huidige sessieddiepte (zoals het paginanummer) voor de eindgebruiker. |
| `num` | Geheel | Het huidige sessienummer voor de eindgebruiker. |
| `timestamp` | Geheel | Een Unix-tijdstempel voor de sessie-invoer. |

## Volgende stappen

In dit document wordt de structuur en het gebruik van hoofdletters en kleine letters besproken voor de extensieveldgroep Analytics. Raadpleeg voor meer informatie over de veldgroep zelf de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Als u deze veldgroep gebruikt om analysegegevens te verzamelen met de SDK van het Web van Adobe Experience Platform, raadpleegt u de handleiding [configureren van een gegevensstroom](../../../edge/datastreams/overview.md) om te leren hoe te om gegevens aan XDM op de serverzijde in kaart te brengen.
