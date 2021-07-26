---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;device;tradein;trade-in;trade in;
solution: Experience Platform
title: Device Trade-In Details-schemaveldgroep
topic-legacy: overview
description: Dit document verstrekt een overzicht van de het schemagebiedgroep van Gegevens handel-binnen van het Apparaat.
source-git-commit: 2592d4f494d4d3dcfba63eb539498416fbdf6707
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---

# [!UICONTROL Device Trade-In Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Device Trade-In Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] klasse](../../classes/experienceevent.md). Het verstrekt één enkel gebied (`deviceTradeInDetails`) dat een apparaat handel-binnen transactie, met inbegrip van handel-binnen waarde, originele apparatenidentiteitskaart, en nieuwe apparatenidentiteitskaart beschrijft

![Device Trade-In-detailstructuur](../../images/field-groups/device-trade-in-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `tradeInValue` | [Valuta](../../data-types/currency.md) | De waarde van het apparaat dat wordt verhandeld. |
| `newDeviceID` | Tekenreeks | De id van het nieuwe apparaat waarvoor wordt verhandeld. |
| `originalDeviceID` | Tekenreeks | De id van het apparaat dat wordt verhandeld. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-device-trade-in-details.schema.json)
