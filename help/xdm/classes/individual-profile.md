---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: Afzonderlijke XDM-profielklasse
topic-legacy: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] is een standaard XDM-klasse (Experience Data Model) die een enkelvoudige representatie (of &quot;profiel&quot;) van een individuele persoon vormt. Specifiek, vangen de klasse (en zijn compatibele gebiedsgroepen) de attributen en de belangen van zowel geïdentificeerde als gedeeltelijk geïdentificeerde individuen die met uw merk in wisselwerking staan.

Profielen kunnen variëren van anonieme gedragssignalen (zoals browsercookies) tot sterk geïdentificeerde profielen met gedetailleerde informatie zoals naam, geboortedatum, locatie en e-mailadres. Naarmate een profiel groeit, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identiteiten, contactgegevens en communicatievoorkeuren voor een individu. Raadpleeg voor meer informatie op hoog niveau over het gebruik van deze klasse in het ecosysteem van het Platform de [XDM-overzicht](../home.md#data-behaviors).

De [!DNL XDM Individual Profile] -klasse zelf biedt meerdere door het systeem gegenereerde waarden die automatisch worden ingevuld wanneer gegevens worden ingevoerd, terwijl alle andere velden moeten worden toegevoegd door het gebruik van [compatibele groepen schemavelden](#field-groups):

![](../images/classes/individual-profile.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object dat het volgende bevat [!UICONTROL DateTime] velden: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag werd gemaakt, bijvoorbeeld wanneer gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en het tijdstip waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke tekenreeks-id voor de record. Dit veld wordt gebruikt om de uniciteit van een individueel record te volgen, om te voorkomen dat gegevens worden herhaald en om die record op te zoeken in downstreamservices. In sommige gevallen `_id` kan [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) of [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0).<br><br>Als u gegevens streamt vanuit een bronverbinding of rechtstreeks vanuit een Parquet-bestand opgeeft, moet u deze waarde genereren door een bepaalde combinatie van velden samen te voegen die de record uniek maken, zoals een primaire id, tijdstempel, recordtype, enzovoort. De samengevoegde waarde moet een `uri-reference` geformatteerde tekenreeks: eventuele dubbele tekens moeten worden verwijderd. Daarna, zou de samengevoegde waarde moeten worden gehakt gebruikend SHA-256 of een ander algoritme van uw keus.<br><br>Het is van belang te onderscheiden dat **dit veld vertegenwoordigt geen identiteit die betrekking heeft op een individuele persoon**, maar eerder de gegevensregistratie zelf. Identiteitsgegevens betreffende een persoon moeten worden beperkt tot [identiteitsvelden](../schema/composition.md#identity) in plaats daarvan worden verstrekt door compatibele veldgroepen. |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `personID` | Een unieke id voor de individuele persoon waarop deze record betrekking heeft. Dit veld vertegenwoordigt niet noodzakelijkerwijs een identiteit die betrekking heeft op de persoon, tenzij het ook als een [identiteitsveld](../schema/composition.md#identity). |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |

{style=&quot;table-layout:auto&quot;}

## Compatibele veldgroepen {#field-groups}

>[!NOTE]
>
>De namen van verschillende veldgroepen zijn gewijzigd. Document weergeven op [veldgroepnaapupdates](../field-groups/name-updates.md) voor meer informatie .

Adobe biedt verschillende standaardveldgroepen voor gebruik met de [!DNL XDM Individual Profile] klasse. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

* [[!UICONTROL Consents and Preferences]](../field-groups/profile/consents.md)
* [[!UICONTROL Demographic Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Loyalty Details]](../field-groups/profile/loyalty-details.md)
* [[!UICONTROL Personal Contact Details]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Segment Membership Details]](../field-groups/profile/segmentation.md)
* [[!UICONTROL Telecom Subscription]](../field-groups/profile/telecom-subscription.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL XDM Business Person Components]](../field-groups/profile/business-person-components.md)\*
* [[!UICONTROL XDM Business Person Details]](../field-groups/profile/business-person-details.md)\*

*\*Deze veldgroep is alleen beschikbaar voor organisaties met toegang tot de B2B-editie van Adobe Real-time Customer Data Platform.*

Voor een volledige lijst van alle compatibele gebiedsgroepen voor [!DNL XDM Individual Profile], verwijst u naar de [XDM GitHub-repo](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
