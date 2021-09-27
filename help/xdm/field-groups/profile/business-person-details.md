---
title: XDM Business Person Details-schemaveldgroep
description: Dit document biedt een overzicht van de XDM Business Person Details schema veldgroep.
source-git-commit: 319d508925d22e76a3d75ae473f6ea000b5c655b
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 2%

---


# [!UICONTROL XDM Business Person Details] schemaveldgroep

>[!NOTE]
>
>Deze veldgroep is alleen beschikbaar voor organisaties die toegang hebben tot de B2B-editie van Real-time Customer Data Platform.

[!UICONTROL XDM Business Person Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klasse die informatie over een individuele persoon in de context van een zaken-aan-zaken (B2B) onderneming vangt.

![](../../images/field-groups/business-person-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `b2b` | Object | Een object dat de B2B-specifieke gegevens over de persoon vastlegt. |
| `b2b.accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificatiecode voor de zakelijke rekening die met de persoon verband houdt. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de bijbehorende contactpersoon als de lead is omgezet. |
| `b2b.personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon of het profielfragment. |
| `b2b.accountID` | Tekenreeks | Een unieke id voor de zakelijke account waaraan deze persoon is gekoppeld. |
| `b2b.blockedCause` | Tekenreeks | Als de persoon wordt geblokkeerd, verstrekt dit bezit de reden waarom. |
| `b2b.convertedContactID` | Tekenreeks | De contact-id als de lead is geconverteerd. |
| `b2b.convertedDate` | DateTime | De conversiedatum als de lead is geconverteerd. |
| `b2b.isBlocked` | Boolean | Geeft aan of de persoon is geblokkeerd. |
| `b2b.isConverted` | Boolean | Geeft aan of de lead wordt geconverteerd. |
| `b2b.isMarketingSuspended` | Boolean | Geeft aan of het op de markt brengen is opgeschort voor de persoon. |
| `b2b.marketingSuspendedCause` | Tekenreeks | Als het op de markt brengen voor de persoon wordt opgeschort, verstrekt dit bezit de reden waarom. |
| `b2b.personGroupID` | Tekenreeks | Een groepsidentificatie voor de persoon. |
| `b2b.personScore` | Dubbel | Een score die door een CRM-systeem voor de persoon wordt gegenereerd. |
| `b2b.personSource` | Tekenreeks | De bron waarvan de informatie van de persoon is ontvangen. |
| `b2b.personStatus` | Tekenreeks | De huidige handels- of verkoopstatus van de persoon. |
| `b2b.personType` | Tekenreeks | Het type B2B-persoon. |
| `extSourceSystemAudit` | [Kenmerken externe bronsysteemcontrole](../../data-types/external-source-system-audit-attributes.md) | Als de relatie met de ondernemer uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `extendedWorkDetails` | Object | Hiermee legt u aanvullende gegevens over de persoon vast die betrekking hebben op het werk. |
| `extendedWorkDetails.assistantDetails` | Object | Vangt de volgende attributen met betrekking tot de medewerker van de persoon: <ul><li>`name`: (Naam [persoon](../../data-types/person-name.md)) De volledige naam van de medewerker.</li><li>`phone`: ([Telefoonnummer](../../data-types/phone-number.md)) Het telefoonnummer van de medewerker.</li></ul> |
| `extendedWorkDetails.departments` | Array van tekenreeksen | Een lijst met afdelingsnamen waar de persoon werkt. |
| `extendedWorkDetails.jobTitle` | Tekenreeks | De functie van de persoon. |
| `extendedWorkDetails.photoUrl` | Tekenreeks | Een URL naar een foto van de persoon. |
| `extendedWorkDetails.reportsToID` | Tekenreeks | Een id voor de rapportageleider van de persoon. |
| `faxPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Het faxnummer van de persoon. |
| `homeAddress` | [Postadres](../../data-types/postal-address.md) | Het thuisadres van de persoon. |
| `homePhone` | [Telefoonnummer](../../data-types/phone-number.md) | Het telefoonnummer van de persoon thuis. |
| `mobilePhone` | [Telefoonnummer](../../data-types/phone-number.md) | Het mobiele telefoonnummer van de persoon. |
| `otherAddress` | [Postadres](../../data-types/postal-address.md) | Een alternatief adres voor de persoon. |
| `otherPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Een alternatief telefoonnummer voor de persoon. |
| `person` | [Persoon](../../data-types/person.md) | Een individuele actor, contactpersoon of eigenaar. |
| `personalEmail` | [E-mailadres](../../data-types/email-address.md) | Het persoonlijke e-mailadres van de persoon. |
| `workAddress` | [Postadres](../../data-types/postal-address.md) | Het werkadres van de persoon. |
| `workEmail` | [E-mailadres](../../data-types/email-address.md) | Het e-mailadres van het werk van de persoon. |
| `workPhone` | [Telefoonnummer](../../data-types/phone-number.md) | Het telefoonnummer van het werktelefoonnummer van de persoon. |
| `identityMap` | Kaart | Een kaartveld dat een set naamloze identiteiten voor de persoon bevat. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Als u dit veld correct wilt gebruiken voor [Real-time klantprofiel](../../../profile/home.md), moet u niet handmatig de inhoud van het veld bijwerken in uw gegevensbewerkingen.<br /><br />Zie de sectie over identiteitskaarten in de  [grondbeginselen van schemacompositie voor meer informatie ](../../schema/composition.md#identityMap) over hun gebruiksgeval. |
| `organizations` | Array van tekenreeksen | Een lijst van organisatienamen waar de persoon werkt. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
