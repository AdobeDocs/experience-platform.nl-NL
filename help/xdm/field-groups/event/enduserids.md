---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;ExperienceEvent;fields;schema's;Schema's;Schemaontwerp;veldgroep;veldgroep;enduserids;eindgebruiker;eindgebruiker;id's;
solution: Experience Platform
title: Detailsveldgroep eindgebruiker - ID
description: Meer informatie over de veldgroep Eindgebruikersdetails van het detailschema.
exl-id: ff5b74f4-7700-4d10-821e-b50f80ea8c05
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%

---


# [!UICONTROL End User ID Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [&#x200B; de naamupdates van de gebiedsgroep &#x200B;](../name-updates.md) voor meer informatie.

[!UICONTROL End User ID Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM ExperienceEvent]  klasse &#x200B;](../../classes/experienceevent.md), die wordt gebruikt om de identiteitsinformatie van een individu over verscheidene toepassingen van Adobe te beschrijven. De veldgroep biedt een `endUserIDs` -object op hoofdniveau dat zelf een `_experience` -veld met het kenmerk Alleen-lezen bevat waarvan de waarden automatisch worden bijgewerkt terwijl er gegevens worden ingevoerd.

![](../../images/field-groups/enduserids.png){width=700}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `aacustomid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Aangepaste eindgebruiker-id&#39;s voor Adobe Analytics Cloud. |
| `aaid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Analytics Cloud. |
| `acid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Campaign. |
| `adcloud` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Advertising. |
| `emailid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | E-mailadres-id&#39;s. |
| `mcid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Adobe Marketing Cloud-id (MCID). De MCID wordt nu de Experience Cloud-id (ECID) genoemd. |
| `phonenumberid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Telefoonnummer-id&#39;s. |
| `tntid` | [&#x200B; Identiteit &#x200B;](../../data-types/identity.md) | Eindgebruiker-id&#39;s voor Adobe Target. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-enduserids.schema.json)
