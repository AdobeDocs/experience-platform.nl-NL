---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;milieu;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype omgeving
description: Leer over het milieu XDM gegevenstype.
exl-id: ec806ee5-ed65-4148-9dbe-e297d9e8cd73
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 0%

---

# [!UICONTROL Environment] gegevenstype

[!UICONTROL Environment] is een standaard XDM gegevenstype dat het omringende milieu van een waargenomen gebeurtenis beschrijft, specifiek die overgangsinformatie zoals netwerk en softwareversies detailleert.

>[!IMPORTANT]
>
>Alle waarden moeten op de knop [DeviceAtlas](https://deviceatlas.com) database, in licentie gegeven door Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_dc` | Object | Een object dat één veld bevat, `language`, waarin de taal van de omgeving wordt aangegeven die de taalkundige, geografische of culturele voorkeuren van de gebruiker voor de gegevenspresentatie vertegenwoordigt. Talen worden opgegeven in taalcode zoals gedefinieerd in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Browserdetails](./browser-details.md) | Beschrijft de browser-specifieke details van het milieu, zoals browser naam, versie, versie JavaScript versie, userAgent koord, en keurt taal goed. |
| `ISP` | String | De naam van de internetprovider van de gebruiker. |
| `carrier` | String | De naam van de mobiele netwerkprovider of MNO (ook bekend als een draadloze serviceprovider, draadloze provider, mobiel bedrijf of mobiele netwerkprovider) die communicatiediensten aan de gebruiker verkoopt en levert. |
| `colorDepth` | Geheel | Het aantal bits dat wordt gebruikt voor elke kleurcomponent van één pixel. |
| `connectionType` | String | Het type internetverbinding. Tot de geaccepteerde waarden behoren: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | String | Het domein van ISP van de gebruiker. |
| `ipV4` | String | Het numerieke label dat is toegewezen aan een apparaat dat deelneemt aan een computernetwerk dat het Internet Protocol voor communicatie (32 bits) gebruikt. |
| `ipV6` | String | Het numerieke label dat is toegewezen aan een apparaat dat deelneemt aan een computernetwerk dat het Internet Protocol voor communicatie (128 bits) gebruikt. |
| `operatingSystem` | String | De naam van het besturingssysteem dat bij de waarneming werd gebruikt. Het kenmerk mag geen versiegegevens bevatten zoals `10.5.3`, maar bevat in plaats daarvan &quot;edition&quot;-aanduidingen zoals `Ultimate` of `Professional`. |
| `operatingSystemVendor` | String | De naam van de leverancier van het besturingssysteem die is gebruikt bij de waarneming. |
| `operatingSystemVersion` | String | De volledige versie-id voor het besturingssysteem dat bij de waarneming werd gebruikt. Versies worden meestal numeriek samengesteld, maar kunnen in een door de leverancier gedefinieerde indeling worden gebruikt. |
| `type` | String | Het type van de toepassingsomgeving. Zie de [aanhangsel](#type) voor geaccepteerde waarden. |
| `viewportHeight` | Geheel | De verticale grootte in pixels van het venster waarin de ervaring is weergegeven. Voor een webweergavegebeurtenis is dit de hoogte van de viewport van de browser. |
| `viewPortWidth` | Geheel | De horizontale grootte in pixels van het venster waarin de ervaring is weergegeven. Voor een webweergavegebeurtenis is dit de breedte van de viewport van de browser. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Bijlage

De volgende sectie bevat aanvullende informatie over de [!UICONTROL Device] gegevenstype.

## Geaccepteerde waarden voor tekst {#type}

In de volgende tabel worden de toegestane waarden voor `type` en de betekenis ervan:

| Waarde | Beschrijving |
| --- | --- |
| `browser` | Browser |
| `application` | Toepassing |
| `iot` | Internet |
| `external` | Extern systeem |
| `widget` | Application Extension |
