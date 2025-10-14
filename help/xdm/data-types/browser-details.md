---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Schema's;browser;browserdetails;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Gegevenstype browserdetails
description: Leer over Browser Details XDM gegevenstype.
exl-id: c67ff8bc-0614-4422-9bb7-689b98d7086d
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# [!UICONTROL Browser details] gegevenstype

[!UICONTROL Browser details] is een standaard XDM gegevenstype dat details met betrekking tot browser of toepassing beschrijft.

![](../images/data-types/browser-details.png){width=450}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `acceptLanguage` | String | Een IETF taalmarkering ([&#x200B; RFC 5646 &#x200B;](https://tools.ietf.org/html/rfc5646)). |
| `cookiesEnabled` | Boolean | Geeft aan of de instellingen van de gebruiker het schrijven van cookies toestaan. |
| `javaEnabled` | Boolean | Geeft aan of Java is ingeschakeld in het apparaat waaruit de waarneming is uitgevoerd. |
| `javaScriptEnabled` | Boolean | Geeft aan of JavaScript is ingeschakeld in het apparaat waaruit de waarneming is uitgevoerd. |
| `javaScriptVersion` | String | De versie van JavaScript werd tijdens de observatie ondersteund. |
| `javaVersion` | String | De versie van Java die tijdens de observatie wordt ondersteund. |
| `name` | String | De naam van de toepassing of browser. |
| `quicktimeVersion` | String | De versie van Apple Quicktime die tijdens de observatie wordt ondersteund. |
| `thirdPartyCookiesEnabled` | Boolean | Geeft aan of cookies van derden zijn ingeschakeld in het apparaat waaruit de waarneming is uitgevoerd. |
| `userAgent` | String | De user-agent van HTTP koord van het cliëntverzoek. |
| `vendor` | String | De toepassings- of browserleverancier. |
| `version` | String | De toepassing of browserversie. |
| `viewportHeight` | Geheel | De verticale grootte in pixels van het venster waarin de gebeurtenis werd weergegeven. Voor een webweergavegebeurtenis is dit de hoogte van de viewport van de browser. |
| `viewportWidth` | Geheel | De horizontale grootte in pixels van het venster waarin de gebeurtenis werd weergegeven. Voor een webweergavegebeurtenis is dit de breedte van de viewport van de browser. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/browserdetails.schema.json)
