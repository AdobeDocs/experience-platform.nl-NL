---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;ExperienceEvent;fields;schemas;Schemas;Schema design;mixin;mixin;enduserids;end-user;end user;ids;
solution: Experience Platform
title: ExperienceEvent EndUserIDs mixin
topic: overview
description: Dit document biedt een overzicht van de mix van ExperienceEvent EndUserID's.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 0%

---


# [!UICONTROL ExperienceEvent EndUserIDs] mixin

[!UICONTROL ExperienceEvent EndUserIDs] is een standaardmengeling voor de [[!DNL XDM ExperienceEvent] klasse](../../classes/individual-profile.md), die wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van Adobe te beschrijven. De mix biedt een `endUserIDs` `_experience` object op hoofdniveau dat zelf een alleen-lezen veld bevat waarvan de waarden automatisch worden bijgewerkt terwijl er gegevens worden ingevoerd.

<img src="../../images/mixins/enduserids.png" width="700" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `aacustomid` | [Identiteit](../../data-types/identity.md) | Aangepaste eindgebruiker-id&#39;s voor Adobe Analytics Cloud. |
| `aaid` | [Identiteit](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Analytics Cloud. |
| `acid` | [Identiteit](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Campaign. |
| `adcloud` | [Identiteit](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Advertising Cloud. |
| `emailid` | [Identiteit](../../data-types/identity.md) | E-mailadres-id&#39;s. |
| `mcid` | [Identiteit](../../data-types/identity.md) | Adobe Marketing Cloud-id. |
| `phonenumberid` | [Identiteit](../../data-types/identity.md) | Telefoonnummer-id&#39;s. |
| `tntid` | [Identiteit](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Target. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
