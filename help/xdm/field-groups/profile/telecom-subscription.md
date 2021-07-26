---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;telecommunicatie;telecommunicatie;Schema ontwerp;gebiedsgroep;De groep van het Gebied;
solution: Experience Platform
title: Telecom Subscription Schema Field Group
topic-legacy: overview
description: Dit document verstrekt een overzicht van de het schemagebiedgroep van het Abonnement van Telecom.
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '709'
ht-degree: 1%

---

# [!UICONTROL Telecom Subscription] schemaveldgroep

>[!NOTE]
>
>De namen van verschillende groepen schemavelden zijn gewijzigd. Zie het document op [updates van de gebiedsgroepnaam](../name-updates.md) voor meer informatie.

[!UICONTROL Telecom Subscription] is een standaardschemagebiedgroep voor de  [[!DNL XDM Individual Profile] ](../../classes/individual-profile.md) klasse die het abonnement van een klant op telecom, met inbegrip van tarifering, pakketten, en individuele productabonnementen beschrijft.

De veldgroep biedt één objecttype veld, `telecomSubscription`, waarvan de eigenschappen hieronder worden beschreven.

![Telecom Subscription Structure](../../images/field-groups/telecom-subscription/structure.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `internetSubscription` | Array van objecten | Beschrijft de details van het Internet abonnementsplan zoals gegevensGLB, verbindingstype, en snelheidsdetails. Zie de [sectie onder](#internetSubscription) voor meer informatie. |
| `landlineSubscription` | Array van objecten | Beschrijft de details van het landline abonnementsplan, met inbegrip van geselecteerde eigenschappen, notulen, en het draaien plannen. Zie de [sectie onder](#landlineSubscription) voor meer informatie. |
| `mediaSubscription` | Array van objecten | Beschrijft de details van het media abonnementsplan, met inbegrip van het aantal kanalen en inbegrepen het stromen diensten. Zie de [sectie onder](#mediaSubscription) voor meer informatie. |
| `mobileSubscription` | Array van objecten | Beschrijft mobiele details van het abonnementsabonnement, met inbegrip van het aantal lijnen, gegevenstarieven, kosten, en meer. Zie de [sectie onder](#mobileSubscription) voor meer informatie. |
| `primarySubscriber` | [[!UICONTROL Person]](../../data-types/person.md) | Beschrijft de eigenaar van het abonnement. |
| `bundleName` | Tekenreeks | Vangt de naam van om het even welk type van abonnementsbundel waarin de klant, zoals `Internet + Media` wordt ingeschreven. |
| `primaryPartyID` | Tekenreeks | Een herkenningsteken voor de primaire persoon verantwoordelijk voor het abonnement, die typisch hun aantal van de apparatentelefoon zou kunnen zijn. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-personal-details.schema.json)

## `internetSubscription` {#internetSubscription}

`internetSubscription` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![InternetSubscription](../../images/field-groups/telecom-subscription/internetSubscription.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beschrijft algemene details over het abonnement, met inbegrip van abonnementslengte, kosten, status, en meer. Beschrijft algemene details over het abonnement, met inbegrip van abonnementslengte, kosten, status, en meer. |
| `connectionType` | Tekenreeks | Het verbindingstype voor het abonnement. |
| `dataCap` | Geheel | De limiet voor het maximale gegevensbereik van de account, in megabytes (MB). |
| `downloadSpeed` | Geheel | De maximale downloadsnelheid die beschikbaar is voor het abonnement, in megabytes (MB). |
| `selfSetup` | Boolean | Geeft aan of een klant in aanmerking komt voor de installatie van internet zonder bezoek van een technicus. |
| `uploadSpeed` | Geheel | De maximale uploadsnelheid die beschikbaar is voor het abonnement, in megabytes (MB). |

{style=&quot;table-layout:auto&quot;}

## `landlineSubscription` {#landlineSubscription}

`landlineSubscription` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![landlineSubscription](../../images/field-groups/telecom-subscription/landlineSubscription.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Phone Number]](../../data-types/telecom-subscription.md) | Het telefoonnummer dat aan dit abonnement is toegewezen. |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beschrijft algemene details over het abonnement, met inbegrip van abonnementslengte, kosten, status, en meer. |
| `callBlocking` | Boolean | Wijst erop of de eigenschappen van het landlineabonnement vraag het blokkeren omvatten. |
| `callForwarding` | Boolean | Wijst erop of de eigenschappen van het landlineabonnement vraag door:sturen omvatten. |
| `callWaiting` | Boolean | Wijst erop of de eigenschappen van het landlineabonnement vraag het wachten omvatten. |
| `callerID` | Boolean | Wijst erop of de eigenschappen van het landlineabonnement bezoekersidentiteitskaart omvatten. |
| `internationalCalling` | Boolean | Geeft aan of de abonnementsfuncties voor vaste netwerken internationale aanroepen bevatten. |
| `minutes` | Geheel | Het aantal maandelijkse minuten dat beschikbaar is in het abonnement. |
| `threeWayCalling` | Boolean | Wijst erop of de eigenschappen van het landlineabonnement driewegvraag omvatten. |
| `unlimitedDomesticLongDistance` | Boolean | Geeft aan of de abonnementsfuncties voor vaste netwerken een onbeperkte binnenlandse aanroep over lange afstand bevatten. |
| `unlimitedLocalCalling` | Boolean | Geeft aan of de abonnementsfuncties van de vaste lijn een onbeperkte lokale aanroep bevatten. |
| `voicemail` | Boolean | Wijst erop of de eigenschappen van het landlineabonnement audio-messagerie omvatten. |

{style=&quot;table-layout:auto&quot;}

## `mediaSubscription` {#mediaSubscription}

`mediaSubscription` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![mediaSubscription](../../images/field-groups/telecom-subscription/mediaSubscription.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `streamingServices` | Array van objecten | Een lijst met alle streamingservices die bij het abonnement zijn inbegrepen. Elk arrayitem bevat de volgende eigenschappen: <ul><li>`promotionLength`: De duur van de bevordering, in maanden, als de het stromen dienst als deel van een bevordering werd toegevoegd.</li><li>`promotionalAddition`: Geeft aan of de streamingservice is toegevoegd als onderdeel van een promotie.</li><li>`serviceName`: De naam van de streamingservice.</li></ul> |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beschrijft algemene details over het abonnement, met inbegrip van abonnementslengte, kosten, status, en meer. |
| `channels` | Geheel | Het aantal kanalen dat is opgenomen in het mediaabonnement. |

{style=&quot;table-layout:auto&quot;}

## `mobileSubscription` {#mobileSubscription}

`mobileSubscription` wordt opgegeven als een array van objecten. De structuur van elk object wordt hieronder beschreven.

![mobileSubscription](../../images/field-groups/telecom-subscription/mobileSubscription.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `phoneNumber` | [[!UICONTROL Phone Number]](../../data-types/telecom-subscription.md) | Het telefoonnummer dat aan dit abonnement is toegewezen. |
| `subscriptionDetails` | [[!UICONTROL Telecom Subscription]](../../data-types/telecom-subscription.md) | Beschrijft algemene details over het abonnement, met inbegrip van abonnementslengte, kosten, status, en meer. |
| `earlyUpgradeEnrollment` | Boolean | Geeft aan of de klant ervoor kiest een eerste upgrade uit te voeren. |
| `planLevel` | Tekenreeks | De naam van het mobiele abonnement dat aan dit abonnement is toegewezen. |
| `portedNumber` | Boolean | Geeft aan of de klant zijn of haar nummer van een andere provider poorten. |

{style=&quot;table-layout:auto&quot;}

