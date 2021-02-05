---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;geo;datatype;data-type;data-type;
solution: Experience Platform
title: Geo-gegevenstype
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Geo XDM.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 3%

---


# [!UICONTROL Het type ] Geodata

 Geois een standaard XDM gegevenstype dat het geografische gebied beschrijft waar een gebeurtenis werd waargenomen.

<img src="../images/data-types/geo.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo-coördinaten]](./geo-coordinates.md) | Beschrijft de geografische coördinaten van een plaats. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de coördinaten. |
| `city` | Tekenreeks | De naam van de stad. |
| `countryCode` | Tekenreeks | De code van twee tekens <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> voor het land. |
| `dmaID` | Geheel | Het Nielsen-mediaonderzoek heeft een marktgebied aangewezen. |
| `msaID` | Geheel | Het statistische metropolitane gebied in de Verenigde Staten waar de waarneming plaatsvond. |
| `postalCode` | Tekenreeks | De postcode van de locatie. Postcodes zijn niet voor alle landen beschikbaar. In sommige landen zal dit slechts een deel van de postcode bevatten. |
| `stateProvince` | Tekenreeks | De staat of provincie van de observatie. De notatie volgt de [ISO 3166-2 (land en deelsector)](http://www.unece.org/cefact/locode/subdivisions.html) standaard. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/geo.schema.json)