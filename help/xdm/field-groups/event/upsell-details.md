---
title: Upsell details-schemaveldgroep
description: Meer informatie over de veldgroep Upsell Details.
exl-id: 6b69805d-03bc-489b-945a-03e61b99842e
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# [!UICONTROL Upsell Details] schemaveldgroep

[!UICONTROL Upsell Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md) wordt gebruikt om informatie over een upsell-marketinggebeurtenis te verzamelen, met inbegrip van details over de transactie en de verschillende manieren waarop de aanbieding aan een klant werd getoond.

De veldgroep bevat één veld van het objecttype. `upsells`. De eigenschappen in dit object worden hieronder uitgelegd.

![Structuur van Details uploaden](../../images/field-groups/upsell-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `upsellImpressions` | Array van [Impressies](../../data-types/impressions.md) | Een array die de opgenomen indrukken (digitale weergaven of overeenkomsten met de upsellaanbieding) voor de klant opsomt. |
| `upsellTransaction` | [Transactie](../../data-types/transaction.md) | Beschrijft de valutatransactie voor upsell. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upsell-details.schema.json)
