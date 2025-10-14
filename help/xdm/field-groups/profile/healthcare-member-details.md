---
title: Gezondheidszorg Lid Details Schema Veldgroep
description: Meer informatie over de veldgroep Details schema van het lid in de gezondheidszorg.
exl-id: 43ba025e-2acf-4cb7-8487-e6c7c7240867
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# [!UICONTROL Healthcare Member Details] schemaveldgroep

[!UICONTROL Healthcare Member Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../classes/individual-profile.md) die details van een persoon vangt die medische dienst of zorg, zoals contactinformatie, primaire zorgarts, en planinformatie heeft of zal ontvangen.

![&#x200B; de groepsstructuur van het Gebied &#x200B;](../../images/field-groups/healthcare-member-details/structure.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `billingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het factuuradres van de persoon. |
| `faxPhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het faxnummer van de persoon. |
| `homeAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het thuisadres van de persoon. |
| `homePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het telefoonnummer van de persoon thuis. |
| `mailingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het postadres van de persoon. |
| `memberDetails` | Object | Een object dat gedetailleerde informatie bevat over de aan gezondheidszorg gerelateerde kenmerken en relaties van de persoon. Zie de [&#x200B; onderafdeling hieronder &#x200B;](#memberDetails) voor meer informatie over de structuur van de objecten. |
| `mobilePhone` | [[!UICONTROL Phone number]](../../data-types/phone-number.md) | Het mobiele telefoonnummer van de persoon. |
| `person` | [[!UICONTROL Person]](../../data-types/person.md) | Een individuele actor, contactpersoon of eigenaar in verband met het lidmaatschap van de gezondheidszorg van de persoon. |
| `personalEmail` | [[!UICONTROL Email address]](../../data-types/email-address.md) | Het persoonlijke e-mailadres van de persoon. |
| `shippingAddress` | [[!UICONTROL Postal address]](../../data-types/postal-address.md) | Het verzendadres van de persoon. |

{style="table-layout:auto"}

## `memberDetails` {#memberDetails}

`memberDetails` is een object dat gedetailleerde informatie bevat over de kenmerken en relaties van de persoon in de gezondheidszorg. De structuur van `memberDetails` wordt hieronder beschreven.

![&#x200B; memberDetails structuur &#x200B;](../../images/field-groups/healthcare-member-details/memberDetails.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `emergencyContact` | Object | Vangt de volgende noodcontactgegevens voor de persoon: <ul><li>`fullName`: (Tekenreeks) De volledige naam van de contactpersoon voor noodgevallen.</li><li>`phone`: (Koord) het telefoonaantal voor het noodcontact.</li><li>`relationshipToMember`: (Tekenreeks) De relatie van het noodcontact met de persoon.</li></ul> |
| `medications` | Array van objecten | Hier worden de details weergegeven van de huidige en vroegere medicatie die aan de persoon is gerelateerd. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`refillLocation`: ([[!UICONTROL Postal address]](../../data-types/postal-address.md)) De navullocatie voor de medicatie.</li><li>`ID`: (String) Medication ID.</li><li>`isCurrent`: (Boolean) Geeft aan of de medicatie actief of ouder is.</li><li>`numberOfRefills`: (Geheel getal) Het aantal vullingen dat door de leverancier van deze medicatie wordt voorgeschreven.</li><li>`startDate`: (DateTime) De datum waarop de persoon de medicatie begon in te nemen.</li></ul> |
| `multipleBirth` | Object | Gegevens over meerlinggeboorten vastleggen: <ul><li>`isMultipleBirth`: (Boolean) Geeft aan of de persoon meerdere geboorten heeft gegeven.</li><li>`multipleBirthNumber`: (Geheel getal) Het aantal geboren baby&#39;s als `isMultipleBirth` true is.</li></ul> |
| `plans` | Array van objecten | Hier worden de details weergegeven van de huidige en eerdere medische plannen die bij de persoon horen. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`coverageEndDate`: (DateTime) De datum waarop de dekking van het abonnement eindigt.</li><li>`coverageStartDate`: (DateTime) De datum waarop de dekking van het abonnement begint.</li><li>`isActive`: (Boolean) Geeft aan of het abonnement actief is.</li><li>`planId`: (Tekenreeks) De plan-id.</li></ul> |
| `primaryCarePhysicians` | Array van objecten | Hier worden de gegevens weergegeven van artsen in de eerstelijnszorg die bij de persoon horen. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`endDate`: (DateTime) De datum waarop de eerstelijnsarts de zorg voor de persoon beëindigde.</li><li>`fullname`: (String) De volledige naam van de arts.</li><li>`providerId`: (Tekenreeks) Een unieke id voor de arts.</li><li>`startDate`: (DateTime) De datum waarop de eerstelijnsarts de zorg voor de persoon is begonnen.</li></ul> |
| `specialists` | Array van objecten | Hier worden de gegevens weergegeven van specialisten in de gezondheidszorg die bij de persoon horen. Elk arrayitem is een object dat de volgende details vastlegt: <ul><li>`fullname`: (String) De volledige naam van de specialist.</li><li>`providerId`: (Tekenreeks) Een unieke id voor de specialist.</li><li>`specialty`: (String) De specialiteit van de provider (zoals anesthesiologie, urologie, radiologie, dermatologie, enzovoort).</li></ul> |
| `beneficiaryRelationship` | String | De relatie van de begunstigde met het lid van de gezondheidszorg als de persoon ten laste komt (voorbeelden zijn onder meer: zelf, echtgenoot, kind, enzovoort). |
| `billingAccountID` | String | Een unieke id voor de factureringsaccount van de persoon. |
| `dateAgeCollected` | DateTime | De datum waarop de leeftijd van de persoon is verzameld. |
| `deceasedDate` | DateTime | De datum waarop de persoon overleden is. |
| `isDeceased` | Boolean | Geeft aan of de persoon overleden is. |
| `isDependent` | Boolean | Geeft aan of de persoon afhankelijk is. |
| `nationality` | String | De juridische relatie tussen de persoon en zijn staat, vertegenwoordigd door middel van de ISO 3166-1 Alpha-2 code. |
| `preferredAvailability` | String | De voorkeursdag en -tijd van de persoon voor een afspraak. |
| `primaryMemberID` | String | Een unieke id van de primaire abonnee als de persoon afhankelijk is. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-healthcare-member.schema.json)

Verwijs naar de documentatie van het industrieschema voor meer informatie over hoe deze gebiedsgroep kan worden gebruikt om gemeenschappelijke [&#x200B; het gebruiksgevallen van de gezondheidszorgindustrie te dienen &#x200B;](../../schema/industries/healthcare.md).
