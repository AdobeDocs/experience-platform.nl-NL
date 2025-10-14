---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;adres;xdm:adres;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype postadres
description: Leer over het de gegevenstype van het Adres XDM van de Post.
exl-id: 94457fe5-80bc-4822-9f6c-48f77d56c89b
source-git-commit: 1d1224b263b55b290d2cac9c07dfd1b852c4cef5
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# [!UICONTROL Postal address] gegevenstype

[!UICONTROL Postal address] is een standaard XDM gegevenstype dat de details van een postend adres beschrijft.

![](../images/data-types/postal-address.png){width=450}

| Eigenschap | Beschrijving |
| --- | --- |
| `city` | De naam van de stad. |
| `country` | De naam van het door de overheid bestuurde gebied. Dit is een veld met vrije vorm dat de naam van het land in elke taal kan hebben. |
| `countryCode` | De twee karakter <a href="https://datahub.io/core/country-list"> ISO 3166-1 alpha-2 </a> code voor het land. |
| `createdByBatchID` | De id van het ingesloten batchbestand waarmee de adresrecord is gemaakt. |
| `dmaID` | Het Nielsen-mediaonderzoek heeft een marktgebied aangewezen. |
| `label` | Een vrije-vormnaam voor het adres. |
| `lastVerifiedDate` | De datum dat het adres het laatst als nog verbonden aan de persoon werd geverifieerd. |
| `modifiedByBatchID` | De id van het ingesloten batchbestand waarmee de record het laatst is gewijzigd. |
| `msaID` | Het statistische metropolitane gebied in de Verenigde Staten waar de waarneming plaatsvond. |
| `postOfficeBox` | Het postkantoor vak van het adres. |
| `postalCode` | De postcode van de locatie. Postcodes zijn niet voor alle landen beschikbaar. In sommige landen zal dit slechts een deel van de postcode bevatten. |
| `primary` | Een Booleaanse waarde die aangeeft of dit het primaire adres van de betrokkene is. Een profiel kan slechts één `primary` -adres op een bepaald tijdstip hebben. |
| `region` | Het gebied, het graafschap, of het districtsgedeelte van het adres. |
| `repositoryCreatedBy` | De id van de gebruiker die de record heeft gemaakt. |
| `repositoryLastModifiedBy` | De id van de gebruiker die de record als laatste heeft gewijzigd. |
| `stateProvince` | De staat of provincie van de observatie. Het formaat volgt [&#x200B; ISO 3166-2 (land en onderverdeling) &#x200B;](https://www.unece.org/cefact/locode/subdivisions.html) norm. |
| `status` | Geeft aan of het adres momenteel kan worden gebruikt. |
| `statusReason` | Een beschrijving van de huidige `status` . |
| `street1` - `street4` | Deze vier velden zijn bedoeld om informatie op het niveau van de primaire straat, het appartementnummer, het straatnummer en de straatnaam te bevatten. `street2` naar `street4` zijn optioneel. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype van het postadres:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/demographic/address.schema.json)
