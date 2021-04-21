---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schemaontwerp;mixin;mixin;het werkdetails;het profielwerk;
solution: Experience Platform
title: Contactgegevens bewerken
topic-legacy: overview
description: Dit document bevat een overzicht van de mix Details van werkcontact.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# [!UICONTROL Work Contact Details] mixen

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

[!UICONTROL Work Contact Details] is een standaardmix voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix biedt verschillende velden waarin bedrijfsinformatie over een individuele persoon wordt vastgelegd, zoals het werkadres, het werkbericht, het telefoonnummer van de werktelefoon en de organisaties waartoe de persoon behoort.

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
