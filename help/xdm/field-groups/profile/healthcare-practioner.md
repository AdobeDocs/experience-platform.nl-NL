---
title: Praktijkschema-veldgroep
description: Leer over de het gebiedsgroep van het Schema van de Praktijk.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---

# [!UICONTROL Practioner] schemaveldgroep

[!UICONTROL Practioner] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse ](../../classes/individual-profile.md) en [[!DNL Provider class]](../../classes/provider.md). Het verstrekt één enkel voorwerp-type gebied `healthcarePractioner` dat informatie over een persoon bevat die direct of indirect bij de levering van gezondheidszorg of verwante diensten betrokken is.

![ de groepsstructuur van het Gebied ](../../images/field-groups/healthcare-practitioner/practitioner.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Address] | `address` | Array van [[!UICONTROL Address]](../../data-types/healthcare/address.md) | Adres(sen) van de arts die zich buiten hun werkplek bevinden, zoals een huisadres. |
| [!UICONTROL Communication] | `communication` | Array van object | Een taal die kan worden gebruikt om met de arts te communiceren. Zie de [ sectie hieronder ](#communication) voor meer informatie |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Een id die op deze persoon in deze rol van toepassing is. |
| [!UICONTROL Name] | `name` | Array van [[!UICONTROL Human Name]](../../data-types/healthcare/human-name.md) | De namen die aan de arts zijn gekoppeld. |
| [!UICONTROL Qualification] | `qualification` | Array van object | De officiële kwalificaties, certificeringen, accreditaties, opleiding, vergunningen of dergelijke die de beroepsbeoefenaar toestaan of anderszins aan het verlenen van zorg onderwerpen. Zie de [ sectie hieronder ](#qualification) voor meer informatie. |
| [!UICONTROL Contact Details] | `telecom` | Array van [[!UICONTROL Contact Point]](../../data-types/healthcare/contact-point.md) | De contactgegevens van de arts. |
| [!UICONTROL Active] | `active` | Boolean | Geeft aan of de registers van artsen actief worden gebruikt. |
| [!UICONTROL Birth Date] | `birthDate` | Datum | De geboortedatum van de arts. |
| [!UICONTROL Deceased Indicator] | `deceasedBoolean` | Boolean | Hiermee wordt aangegeven of de operator overleden is. |
| [!UICONTROL Deceased Date Time] | `deceasedDateTime` | DateTime | Datum en tijdstip van overlijden van de arts. |
| [!UICONTROL Gender] | `gender` | String | De genderidentiteit van de persoon. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `female` </li> <li> `male` </li> <li> `other` </li> <li> `unknown`</li> |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/practitioner.schema.json)

## `communication` {#communication}

`communication` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ communicatie structuur ](../../images/field-groups/healthcare-practitioner/communication.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Language] | `language` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De taal die kan worden gebruikt om met de persoon over hun gezondheid te communiceren. |
| [!UICONTROL Is Preferred Language] | `preferred` | Boolean | Geeft aan of de taal de voorkeurstaal is. |

{style="table-layout:auto"}

## `qualification` {#qualification}

`qualification` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ kwalificatiestructuur ](../../images/field-groups/healthcare-practitioner/qualification.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De gecodeerde representatie van de kwalificatie. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Een id voor de kwalificatie. |
| [!UICONTROL Issuer] | `issuer` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De organisatie die de kwalificatie regelt en afgeeft. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../../data-types/healthcare/period.md) | De periode waarin de kwalificatie geldig is. |

{style="table-layout:auto"}
