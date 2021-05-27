---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;apparaat;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype apparaat
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype van het apparaat.
exl-id: 049a2ca1-6bc3-4b9c-832a-77102e8a0ed2
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 3%

---

# [!UICONTROL Device] gegevenstype

[!UICONTROL Device] is een standaard XDM gegevenstype dat een geïdentificeerd apparaat beschrijft. Een apparaat is een toepassing of browserinstantie die tijdens verschillende sessies kan worden bijgehouden, meestal door cookies.

<img src="../images/data-types/device.png" width="450" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `colorDepth` | Geheel | Het aantal kleuren dat de weergave kan vertegenwoordigen. |
| `manufacturer` | Tekenreeks | De naam van de organisatie die eigenaar is van het ontwerp en de creatie van het apparaat. |
| `model` | Tekenreeks | De naam van het model voor het apparaat. Dit is de algemene, leesbare of marketingnaam voor het apparaat. De &quot;iPhone 6S&quot; is bijvoorbeeld een bepaald model voor mobiele telefoons. |
| `modelNumber` | Tekenreeks | De unieke modelnummeraanduiding die door de fabrikant voor deze voorziening is toegekend. Modelnummers zijn geen versies, maar unieke id&#39;s die een bepaalde modelconfiguratie identificeren. |
| `screenHeight` | Geheel | Het aantal verticale pixels van de actieve weergave van het apparaat in de standaardoriëntatie. |
| `screenOrientation` | Tekenreeks | De huidige schermstand. Tot de geaccepteerde waarden behoren `portrait` en `landscape`. |
| `screenWidth` | Tekenreeks | Het aantal horizontale pixels van de actieve weergave van het apparaat in de standaardoriëntatie. |
| `type` | Tekenreeks | Het type apparaat dat wordt bijgehouden. Tot de geaccepteerde waarden behoren: <ul><li>`mobile`</li><li>`tablet`</li><li>`desktop`</li><li>`ereader`</li><li>`gaming`</li><li>`television`</li><li>`settop`</li><li>`mediaplayer`</li><li>`computers`</li><li>`tv screens`</li></ul> |
| `typeID` | Tekenreeks | Een id voor het apparaat. Dit kan een herkenningsteken van DeviceAtlas of een andere dienst zijn die de hardware identificeert die wordt gebruikt. |
| `typeIDService` | Tekenreeks | De naamruimte van de service die wordt gebruikt om het apparaattype te identificeren. Zie [appendix](#typeIDService) voor meer informatie over toegestane waarden. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/device.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/device.schema.json)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Device].

## Geaccepteerde waarden voor typeIDService {#typeIDService}

In de volgende tabel worden de geaccepteerde waarden voor `typeIDService` en de bijbehorende betekenissen weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `https://ns.adobe.com/xdm/external/deviceatlas` | Het apparaat is geïdentificeerd met DeviceAtlas. |
| `https://ns.adobe.com/xdm/external/adobecampaign` | Het apparaat is geïdentificeerd met Adobe Campaign. |
