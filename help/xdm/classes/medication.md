---
title: Geneesmiddelenklasse
description: Dit document biedt een overzicht van de klasse Medication in Experience Data Model (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# [!UICONTROL Medication] class

In het Model van de Gegevens van de Ervaring (XDM), [!UICONTROL Medication] klasse geeft de minimumreeks eigenschappen weer die een stof definiëren die wordt gebruikt voor medische behandeling, met name een geneesmiddel of geneesmiddel.

![Klassenstructuur](../images/classes/medication.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `medicationId` | [!UICONTROL String] | Een unieke identificatie voor de medicatie. |
| `medicationName` | [!UICONTROL String] | De naam van het geneesmiddel. |

{style=&quot;table-layout:auto&quot;}

De klasse kan worden uitgebreid met de [[!UICONTROL Healthcare medication] veldgroep](../field-groups/medication/healthcare-medication.md) voor meer informatie over het geneesmiddel of het geneesmiddel.
