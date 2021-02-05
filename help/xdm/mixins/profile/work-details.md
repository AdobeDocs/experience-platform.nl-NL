---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schemaontwerp;mixin;mixin;het werkdetails;het profielwerk;
solution: Experience Platform
title: Contactgegevens bewerken
topic: overview
description: Dit document bevat een overzicht van de mix Details van werkcontact.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---


# [!UICONTROL Gegevensmix ] werkcontact

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

[!UICONTROL De Gegevens van het Contact van het werk ] detailseert een standaardmengeling voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix biedt verschillende velden waarin bedrijfsinformatie over een individuele persoon wordt vastgelegd, zoals het werkadres, het werkbericht, het telefoonnummer van de werktelefoon en de organisaties waartoe de persoon behoort.

<img src="../../images/mixins/profile-work-details.png" width="550" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `workAddress` | [Postadres](../../data-types/postal-address.md) | Beschrijft het het werkadres van de persoon. |
| `workEmail` | [E-mailadres](../../data-types/email-address.md) | Beschrijft het het werk e-mailadres van de persoon. |
| `workPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het het het werktelefoonnummer van de persoon. |
| `organizations` | String (Array) | Een array van vrije-vormreeksen die de organisaties vertegenwoordigen waarvan de persoon lid is. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)