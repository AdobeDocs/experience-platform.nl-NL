---
title: Planningsklasse
description: Dit document verstrekt een overzicht van de klasse van het Plan in het Model van de Gegevens van de Ervaring (XDM).
source-git-commit: cf39f943e27cd11b0eabbc344774fa12482a8f92
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---

# [!UICONTROL Plan] class

In het Model van de Gegevens van de Ervaring (XDM), [!UICONTROL Plan] klasse legt de minimumreeks eigenschappen vast die een regeling definiëren, zoals een ziektekostenplan of een verzekeringsplan.

![Klassenstructuur](../images/classes/plan.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `planId` | [!UICONTROL String] | Een unieke id voor het plan. |
| `planName` | [!UICONTROL String] | De naam van het plan. |

{style=&quot;table-layout:auto&quot;}

De klasse kan worden uitgebreid met de [[!UICONTROL Healthcare Plan Details] veldgroep](../field-groups/plan/healthcare-plan-details.md) nadere bijzonderheden over een ziektekostenverzekering te verstrekken.
