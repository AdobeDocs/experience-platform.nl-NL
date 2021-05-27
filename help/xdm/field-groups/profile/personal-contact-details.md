---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;persoonlijke details;Schema ontwerp;gebiedsgroep;De groep van het Gebied;
solution: Experience Platform
title: Persoonlijke veldgroep contactgegevens
topic-legacy: overview
description: Dit document verstrekt een overzicht van de Persoonlijke het schemagebiedgroep van de Details van het Contact.
exl-id: a78d9aee-ecf6-45a9-b270-cdad5b800a86
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# [!UICONTROL Personal Contact Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Personal Contact Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klasse die de contactinformatie voor een individuele persoon beschrijft.

![](../../images/field-groups/personal-contact-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `faxPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het faxnummer van de persoon. |
| `homeAddress` | [Postadres](../../data-types/postal-address.md) | Beschrijft het woonadres van de persoon. |
| `homePhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het huistelefoonaantal van de persoon. |
| `mobilePhone` | [Telefoonnummer](../../data-types/phone-number.md) | Beschrijft het mobiele telefoonnummer van de persoon. |
| `personalEmail` | [E-mailadres](../../data-types/email-address.md) | Beschrijft het e-mailadres van de persoon. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
