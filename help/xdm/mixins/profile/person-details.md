---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;mixin;mixin;person;person details;profile person details;person;
solution: Experience Platform
title: Gedetailleerde mix van profielgegevens
topic: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
translation-type: tm+mt
source-git-commit: 27ce9b6e8608bbfccac25387ba96f998272273c1
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---


# [!UICONTROL Gedetailleerde] mix van profielgegevens

[!UICONTROL Details] van de profielpersoon is een standaardmix voor de [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix biedt een `person` object op hoofdniveau, waarvan de subvelden informatie over een individuele persoon beschrijven.

<img src="../../images/mixins/profile-person-details.png" width="600" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `person.name` | [Naam persoon](../../data-types/person-name.md) | Een object waarvan de subvelden verschillende elementen van de naam van een persoon beschrijven. |
| `person.birthDate` | Datum | De volledige datum waarop een persoon is geboren, in de vorm van een tijdstempel van ISO 8601. |
| `person.birthDayAndMonth` | Tekenreeks | De dag en de maand waarin een persoon is geboren, in de notatie MM-DD. Dit veld moet worden gebruikt wanneer de dag en de maand van de geboorte van een persoon bekend is, maar niet het jaar. |
| `person.birthYear` | Geheel | Het jaar waarin een persoon geboren is, inclusief de eeuw (zoals 1989). Dit veld moet worden gebruikt wanneer alleen de leeftijd van de persoon bekend is, niet de volledige geboortedatum. |
| `person.gender` | Tekenreeks | De genderidentiteit van de persoon. |
| `person.martialStatus` | Tekenreeks | Beschrijft de verhouding van een persoon met significante andere. |
| `person.nationality` | Tekenreeks | De juridische relatie tussen een persoon en zijn staat die wordt vertegenwoordigd door middel van de ISO 3166-1 Alpha-2-code. |
| `person.taxId` | Tekenreeks | De belasting-/fiscale ID van de persoon, zoals het TIN in de VS of het CIF/NIF in Spanje. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)
