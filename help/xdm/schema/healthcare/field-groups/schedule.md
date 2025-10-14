---
title: Schema-veldgroep plannen
description: Meer informatie over de veldgroep Schema plannen.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: fcabef50-203c-4239-81b4-210aaf5b26ca
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# [!UICONTROL Schedule] schemaveldgroep

[!UICONTROL Schedule] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../../classes/individual-profile.md) en [[!DNL Provider class]](../../../classes/provider.md). Het verstrekt één enkel voorwerp-type gebied `healthcareSchedule` dat een container voor groeven van tijd is die voor boekingsbenoemingen beschikbaar kunnen zijn.

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../../images/healthcare/field-groups/schedule.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | De sleuven die naar dit schema verwijzen en die de beschikbaarheidsdetails verschaffen aan deze resource(s) waarnaar wordt verwezen. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | De externe id&#39;s voor het programma. |
| [!UICONTROL Planning Horizon] | `planningHorizon` | [[!UICONTROL Period]](../data-types/period.md) | De periode die de slots die naar dit schema verwijzen, bestrijken, zelfs als er geen slots zijn. |
| [!UICONTROL Service Category] | `serviceCategory` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Een brede categorisering van de dienst die tijdens de benoeming moet worden verricht. |
| [!UICONTROL Service Type] | `serviceType` | Array van [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De specifieke dienst die tijdens de benoeming moet worden uitgevoerd. |
| [!UICONTROL Speciality] | `specialty` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De specialiteit van de deskundige die de in de aanstelling gevraagde dienst moet verrichten. |
| [!UICONTROL Active] | `active` | Boolean | Geeft aan of de planningsrecord actief wordt gebruikt. |
| [!UICONTROL Comment] | `comment` | String | Opmerkingen over de beschikbaarheid met als doel het beschrijven van alle uitgebreide informatie, zoals aangepaste beperkingen op de slots. |
| [!UICONTROL Name] | `name` | String | De beschrijving van het schema zoals dat tijdens het zoeken aan een consument zou worden aangeboden. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/schedule.schema.json)
