---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;device;tradein;trade-in;trade in;
solution: Experience Platform
title: Device Trade-In Details-schemaveldgroep
description: Leer over de handel-binnen het schemagebiedgroep van Details van het Apparaat.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# [!UICONTROL Device Trade-In Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [&#x200B; de naamupdates van de gebiedsgroep &#x200B;](../name-updates.md) voor meer informatie.

[!UICONTROL Device Trade-In Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md). Het verstrekt één enkel gebied (`deviceTradeInDetails`) dat een apparaat handel-binnen transactie, met inbegrip van handel-binnen waarde, originele apparatenidentiteitskaart, en nieuwe apparatenidentiteitskaart beschrijft.

![&#x200B; dossier-binnen structuur van Details van het Apparaat &lbrace;](../../images/field-groups/device-trade-in-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `tradeInValue` | [&#x200B; Valuta &#x200B;](../../data-types/currency.md) | De waarde van het apparaat dat wordt verhandeld. |
| `newDeviceID` | String | De id van het nieuwe apparaat waarvoor wordt verhandeld. |
| `originalDeviceID` | String | De id van het apparaat dat wordt verhandeld. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
