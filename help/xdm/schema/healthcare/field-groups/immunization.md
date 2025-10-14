---
title: Veldgroep immuniteitsschema
description: Leer meer over de het gebiedsgroep van het Schema van de Bevordering.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: a392e26b-7631-4f54-b9ad-cc4586673ac5
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 1%

---

# [!UICONTROL Immunization] schemaveldgroep

[!UICONTROL Immunization] is een standaardgroep van het schemagebied voor de [[!DNL XDM Experience Event]  klasse &#x200B;](../../../classes/experienceevent.md). Het biedt één objecttype veld `healthcareImmunization` waarin informatie over immunisatiegebeurtenissen wordt vastgelegd.

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../../images/healthcare/field-groups/immunization/immunization.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Administered Product] | `administeredProduct` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Het toegediende product. |
| [!UICONTROL Based On] | `basedOn` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | De autoriteit waarop de immunisatiegebeurtenis is gebaseerd. |
| [!UICONTROL Dose Quantity] | `doseQuantity` | [[!UICONTROL Simple Quantity]](../data-types/simple-quantity.md) | De toegediende hoeveelheid vaccin. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Reference]](../data-types/reference.md) | De ontmoeting met de immunisatie maakte deel uit van de vaccinatie. |
| [!UICONTROL Funding Source] | `fundingSource` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De financieringsbron voor het vaccin. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | De bedrijfsidentificatie. |
| [!UICONTROL Information Source] | `informationSource` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Geeft de bron van de gerapporteerde record aan. |
| [!UICONTROL Location] | `location` | [[!UICONTROL Reference]](../data-types/reference.md) | De plaats waar de immunisatie plaatsvond. |
| [!UICONTROL Manufacturer] | `manufacturer` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De fabrikant van het vaccin. |
| [!UICONTROL Note] | `note` | Array van [[!UICONTROL Annotation]](../data-types/annotation.md) | Aanvullende immunisatienota&#39;s. |
| [!UICONTROL Patient] | `patient` | [[!UICONTROL Reference]](../data-types/reference.md) | Wie was geïmmuniseerd. |
| [!UICONTROL Batch] | `performer` | Array van objecten | Wie de immunisatiegebeurtenis heeft uitgevoerd. Zie de [&#x200B; sectie hieronder &#x200B;](#performer) voor meer informatie. |
| [!UICONTROL Program Eligibility] | `programEligibility` | Array van objecten | De patiënt komt in aanmerking voor een specifiek vaccinatieprogramma. Zie de [&#x200B; sectie hieronder &#x200B;](#program-eligibility) voor meer informatie. |
| [!UICONTROL Protocol Applied] | `protocolApplied` | Array van objecten | Het protocol dat door de leverancier wordt verstrekt. Zie de [&#x200B; sectie hieronder &#x200B;](#protocol-applied) voor meer informatie. |
| [!UICONTROL Reaction] | `reaction` | Array van objecten | De details van een reactie na immunisatie. Zie de [&#x200B; sectie hieronder &#x200B;](#reaction) voor meer informatie. |
| [!UICONTROL Reason] | `reason` | Array van [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | De reden voor de immunisatie. |
| [!UICONTROL Route] | `route` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Hoe het vaccin in het lichaam is terechtgekomen. |
| [!UICONTROL Site] | `site` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De plaats op het lichaam waar het vaccin werd toegediend |
| [!UICONTROL Status Reason] | `statusReason` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De reden voor de huidige status. |
| [!UICONTROL Subpotent Reason] | `subpotentReason` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De reden voor het toedienen van het vaccin. |
| [!UICONTROL Supporting Information] | `supportingInformation` | Array van [[!UICONTROL Reference]](../data-types/reference.md) | Aanvullende informatie ter ondersteuning van de immunisatie. |
| [!UICONTROL Vaccine Code] | `vaccineCode` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De code voor het toegediende vaccin. |
| [!UICONTROL Expiration Date] | `expirationDate` | Datum | De vervaldatum van het vaccin. |
| [!UICONTROL Is Subpotent] | `isSubpotent` | Boolean | De indicator om aan te geven of het vaccin al dan niet geïnjecteerd is. |
| [!UICONTROL Lot Number] | `lotNumber` | String | Het partijnummer van het vaccin. |
| [!UICONTROL Occurence DateTime] | `occurenceDateTime` | DateTime | De toedieningsdatum van het vaccin. |
| [!UICONTROL Occurence String] | `occurenceString` | String | De toedieningsdatum van het vaccin. |
| [!UICONTROL Primary Source] | `primarySource` | Boolean | Geeft aan of de gegevens zijn vastgelegd vanuit een primaire bron. |
| [!UICONTROL Status] | `status` | String | De status van de immunisatie. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `completed` </li> <li> `entered-in-error` </li> <li> `not-done` </li> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/immunization.schema.json)

## `performer` {#performer}

`performer` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; uitvoerderstructuur &#x200B;](../../../images/healthcare/field-groups/immunization/performer.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Reference]](../data-types/reference.md) | De persoon of organisatie die de actie uitvoerde. |
| [!UICONTROL Function] | `function` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Welk type prestatie is uitgevoerd. |

## `programEligibility` {#program-eligibility}

`programEligibility` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; programEligibility structuur &#x200B;](../../../images/healthcare/field-groups/immunization/program-eligibility.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Program] | `program` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Het programma waarvoor subsidiabiliteit wordt aangegeven. |
| [!UICONTROL Program Status] | `programStatus` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De geschiktheidsstatus van de patiënt voor het programma. |

## `protocolApplied` {#protocol-applied}

`protocolApplied` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; protocolApplied structure &#x200B;](../../../images/healthcare/field-groups/immunization/protocol-applied.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Authority] | `authority` | [[!UICONTROL Reference]](../data-types/reference.md) | Wie is verantwoordelijk voor het publiceren van de aanbevelingen. |
| [!UICONTROL Target Disease] | `targetDisease` | Array van [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De te voorkomen ziekte waarop het vaccin zich richt. |
| [!UICONTROL Dose Number] | `doseNumber` | String | Het dosisnummer in de reeks. |
| [!UICONTROL Series] | `series` | String | De naam van de vaccinserie. |
| [!UICONTROL Series Doses] | `seriesDoses` | String | Aanbevolen aantal doses voor immuniteit. |

## `reaction` {#reaction}

`reaction` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; reactiestructuur &#x200B;](../../../images/healthcare/field-groups/immunization/reaction.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Manifestation] | `manifestation` | [[!UICONTROL Codeable Reference]](../data-types/codeable-concept.md) | Aanvullende informatie over de reactie. |
| [!UICONTROL Date] | `date` | DateTime | Toen de reactie begon. |
| [!UICONTROL Reported] | `reported` | String | Geeft aan of de reactie zelf werd gerapporteerd. |
