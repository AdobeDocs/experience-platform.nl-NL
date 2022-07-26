---
title: Gezondheidszorg Lid Details Schema Veldgroep
description: Dit document biedt een overzicht van de veldgroep Details schema van het zorglid.
source-git-commit: a51079ff1686ecae3e5fe9f0170b28bc16bcef86
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 1%

---

# [!UICONTROL Healthcare Member Details] schemaveldgroep

[!UICONTROL Healthcare Member Details] is een standaardschemagebiedgroep voor [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) die gegevens vastlegt van een persoon die een medische dienst of zorg heeft of zal ontvangen, zoals contactinformatie, eerstelijnsarts en planningsinformatie.

![Groepsstructuur van veld](../../images/field-groups/healthcare-member-details/structure.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het factuuradres van de persoon. |
| `faxPhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het faxnummer van de persoon. |
| `homeAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het thuisadres van de persoon. |
| `homePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het telefoonnummer van de persoon thuis. |
| `mailingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het postadres van de persoon. |
| `memberDetails` | Object | Een object dat gedetailleerde informatie bevat over de aan gezondheidszorg gerelateerde kenmerken en relaties van de persoon. Zie de [onderafdeling](#memberDetails) voor meer informatie over de structuur van het object. |
| `mobilePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het mobiele telefoonnummer van de persoon. |
| `person` | [[!UICONTROL Person]](../../data-types/person.md) | Een individuele actor, contactpersoon of eigenaar in verband met het lidmaatschap van de gezondheidszorg van de persoon. |
| `personalEmail` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Het persoonlijke e-mailadres van de persoon. |
| `shippingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het verzendadres van de persoon. |

{style=&quot;table-layout:auto&quot;}

## `memberDetails` {#memberDetails}

`memberDetails` is een object dat gedetailleerde informatie bevat over de gezondheidsgerelateerde kenmerken en relaties van de persoon. De structuur van `memberDetails` wordt hieronder beschreven.

![memberDetails-structuur](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `emergencyContact` | Object | Vangt de volgende noodcontactgegevens voor de persoon: <ul><li>`fullName`: (Tekenreeks) De volledige naam van de contactpersoon voor noodgevallen.</li><li>`phone`: (Tekenreeks) Het telefoonnummer voor de contactpersoon voor noodgevallen.</li><li>`relationshipToMember`: (Tekenreeks) De relatie van het noodcontact met de persoon.</li></ul> |
| `medications` | Array van objecten | Hier worden de details weergegeven van de huidige en vroegere medicatie die aan de persoon is gerelateerd. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`refillLocation`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)) De navullocatie voor het geneesmiddel.</li><li>`ID`: (String) Medication ID.</li><li>`isCurrent`: (Boolean) Geeft aan of de medicatie actueel of verleden is.</li><li>`numberOfRefills`: (Geheel getal) Het aantal vullingen dat door de leverancier van dit geneesmiddel wordt voorgeschreven.</li><li>`startDate`: (DateTime) De datum waarop de persoon de medicatie begon in te nemen.</li></ul> |
| `multipleBirth` | Object | Gegevens over meerlinggeboorten vastleggen: <ul><li>`isMultipleBirth`: (Boolean) Geeft aan of de persoon meerdere geboorten heeft gegeven.</li><li>`multipleBirthNumber`: (Geheel getal) Het aantal geboren baby&#39;s als `isMultipleBirth` is waar.</li></ul> |
| `plans` | Array van objecten | Hier worden de details weergegeven van de huidige en eerdere medische plannen die bij de persoon horen. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`coverageEndDate`: (DateTime) De datum waarop de dekking van de regeling eindigt.</li><li>`coverageStartDate`: (DateTime) De datum waarop de dekking van het plan begint.</li><li>`isActive`: (Boolean) Geeft aan of het abonnement actief is.</li><li>`planId`: (Tekenreeks) De plan-id.</li></ul> |
| `primaryCarePhysicians` | Array van objecten | Hier worden de gegevens weergegeven van artsen in de eerstelijnszorg die bij de persoon horen. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`endDate`: (DateTime) De datum waarop de eerstelijnsarts de zorg voor de persoon beëindigde.</li><li>`fullname`: (String) De volledige naam van de arts.</li><li>`providerId`: (Tekenreeks) Een unieke id voor de arts.</li><li>`startDate`: (DateTime) De datum waarop de eerstelijnsarts de zorg voor de persoon begon.</li></ul> |
| `specialists` | Array van objecten | Hier worden de gegevens weergegeven van specialisten in de gezondheidszorg die bij de persoon horen. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`fullname`: (String) De volledige naam van de specialist.</li><li>`providerId`: (Tekenreeks) Een unieke id voor de specialist.</li><li>`specialty`: (String) Het specialisme van de provider (zoals anesthesiologie, urologie, radiologie, dermatologie, enzovoort).</li></ul> |
| `beneficiaryRelationship` | Tekenreeks | De relatie van de begunstigde met het lid van de gezondheidszorg als de persoon ten laste komt (voorbeelden zijn onder meer: zelf, echtgenoot, kind, enzovoort). |
| `billingAccountID` | Tekenreeks | Een unieke id voor de factureringsaccount van de persoon. |
| `dateAgeCollected` | DateTime | De datum waarop de leeftijd van de persoon is verzameld. |
| `deceasedDate` | DateTime | De datum waarop de persoon overleden is. |
| `isDeceased` | Boolean | Geeft aan of de persoon overleden is. |
| `isDependent` | Boolean | Geeft aan of de persoon afhankelijk is. |
| `nationality` | Tekenreeks | De juridische relatie tussen de persoon en zijn staat, vertegenwoordigd door middel van de ISO 3166-1 Alpha-2 code. |
| `preferredAvailability` | Tekenreeks | De voorkeursdag en -tijd van de persoon voor een afspraak. |
| `primaryMemberID` | Tekenreeks | Een unieke id van de primaire abonnee als de persoon afhankelijk is. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Raadpleeg de documentatie bij het industrieschema voor meer informatie over hoe deze veldgroep kan worden gebruikt om algemene informatie te gebruiken [zorgindustrie](../../schema/industries/healthcare.md).
