---
title: XDM Business Person Details-schemaveldgroep
description: Meer informatie over de XDM Business Person Details schema veldgroep.
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html#rtcdp-editions" newtab=true
exl-id: e9da5c1c-5a30-4cbc-beb2-cc5efe57cab0
source-git-commit: 3fafccef44823b80938db96a7751edbff5a2fd02
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# [!UICONTROL XDM Business Person Details] schemaveldgroep

>[!AVAILABILITY]
>
>Deze veldgroep is alleen beschikbaar voor organisaties die toegang hebben tot de Real-Time CDP B2B edition.

[!UICONTROL XDM Business Person Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse &#x200B;](../../classes/individual-profile.md) die informatie over een individuele persoon in de context van een zaken-aan-zaken (B2B) onderneming vangt.

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
| `extSourceSystemAudit` | [&#x200B; Externe Attributen van de Controle van het Systeem van Source &#x200B;](../../data-types/external-source-system-audit-attributes.md) | Als de relatie met de ondernemer uit een extern bronsysteem komt, vangt dit voorwerp controleattributen voor dat systeem. |
| `extendedWorkDetails` | Object | Hiermee legt u aanvullende gegevens over de persoon vast die betrekking hebben op het werk. |
| `extendedWorkDetails.assistantDetails` | Object | Vangt de volgende attributen met betrekking tot de medewerker van de persoon: <ul><li>`name`: ([&#x200B; Naam van de Persoon &#x200B;](../../data-types/person-name.md)) de volledige naam van de medewerker.</li><li>`phone`: ([&#x200B; aantal van de Telefoon &#x200B;](../../data-types/phone-number.md)) het de telefoonaantal van de medewerker.</li></ul> |
| `extendedWorkDetails.departments` | Array van tekenreeksen | Een lijst met afdelingsnamen waar de persoon werkt. |
| `extendedWorkDetails.jobTitle` | String | De functie van de persoon. |
| `extendedWorkDetails.photoUrl` | String | Een URL naar een foto van de persoon. |
| `extendedWorkDetails.reportsToID` | String | Een id voor de rapportageleider van de persoon. |
| `faxPhone` | [&#x200B; Aantal van de Telefoon &#x200B;](../../data-types/phone-number.md) | Het faxnummer van de persoon. |
| `homeAddress` | [&#x200B; Postadres &#x200B;](../../data-types/postal-address.md) | Het thuisadres van de persoon. |
| `homePhone` | [&#x200B; Aantal van de Telefoon &#x200B;](../../data-types/phone-number.md) | Het telefoonnummer van de persoon thuis. |
| `mobilePhone` | [&#x200B; Aantal van de Telefoon &#x200B;](../../data-types/phone-number.md) | Het mobiele telefoonnummer van de persoon. |
| `otherAddress` | [&#x200B; Postadres &#x200B;](../../data-types/postal-address.md) | Een alternatief adres voor de persoon. |
| `otherPhone` | [&#x200B; Aantal van de Telefoon &#x200B;](../../data-types/phone-number.md) | Een alternatief telefoonnummer voor de persoon. |
| `person` | [&#x200B; Persoon &#x200B;](../../data-types/person.md) | Een individuele actor, contactpersoon of eigenaar. |
| `personalEmail` | [&#x200B; E-mailadres &#x200B;](../../data-types/email-address.md) | Het persoonlijke e-mailadres van de persoon. |
| `workAddress` | [&#x200B; Postadres &#x200B;](../../data-types/postal-address.md) | Het werkadres van de persoon. |
| `workEmail` | [&#x200B; E-mailadres &#x200B;](../../data-types/email-address.md) | Het e-mailadres van het werk van de persoon. |
| `workPhone` | [&#x200B; Aantal van de Telefoon &#x200B;](../../data-types/phone-number.md) | Het telefoonnummer van het werktelefoonnummer van de persoon. |
| `identityMap` | Kaart | Een kaartveld dat een set naamloze identiteiten voor de persoon bevat. Dit veld wordt automatisch door het systeem bijgewerkt wanneer er identiteitsgegevens worden ingevoerd. Om dit gebied voor [&#x200B; Real-Time Profiel van de Klant &#x200B;](../../../profile/home.md) behoorlijk te gebruiken, probeer niet manueel om de inhoud van het gebied in uw gegevensverrichtingen bij te werken.<br /><br /> zie de sectie over identiteitskaarten in de [&#x200B; grondbeginselen van schemacompositie &#x200B;](../../schema/composition.md#identityMap) voor meer informatie over hun gebruiksgeval. |
| `isDeleted` | Boolean | Geeft aan of deze persoon is verwijderd in Marketo Engage.<br><br> wanneer het gebruiken van de [&#x200B; Marketo bronschakelaar &#x200B;](../../../sources/connectors/adobe-applications/marketo/marketo.md), worden om het even welke verslagen die in Marketo worden geschrapt automatisch weerspiegeld in Real-Time Profiel van de Klant. In het Data Lake kunnen echter nog steeds gegevens over deze profielen worden bewaard. Door `isDeleted` in te stellen op `true` , kunt u het veld gebruiken om uit te filteren welke records uit uw bronnen zijn verwijderd wanneer u een query uitvoert op het gegevensmeer. |
| `organizations` | Array van tekenreeksen | Een lijst van organisatienamen waar de persoon werkt. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/b2b-person-details.schema.json)
