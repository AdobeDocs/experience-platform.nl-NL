---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;geo;datatype;data-type;data-type;
solution: Experience Platform
title: Geo-gegevenstype
topic-legacy: overview
description: Dit document biedt een overzicht van het gegevenstype Geo XDM.
exl-id: d0eef943-ef86-4abd-8a51-dc45f2ed782d
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 3%

---

# [!UICONTROL Geo] gegevenstype

[!UICONTROL Geo] is een standaard XDM gegevenstype dat het geografische gebied beschrijft waar een gebeurtenis werd waargenomen.

<img src="../images/data-types/geo.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `_schema` | [[!UICONTROL Geo Coordinates]](./geo-coordinates.md) | Beschrijft de geografische coördinaten van een plaats. |
| `_id` | Tekenreeks | Een unieke, door het systeem gegenereerde id voor de coördinaten. |
| `city` | Tekenreeks | De naam van de stad. |
| `countryCode` | Tekenreeks | Het twee-karakter <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> code voor het land. |
| `dmaID` | Geheel | Het Nielsen-mediaonderzoek heeft een marktgebied aangewezen. |
| `msaID` | Geheel | Het statistische metropolitane gebied in de Verenigde Staten waar de waarneming plaatsvond. |
| `postalCode` | Tekenreeks | De postcode van de locatie. Postcodes zijn niet voor alle landen beschikbaar. In sommige landen zal dit slechts een deel van de postcode bevatten. |
| `stateProvince` | Tekenreeks | De staat of provincie van de observatie. De notatie volgt de [ISO 3166-2 (land en deelsector)](https://www.unece.org/cefact/locode/subdivisions.html) standaard. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/geo.schema.json)
