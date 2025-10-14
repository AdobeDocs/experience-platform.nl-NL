---
title: Locatieklasse
description: Leer over de klasse van de Plaats in het Model van Gegevens van de Ervaring (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1d100981-49fb-4f02-b2c6-324f9c541f76
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# [!UICONTROL Location] -klasse

In Experience Data Model (XDM) legt de klasse [!UICONTROL Location] locatie-informatie voor livegebeurtenissen vast, zoals een reishal of sportarena.

![&#x200B; de klassenstructuur van de Plaats &#x200B;](../../../images/healthcare/classes/location.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Identifier] | `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, te hoeven het niet om een expliciete waarde tijdens gegevensopname te worden verstrekt. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| [!UICONTROL Location Identifier] | `locationID` | [!UICONTROL String] | Een unieke id voor de locatie. |
| [!UICONTROL Location Name] | `locationName` | [!UICONTROL String] | De naam van de locatie. |

De klasse kan met de [[!UICONTROL Location] gebiedsgroep &#x200B;](../field-groups/location.md) worden uitgebreid om verdere details over een plaats te beschrijven.
