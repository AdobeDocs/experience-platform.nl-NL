---
title: Payer-klasse
description: Dit document biedt een overzicht van de klasse Payer in het XDM-model (Experience Data Model).
source-git-commit: 3937963ceee8502b0669a3f007fd38ecf2824e9b
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# [!UICONTROL Payer] class

In het Model van de Gegevens van de Ervaring (XDM), [!UICONTROL Payer] klasse geeft de minimumreeks eigenschappen weer die een betalingsdienstentiteit definiëren die gegevens verzamelt die betrekking hebben op verzekeringsondernemingen (zoals ziektekostenverzekeringen).

![Klassenstructuur](../images/classes/payer.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `payerId` | [!UICONTROL String] | Een unieke identificatiecode voor de betaler. |
| `payerName` | [!UICONTROL String] | De naam van de betaler. |

{style=&quot;table-layout:auto&quot;}
