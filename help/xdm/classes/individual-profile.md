---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: Afzonderlijke XDM-profielklasse
topic-legacy: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
source-git-commit: eddaa7090af2d2c947f154272bb219dc2e3bca08
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] is een standaard XDM-klasse (Experience Data Model) die een enkelvoudige representatie (of &quot;profiel&quot;) van een individuele persoon vormt. Met name worden in de klasse (en de compatibele mixen) de kenmerken en belangen vastgelegd van zowel geïdentificeerde als gedeeltelijk geïdentificeerde personen die met uw merk communiceren.

Profielen kunnen variëren van anonieme gedragssignalen (zoals browsercookies) tot sterk geïdentificeerde profielen met gedetailleerde informatie zoals naam, geboortedatum, locatie en e-mailadres. Naarmate een profiel groeit, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identiteiten, contactgegevens en communicatievoorkeuren voor een individu. Voor meer informatie op hoog niveau over het gebruik van deze klasse in het Platform ecosysteem, verwijs naar [XDM overzicht](../home.md#data-behaviors).

De [!DNL XDM Individual Profile] klasse zelf verstrekt verscheidene systeem-geproduceerde waarden die automatisch bevolkt zijn wanneer het gegeven wordt opgenomen, terwijl alle andere gebieden door het gebruik van [compatibele groepen van het schemagebied](#field-groups) moeten worden toegevoegd:

![](../images/classes/individual-profile.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object met de volgende velden [!UICONTROL DateTime]: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag werd gemaakt, bijvoorbeeld wanneer gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en het tijdstip waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke tekenreeks-id voor de record. Dit veld wordt gebruikt om de uniciteit van een individueel record te volgen, om te voorkomen dat gegevens worden herhaald en om die record op te zoeken in downstreamservices. In sommige gevallen kan `_id` een [Universally Unique Identifier (UUID)](https://tools.ietf.org/html/rfc4122) of [Globally Unique Identifier (GUID)](https://docs.microsoft.com/en-us/dotnet/api/system.guid?view=net-5.0) zijn.<br><br>Als u gegevens streamt vanuit een bronverbinding of rechtstreeks vanuit een Parquet-bestand opgeeft, moet u deze waarde genereren door een bepaalde combinatie van velden samen te voegen die de record uniek maken, zoals een primaire id, tijdstempel, recordtype, enzovoort. De samengevoegde waarde moet een tekenreeks met de indeling `uri-reference` zijn. Dit houdt in dat alle dubbele tekens moeten worden verwijderd. Daarna, zou de samengevoegde waarde moeten worden gehakt gebruikend SHA-256 of een ander algoritme van uw keus.<br><br>Het is belangrijk om te onderscheiden dat  **dit veld geen identiteit vertegenwoordigt die verband houdt met een individuele persoon**, maar eerder de registratie van gegevens zelf. Identiteitsgegevens die betrekking hebben op een persoon moeten worden overgebracht naar [identiteitsvelden](../schema/composition.md#identity) die in plaats daarvan door compatibele veldgroepen worden verschaft. |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `personID` | Een unieke id voor de individuele persoon waarop deze record betrekking heeft. Dit veld vertegenwoordigt niet noodzakelijkerwijs een identiteit die betrekking heeft op de persoon, tenzij het ook wordt aangeduid als een [identiteitsveld](../schema/composition.md#identity). |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |

{style=&quot;table-layout:auto&quot;}

## Compatibele veldgroepen {#field-groups}

>[!NOTE]
>
>De namen van verschillende veldgroepen zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../field-groups/name-updates.md) voor meer informatie.

Adobe biedt verschillende standaardveldgroepen voor gebruik met de klasse [!DNL XDM Individual Profile]. Hieronder volgt een lijst met enkele veelgebruikte veldgroepen voor de klasse:

* [[!UICONTROL IdentityMap]](../field-groups/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../field-groups/profile/demographic-details.md)
* [[!UICONTROL Personal Contact Details]](../field-groups/profile/personal-contact-details.md)
* [[!UICONTROL Work Contact Details]](../field-groups/profile/work-contact-details.md)
* [[!UICONTROL Segment Membership Details]](../field-groups/profile/segmentation.md)

Voor een volledige lijst van alle compatibele gebiedsgroepen voor [!DNL XDM Individual Profile], verwijs naar [XDM GitHub repo](https://github.com/adobe/xdm/tree/master/components/mixins/profile).
