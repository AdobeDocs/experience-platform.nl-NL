---
title: Upgradedetails in het schemaveld
description: Dit document biedt een overzicht van de veldgroep voor het bijwerken van details in het schema.
source-git-commit: 4a74faad811d9b13f93799686df44f04a8d1b784
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---

# [!UICONTROL Upgrade Details] schemaveldgroep

[!UICONTROL Upgrade Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] ](../../classes/experienceevent.md) klasse die wordt gebruikt om informatie betreffende een verbetering marketing gebeurtenis, met inbegrip van details over de transactie en de verschillende manieren te vangen de aanbieding aan een klant werd getoond.

De veldgroep bevat één objecttype veld, `upgrades`. De eigenschappen in dit object worden hieronder uitgelegd.

![Upgrade van detailstructuur](../../images/field-groups/upgrade-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `upgradeImpressions` | Array van [Impressies](../../data-types/impressions.md) | Een array die de opgenomen indrukken (digitale weergaven of overeenkomsten met de upgradeaanbieding) voor de klant opsomt. |
| `upgradeTransaction` | [Transactie](../../data-types/transaction.md) | Beschrijft de valutatransactie voor de verbetering. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
