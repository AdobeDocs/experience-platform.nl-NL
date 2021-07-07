---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;field group;field group;enduserids;end-user;end user;ids;
solution: Experience Platform
title: Detailsveldgroep eindgebruiker - ID
topic-legacy: overview
description: This document provides an overview of the End User ID Details schema field group.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] schemaveldgroep

>[!NOTE]
>
>The names of several schema field groups have changed. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL End User ID Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] klasse](../../classes/experienceevent.md), die wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van Adobe te beschrijven. De veldgroep biedt een `endUserIDs`-object op hoofdniveau, dat zelf een alleen-lezen `_experience`-veld bevat waarvan de waarden automatisch worden bijgewerkt terwijl er gegevens worden ingevoerd.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

| Property | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `aacustomid` | [Identity](../../data-types/identity.md) | Aangepaste eindgebruiker-id&#39;s voor Adobe Analytics Cloud. |
| `aaid` | [Identiteit](../../data-types/identity.md) | End user IDs for Adobe Analytics Cloud. |
| `acid` | [Identity](../../data-types/identity.md) | End user IDs for Adobe Campaign. |
| `adcloud` | [Identiteit](../../data-types/identity.md) | End user IDs for Adobe Advertising Cloud. |
| `emailid` | [Identity](../../data-types/identity.md) | E-mailadres-id&#39;s. |
| `mcid` | [Identiteit](../../data-types/identity.md) | Adobe Marketing Cloud-id. |
| `phonenumberid` | [Identiteit](../../data-types/identity.md) | Phone number IDs. |
| `tntid` | [Identity](../../data-types/identity.md) | End user IDs for Adobe Target. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
