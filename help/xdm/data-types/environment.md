---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;milieu;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype omgeving
topic: overview
description: Dit document biedt een overzicht van het milieu-XDM-gegevenstype.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '464'
ht-degree: 3%

---


# [!UICONTROL Gegevenstype ] Omgeving

 Environment is een standaard XDM-gegevenstype dat de omringende omgeving van een waargenomen gebeurtenis beschrijft, met name met gedetailleerde informatie over tijdelijke gegevens zoals netwerk- en softwareversies.

>[!IMPORTANT]
>
>Alle waarden moeten worden uitgelijnd met de [DeviceAtlas](https://deviceatlas.com)-database, die in licentie is gegeven door Adobe.

<img src="../images/data-types/environment.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_dc` | Object | Een object dat één veld bevat, `language`, dat de taal van de omgeving aangeeft die de taalkundige, geografische of culturele voorkeuren van de gebruiker voor de gegevenspresentatie vertegenwoordigt. Talen worden gespecificeerd in taalcode zoals bepaald in [IETF RFC 3066](https://www.ietf.org/rfc/rfc3066.txt). |
| `browserDetails` | [Browserdetails](./browser-details.md) | Beschrijft de browser-specifieke details van het milieu, zoals browser naam, versie, versie JavaScript versie, userAgent koord, en keurt taal goed. |
| `ISP` | Tekenreeks | De naam van de internetprovider van de gebruiker. |
| `carrier` | Tekenreeks | De naam van de mobiele netwerkprovider of MNO (ook bekend als een draadloze serviceprovider, draadloze provider, mobiel bedrijf of mobiele netwerkprovider) die communicatiediensten aan de gebruiker verkoopt en levert. |
| `colorDepth` | Geheel | Het aantal bits dat wordt gebruikt voor elke kleurcomponent van één pixel. |
| `connectionType` | Tekenreeks | Het type internetverbinding. Tot de geaccepteerde waarden behoren: <ul><li>`dialup`</li><li>`isdn`</li><li>`bisdn`</li><li>`dsl`</li><li>`cable`</li><li>`wireless_wifi`</li><li>`mobile`</li><li>`mobile_edge`</li><li>`mobile_2g`</li><li>`mobile_3g`</li><li>`mobile_lte`</li><li>`t1`</li><li>`t3`</li><li>`oc3`</li><li>`lan`</li><li>`modem`</li></ul> |
| `domain` | Tekenreeks | Het domein van ISP van de gebruiker. |
| `ipV4` | Tekenreeks | Het numerieke label dat is toegewezen aan een apparaat dat deelneemt aan een computernetwerk dat het Internet Protocol voor communicatie (32 bits) gebruikt. |
| `ipV6` | Tekenreeks | Het numerieke label dat is toegewezen aan een apparaat dat deelneemt aan een computernetwerk dat het Internet Protocol voor communicatie (128 bits) gebruikt. |
| `operatingSystem` | Tekenreeks | De naam van het besturingssysteem dat bij de waarneming werd gebruikt. Het kenmerk mag geen versiegegevens zoals `10.5.3` bevatten, maar moet in plaats daarvan &#39;edition&#39;-aanduidingen zoals `Ultimate` of `Professional` bevatten. |
| `operatingSystemVendor` | Tekenreeks | De naam van de leverancier van het besturingssysteem die is gebruikt bij de waarneming. |
| `operatingSystemVersion` | Tekenreeks | De volledige versie-id voor het besturingssysteem dat bij de waarneming werd gebruikt. Versies worden meestal numeriek samengesteld, maar kunnen in een door de leverancier gedefinieerde indeling worden gebruikt. |
| `type` | Tekenreeks | Het type toepassingsomgeving. Zie [appendix](#type) voor geaccepteerde waarden. |
| `viewportHeight` | Geheel | De verticale grootte in pixels van het venster waarin de ervaring is weergegeven. Voor een webweergavegebeurtenis is dit de hoogte van de viewport van de browser. |
| `viewPortWidth` | Geheel | De horizontale grootte in pixels van het venster waarin de ervaring is weergegeven. Voor een webweergavegebeurtenis is dit de breedte van de viewport van de browser. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/environment.schema.json)

## Aanhangsel

De volgende sectie bevat aanvullende informatie over het gegevenstype [!UICONTROL Device].

## Geaccepteerde waarden voor het type {#type}

In de volgende tabel worden de geaccepteerde waarden voor `type` en de bijbehorende betekenissen weergegeven:

| Value | Beschrijving |
| --- | --- |
| `browser` | Browser |
| `application` | Toepassing |
| `iot` | Internet |
| `external` | Extern systeem |
| `widget` | Toepassingsextensie |