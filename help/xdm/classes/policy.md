---
title: Beleidsklasse
description: Dit document verstrekt een overzicht van de klasse van het Beleid in het Model van de Gegevens van de Ervaring (XDM).
source-git-commit: c0437b8f9d93c46dbec991a33a893a5b9e0cdf2c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# [!UICONTROL Policy] class

In het Model van de Gegevens van de Ervaring (XDM), [!UICONTROL Policy] klasse legt de minimumreeks eigenschappen vast die een verzekeringspolis definiëren.

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
| `_id` | [!UICONTROL String] | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten.<br><br>Aangezien dit veld door het systeem wordt gegenereerd, wordt er geen expliciete waarde opgegeven tijdens het invoeren van gegevens. U kunt er echter desgewenst nog voor kiezen om uw eigen unieke id-waarden op te geven. |
| `endDate` | [!UICONTROL DateTime] | De datum waarop de dekking van de verzekeringspolis eindigt (of eindigt). |
| `hasAssignedBeneficiary` | [!UICONTROL Boolean] | Geeft aan of aan het beleid een begunstigde is toegewezen. |
| `name` | [!UICONTROL String] | De naam van de verzekeringspolis. |
| `startDate` | [!UICONTROL DateTime] | De datum waarop de dekking van de verzekeringspolis begint (of is begonnen). |
| `type` | [!UICONTROL String] | Het type verzekeringspolis, zoals thuis, auto, binnenplaats of boot. |

{style=&quot;table-layout:auto&quot;}
