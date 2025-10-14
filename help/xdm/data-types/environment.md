---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;milieu;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype omgeving
description: Leer over het milieu XDM gegevenstype.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# [!UICONTROL Environment] gegevenstype

[!UICONTROL Environment] is een standaard XDM gegevenstype dat het omringende milieu van een waargenomen gebeurtenis beschrijft, specifiek die overgangsinformatie zoals netwerk en softwareversies detailleert.

>[!IMPORTANT]
>
>Alle waarden zouden met het [&#x200B; DeviceAtlas &#x200B;](https://deviceatlas.com) gegevensbestand moeten worden gericht, dat door Adobe wordt vergunning gegeven.

![](../images/data-types/environment.png){width=400}

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_dc` | Object | Een object dat één veld bevat, `language` , dat de taal van de omgeving aangeeft die de taalkundige, geografische of culturele voorkeuren van de gebruiker voor de gegevenspresentatie vertegenwoordigt. De talen worden gespecificeerd in taalcode zoals die in [&#x200B; wordt bepaald IETF RFC 3066 &#x200B;](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [&#x200B; Browser details &#x200B;](./browser-details.md) | Beschrijft browser-specifieke details van het milieu, zoals browser naam, versie, versie van JavaScript, gebruikersagent koord, en keurt taal goed. |
| `ISP` | String | De naam van de internetprovider van de gebruiker. |
| `carrier` | String | De naam van de mobiele netwerkprovider of MNO (ook bekend als een draadloze serviceprovider, draadloze provider, mobiel bedrijf of mobiele netwerkprovider) die communicatiediensten aan de gebruiker verkoopt en levert. |
| `colorDepth` | Geheel | Het aantal bits dat wordt gebruikt voor elke kleurcomponent van één pixel. |
| `connectionType` | String | Het type internetverbinding. Tot de geaccepteerde waarden behoren: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | String | Het domein van ISP van de gebruiker. |
| `ipV4` | String | Het numerieke label dat is toegewezen aan een apparaat dat deelneemt aan een computernetwerk dat het Internet Protocol voor communicatie (32 bits) gebruikt. |
| `ipV6` | String | Het numerieke label dat is toegewezen aan een apparaat dat deelneemt aan een computernetwerk dat het Internet Protocol voor communicatie (128 bits) gebruikt. |
| `operatingSystem` | String | De naam van het besturingssysteem dat bij de waarneming werd gebruikt. Het kenmerk mag geen versiegegevens zoals `10.5.3` bevatten, maar wel &#39;editie&#39;-aanduidingen zoals `Ultimate` of `Professional` . |
| `operatingSystemVendor` | String | De naam van de leverancier van het besturingssysteem die is gebruikt bij de waarneming. |
| `operatingSystemVersion` | String | De volledige versie-id voor het besturingssysteem dat bij de waarneming werd gebruikt. Versies worden meestal numeriek samengesteld, maar kunnen in een door de leverancier gedefinieerde indeling worden gebruikt. |
| `type` | String | Het type van de toepassingsomgeving. Zie [&#x200B; bijlage &#x200B;](#type) voor toegelaten waarden. |
| `viewportHeight` | Geheel | De verticale grootte in pixels van het venster waarin de ervaring is weergegeven. Voor een webweergavegebeurtenis is dit de hoogte van de viewport van de browser. |
| `viewPortWidth` | Geheel | De horizontale grootte in pixels van het venster waarin de ervaring is weergegeven. Voor een webweergavegebeurtenis is dit de breedte van de viewport van de browser. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Bijlage

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Device] .

## Geaccepteerde waarden voor tekst {#type}

In de volgende tabel worden de geaccepteerde waarden voor `type` en de bijbehorende betekenissen weergegeven:

| Waarde | Beschrijving |
| --- | --- |
| `browser` | Browser |
| `application` | Toepassing |
| `iot` | Internet |
| `external` | Extern systeem |
| `widget` | Application Extension |
