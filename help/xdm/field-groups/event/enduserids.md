---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schemaontwerp;veldgroep;veldgroep;enduserids;eindgebruiker;eindgebruiker;ids;
solution: Experience Platform
title: Detailsveldgroep eindgebruiker - ID
topic-legacy: overview
description: Dit document bevat een overzicht van de veldgroep Eindgebruikersgegevens.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL End User ID Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM ExperienceEvent] klasse](../../classes/individual-profile.md), die wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van Adobe te beschrijven. De veldgroep biedt een `endUserIDs`-object op hoofdniveau, dat zelf een alleen-lezen `_experience`-veld bevat waarvan de waarden automatisch worden bijgewerkt terwijl er gegevens worden ingevoerd.

<img src="../../images/field-groups/enduserids.png" width="700" /><br />

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

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/experience-event/experienceevent-enduserids.schema.json)
