---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Webpagina-details;datatype;gegevenstype;gegevenstype;webpagina
solution: Experience Platform
title: Gegevenstype Ervaring Channel
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype (Experience Channel Experience Data Model).
source-git-commit: b9168052174c250810e59e403cb77419d510df3b
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 2%

---

# [!UICONTROL Experience channel] gegevenstype

[!UICONTROL Experience channel] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een ervaringskanaal beschrijft. Een ervaringskanaal vertegenwoordigt een methode of pad voor het gebruik van digitale ervaringen.

Er zijn veelvoudige ervaringskanalen, elk met verschillende beperkingen op hoe de inhoud wordt geleverd, en hoe de klanteninteractie kan worden waargenomen, en hoe de gegevens worden verzameld. Binnen een kanaal, kunnen de ervaringen aan specifieke plaatsen worden geleverd. De locaties en typen locaties in een kanaal verschillen van kanaal tot kanaal.

![](../images/data-types/experience-channel.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | Tekenreeks | Een id die het kanaal op unieke wijze identificeert. Elk specifiek ervaringskanaal definieert een constante `@id`. |
| `_type` | Tekenreeks | Verstrekt een ruw classificatielabel voor kanalen met gelijkaardige eigenschappen. |
| `contentTypes` | Array van tekenreeksen | De inhoudstypen die dit kanaal kan leveren. |
| `locationTypes` | Array van tekenreeksen | De typen locaties (virtuele locaties) waar dit kanaal uit bestaat en waaraan inhoud kan worden geleverd. |
| `mediaAction` | Tekenreeks | Beschrijft een Actie van de Media van de Gebeurtenis van de Ervaring, als toepasselijk. |
| `mediaType` | Tekenreeks | Beschrijft of het mediatype betaald, bezeten of verdiend is. |
| `metricTypes` | Array van tekenreeksen | De metriek die in dit kanaal kan worden verzameld. |
| `mode` | Tekenreeks | Hoe ervaringen worden opgedaan in dit kanaal. |
| `typeAtSource` | Tekenreeks | Een aangepaste naam voor het kanaal. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
