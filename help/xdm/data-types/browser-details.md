---
keywords: Experience Platform;home;popular topics;schema;Schema;XDM;fields;schemas;Schemas;browser;browser details;datatype;data-type;data type;
solution: Experience Platform
title: Gegevenstype browserdetails
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor browserdetails.
translation-type: tm+mt
source-git-commit: f5bddb39c16eb25e85297f56e331d3aa51510eb9
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 5%

---


# [!UICONTROL Browserdetails] , gegevenstype

[!UICONTROL Browserdetails] zijn een standaard XDM-gegevenstype dat details beschrijft die betrekking hebben op een browser of toepassing.

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