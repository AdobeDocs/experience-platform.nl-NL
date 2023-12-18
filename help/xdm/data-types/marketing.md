---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;apparaat;datatype;data-type;data-type;
solution: Experience Platform
title: Type marketinggegevens
description: Meer informatie over het XDM-gegevenstype Marketing.
exl-id: b5ac0127-15fe-42b6-b7fc-2fbcda7e7e27
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# [!UICONTROL Marketing] gegevenstype

[!UICONTROL Marketing] is een standaard XDM gegevenstype dat marketing activiteiten beschrijft die met een bepaald aanraakpunt actief zijn.

![](../images/data-types/marketing.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignGroup` | String | De naam van de campagnegroep (wanneer meerdere campagnes op dezelfde manier worden gegroepeerd) `50%_DISCOUNT`). |
| `campaignName` | String | De naam van de marketingcampagne, zoals `50%_DISCOUNT_USA` of `50%_DISCOUNT_ASIA`. |
| `trackingCode` | String | De code voor bijhouden die kan worden gebruikt om de marketingcampagne te identificeren waaraan de gebeurtenis is gekoppeld. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
