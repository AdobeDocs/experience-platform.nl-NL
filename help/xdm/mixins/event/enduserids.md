---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schemaontwerp;mixin;mixin;enduserids;eindgebruiker;eindgebruiker;ids;
solution: Experience Platform
title: Mengsel met details over eindgebruiker
topic: overview
description: Dit document bevat een overzicht van de mix Details van de eindgebruiker.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---


# [!UICONTROL Eindgebruiker - ID ] Detailsmix

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

[!UICONTROL De Eind - identiteitskaart ] detailleert een standaardmengeling voor de  [[!DNL XDM ExperienceEvent] klasse](../../classes/individual-profile.md), die wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van Adobe te beschrijven. De mix biedt een `endUserIDs`-object op hoofdniveau, dat zelf een alleen-lezen veld `_experience` bevat waarvan de waarden automatisch worden bijgewerkt terwijl er gegevens worden ingevoerd.

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
