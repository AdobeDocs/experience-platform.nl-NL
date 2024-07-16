---
title: Payer-klasse
description: Leer over de klasse van de Laag in het Model van Gegevens van de Ervaring (XDM).
exl-id: 8d3e0a6d-41eb-4ffe-81dd-c7b7d532a531
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---

# [!UICONTROL Payer] -klasse

In Experience Data Model (XDM) legt de [!UICONTROL Payer] -klasse de minimale reeks eigenschappen vast die een zakelijke entiteit definiëren die gegevens verzamelt die betrekking hebben op verzekeringsmaatschappijen (zoals ziektekostenverzekeringen).

![ structuur van de Klasse ](../images/classes/payer.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, wordt het geen expliciete waarde geleverd tijdens gegevensopname. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `payerId` | [!UICONTROL String] | Een unieke identificatiecode voor de betaler. |
| `payerName` | [!UICONTROL String] | De naam van de betaler. |

{style="table-layout:auto"}
