---
solution: Experience Platform
title: Gegevenstype van goedgekeurde tekenreeks
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor tekenreeks met toestemming.
source-git-commit: 7a0ac3970713e95438c6f0fdbd6175545ea7fdd0
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 2%

---

# [!UICONTROL Consent String] gegevenstype

[!UICONTROL Consent String] is een standaard XDM gegevenstype dat een koordwaarde beschrijft die de toestemming van een klant vertegenwoordigt. Het omvat contextuele informatie zoals de norm voor het toestemmingskoord (bijvoorbeeld, [IAB Transparantie en het Kader van de Toestemming (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `consentStandard` | Tekenreeks | De standaard voor de toestemmingstekenreeks. Dit helpt de formaat van het toestemmingskoord bepalen zoals die door de diensten van het toestemmingsbeheer wordt geplaatst. |
| `consentStandardVersion` | Tekenreeks | De versie van de toestemmingsnorm, die wordt gebruikt om het formaat van het toestemmingskoord nauwkeurig te bepalen zoals die door de diensten van het toestemmingsbeheer wordt geplaatst. |
| `consentStringValue` | Tekenreeks | De tekenreeks voor volledige toestemming zoals verstrekt door de service voor het beheer van de toestemming. `consentStandard` en  `consentStandardVersion` help definiëren hoe deze tekenreeks moet worden geparseerd. |
| `containsPersonalData` | Boolean | Als dit veld waar is, betekent dit dat deze toestemmingsreeks moet worden verwerkt voor het afdwingen van toestemming. |
| `gdprApplies` | Boolean | Als dit veld waar is, betekent dit dat er toestemming komt met persoonsgegevens. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
