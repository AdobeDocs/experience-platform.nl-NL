---
title: Gebruikersschemaveldgroep
description: Leer over de het schemagebiedgroep van de Organisatie.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: b0698d36-ebc3-4b76-adcc-1deb2cbb1564
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# [!UICONTROL Organization] schemaveldgroep

[!UICONTROL Organization] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../../classes/individual-profile.md) en [[!DNL Provider class]](../../../classes/provider.md). Het verstrekt één enkel voorwerp-type gebied `healthcareOrganization` dat informatie betreffende groeperingen van mensen of organisaties met een gemeenschappelijk doel bevat.

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../../images/healthcare/field-groups/organization/organization.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| ---| --- | --- | --- |
| [!UICONTROL Contact Details] | `contact` | Array van [[!UICONTROL Extended Contact Details]](../data-types/extended-contact-detail.md) | De contactgegevens van de communicatiemiddelen die beschikbaar zijn voor de specifieke organisatie. Dit kunnen adressen, telefoonaantallen, faxaantallen, mobiele aantallen, e-mailadressen, en websites omvatten. |
| [!UICONTROL End Point] | `endpoint` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Technische eindpunten die toegang bieden tot diensten die voor de organisatie worden geëxploiteerd. |
| [!UICONTROL Identifier] | `indentifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | De id die wordt gebruikt om de organisatie in meerdere verschillende systemen te identificeren. |
| [!UICONTROL Part Of Organization] | `partOf` | [[!UICONTROL Reference]](../data-types/reference.md) | De organisatie waarvan deze organisatie deel uitmaakt. |
| [!UICONTROL Qualification] | `qualification` | Array van objecten | De officiële certificeringen, accreditaties, opleiding, aanwijzingen en licenties die de verlening van zorg door de organisatie toestaan en/of anderszins bevestigen. Zie de [&#x200B; sectie hieronder &#x200B;](#qualification) voor meer informatie. |
| [!UICONTROL Type] | `type` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Het soort organisatie dat het is. |
| [!UICONTROL Active] | `active` | Boolean | Of het verslag van de organisatie nog in actief gebruik is. |
| [!UICONTROL Alias] | `alias` | Array van tekenreeksen | Een lijst met alternatieve namen die de organisatie in het verleden bekend staat als of bekend stond als. |
| [!UICONTROL Description] | `description` | String | De beschrijving van de organisatie die helpt algemene context te verstrekken om de correcte organisatie te verzekeren wordt geselecteerd. |
| [!UICONTROL Name] | `name` | String | De naam die aan de organisatie is gekoppeld. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `qualification` {#qualification}

`qualification` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; kwalificatiestructuur &#x200B;](../../../images/healthcare/field-groups/organization/qualification.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Gecodeerde representatie van de kwalificatie. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | Een id die is toegewezen aan deze kwalificatie voor deze organisatie. |
| [!UICONTROL Issuer] | `issuer` | [[!UICONTROL Reference]](../data-types/reference.md) | Organisatie die de kwalificatie regelt en afgeeft. |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Periode waarin de kwalificatie geldig is. |
