---
title: Werkgroep Gezondheidszorg
description: Meer informatie over de veldgroep Gezondheidszorg medicatieschema.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 0%

---

# [!UICONTROL Healthcare medication] schemaveldgroep

[!UICONTROL Healthcare medication] is een standaardgroep van het schemagebied voor de [[!UICONTROL Medication] klasse &#x200B;](../../classes/medication.md). Dit veld bevat één objecttype `medication` waarin details worden vastgelegd, zoals de merknaam, het nummer van de partij en het aantal.

![](../../images/field-groups/healthcare-medication.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `ingredients` | Array van objecten | Vermeldt de ingrediënten in de medicatie. Elk object bevat de volgende eigenschappen: <ul><li>`isActive`: (Boolean) Geeft aan of dit ingrediënt nog steeds actief wordt gebruikt in deze medicatie.</li><li>`name`: (String) De naam van het ingrediënt.</li><li>`quantity`: (String) De hoeveelheid van het ingrediënt in de medicatie.</li></ul> |
| `brandName` | String | De merknaam van het geneesmiddel. |
| `codes` | Array van tekenreeksen | Een lijst met codes die deze medicatie identificeren. |
| `dosageUnitNumber` | Dubbel | Het doseringseenheidnummer voor de medicatie. |
| `dosageUnitOfMeasurement` | String | De maateenheid voor het doseringsnummer. |
| `expiryDate` | DateTime | Vervaldatum van het geneesmiddel. |
| `genericName` | String | De generieke naam van het geneesmiddel. |
| `lotNumber` | String | De unieke id voor de batch van het geneesmiddel. |
| `manufacturerName` | String | De naam van de fabrikant van het geneesmiddel. |
| `quantity` | Dubbel | De hoeveelheid geneesmiddel in de verpakking. |
| `status` | String | Een algemene status die aangeeft of het geneesmiddel/de medicatie al dan niet actief is. |
| `volume` | Dubbel | De hoeveelheid van het geneesmiddel. |

{style="table-layout:auto"}

Voor meer details op de gebiedsgroep, verwijs naar de [&#x200B; openbare bewaarplaats XDM &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
