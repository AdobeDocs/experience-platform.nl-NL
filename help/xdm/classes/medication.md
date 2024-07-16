---
title: Geneesmiddelenklasse
description: Leer meer over de klasse Medication in Experience Data Model (XDM).
exl-id: e5786241-dd6e-450f-98c8-2de46affb3e2
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---

# [!UICONTROL Medication] -klasse

In de klasse Experience Data Model (XDM) legt de klasse [!UICONTROL Medication] de minimale reeks eigenschappen vast die een stof definiëren die wordt gebruikt voor medische behandeling, met name een geneesmiddel of geneesmiddel.

![ structuur van de Klasse ](../images/classes/medication.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, wordt het geen expliciete waarde geleverd tijdens gegevensopname. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `medicationId` | [!UICONTROL String] | Een unieke identificatie voor de medicatie. |
| `medicationName` | [!UICONTROL String] | De naam van het geneesmiddel. |

{style="table-layout:auto"}

De klasse kan met de [[!UICONTROL Healthcare medication] gebiedsgroep ](../field-groups/medication/healthcare-medication.md) worden uitgebreid om verdere details over het geneesmiddel of het geneesmiddel te beschrijven.
