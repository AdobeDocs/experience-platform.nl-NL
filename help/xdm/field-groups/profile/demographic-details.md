---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Schema ontwerp;gebiedsgroep;field groep;persoon;persoondetails;profiel persoondetails;persoon; persoon
solution: Experience Platform
title: Demografische details schema-veldgroep
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep Demographic Details.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 2%

---


# [!UICONTROL Demographic Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Demographic Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De veldgroep biedt een `person`-object op hoofdniveau, waarvan de subvelden informatie over een individuele persoon beschrijven.

![](../../images/field-groups/demographic-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `person.name` | [Naam persoon](../../data-types/person-name.md) | Een object waarvan de subvelden verschillende elementen van de naam van een persoon beschrijven. |
| `person.birthDate` | Datum | De volledige datum waarop een persoon is geboren, in de vorm van een tijdstempel van ISO 8601. |
| `person.birthDayAndMonth` | Tekenreeks | De dag en de maand waarin een persoon is geboren, in de notatie MM-DD. Dit veld moet worden gebruikt wanneer de dag en de maand van de geboorte van een persoon bekend is, maar niet het jaar. |
| `person.birthYear` | Geheel | Het jaar waarin een persoon werd geboren, inclusief de eeuw (zoals 1989). Dit veld moet worden gebruikt wanneer alleen de leeftijd van de persoon bekend is, niet de volledige geboortedatum. |
| `person.gender` | Tekenreeks | De genderidentiteit van de persoon. |
| `person.martialStatus` | Tekenreeks | Beschrijft de verhouding van een persoon met significante andere. |
| `person.nationality` | Tekenreeks | De juridische relatie tussen een persoon en zijn staat die wordt vertegenwoordigd door middel van de ISO 3166-1 Alpha-2-code. |
| `person.taxId` | Tekenreeks | De belasting-/fiscale ID van de persoon, zoals het TIN in de VS of het CIF/NIF in Spanje. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-person-details.schema.json)