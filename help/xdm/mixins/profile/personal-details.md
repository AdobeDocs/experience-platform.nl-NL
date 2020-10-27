---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;personal details;Schema design;mixin;Mixin;
solution: Experience Platform
title: Persoonlijke contactpersoon
topic: overview
description: Dit document geeft een overzicht van de mix Persoonlijke contactgegevens.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# [!UICONTROL Persoonlijke contactgegevens] , mix

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document over de updates [van de](../name-updates.md) mixnaam voor meer informatie.

[!UICONTROL De persoonlijke Details] van het Contact is een standaardmengeling voor de [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md) die de contactinformatie voor een individuele persoon beschrijft.

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
