---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;loyaliteitsdetails;Schema ontwerp;gebiedsgroep;De groep van het Gebied;
solution: Experience Platform
title: Loyalty Details Schema Field Group
topic-legacy: overview
description: Dit document biedt een overzicht van de veldgroep Loyalty Details.
source-git-commit: fe49560a69c4c02835f00e4ebc0a5b9dc88eae90
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---


# [!UICONTROL Loyalty Details] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Loyalty Details] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De veldgroep biedt één objecttype veld, `loyalty`, waarin informatie wordt vastgelegd die betrekking heeft op het lidmaatschap van een persoon in een klantenbindingsprogramma.

![](../../images/field-groups/loyalty-details.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `pointsExpiration` | Array van objecten | Maakt een lijst van om het even welke loyaliteitspunten (of groepen loyaliteitspunten) die zullen verlopen, en de data die zij zullen verlopen op. Elk arrayitem moet een object zijn dat de volgende twee eigenschappen bevat: <ul><li>`pointsExpirationDate`: Een ISO 8601-datum waarop de punten verlopen.</li><li>`pointsExpiring`: De puntbalans die vervalt op de bijbehorende vervaldatum.</li></ul> |
| `joinDate` | DateTime | Een ISO 8601 datetime van toen de persoon zich bij het loyaliteitsprogramma aansloot. |
| `loyaltyID` | Array van tekenreeksen | Vertegenwoordigt de programma-id(&#39;s) van de loyaliteit die aan het lid van het loyaliteitsprogramma zijn gekoppeld. |
| `points` | Dubbel | De huidige balans van loyaliteitspunten of beloningen voor het loyaliteitslid. |
| `pointsRedeemed` | Dubbel | Het bedrag van de punten die het loyaliteitslid heeft toegepast op een aankoop of anderszins heeft afgelost. |
| `program` | Tekenreeks | De naam van het loyaliteitsprogramma waarin de persoon is ingeschreven. |
| `status` | Tekenreeks | De huidige status van het loyaliteitslidmaatschap van de persoon, zoals `active`, `disabled` of `suspended`. |
| `tier` | Tekenreeks | Vangt de lijst van het loyaliteitsprogramma waarin de persoon wordt ingeschreven. |
| `upgradeDate` | Tekenreeks | De datum waarop het loyaliteitslid werd bevorderd tot het meest recente niveau. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-loyalty-details.schema.json)
