---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Schema's;browser;browserdetails;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Gegevenstype browserdetails
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor browserdetails.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 4%

---


# [!UICONTROL Browser ] detailsgegevenstype

[!UICONTROL Browser ] detailleert een standaard XDM gegevenstype dat details met betrekking tot browser of toepassing beschrijft.

<img src="../images/data-types/browser-details.png" width="450" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `acceptLanguage` | Tekenreeks | Een IETF-taaltag ([RFC 5646](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolean | Geeft aan of de instellingen van de gebruiker het schrijven van cookies toestaan. |
| `javaEnabled` | Boolean | Geeft aan of Java is ingeschakeld in het apparaat waaruit de waarneming is uitgevoerd. |
| `javaScriptEnabled` | Boolean | Geeft aan of JavaScript is ingeschakeld in het apparaat waaruit de waarneming is uitgevoerd. |
| `javaScriptVersion` | Tekenreeks | De versie van JavaScript die tijdens de observatie wordt ondersteund. |
| `javaVersion` | Tekenreeks | De versie van Java die tijdens de observatie wordt ondersteund. |
| `name` | Tekenreeks | De naam van de toepassing of browser. |
| `quicktimeVersion` | Tekenreeks | De versie van Apple Quicktime wordt ondersteund tijdens de observatie. |
| `thirdPartyCookiesEnabled` | Boolean | Geeft aan of cookies van derden zijn ingeschakeld in het apparaat waaruit de waarneming is uitgevoerd. |
| `userAgent` | Tekenreeks | De user-agent van HTTP koord van het cliëntverzoek. |
| `vendor` | Tekenreeks | De toepassings- of browserleverancier. |
| `version` | Tekenreeks | De toepassing of browserversie. |
| `viewportHeight` | Geheel | De verticale grootte in pixels van het venster waarin de gebeurtenis werd weergegeven. Voor een webweergavegebeurtenis is dit de hoogte van de viewport van de browser. |
| `viewportWidth` | Geheel | De horizontale grootte in pixels van het venster waarin de gebeurtenis werd weergegeven. Voor een webweergavegebeurtenis is dit de breedte van de viewport van de browser. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)