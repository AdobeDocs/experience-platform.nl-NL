---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schemaontwerp;mixin;mixin;het werkdetails;het profielwerk;
solution: Experience Platform
title: Werkgroep Contactgegevens schema
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep met het schema Contactgegevens werken.
exl-id: 0133622c-e95f-4833-b2f8-3694d41751b4
translation-type: tm+mt
source-git-commit: 4755f9b7666efd8354a5f15aeed40a7da4a06efe
workflow-type: tm+mt
source-wordcount: '184'
ht-degree: 0%

---


# [!UICONTROL Work Contact Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Work Contact Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De veldgroep bevat verschillende velden waarin beroepsinformatie over een individuele persoon wordt vastgelegd, zoals het werkadres, e-mail over het werk, het telefoonnummer van de werkplek en de organisaties waartoe de persoon behoort.

![](../../images/field-groups/work-contact-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `workAddress` | [Postadres](../../data-types/postal-address.md) | Beschrijft het het werkadres van de persoon. |
| `workEmail` | [E-mailadres](../../data-types/email-address.md) | Beschrijft het het werk e-mailadres van de persoon. |
| `workPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het het het werktelefoonnummer van de persoon. |
| `organizations` | String (Array) | Een array van vrije-vormreeksen die de organisaties vertegenwoordigen waarvan de persoon lid is. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-work-details.schema.json)
