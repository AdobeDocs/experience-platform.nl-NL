---
title: Medicatie Dispense Schema Field Group
description: Meer informatie over de veldgroep Medication Dispense schema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: e01a6cd4cf42338f87222a5e2871cd6c3683309a
workflow-type: tm+mt
source-wordcount: '608'
ht-degree: 0%

---

# [!UICONTROL Medication Dispense] schemaveldgroep

[!UICONTROL Medication Dispense] is een standaardgroep van het schemagebied voor de [[!DNL Medication]  klasse ](../../classes/location.md), de [[!DNL XDM Individual Profile]  Klasse ](../../classes/individual-profile.md), en [[!DNL Provider class]](../../classes/provider.md). Het verstrekt één enkel voorwerp-type gebied `healthcareMedicationDispense` dat informatie over een medicatie vangt die voor een genoemde persoon/patiënt moet worden of is verstrekt.

![ de groepsstructuur van het Gebied ](../../images/field-groups/healthcare-medication-dispense/medication-dispense.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Authorizing Prescription] | `authorizingPrescription` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De volgorde waarin het recept kan worden verstrekt. |
| [!UICONTROL Based On] | `basedOn` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Het plan voor het toedienen van de medicatie is gebaseerd op. |
| [!UICONTROL Category] | `category` | Array van [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | De categorie van het geneesmiddel dat wordt verstrekt, valt onder de categorie van het geneesmiddel, zoals de juridische categorie van het geneesmiddel of de categorie geneesmiddelen. |
| [!UICONTROL Days Supply] | `daysSupply` | [[!UICONTROL Simple Quantity]](../../data-types/healthcare/simple-quantity.md) | Het aantal dagen dat de medicatie de patiënt voor zal leveren. |
| [!UICONTROL Destintation] | `destination` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De faciliteit of locatie waar de medicatie werd of zal worden verzonden naar, als onderdeel van het dispensatieevenement. |
| [!UICONTROL Dosage Instruction] | `dosageInstruction` | Array van [[!UICONTROL Dosage]](../../data-types/healthcare/dosage.md) | Beschrijft hoe het geneesmiddel door de patiënt moet worden gebruikt. |
| [!UICONTROL Encounter] | `encounter` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De gebeurtenis die de context voor deze gebeurtenis bepaalt. |
| [!UICONTROL Event History] | `eventHistory` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Een overzicht van de gebeurtenissen die zich hebben voorgedaan rondom de dispensing. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../../data-types/healthcare/identifier.md) | Identificatienummers die bij de verstrekking horen. De id&#39;s moeten worden gedefinieerd door bedrijfsprocessen en/of worden gebruikt om ernaar te verwijzen wanneer een directe URL-verwijzing niet geschikt is. |
| [!UICONTROL Location] | `location` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De belangrijkste fysieke locatie waar het geneesmiddel werd toegediend. |
| [!UICONTROL Medication] | `medication` | [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | Identificeert de gewenste medicatie. Dit moet een link zijn naar een bron die details van de medicatie vertegenwoordigt, of een code die de medicatie identificeert. |
| [!UICONTROL Not Performed Reason] | `notPerformedReason` | [[!UICONTROL Codeable Reference]](../../data-types/healthcare/codeable-reference.md) | De reden waarom het geneesmiddel niet werd toegediend. |
| [!UICONTROL Note] | `note` | Array van [[!UICONTROL Annotation]](../../data-types/healthcare/annotation.md) | Aanvullende informatie over de verstrekking. |
| [!UICONTROL Part Of] | `partOf` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De procedure of het verzoek om medicatie die de toevoer heeft veroorzaakt. |
| [!UICONTROL Performer] | `performer` | Array van objecten | Hiermee wordt aangegeven wie of wat de verzendgebeurtenis heeft uitgevoerd. Zie de [ sectie hieronder ](#performer) voor meer informatie. |
| [!UICONTROL Quantity] | `quantity` | [[!UICONTROL Simple Quantity]](../../data-types/healthcare/simple-quantity.md) | De hoeveelheid geneesmiddel die wordt toegediend, inclusief de maateenheid. |
| [!UICONTROL Receiver] | `receiver` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Identificeert de persoon die de medicatie heeft opgepakt of de plaats waar de medicatie is afgeleverd. |
| [!UICONTROL Subject] | `subject` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Een link naar een bron die de persoon of groep vertegenwoordigt aan wie de medicatie zal worden gegeven. |
| [!UICONTROL Substitution] | `substitution` | Object | Geeft aan of vervanging al dan niet als onderdeel van de vrijstelling is gemaakt. Bevat vier eigenschappen: <li>`wasSubstituted`: Een Booleaanse waarde die waar is als de dispenser om vervanging heeft gevraagd.</li> <li>`type`: Een [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) -waarde die een code bevat die aangeeft of een vervanging is gemaakt.</li> <li>`reason`: een array van [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) -waarden die de reden(en) voor de vervanging bevat.</li> <li>`responsibleParty`: Een [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) -waarde die de persoon of de partij die verantwoordelijk is voor de vervanging biedt. </li> |
| [!UICONTROL Supporting Information] | `supportingInformation` | Array van [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | Aanvullende informatie die het toedienen van het geneesmiddel ondersteunt. |
| [!UICONTROL Type] | `type` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Beschrijft het type van het verstrekken gebeurtenis die zoals een noodvulling of gedeeltelijke vulling wordt uitgevoerd. |
| [!UICONTROL Recorded] | `recorded` | DateTime | De datum en tijd waarop de afstotingsactiviteit is gestart als `whenPrepared` of `whenHandedOver` niet is gevuld. |
| [!UICONTROL Rendered Dosage Instruction] | `renderedDosageInstruction` | String | De volledige weergave van de dosis die in alle doseringsinstructies is opgenomen. Te gebruiken wanneer meerdere doseringsinstructies worden meegeleverd om complexe doseringen te vertegenwoordigen, zoals verhoging of vermindering van de dosering. |
| [!UICONTROL Status] | `status` | String | De status van de verstrekking. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `preperation` </li> <li> `in-progress` </li> <li> `cancelled` </li> <li> `on-hold` </li> <li> `completed` </li> <li> `entered-in-error` </li> <li> `stopped` </li> <li> `declined` </li> <li> `unknown` </li> |
| [!UICONTROL Status Changed] | `statusChanged` | DateTime | De datum en het tijdstip waarop de status van de dispensatie-record is gewijzigd. |
| [!UICONTROL When Handed Over] | `whenHandedOver` | DateTime | De datum en het tijdstip waarop het geneesmiddel aan de patiënt is verstrekt. |
| [!UICONTROL When Prepared] | `whenPrepared` | DateTime | De datum en het tijdstip waarop het toegediende geneesmiddel is verpakt en beoordeeld. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medicationdispense.schema.json)

## `performer` {#performer}

`performer` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![ uitvoerderstructuur ](../../images/field-groups/healthcare-medication-dispense/performer.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Actor] | `actor` | [[!UICONTROL Reference]](../../data-types/healthcare/reference.md) | De deskundige (of gelijkaardige) die de actie uitvoerde. Er moet worden aangenomen dat de actor de dispenser van de medicatie is. |
| [!UICONTROL Function] | `function` | [[!UICONTROL Codeable Concept]](../../data-types/healthcare/codeable-concept.md) | Het type uitvoerder in de dispensing, zoals de datum waarop het item, de verpakker of de laatste controle wordt ingevoerd. |
