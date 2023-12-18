---
solution: Experience Platform
title: Gegevenstype van goedgekeurde tekenreeks
description: Meer informatie over het XDM-gegevenstype voor tekenreeks met toestemming.
exl-id: 288ec79e-074a-4d72-9c5f-e9cd8485b804
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---

# [!UICONTROL Consent String] gegevenstype

[!UICONTROL Consent String] is een standaard XDM gegevenstype dat een koordwaarde beschrijft die de toestemming van een klant vertegenwoordigt. Het bevat contextafhankelijke informatie zoals de standaard voor de toestemmingstekenreeks (bijvoorbeeld de [IAB Transparency and Consent Framework (TCF) 2.0](../field-groups/profile/iab.md)).

![](../images/data-types/consent-string.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `consentStandard` | String | De standaard voor de toestemmingstekenreeks. Dit helpt de formaat van het toestemmingskoord bepalen zoals die door de diensten van het toestemmingsbeheer wordt geplaatst. |
| `consentStandardVersion` | String | De versie van de toestemmingsnorm, die wordt gebruikt om het formaat van het toestemmingskoord nauwkeurig te bepalen zoals die door de diensten van het toestemmingsbeheer wordt geplaatst. |
| `consentStringValue` | String | De tekenreeks voor volledige toestemming zoals verstrekt door de service voor het beheer van de toestemming. `consentStandard` en `consentStandardVersion` help bepalen hoe deze tekenreeks moet worden geparseerd. |
| `containsPersonalData` | Boolean | Als dit veld waar is, betekent dit dat deze toestemmingsreeks moet worden verwerkt voor het afdwingen van toestemming. |
| `gdprApplies` | Boolean | Als dit veld waar is, betekent dit dat er toestemming komt met persoonsgegevens. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consentstring.schema.json)
