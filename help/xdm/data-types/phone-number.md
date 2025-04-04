---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;phoneNumber;xdm:phoneNumber;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Gegevenstype telefoonnummer
description: Leer over het het gegevenstype van het Aantal van de Telefoon XDM.
exl-id: b84e48f9-bbb4-4b8b-9476-4bc1c455ecfd
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---

# [!UICONTROL Phone number] gegevenstype

[!UICONTROL Phone number] is een standaard XDM gegevenstype dat de details van een telefoonaantal beschrijft.

![](../images/data-types/phone-number.png){width=600}

| Eigenschap | Beschrijving |
| --- | --- |
| `extension` | Het interne kiesnummer dat wordt gebruikt om te bellen van een persoonlijke uitwisseling, operator of switchboard. |
| `number` | Het telefoonnummer. Het telefoonnummer is een tekenreeks en kan betekenisvolle tekens bevatten, zoals vierkante haakjes `()` , afbreekstreepjes `-` of tekens om subdialing-id&#39;s aan te geven, zoals extensies `x` , bijvoorbeeld `1-353(0)18391111` of `+613 9403600x1234` . |
| `primary` | Een Booleaanse waarde die aangeeft of dit het primaire telefoonnummer van de persoon is. In tegenstelling tot adres of e-mailadres, kunnen er veelvoudige primaire telefoonaantallen zijn; één per communicatiekanaal. Het communicatiekanaal wordt gedefinieerd door het type (aangegeven door de naam van de bovenliggende eigenschap): `textMessaging`, `mobile`, `phone`, `home`, `work`, `unknown` en `fax` . |
| `status` | Geeft aan of het telefoonnummer momenteel kan worden gebruikt. |
| `statusReason` | Een beschrijving van de huidige status. |
| `validity` | Een niveau van technische correctheid van het telefoonaantal. |

{style="table-layout:auto"}

Voor meer details op het gegevenstype van het telefoonaantal, verwijs naar de openbare bewaarplaats XDM:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/phonenumber.schema.json)
