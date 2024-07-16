---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: Afzonderlijke XDM-profielklasse
description: Meer informatie over de klasse XDM Individual Profile.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: ce937f1335283382189fa40f65aa268735c02715
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] -klasse

[!DNL XDM Individual Profile] is een standaard XDM-klasse (Experience Data Model) die een enkelvoudige representatie (of profiel) van een individuele persoon vormt. Specifiek, vangen de klasse (en zijn compatibele gebiedsgroepen) de attributen en de belangen van zowel geïdentificeerde als gedeeltelijk geïdentificeerde individuen die met uw merk in wisselwerking staan.

Profielen kunnen variëren van anonieme gedragssignalen (zoals browsercookies) tot sterk geïdentificeerde profielen met gedetailleerde informatie zoals naam, geboortedatum, locatie en e-mailadres. Naarmate een profiel groeit, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identiteiten, contactgegevens en communicatievoorkeuren voor een individu. Voor meer informatie op hoog niveau over het gebruik van deze klasse in het ecosysteem van het Platform, verwijs naar het [ XDM overzicht ](../home.md#data-behaviors).

![ het schemadiagram van A van de individuele klasse van het Profiel XDM.](../images/classes/individual-profile.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object dat de volgende [!UICONTROL DateTime] -velden bevat: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag is gemaakt, bijvoorbeeld wanneer de gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en tijd waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke tekenreeks-id voor de record. Dit veld wordt gebruikt om de uniciteit van een individueel record te volgen, om te voorkomen dat gegevens worden herhaald en om die record op te zoeken in downstreamservices. In sommige gevallen, `_id` kan a [ Universally Unique Identifier (UUID) ](https://tools.ietf.org/html/rfc4122) of [ globally Unieke Identifier (GUID) ](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) zijn.<br><br> als u gegevens van een bronverbinding stroomt of direct van een dossier van het Pakket inneemt, zou u deze waarde moeten produceren door een bepaalde combinatie gebieden aaneenschakelen die het verslag uniek maken, zoals primaire identiteitskaart, timestamp, verslagtype, etc. De samengevoegde waarde moet een tekenreeks met `uri-reference` opmaak zijn. Dit houdt in dat alle dubbele tekens moeten worden verwijderd. Daarna, zou de samengevoegde waarde moeten worden gehakt gebruikend SHA-256 of een ander algoritme van uw keus.<br><br> het is belangrijk om te onderscheiden dat **dit gebied geen identiteit met betrekking tot een individuele persoon** vertegenwoordigt, maar eerder het verslag van gegevens zelf. Identiteitsgegevens met betrekking tot een persoon zouden aan [ identiteitsgebieden ](../schema/composition.md#identity) moeten worden beperkt die door compatibele gebiedsgroepen in plaats daarvan worden verstrekt. |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `personID` | Een unieke id voor de individuele persoon waarop deze record betrekking heeft. Dit gebied vertegenwoordigt noodzakelijk geen identiteit met betrekking tot de persoon tenzij het ook als [ identiteitsgebied ](../schema/composition.md#identity) wordt aangewezen. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |

{style="table-layout:auto"}

## Compatibele veldgroepen {#field-groups}

>[!NOTE]
>
>De namen van verschillende veldgroepen zijn gewijzigd. Zie het document op [ de naamupdates van de gebiedsgroep ](../field-groups/name-updates.md) voor meer informatie.

Adobe biedt verschillende standaardveldgroepen voor gebruik met de [!DNL XDM Individual Profile] -klasse. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

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

*\*Deze gebiedsgroep is slechts beschikbaar aan organisaties met toegang tot B2B uitgave van Adobe Real-time Customer Data Platform.*

Voor een volledige lijst van alle compatibele gebiedsgroepen voor [!DNL XDM Individual Profile], verwijs naar [ XDM GitHub repo ](https://github.com/adobe/xdm/tree/master/components/fieldgroups/profile).
