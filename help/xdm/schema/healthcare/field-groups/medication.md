---
title: Medicatieschema veldgroep
description: Meer informatie over de veldgroep Geneesmiddelenschema.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: e1f53ff8-3079-4b2f-9e73-31a773907a63
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 0%

---

# [!UICONTROL Medication] schemaveldgroep

[!UICONTROL Medication] is een standaardgroep van het schemagebied voor de [[!DNL Medication]  klasse &#x200B;](../../../classes/medication.md). Het biedt één objecttype veld `healthcareMedication` waarin de gegevens van een medicatie worden vastgelegd.

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../../images/healthcare/field-groups/medication/medication.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| ---|  --- | --- | --- |
| [!UICONTROL Batch] | `batch` | Object | Gegevens over een verpakte medicatie. Bevat twee eigenschappen: <li>`lotNumber`: Een tekenreekswaarde voor de id die is toegewezen aan de batch.</li> <li>`expirationDate`: Een DateTime-waarde voor wanneer de batch vervalt.</li> |
| [!UICONTROL Code] | `code` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De code die deze medicatie identificeert. |
| [!UICONTROL Definition] | `definition` | [[!UICONTROL Reference]](../data-types/reference.md) | De definitie van het geneesmiddel. |
| [!UICONTROL Dose Form] | `doseForm` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | Beschrijft de vorm van de dosering van het geneesmiddel, zoals tabletten of capsules. |
| [!UICONTROL Identifier] | `identifier` | Array van [[!UICONTROL Identifier]](../data-types/identifier.md) | Een id voor de medicatie. |
| [!UICONTROL Ingredient] | `ingredient` | Array van objecten | Beschrijft informatie over ingrediënten voor de medicatie. Zie de [&#x200B; sectie hieronder &#x200B;](#ingredient) voor meer informatie. |
| [!UICONTROL Marketing Authorization Holder] | `marketingAuthorizationHolder` | [[!UICONTROL Reference]](../data-types/reference.md) | De organisatie die de vergunning heeft om het geneesmiddel in de handel te brengen. |
| [!UICONTROL Total Volume] | `totalVolume` | [[!UICONTROL Quantity]](../data-types/quantity.md) | De hoeveelheid product die in de medicatie wordt vermeld wanneer de productcode geen verpakkingsgrootte afleidt. |
| [!UICONTROL Status] | `status` | String | De status van de medicatie. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `active` </li> <li> `inactive` </li> <li> `entered-in-error` </li> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/medication.schema.json)

## `ingredient` {#ingredient}

`ingredient` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![&#x200B; ingrediëntenstructuur &#x200B;](../../../images/healthcare/field-groups/medication/ingredient.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Item] | `item` | [[!UICONTROL Codeable Reference]](../data-types/codeable-reference.md) | Het ingrediënt dat wordt beschreven. |
| [!UICONTROL Strength Codeable Concept] | `strengthCodeableConcept` | [[!UICONTROL Codeable Concept]](../data-types/codeable-concept.md) | De hoeveelheid van het aanwezige ingrediënt, uitgedrukt in een systeem met gedefinieerde terminologie. |
| [!UICONTROL Strength Quantity] | `strengthQuantity` | [[!UICONTROL Quantity]](../data-types/quantity.md) | De hoeveelheid van het aanwezige ingrediënt. |
| [!UICONTROL Strength Ratio] | `strengthRatio` | [[!UICONTROL Ratio]](../data-types/ratio.md) | De verhouding van het aanwezige ingrediënt. |
| [!UICONTROL Is Active] | `isActive` | Boolean | Geeft aan of het ingrediënt actief is. |
