---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;poi;interactie;point-of-interest;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Interactie punt
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Point of Interest Interaction.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 0%

---

# [!UICONTROL Point of interest interaction] gegevenstype

[!UICONTROL Point of interest interaction] is een standaard XDM gegevenstype dat het draadloze apparaat beschrijft dat identiteitsinformatie aan mobiele toepassingen meedeelt aangezien de mobiele apparaten binnen waaier vallen.

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Beschrijft de details van POI die de gebeurtenis veroorzaakte. |
| `poiEntries` | Object | Beschrijft het aantal tijden een persoon POI is ingegaan. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |
| `poiExits` | Object | Beschrijft het aantal tijden een persoon POI heeft verlaten. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
