---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;individual profile;fields;schemas;Schemas;loyalty details;Schema design;field group;Field group;
solution: Experience Platform
title: Loyalty Details Schema Field Group
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep Loyalty Details.
source-git-commit: afe748d443aad7b6da5b348cd569c9e806e4419b
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---


# [!UICONTROL Loyalty Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Loyalty Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). The field group provides a single object-type field, `loyalty`, which captures information related to a person&#39;s membership in a customer loyalty program.

![](../../images/field-groups/loyalty-details.png)

| Property | Data type | Beschrijving |
| --- | --- | --- |
| `pointsExpiration` | Array of objects | Maakt een lijst van om het even welke loyaliteitspunten (of groepen loyaliteitspunten) die zullen verlopen, en de data die zij zullen verlopen op. Elk arrayitem moet een object zijn dat de volgende twee eigenschappen bevat: <ul><li>`pointsExpirationDate`: Een ISO 8601-datum waarop de punten verlopen.</li><li>`pointsExpiring`: De puntbalans die vervalt op de bijbehorende vervaldatum.</li></ul> |
| `joinDate` | DateTime | An ISO 8601 datetime of when the person joined the loyalty program. |
| `loyaltyID` | Array of strings | Represents the loyalty program ID(s) associated with the loyalty program member. |
| `points` | Dubbel | The current balance of loyalty points or awards for the loyalty member. |
| `pointsRedeemed` | Double | Het bedrag van de punten die het loyaliteitslid heeft toegepast op een aankoop of anderszins heeft afgelost. |
| `program` | Tekenreeks | De naam van het loyaliteitsprogramma waarin de persoon is ingeschreven. |
| `status` | Tekenreeks | The current status of the person&#39;s loyalty membership, such as `active`, `disabled`, or `suspended`. |
| `tier` | Tekenreeks | Vangt de lijst van het loyaliteitsprogramma waarin de persoon wordt ingeschreven. |
| `upgradeDate` | Tekenreeks | De datum waarop het loyaliteitslid werd bevorderd tot het meest recente niveau. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-loyalty-details.schema.json)
