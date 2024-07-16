---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Webpagina-details;datatype;gegevenstype;gegevenstype;webpagina
solution: Experience Platform
title: Gegevenstype Ervaring Channel
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van het kanaal van de Ervaring (XDM).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '240'
ht-degree: 0%

---

# [!UICONTROL Experience channel] gegevenstype

[!UICONTROL Experience channel] is een standaard XDM-gegevenstype (Experience Data Model) waarmee een ervaringskanaal wordt beschreven. Een ervaringskanaal vertegenwoordigt een methode of pad voor het gebruik van digitale ervaringen.

Er zijn veelvoudige ervaringskanalen, elk met verschillende beperkingen op hoe de inhoud wordt geleverd, en hoe de klanteninteractie kan worden waargenomen, en hoe de gegevens worden verzameld. Binnen een kanaal, kunnen de ervaringen aan specifieke plaatsen worden geleverd. De locaties en typen locaties die in een kanaal aanwezig zijn, verschillen van kanaal tot kanaal.

![](../images/data-types/experience-channel.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | String | Een id die het kanaal uniek identificeert. Elk specifiek ervaringskanaal definieert een constante `@id`. |
| `_type` | String | Verstrekt een ruw classificatielabel voor kanalen met gelijkaardige eigenschappen. |
| `contentTypes` | Array van tekenreeksen | De inhoudstypen die dit kanaal kan leveren. |
| `locationTypes` | Array van tekenreeksen | De typen locaties (virtuele locaties) waar dit kanaal uit bestaat en waaraan inhoud kan worden geleverd. |
| `mediaAction` | String | Beschrijft een Actie van de Media van de Gebeurtenis van de Ervaring, als toepasselijk. |
| `mediaType` | String | Beschrijft of het mediatype betaald, bezeten of verdiend is. |
| `metricTypes` | Array van tekenreeksen | De metriek die in dit kanaal kan worden verzameld. |
| `mode` | String | Hoe ervaringen worden opgedaan in dit kanaal. |
| `typeAtSource` | String | Een aangepaste naam voor het kanaal. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
