---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;persoonlijke details;Schema ontwerp;mixin;Mixin;
solution: Experience Platform
title: Persoonlijke contactpersoon
topic: overview
description: Dit document geeft een overzicht van de mix Persoonlijke contactgegevens.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---


# [!UICONTROL Personal Contact ] DetailsMixin

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

[!UICONTROL Persoonlijke contactpersoon ] detailleert een standaardmix voor de  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klasse die de contactinformatie voor een individuele persoon beschrijft.

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
