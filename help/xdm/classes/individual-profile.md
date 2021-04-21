---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;Identiteitskaart;Identiteitskaart;Het ontwerp van het schema;Kaart;Verenigingsschema;Vereniging
solution: Experience Platform
title: Afzonderlijke XDM-profielklasse
topic-legacy: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
exl-id: 83b22462-79ce-4024-aa50-a9bd800c0f81
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 0%

---

# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] is een standaard XDM-klasse die een enkelvoudige representatie (of &quot;profiel&quot;) vormt van de kenmerken en belangen van zowel geïdentificeerde als gedeeltelijk geïdentificeerde personen.

Profielen kunnen variëren van anonieme gedragssignalen (zoals browsercookies) tot sterk geïdentificeerde profielen met gedetailleerde informatie zoals naam, geboortedatum, locatie en e-mailadres. Naarmate een profiel groeit, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identiteiten, contactgegevens en communicatievoorkeuren voor een individu. Voor meer informatie op hoog niveau over het gebruik van deze klasse in het Platform ecosysteem, verwijs naar [XDM overzicht](../home.md#data-behaviors).

De [!DNL XDM Individual Profile] klasse zelf verstrekt verscheidene systeem-geproduceerde waarden die automatisch bevolkt zijn wanneer het gegeven wordt opgenomen, terwijl alle andere gebieden door het gebruik van [compatibele mengen](#mixins) moeten worden toegevoegd:

![](../images/classes/individual-profile.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object met de volgende velden [!UICONTROL DateTime]: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag werd gemaakt, bijvoorbeeld wanneer gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en het tijdstip waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten. Aangezien dit veld door het systeem wordt gegenereerd, mag er tijdens het invoeren van gegevens geen expliciete waarde worden opgegeven.<br><br>Het is belangrijk te onderscheiden dat dit veld  **geen identiteit** bevat die verband houdt met een individuele persoon, maar eerder met de gegevens zelf. Identiteitsgegevens die betrekking hebben op een persoon moeten in plaats daarvan worden beperkt tot [identiteitsvelden](../schema/composition.md#identity). |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |

## Compatibele combinaties {#mixins}

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../mixins/name-updates.md) voor meer informatie.

Adobe biedt verschillende standaardmixen voor gebruik met de klasse [!DNL XDM Individual Profile]. Hieronder volgt een lijst met de meestgebruikte mixen voor de klasse:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demographic Details]](../mixins/profile/person-details.md)
* [[!UICONTROL Personal Contact Details]](../mixins/profile/personal-details.md)
* [[!UICONTROL Work Contact Details]](../mixins/profile/work-details.md)
* [[!UICONTROL Segment Membership Details]](../mixins/profile/segmentation.md)
