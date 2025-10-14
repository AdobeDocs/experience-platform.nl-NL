---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;apparaat;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype apparaat
description: Meer informatie over het XDM-gegevenstype van het apparaat.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# [!UICONTROL Device] gegevenstype

[!UICONTROL Device] is een standaard XDM gegevenstype dat een geïdentificeerd apparaat beschrijft. Een apparaat is een toepassing of browserinstantie die tijdens verschillende sessies kan worden bijgehouden, meestal door cookies.

![](../images/data-types/device.png){width=450}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `colorDepth` | Geheel | Het aantal kleuren dat de weergave kan vertegenwoordigen. |
| `manufacturer` | String | De naam van de organisatie die eigenaar is van het ontwerp en de creatie van het apparaat. |
| `model` | String | De naam van het model voor het apparaat. Dit is de algemene, leesbare of marketingnaam voor het apparaat. De &quot;iPhone 6S&quot; is bijvoorbeeld een bepaald model voor mobiele telefoons. |
| `modelNumber` | String | De unieke modelnummeraanduiding die door de fabrikant voor deze voorziening is toegekend. Modelnummers zijn geen versies, maar unieke id&#39;s die een bepaalde modelconfiguratie identificeren. |
| `screenHeight` | Geheel | Het aantal verticale pixels van de actieve weergave van het apparaat in de standaardoriëntatie. |
| `screenOrientation` | String | De huidige schermstand. Tot de geaccepteerde waarden behoren `portrait` en `landscape` . |
| `screenWidth` | String | Het aantal horizontale pixels van de actieve weergave van het apparaat in de standaardoriëntatie. |
| `type` | String | Het type apparaat dat wordt bijgehouden. Tot de geaccepteerde waarden behoren: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | String | Een id voor het apparaat. Dit kan een herkenningsteken van DeviceAtlas of een andere dienst zijn die de hardware identificeert die wordt gebruikt. |
| `typeIDService` | String | De naamruimte van de service die wordt gebruikt om het apparaattype te identificeren. Zie [&#x200B; bijlage &#x200B;](#typeIDService) voor details op toegelaten waarden. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Bijlage

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Device] .

## Geaccepteerde waarden voor typeIDService {#typeIDService}

In de volgende tabel worden de geaccepteerde waarden voor `typeIDService` en de bijbehorende betekenissen weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Het apparaat is geïdentificeerd met DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Het apparaat is geïdentificeerd met Adobe Campaign. |
