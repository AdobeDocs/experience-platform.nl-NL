---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;poi;interactie;point-of-interest;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Interactie punt
description: Leer over het Punt van Interactie XDM gegevenstype van de Interactie.
exl-id: 398f56d9-1802-458d-b565-4096beb5b014
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# [!UICONTROL Point of interest interaction] gegevenstype

[!UICONTROL Point of interest interaction] is een standaard XDM gegevenstype dat het draadloze apparaat beschrijft dat identiteitsinformatie aan mobiele toepassingen meedeelt aangezien de mobiele apparaten binnen waaier vallen.

![](../images/data-types/poi-interaction.png){width=400}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Point of interest details]](./poi-details.md) | Beschrijft de details van POI die de gebeurtenis veroorzaakte. |
| `poiEntries` | Object | Beschrijft het aantal tijden een persoon POI is ingegaan. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |
| `poiExits` | Object | Beschrijft het aantal tijden een persoon POI heeft verlaten. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/poi-interaction.schema.json)
