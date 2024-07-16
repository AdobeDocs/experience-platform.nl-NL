---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;apparaat;datatype;data-type;data-type;currency;
solution: Experience Platform
title: Gegevenstype valuta
description: Leer meer over het gegevenstype Valuta XDM.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# [!UICONTROL Currency] gegevenstype

[!UICONTROL Currency] is een standaard XDM-gegevenstype dat een hoeveelheid valuta beschrijft, inclusief het valutatype en de conversiedatum.

![](../images/data-types/currency.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `amount` | Dubbel | Het bedrag aan valuta zoals gedefinieerd door `currencyCode`. |
| `conversionDate` | DateTime | Een tijdstempel met het tijdstip waarop de valutaomrekening is uitgevoerd. |
| `currencyCode` | String | Een ISO 4217-code die het type valuta aangeeft dat `amount` vertegenwoordigt. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
