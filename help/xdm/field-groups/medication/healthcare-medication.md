---
title: Werkgroep Gezondheidszorg
description: Dit document biedt een overzicht van de veldgroep van het medicatieschema in de gezondheidszorg.
exl-id: 3423d067-fe8c-44e5-a6f9-ce0458d26ebc
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 3%

---

# [!UICONTROL Healthcare medication] schemaveldgroep

[!UICONTROL Healthcare medication] is een standaardschemagebiedgroep voor [[!UICONTROL Medication] class](../../classes/medication.md). Het biedt één veld van het objecttype `medication` waarin details zijn opgenomen zoals merknaam, partijnummer en aantal.

![](../../images/field-groups/healthcare-medication.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `ingredients` | Array van objecten | Vermeldt de ingrediënten in de medicatie. Elk object bevat de volgende eigenschappen: <ul><li>`isActive`: (Boolean) Geeft aan of dit ingrediënt nog steeds actief wordt gebruikt in deze medicatie.</li><li>`name`: (String) De naam van het ingrediënt.</li><li>`quantity`: (String) De hoeveelheid van het ingrediënt in de medicatie.</li></ul> |
| `brandName` | Tekenreeks | De merknaam van het geneesmiddel. |
| `codes` | Array van tekenreeksen | Een lijst met codes die deze medicatie identificeren. |
| `dosageUnitNumber` | Dubbel | Het doseringseenheidnummer voor de medicatie. |
| `dosageUnitOfMeasurement` | Tekenreeks | De maateenheid voor het doseringsnummer. |
| `expiryDate` | DateTime | Vervaldatum van het geneesmiddel. |
| `genericName` | Tekenreeks | De generieke naam van het geneesmiddel. |
| `lotNumber` | Tekenreeks | De unieke id voor de batch van het geneesmiddel. |
| `manufacturerName` | Tekenreeks | De naam van de fabrikant van het geneesmiddel. |
| `quantity` | Dubbel | De hoeveelheid geneesmiddel in de verpakking. |
| `status` | Tekenreeks | Een algemene status die aangeeft of het geneesmiddel/de medicatie al dan niet actief is. |
| `volume` | Dubbel | De hoeveelheid van het geneesmiddel. |

{style="table-layout:auto"}

Voor meer informatie over de veldgroep raadpleegt u de [openbare XDM-opslagplaats](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json).
