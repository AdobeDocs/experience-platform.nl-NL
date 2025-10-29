---
title: Adobe Analytics ExperienceEvent Full Extension Schema Field Group
description: Leer meer over de Adobe Analytics ExperienceEvent Full Extension schema-veldgroep.
exl-id: b5e17f4a-a582-4059-bbcb-435d46932775
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] schemaveldgroep

[!UICONTROL Adobe Analytics ExperienceEvent Full Extension] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md), die gemeenschappelijke metriek vangt die door Adobe Analytics worden verzameld.

In dit document worden de structuur en het gebruiksscenario van de veldgroep Analytics-extensie beschreven.

>[!NOTE]
>
>Vanwege de grootte en het aantal herhaalde elementen in deze veldgroep zijn veel van de velden in deze handleiding samengevouwen om ruimte te besparen. Om de volledige structuur van deze gebiedsgroep te onderzoeken, kunt u het in Experience Platform UI [ opzoeken of het volledige schema in de ](../../ui/explore.md) openbare bewaarplaats XDM [ bekijken.](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json)

## Groepsstructuur van veld

De veldgroep biedt één `_experience` -object aan een schema, dat zelf één `analytics` -object bevat.

![ Top-level gebieden voor de het gebiedsgroep van Analytics ](../../images/field-groups/analytics-full-extension/full-schema.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `customDimensions` | Object | Hiermee legt u aangepaste afmetingen vast die worden bijgehouden door Analytics. Zie de [ onderafdeling hieronder ](#custom-dimensions) voor meer informatie over de inhoud van dit voorwerp. |
| `endUser` | Object | Hiermee legt u de webinteractiedetails vast voor de eindgebruiker die de gebeurtenis heeft geactiveerd. Zie de [ onderafdeling hieronder ](#end-user) voor meer informatie over de inhoud van dit voorwerp. |
| `environment` | Object | Hiermee legt u informatie vast over de browser en het besturingssysteem die de gebeurtenis hebben geactiveerd. Zie de [ onderafdeling hieronder ](#environment) voor meer informatie over de inhoud van dit voorwerp. |
| `event1to100`<br><br>`event101to200`<br><br>`event201to300`<br><br>`event301to400`<br><br>`event401to500`<br><br>`event501to100`<br><br>`event601to700`<br><br>`event701to800`<br><br>`event801to900`<br><br>`event901to1000` | Object | De veldgroep bevat objectvelden voor het vastleggen van maximaal 1000 aangepaste gebeurtenissen. Zie de [ onderafdeling hieronder ](#events) voor meer informatie over deze gebieden. |
| `session` | Object | Vangt informatie over de zitting die de gebeurtenis teweegbracht. Zie de [ onderafdeling hieronder ](#session) voor meer informatie over de inhoud van dit voorwerp. |

{style="table-layout:auto"}

## `customDimensions` {#custom-dimensions}

`customDimensions` vangt de afmetingen van de douane [ ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/overview.html) die door Analytics worden gevolgd.

![ customDimensions gebied ](../../images/field-groups/analytics-full-extension/customDimensions.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `eVars` | Object | Een voorwerp dat tot 250 omzettingsvariabelen ([ eVars ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/evar.html)) vangt. De eigenschappen van dit object worden `eVar1` naar `eVar250` gekopieerd en accepteren alleen tekenreeksen voor hun gegevenstype. |
| `hierarchies` | Object | Een voorwerp dat tot vijf variabelen van de douanehiërarchie ([ heiers ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/hier.html)) vangt. De eigenschappen van dit object worden `hier1` naar `hier5` geschaald. Dit zijn zelf objecten met de volgende subeigenschappen:<ul><li>`delimiter`: het oorspronkelijke scheidingsteken dat wordt gebruikt om de lijst te genereren die wordt geleverd onder `values` .</li><li>`values`: Een gescheiden lijst met namen op hiërarchisch niveau, weergegeven als een tekenreeks.</li></ul> |
| `listProps` | Object | Een voorwerp dat tot 75 [ lijststeunen ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html#list-props) vangt. De eigenschappen van dit object worden `prop1` naar `prop75` geschaald. Dit zijn zelf objecten met de volgende subeigenschappen:<ul><li>`delimiter`: het oorspronkelijke scheidingsteken dat wordt gebruikt om de lijst te genereren die wordt geleverd onder `values` .</li><li>`values`: Een lijst met gescheiden waarden voor de eigenschap, weergegeven als een tekenreeks.</li></ul> |
| `lists` | Object | Een voorwerp dat tot drie [ lijsten ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/list.html) vangt. De eigenschappen van dit object worden vastgezet `list1` naar `list3` . Elk van deze eigenschappen bevat één `list` -array van [[!UICONTROL Key Value Pair]](../../data-types/key-value-pair.md) -gegevenstypen. |
| `props` | Object | Een voorwerp dat tot 75 [ steunen ](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/prop.html) vangt. De eigenschappen van dit object worden `prop1` naar `prop75` gekopieerd en accepteren alleen tekenreeksen voor hun gegevenstype. |
| `postalCode` | String | Een door de klant opgegeven postcode. |
| `stateProvince` | String | Een door de klant opgegeven staat of provincie. |

{style="table-layout:auto"}

## `endUser` {#end-user}

`endUser` legt de webinteractiedetails vast voor de eindgebruiker die de gebeurtenis heeft geactiveerd.

![ endUser gebied ](../../images/field-groups/analytics-full-extension/endUser.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `firstWeb` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | De informatie over webpagina, koppeling en referentie van de eerste Experience Event voor deze eindgebruiker. |
| `firstTimestamp` | Geheel | Een Unix timestamp voor eerste ExperienceEvent voor deze eindgebruiker. |

## `environment` {#environment}

`environment` legt informatie vast over de browser en het besturingssysteem die de gebeurtenis hebben geactiveerd.

![ milieu gebied ](../../images/field-groups/analytics-full-extension/environment.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `browserIDStr` | String | Het herkenningsteken van Adobe Analytics voor gebruikte browser (anders gekend als [ browser type afmeting ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/browser-type.html)). |
| `operatingSystemIDStr` | String | Het herkenningsteken van Adobe Analytics voor het gebruikte werkende systeem (anders gekend als [ werkend systeemtype dimensie ](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-system-types.html)). |

## Aangepaste gebeurtenisvelden {#events}

De de uitbreidingsgebiedgroep van de Analyse verstrekt tien objecten gebieden die tot 100 [ metriek van de douanegebeurtenis ](https://experienceleague.adobe.com/docs/analytics/components/metrics/custom-events.html) elk vangen, voor een totaal van 1000 voor de gebiedsgroep.

Elk gebeurtenisobject op hoofdniveau bevat de afzonderlijke gebeurtenisobjecten voor het desbetreffende bereik. `event101to200` bevat bijvoorbeeld de gebeurtenissen die van `event101` tot `event200` zijn uitgevoerd.

Elk even object gebruikt het gegevenstype [[!UICONTROL Measure]](../../data-types/measure.md) en verschaft een unieke id en een kwantificeerbare waarde.

![ de gebeurtenisgebied van de Douane ](../../images/field-groups/analytics-full-extension/event-vars.png)

## `session` {#session}

`session` legt informatie vast over de sessie die de gebeurtenis heeft geactiveerd.

![ zittingsgebied ](../../images/field-groups/analytics-full-extension/session.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `search` | [[!UICONTROL Search]](../../data-types/search.md) | Hiermee legt u informatie over het web of de mobiele zoekfunctie voor het sessieitem vast. |
| `web` | [[!UICONTROL Web Information]](../../data-types/web-information.md) | Hiermee legt u informatie vast over het klikken op koppelingen, webpaginadetails, informatie over de referenties en browserdetails voor de sessie. |
| `depth` | Geheel | De huidige sessieddiepte (zoals het paginanummer) voor de eindgebruiker. |
| `num` | Geheel | Het huidige sessienummer voor de eindgebruiker. |
| `timestamp` | Geheel | Een Unix-tijdstempel voor de sessie-invoer. |

## Volgende stappen

In dit document wordt de structuur en het gebruik van hoofdletters en kleine letters besproken voor de veldgroep Analytics-extensie. Voor meer details op de gebiedsgroep zelf, verwijs naar de [ openbare bewaarplaats XDM ](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/analytics/experienceevent-all.schema.json).

Als u deze gebiedsgroep gebruikt om de gegevens van Analytics te verzamelen gebruikend het Web SDK van Adobe Experience Platform, zie de gids op [ vormend een datastream ](../../../datastreams/overview.md) om te leren hoe te om gegevens aan XDM op de serverzijde in kaart te brengen.
