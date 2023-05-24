---
title: Payer-klasse
description: Dit document biedt een overzicht van de klasse Payer in het XDM-model (Experience Data Model).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: 2fd35c4ac29f43391f9dc03c636d20558b701be7
workflow-type: tm+mt
source-wordcount: '128'
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

{style="table-layout:auto"}
