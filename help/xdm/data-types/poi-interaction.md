---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;poi;interactie;point-of-interest;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Interactie punt
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype Point of Interest Interaction.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# [!UICONTROL Gegevenstype van ] interactiepunt

[!UICONTROL Interactie van het punt van belang is een standaardXDM gegevenstype dat het draadloze apparaat beschrijft dat identiteitsinformatie aan mobiele toepassingen meedeelt aangezien de mobiele apparaten binnen waaier vallen. ] 

<img src="../images/data-types/poi-interaction.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `poiDetail` | [[!UICONTROL Details van het belangenpunt]](./poi-details.md) | Beschrijft de details van POI die de gebeurtenis veroorzaakte. |
| `poiEntries` | Object | Beschrijft het aantal tijden een persoon POI is ingegaan. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |
| `poiExits` | Object | Beschrijft het aantal tijden een persoon POI heeft verlaten. Bevat twee eigenschappen: <ul><li>`id`: Een unieke id voor de maat.</li><li>`value`: De kwantificeerbare waarde van de maatregel.</li></ul> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/poi-interaction.schema.json)
