---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;field-groep;device;tradein;trade-in;trade in;
solution: Experience Platform
title: Device Trade-In Details-schemaveldgroep
description: Dit document verstrekt een overzicht van de het schemagebiedgroep van Gegevens handel-binnen van het Apparaat.
exl-id: 744557be-0297-453f-9134-9d0f4ef2df4d
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 1%

---

# [!UICONTROL Device Trade-In Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../name-updates.md) voor meer informatie .

[!UICONTROL Device Trade-In Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Het biedt één veld (`deviceTradeInDetails`), waarin een transactie voor de inruil van een apparaat wordt beschreven, inclusief de inruilwaarde, de oorspronkelijke apparaat-id en de nieuwe apparaat-id.

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
