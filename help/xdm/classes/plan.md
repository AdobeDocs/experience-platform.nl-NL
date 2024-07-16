---
title: Planningsklasse
description: Leer over de klasse van het Plan in het Model van Gegevens van de Ervaring (XDM).
exl-id: ccff962d-3104-482c-8d65-d2bd2602a9be
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# [!UICONTROL Plan] -klasse

In het Model van de Gegevens van de Ervaring (XDM), vangt de [!UICONTROL Plan] klasse de minimumreeks eigenschappen die een plan, zoals een ziekteplan of een verzekeringsplan bepalen.

![ structuur van de Klasse ](../images/classes/plan.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, wordt het geen expliciete waarde geleverd tijdens gegevensopname. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `planId` | [!UICONTROL String] | Een unieke id voor het plan. |
| `planName` | [!UICONTROL String] | De naam van het plan. |

{style="table-layout:auto"}

De klasse kan met de [[!UICONTROL Healthcare Plan Details] gebiedsgroep ](../field-groups/plan/healthcare-plan-details.md) worden uitgebreid om verdere details over een plan van de ziekteverzekering te beschrijven.
