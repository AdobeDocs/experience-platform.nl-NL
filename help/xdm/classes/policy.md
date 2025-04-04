---
title: Beleidsklasse
description: Leer over de klasse van het Beleid in het Model van Gegevens van de Ervaring (XDM).
exl-id: 56cc8c69-84a0-493e-85c5-e0cd994e4bee
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# [!UICONTROL Policy] -klasse

In Experience Data Model (XDM) legt de klasse [!UICONTROL Policy] de minimale set eigenschappen vast die een verzekeringsbeleid definiëren.

![](../images/classes/policy.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `assignedBeneficiary` | Array van [[!UICONTROL Person]](../data-types/person.md) gegevenstypen | Vangt de begunstigde (of begunstigden) aan het beleid toegewezen. |
| `benefitAmount` | [[!UICONTROL Currency]](../data-types/currency.md) | Het bedrag dat moet worden betaald volgens de voorwaarden van het beleid. |
| `location` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | De plaats waar de verzekeringspolis wordt uitgegeven. |
| `owner` | [!UICONTROL Object] | Hiermee legt u de profielgegevens van de verzekeringnemer vast. |
| `owner.faxPhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Het faxnummer van de eigenaar. |
| `owner.homeAddress` | [[!UICONTROL Postal address]](../data-types/postal-address.md) | Het huisadres van de eigenaar. |
| `owner.homePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Het thuistelefoonnummer van de eigenaar. |
| `owner.mobilePhone` | [[!UICONTROL Phone number]](../data-types/phone-number.md) | Het mobiele telefoonnummer van de eigenaar. |
| `owner.personalEmail` | [[!UICONTROL Email address]](../data-types/email-address.md) | Het persoonlijke e-mailadres van de eigenaar. |
| `ID` | [!UICONTROL String] | Een identificatiecode voor de verzekeringspolis. |
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br> Aangezien dit gebied systeem-geproduceerd is, wordt het geen expliciete waarde geleverd tijdens gegevensopname. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `endDate` | [!UICONTROL DateTime] | De datum waarop de dekking van de verzekeringspolis eindigt (of eindigt). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Geeft aan of aan het beleid een begunstigde is toegewezen. |
| `name` | [!UICONTROL String] | De naam van de verzekeringsovereenkomst. |
| `startDate` | [!UICONTROL DateTime] | De datum waarop de dekking van de verzekeringspolis begint (of is begonnen). |
| `type` | [!UICONTROL String] | Het type verzekeringspolis, zoals thuis, auto, binnenplaats of boot. |

{style="table-layout:auto"}
