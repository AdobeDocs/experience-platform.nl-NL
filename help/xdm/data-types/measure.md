---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;maatregel;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype meten
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Meetlat (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: e028fbb82b37b3940b308a860c26f8b5f9884d3a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# [!UICONTROL Measure] gegevenstype

[!UICONTROL Measure] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een beton kwantificeerbaar gegevenspunt van bepaalde metrisch bevat. Een maat bestaat uit een unieke id en een waarde.

![&#x200B; meetbeeld &#x200B;](../images/data-types/measure.PNG) {width= 500}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `id` | String | De unieke id van deze maatregel. In geval van gegevensverzameling met communicatiekanalen met verlies, zoals mobiele apps of websites met offlinefunctionaliteit waarbij de verzending van maatregelen niet kan worden gegarandeerd, bevat deze eigenschap een door de klant gegenereerde, unieke id van de genomen maatregel. Het is de beste praktijk om dit voldoende lang te maken om voldoende willekeur te waarborgen. <br><br> Als informatie zoals tijdstempel, apparaat-id, IP, MAC-adres of andere mogelijk door de gebruiker te identificeren waarden is opgenomen in het genereren van de `id` , moet het resultaat worden gehasht. Dit zorgt ervoor dat geen PII in de waarde wordt gecodeerd, aangezien het doel niet is om een gebruiker of een apparaat te identificeren, maar de specifieke maatregel in tijd. |
| `value` | Dubbel | De kwantificeerbare waarde van deze maatregel. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
