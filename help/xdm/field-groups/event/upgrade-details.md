---
title: Upgradedetails in het schemaveld Groep
description: Meer informatie over de veldgroep voor het schema Details van upgrade.
exl-id: cd3f4cd9-ee0e-4bdf-a630-dd2c3c3cc8c7
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# [!UICONTROL Upgrade Details] schemaveldgroep

[!UICONTROL Upgrade Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse ](../../classes/experienceevent.md) wordt gebruikt om informatie betreffende een verbetering marketing gebeurtenis, met inbegrip van details over de transactie en de verschillende manieren te vangen de aanbieding aan een klant werd getoond die.

De veldgroep bevat één objecttype veld, `upgrades` . De eigenschappen in dit object worden hieronder uitgelegd.

![ structuur van de Details van de Verbetering ](../../images/field-groups/upgrade-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `upgradeImpressions` | Serie van [ Impressions ](../../data-types/impressions.md) | Een array die de opgenomen indrukken (digitale weergaven of overeenkomsten met de upgradeaanbieding) voor de klant opsomt. |
| `upgradeTransaction` | [ Transactie ](../../data-types/transaction.md) | Beschrijft de valutatransactie voor de verbetering. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-upgrade-details.schema.json)
