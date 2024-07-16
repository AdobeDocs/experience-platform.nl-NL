---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;loyaliteitsdetails;Schema ontwerp;gebiedsgroep;De groep van het Gebied;
solution: Experience Platform
title: Loyalty Details Schema Field Group
description: Meer informatie over de veldgroep Loyalty Details.
exl-id: 12c9fef5-4f9e-49b5-894f-f4938bb95c23
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# [!UICONTROL Loyalty Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [ de naamupdates van de gebiedsgroep ](../name-updates.md) voor meer informatie.

[!UICONTROL Loyalty Details] is een standaardgroep van het schemagebied voor de [[!DNL XDM Individual Profile]  klasse ](../../classes/individual-profile.md). De veldgroep biedt één objecttype veld, `loyalty` , waarin informatie wordt vastgelegd die betrekking heeft op het lidmaatschap van een persoon in een klantenbindingsprogramma.

![](../../images/field-groups/loyalty-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `pointsExpiration` | Array van objecten | Maakt een lijst van om het even welke loyaliteitspunten (of groepen van loyaliteitspunten) die zullen verlopen, en de data die zij zullen verlopen op. Elk arrayitem moet een object zijn dat de volgende twee eigenschappen bevat: <ul><li>`pointsExpirationDate`: een ISO 8601-datetime van wanneer de punten verlopen.</li><li>`pointsExpiring`: De puntbalans die vervalt op de bijbehorende vervaldatum.</li></ul> |
| `joinDate` | DateTime | Een ISO 8601 datetime van toen de persoon zich bij het loyaliteitsprogramma aansloot. |
| `loyaltyID` | Array van tekenreeksen | Vertegenwoordigt de programma-id(&#39;s) van de loyaliteit die aan het lid van het loyaliteitsprogramma zijn gekoppeld. |
| `points` | Dubbel | De huidige balans van loyaliteitspunten of beloningen voor het loyaliteitslid. |
| `pointsRedeemed` | Dubbel | Het bedrag van de punten die het loyaliteitslid heeft toegepast op een aankoop of anderszins heeft afgelost. |
| `program` | String | De naam van het loyaliteitsprogramma waarin de persoon is ingeschreven. |
| `status` | String | De huidige status van het loyaliteitslidmaatschap van de persoon, zoals `active`, `disabled` of `suspended` . |
| `tier` | String | Vangt de lijst van het loyaliteitsprogramma waarin de persoon wordt ingeschreven. |
| `upgradeDate` | String | De datum waarop het loyaliteitslid werd bevorderd tot het meest recente niveau. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
