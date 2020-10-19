---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;phoneNumber;xdm:phoneNumber;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype telefoonnummer
topic: overview
description: Dit document verstrekt een overzicht van het het gegevenstype van het Aantal van de Telefoon XDM.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# [!UICONTROL Gegevenstype telefoonnummer]

[!UICONTROL Het aantal] van de telefoon is een standaard XDM gegevenstype dat de details van een telefoonaantal beschrijft.

<img src="../images/data-types/phone-number.png" width="600" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `extension` | Het interne kiesnummer dat wordt gebruikt om te bellen van een persoonlijke uitwisseling, operator of switchboard. |
| `number` | Het telefoonnummer. Het telefoonnummer is een tekenreeks en kan betekenisvolle tekens bevatten, zoals vierkante haakjes `()`, afbreekstreepjes `-`of tekens om subdialing-id&#39;s aan te geven, zoals bijvoorbeeld extensies `x` of `1-353(0)18391111` `+613 9403600x1234`. |
| `primary` | Een Booleaanse waarde die aangeeft of dit het primaire telefoonnummer van de persoon is. In tegenstelling tot adres of e-mailadres, kunnen er veelvoudige primaire telefoonaantallen zijn; één per communicatiekanaal. Het communicatiekanaal wordt gedefinieerd door het type (aangegeven door de naam van de bovenliggende eigenschap): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown`, en `fax`. |
| `status` | Geeft aan of het telefoonnummer momenteel kan worden gebruikt. |
| `statusReason` | Een beschrijving van de huidige status. |
| `validity` | Een niveau van technische correctheid van het telefoonaantal. |

Voor meer details op het gegevenstype van het telefoonaantal, verwijs naar de openbare bewaarplaats XDM:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/phonenumber.schema.json)