---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schema-ontwerp;veldgroep;veldgroep;
solution: Experience Platform
title: Veld groep kanaaldetails
description: Dit document biedt een overzicht van de veldgroep Kanaaldetails.
exl-id: b8ec2f57-6882-466e-9b22-61fb2178fb1e
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '142'
ht-degree: 0%

---

# [!UICONTROL Channel Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../name-updates.md) voor meer informatie .

[!UICONTROL Channel Details] is een standaardschemagebiedgroep voor [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md), gebruikt om kanaalinformatie zoals identiteitskaart, kanaaltype, media type, en plaatstype te beschrijven.

![](../../images/field-groups/channel-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `channel` | [Experience Channel](../../data-types/experience-channel.md) | Een object dat productretourneert, garantieregistratie en processen voor winkelwagentjes/bestellingen beschrijft. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-channel.schema.json)
