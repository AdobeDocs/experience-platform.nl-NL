---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;identityMap;identity map;Identity map;Schema design;map;Map;union schema;union
solution: Experience Platform
title: Afzonderlijke XDM-profielklasse
topic: overview
description: Dit document biedt een overzicht van de klasse Individueel profiel XDM.
translation-type: tm+mt
source-git-commit: f9d8021643e72e3fbb5315b54a19815dcdaaa702
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---


# [!DNL XDM Individual Profile] class

[!DNL XDM Individual Profile] is een standaard XDM-klasse die een enkelvoudige representatie (of &quot;profiel&quot;) vormt van de kenmerken en belangen van zowel geïdentificeerde als gedeeltelijk geïdentificeerde personen.

Profielen kunnen variëren van anonieme gedragssignalen (zoals browsercookies) tot sterk geïdentificeerde profielen met gedetailleerde informatie zoals naam, geboortedatum, locatie en e-mailadres. Naarmate een profiel groeit, wordt het een robuuste opslagplaats voor persoonlijke gegevens, identiteiten, contactgegevens en communicatievoorkeuren voor een individu. Raadpleeg het [XDM-overzicht](../home.md#data-behaviors)voor informatie op hoog niveau over het gebruik van deze klasse in het ecosysteem van het Platform.

De [!DNL XDM Individual Profile] klasse zelf biedt verschillende door het systeem gegenereerde waarden die automatisch worden ingevuld wanneer gegevens worden ingevoerd, terwijl alle andere velden moeten worden toegevoegd door het gebruik van [compatibele combinaties](#mixins):

![](../images/classes/individual-profile.png)

| Eigenschap | Beschrijving |
| --- | --- |
| `_repo` | Een object met de volgende [!UICONTROL DateTime] -velden: <ul><li>`createDate`: De datum en tijd waarop de bron in de gegevensopslag werd gemaakt, bijvoorbeeld wanneer gegevens voor het eerst werden ingevoerd.</li><li>`modifyDate`: De datum en het tijdstip waarop de bron voor het laatst is gewijzigd.</li></ul> |
| `_id` | Een unieke, door het systeem gegenereerde tekenreeks-id voor de record. Dit veld wordt gebruikt om het unieke karakter van een individueel record te volgen, om te voorkomen dat gegevens dubbel worden opgeslagen en om dat record op te zoeken in downstreamdiensten. Aangezien dit veld door het systeem wordt gegenereerd, mag er tijdens het invoeren van gegevens geen expliciete waarde worden opgegeven.<br><br>Het is van belang te onderscheiden dat dit veld **geen** identiteit vertegenwoordigt die verband houdt met een individuele persoon, maar eerder de registratie van gegevens zelf. Identiteitsgegevens betreffende een persoon moeten in plaats daarvan worden beperkt tot [identiteitsvelden](../schema/composition.md#identity) . |
| `createdByBatchID` | De id van de opgenomen batch die ervoor heeft gezorgd dat de record is gemaakt. |
| `modifiedByBatchID` | De id van de laatst opgenomen batch die ervoor zorgde dat de record werd bijgewerkt. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |

## Compatibele combinaties {#mixins}

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document over de updates [van de](../mixins/name-updates.md) mixnaam voor meer informatie.

Adobe biedt verschillende standaardmixen voor gebruik met de [!DNL XDM Individual Profile] klasse. Hieronder volgt een lijst met de meestgebruikte mixen voor de klasse:

* [[!UICONTROL IdentityMap]](../mixins/profile/identitymap.md)
* [[!UICONTROL Demografische details]](../mixins/profile/person-details.md)
* [[!UICONTROL Persoonlijke contactgegevens]](../mixins/profile/personal-details.md)
* [[!UICONTROL Contactgegevens werken]](../mixins/profile/work-details.md)
* [[!UICONTROL Details segmentlidmaatschap]](../mixins/profile/segmentation.md)