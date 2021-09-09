---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;apparaat;datatype;data-type;data-type;currency;
solution: Experience Platform
title: Gegevenstype valuta
topic-legacy: overview
description: Dit document biedt een overzicht van het XDM-gegevenstype voor valuta.
exl-id: eaf4812e-32ec-4b07-82ef-60777f03623d
source-git-commit: 5e92b288bb8c996cfcf343d8ac1ab1665b0d3ad0
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 1%

---

# [!UICONTROL Currency] gegevenstype

[!UICONTROL Currency] is een standaard XDM gegevenstype dat een hoeveelheid valuta, met inbegrip van het munttype en de omzettingsdatum beschrijft.

![](../images/data-types/currency.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `amount` | Dubbel | Het bedrag aan valuta zoals gedefinieerd door `currencyCode`. |
| `conversionDate` | DateTime | Een tijdstempel met het tijdstip waarop de valutaomrekening is uitgevoerd. |
| `currencyCode` | Tekenreeks | Een ISO 4217-code die het type valuta aangeeft dat `amount` vertegenwoordigt. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de veldgroep:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/currency.schema.json)
