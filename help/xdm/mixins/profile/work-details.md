---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixins;work details;profile work;
solution: Experience Platform
title: Contactgegevens bewerken, mix
topic: overview
description: Dit document bevat een overzicht van de mix Details van werkcontact.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 0%

---


# [!UICONTROL Contactgegevens] voor werk, mixen

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document over de updates [van de](../name-updates.md) mixnaam voor meer informatie.

[!UICONTROL De Details] van het Contact van het werk is een standaardmengeling voor de [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix biedt verschillende velden waarin bedrijfsinformatie over een individuele persoon wordt vastgelegd, zoals het werkadres, het werkbericht, het telefoonnummer van de werktelefoon en de organisaties waartoe de persoon behoort.

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