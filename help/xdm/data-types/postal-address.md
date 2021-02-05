---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;adres;xdm:adres;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype postadres
topic: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor postadres.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# [!UICONTROL Gegevenstype ] postadres

[!UICONTROL Het postale ] adres is een standaard XDM gegevenstype dat de details van een postend adres beschrijft.

<img src="../images/data-types/postal-address.png" width="450" /><br />

| Eigenschap | Beschrijving |
| --- | --- |
| `city` | De naam van de stad. |
| `country` | De naam van het door de overheid bestuurde gebied. Dit is een veld met vrije vorm dat de naam van het land in elke taal kan hebben. |
| `countryCode` | De code van twee tekens <a href="https://datahub.io/core/country-list">ISO 3166-1 alpha-2</a> voor het land. |
| `createdByBatchID` | De id van het ingesloten batchbestand waarmee de adresrecord is gemaakt. |
| `dmaID` | Het Nielsen-mediaonderzoek heeft een marktgebied aangewezen. |
| `label` | Een vrije-vormnaam voor het adres. |
| `lastVerifiedDate` | De datum dat het adres het laatst als nog verbonden aan de persoon werd geverifieerd. |
| `modifiedByBatchID` | De id van het ingesloten batchbestand waarmee de record het laatst is gewijzigd. |
| `msaID` | Het statistische metropolitane gebied in de Verenigde Staten waar de waarneming plaatsvond. |
| `postOfficeBox` | Het postkantoor vak van het adres. |
| `postalCode` | De postcode van de locatie. Postcodes zijn niet voor alle landen beschikbaar. In sommige landen zal dit slechts een deel van de postcode bevatten. |
| `primary` | Een Booleaanse waarde die aangeeft of dit het primaire adres van de betrokkene is. Een profiel kan slechts één `primary` adres op een bepaald punt van tijd hebben. |
| `region` | Het gebied, het graafschap, of het districtsgedeelte van het adres. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |
| `stateProvince` | De staat of provincie van de observatie. De notatie volgt de [ISO 3166-2 (land en deelsector)](http://www.unece.org/cefact/locode/subdivisions.html) standaard. |
| `status` | Geeft aan of het adres momenteel kan worden gebruikt. |
| `statusReason` | Een beschrijving van de huidige `status`. |
| `street1` - `street4` | Deze vier velden zijn bedoeld om informatie op het niveau van de primaire straat, het appartementnummer, het straatnummer en de straatnaam te bevatten. `street2` op  `street4` optioneel. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het postadres:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/address.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/address.schema.json)