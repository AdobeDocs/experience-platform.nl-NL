---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;Schema design;field group;field group;person;person details;profile person details;person;
solution: Experience Platform
title: Demografische details schema-veldgroep
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep Demographic Details.
exl-id: 588c044c-b80d-4cb9-9f97-92f040d54bb4
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
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

| Property | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `person.name` | [Naam persoon](../../data-types/person-name.md) | An object whose sub-fields describe various elements of a person&#39;s name. |
| `person.birthDate` | Datum | The full date a person was born on, in the form of an ISO 8601 timestamp. |
| `person.birthDayAndMonth` | Tekenreeks | The day and month a person was born, in the format MM-DD. Dit veld moet worden gebruikt wanneer de dag en de maand van de geboorte van een persoon bekend is, maar niet het jaar. |
| `person.birthYear` | Geheel | Het jaar waarin een persoon werd geboren, inclusief de eeuw (zoals 1989). Dit veld moet worden gebruikt wanneer alleen de leeftijd van de persoon bekend is, niet de volledige geboortedatum. |
| `person.gender` | Tekenreeks | The gender identity of the person. |
| `person.martialStatus` | Tekenreeks | Beschrijft de verhouding van een persoon met significante andere. |
| `person.nationality` | Tekenreeks | De juridische relatie tussen een persoon en zijn staat die wordt vertegenwoordigd door middel van de ISO 3166-1 Alpha-2-code. |
| `person.taxId` | Tekenreeks | De belasting-/fiscale ID van de persoon, zoals het TIN in de VS of het CIF/NIF in Spanje. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Populated example](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.example.1.json)
* [Full schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-person-details.schema.json)