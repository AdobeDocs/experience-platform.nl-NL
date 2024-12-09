---
title: Patiëntenschema-veldgroep
description: Meer informatie over de veldgroep Patiëntenschema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# [!UICONTROL Patient] schemaveldgroep

[!UICONTROL Patient] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse ](../../classes/individual-profile.md). Het verstrekt één enkel voorwerp-type gebied `healthcarePatient` dat de demografie en andere administratieve details over een individu of een dier beschrijft die zorg of andere aan gezondheid gerelateerde diensten ontvangt.

![ de groepsstructuur van het Gebied ](../../images/field-groups/patient.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | Array van [[!UICONTROL Address]](../../data-types/healthcare/address.md) | De adresgegevens van de patiënt. |
| [!UICONTROL Communication] | `communication` | Array van objecten | Een taal die kan worden gebruikt om met de patiënt te communiceren over zijn of haar gezondheid. Zie de [ sectie hieronder ](#communication) voor meer informatie. |
| [!UICONTROL Patient Contacts] | `contact` | Array van objecten | Een contactpartij van een patiënt, zoals voogd, partner of vriend. Zie de [ sectie hieronder ](#contact) voor meer informatie. |
| [!UICONTROL General Practitioner] | `generalPractioner` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De primaire zorgverlener van de patiënt. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Een id voor de patiënt. |
| [!UICONTROL Patient Link Details] | `link` | Array van objecten | Een link naar de bron van een patiënt of verwante persoon die betrekking heeft op dezelfde persoon. Zie de [ sectie hieronder ](#link) voor meer informatie. |
| [!UICONTROL Managing Organization] | `managingOrganization` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De bewaarnemingsorganisatie van het patiëntendossier. |
| [!UICONTROL Marital Status] | `maritalStatus` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De burgerlijke staat van de patiënt. |
| [!UICONTROL Name] | `name` | Array van [[!UICONTROL Human name]](../../data-types/healthcare/human-name.md) | De naam die aan de patiënt is gekoppeld. |
| [!UICONTROL Contact Details] | `telecom` | Array van [[!UICONTROL Contact Point]](../../data-types/healthcare/contact-point.md) | Een contactgegeven, zoals een telefoonnummer of e-mailadres, waarmee de patiënt contact kan opnemen. |
| [!UICONTROL Is Active] | `active` | Boolean | Geeft aan of de patiëntgegevens actief worden gebruikt. |
| [!UICONTROL Birth Date] | `birthDate` | Datum | De geboortedatum van de patiënt. |
| [!UICONTROL Deceased Indicator] | `deceasedBoolean` | Boolean | Geeft aan of de patiënt al dan niet overleden is. |
| [!UICONTROL Deceased Date Time] | `deceasedDateTime` | DateTime | De datum en het tijdstip van overlijden van de patiënt. |
| [!UICONTROL Gender] | `gender` | String | De genderidentiteit van de persoon. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |
| [!UICONTROL Is Part Of Multiple Birth] | `multipleBirthBoolean` | Boolean | Geeft aan of de patiënt deel uitmaakt van een meervoudige geboorte. |
| [!UICONTROL Birth Number] | `multipleBirthInteger` | Geheel | Het geboortegetal in de reeks. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/patient.schema.json)

## `communication` {#communication}

`communication` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ communicatie structuur ](../../images/field-groups/healthcare-patient/communication.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Language] | `language` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De taal die kan worden gebruikt om met de persoon over hun gezondheid te communiceren. |
| [!UICONTROL Is Preferred Language] | `preferred` | Boolean | Geeft aan of de taal de voorkeurstaal is. |

## `contact` {#contact}

`contact` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ de structuur van het contact ](../../images/field-groups/healthcare-patient/contact.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Contact Address] | `address` | [[!UICONTROL Address]](../../data-types/healthcare/address.md) | Het adres van de contactpersoon. |
| [!UICONTROL Contact Name] | `name` | [[!UICONTROL Human Name]](../../data-types/healthcare/human-name.md) | De naam van de contactpersoon. |
| [!UICONTROL Contact Organization] | `organization` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De organisatie die met de contactpersoon is geassocieerd. |
| [!UICONTROL Contact Period] | `period` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | De tijdsperiode waarin het contact was of in gebruik is. |
| [!UICONTROL Relationship'] | `relationship` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De relatie tussen de patiënt en de contactpersoon. |
| [!UICONTROL Contact Details] | `telecom` | Array van objecten | De contactgegevens van de contactpersoon. Zie de [ sectie hieronder ](#telecom) voor meer informatie. |
| [!UICONTROL Gender] | `gender` | String | De genderidentiteit van de persoon. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

### `telecom` {#telecom}

`telecom` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ telecommunicatiestructuur ](../../images/field-groups/healthcare-patient/telecom.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Contact Point] | `contactPoint` | [[!UICONTROL Contact point]](../../data-types/healthcare/contact-point.md) | De contactgegevens van de persoon. |

## `link` {#link}

`link` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ verbindingsstructuur ](../../images/field-groups/healthcare-patient/link.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Other] | `other` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Een link naar de bron van een patiënt of verwante persoon die betrekking heeft op dezelfde persoon. |
| [!UICONTROL Type] | `type` | String | Het type verband tussen de twee patiëntmiddelen. |
