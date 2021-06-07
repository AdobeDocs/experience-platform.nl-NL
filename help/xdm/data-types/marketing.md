---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;apparaat;datatype;data-type;data-type;
solution: Experience Platform
title: Type marketinggegevens
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor marketing.
source-git-commit: cb4afb0979bd65a9a82a6018323fa7beacdbf605
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---


# [!UICONTROL Marketing] gegevenstype

[!UICONTROL Marketing] is een standaard XDM gegevenstype dat marketing activiteiten beschrijft die met een bepaald aanraakpunt actief zijn.

![](../images/data-types/marketing.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `campaignGroup` | Tekenreeks | De naam van de campagnegroep (in gevallen waarin meerdere campagnes zijn gegroepeerd, zoals `50%_DISCOUNT`). |
| `campaignName` | Tekenreeks | De naam van de marketingcampagne, zoals `50%_DISCOUNT_USA` of `50%_DISCOUNT_ASIA`. |
| `trackingCode` | Tekenreeks | De code voor bijhouden die kan worden gebruikt om de marketingcampagne te identificeren waaraan de gebeurtenis is gekoppeld. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/marketing.schema.json)
