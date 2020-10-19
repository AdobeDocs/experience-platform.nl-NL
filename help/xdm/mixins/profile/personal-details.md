---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: Persoonlijke gegevens in profiel mengen
topic: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
translation-type: tm+mt
source-git-commit: e58c669b5542453b7fbf6d90deedcd2cf349c0b6
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# [!UICONTROL Profiel van persoonlijke gegevens] mengen

[!UICONTROL Persoonlijke gegevens] van profielen zijn een standaardmix voor de [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix biedt een `person` object op hoofdniveau, waarvan de subvelden contactgegevens over een individuele persoon beschrijven.

<img src="../../images/mixins/profile-personal-details.png" width="700" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `faxPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het faxnummer van de persoon. |
| `homeAddress` | [Postadres](../../data-types/postal-address.md) | Beschrijft het woonadres van de persoon. |
| `homePhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het huistelefoonaantal van de persoon. |
| `mobilePhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het mobiele telefoonnummer van de persoon. |
| `personalEmail` | [E-mailadres](../../data-types/email-address.md) | Beschrijft het e-mailadres van de persoon. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
