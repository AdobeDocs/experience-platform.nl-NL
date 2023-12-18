---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;maatregel;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype meten
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Meetlat (XDM).
exl-id: 5d6cc15d-63cf-4af5-9ae9-12c886dd6735
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# [!UICONTROL Measure] gegevenstype

[!UICONTROL Measure] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een beton kwantificeerbaar gegevenspunt van bepaalde metrisch bevat. Een maat bestaat uit een unieke id en een waarde.

<img src="../images/data-types/measure.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `id` | String | De unieke id van deze maatregel. In geval van gegevensverzameling met communicatiekanalen met verlies, zoals mobiele apps of websites met offlinefunctionaliteit waarbij de verzending van maatregelen niet kan worden gegarandeerd, bevat deze eigenschap een door de klant gegenereerde, unieke id van de genomen maatregel. Het is de beste praktijk om dit voldoende lang te maken om voldoende willekeur te waarborgen. <br><br> Als gegevens zoals tijdstempel, apparaat-id, IP, MAC-adres of andere mogelijk door de gebruiker herkende waarden zijn opgenomen in het genereren van het dialoogvenster `id`, moet het resultaat worden gehasht. Dit zorgt ervoor dat geen PII in de waarde wordt gecodeerd, aangezien het doel niet is om een gebruiker of een apparaat te identificeren, maar de specifieke maatregel in tijd. |
| `value` | Dubbel | De kwantificeerbare waarde van deze maatregel. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/data/measure.schema.json)
