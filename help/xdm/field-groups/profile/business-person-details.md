---
title: XDM Business Person Details-schemaveldgroep
description: Meer informatie over de XDM Business Person Details schema veldgroep.
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 0%

---

# [!UICONTROL XDM Business Person Details] schemaveldgroep

[!UICONTROL XDM Business Person Details] is een standaardschemagebiedgroep voor [[!DNL XDM Individual Profile] class](../../classes/individual-profile.md) die informatie over een individuele persoon opneemt in het kader van een business-to-business (B2B)-onderneming.

![](../../images/field-groups/business-person-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `b2b` | Object | Een object dat de B2B-specifieke gegevens over de persoon vastlegt. |
| `b2b.accountKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde identificatiecode voor de zakelijke rekening die met de persoon verband houdt. |
| `b2b.convertedContactKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de bijbehorende contactpersoon als de lead is omgezet. |
| `b2b.personKey` | [[!UICONTROL B2B Source]](../../data-types/b2b-source.md) | Een samengestelde id voor de persoon of het profielfragment. |
| `b2b.accountID` | String | Een unieke id voor de zakelijke account waaraan deze persoon is gekoppeld. |
| `b2b.blockedCause` | String | Als de persoon wordt geblokkeerd, verstrekt dit bezit de reden waarom. |
| `b2b.convertedContactID` | String | De contact-id als de lead is omgezet. |
| `b2b.convertedDate` | DateTime | De conversiedatum als de lead is geconverteerd. |
| `b2b.isBlocked` | Boolean | Geeft aan of de persoon is geblokkeerd. |
| `b2b.isConverted` | Boolean | Geeft aan of de lead wordt geconverteerd. |
| `b2b.isMarketingSuspended` | Boolean | Geeft aan of het op de markt brengen is opgeschort voor de persoon. |
| `b2b.marketingSuspendedCause` | String | Als het op de markt brengen voor de persoon wordt opgeschort, verstrekt dit bezit de reden waarom. |
| `b2b.personGroupID` | String | Een groepsidentificatie voor de persoon. |
| `b2b.personScore` | Dubbel | Een score die door een CRM-systeem voor de persoon wordt gegenereerd. |
| `b2b.personSource` | String | De bron waarvan de informatie van de persoon is ontvangen. |
| `b2b.personStatus` | String | De huidige handels- of verkoopstatus van de persoon. |
| `b2b.personType` | String | Het type B2B-persoon. |
| `extSourceSystemAudit` | [Kenmerken externe bronsysteemcontrole](../../data-types/external-source-system-audit-attributes.md) | Als de relatie met de ondernemer uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `extendedWorkDetails` | Object | Hiermee legt u aanvullende gegevens over de persoon vast die betrekking hebben op het werk. |
| `extendedWorkDetails.assistantDetails` | Object | Vangt de volgende attributen met betrekking tot de medewerker van de persoon: <ul><li>`name`: ([Naam persoon](../../data-types/person-name.md)) De volledige naam van de assistent.</li><li>`phone`: ([Telefoonnummer](../../data-types/phone-number.md)) Het telefoonnummer van de assistent.</li></ul> |
| `extendedWorkDetails.departments` | Array van tekenreeksen | Een lijst met afdelingsnamen waar de persoon werkt. |
| `extendedWorkDetails.jobTitle` | String | De functie van de persoon. |
| `extendedWorkDetails.photoUrl` | String | Een URL naar een foto van de persoon. |
| `extendedWorkDetails.reportsToID` | String | Een id voor de rapportageleider van de persoon. |
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
| `identityMap` | Kaart | Een kaartveld dat een set naamloze identiteiten voor de persoon bevat. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Voor een juist gebruik van dit veld voor [Klantprofiel in realtime](../../../profile/home.md)Probeer niet handmatig de inhoud van het veld bij te werken in uw gegevensbewerkingen.<br /><br />Zie de sectie over identiteitskaarten in het dialoogvenster [grondbeginselen van de schemacompositie](../../schema/composition.md#identityMap) voor meer informatie over het gebruik ervan . |
| `isDeleted` | Boolean | Geeft aan of deze persoon in het Marketo Engage is verwijderd.<br><br>Wanneer u de opdracht [Marketo-bronaansluiting](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden alle records die in Marketo worden verwijderd, automatisch weergegeven in Real-Time klantprofiel. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door in te stellen `isDeleted` tot `true`, kunt u het gebied gebruiken om uit te filteren welke verslagen uit uw bronnen zijn geschrapt wanneer het vragen van het meer van Gegevens. |
| `organizations` | Array van tekenreeksen | Een lijst van organisatienamen waar de persoon werkt. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
