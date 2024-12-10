---
title: Gegevenstype adres
description: Leer over het gegevenstype van de Gegevens van de Ervaring van het Adres Model (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 21213bd5-00f4-43cc-80cf-2c0dcf878a23
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# [!UICONTROL Address] gegevenstype

[!UICONTROL Address] is een standaard XDM-gegevenstype (Experience Data Model) dat een adres beschrijft dat wordt uitgedrukt met postconventies (in tegenstelling tot GPS of andere notaties voor locatiedefinitie). Dit gegevenstype wordt gecreeerd volgens de specificaties van Versie 5 van HL7 FHIR.

![ het gegevenstype van het Adres structuur ](../../../images/healthcare/data-types/address.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- | --- |
| [!UICONTROL Period] | `period` | [[!UICONTROL Period]](../data-types/period.md) | Tijdsperiode waarin het adres in gebruik was/is. |
| [!UICONTROL City] | `city` | String | Naam van de stad. |
| [!UICONTROL Country] | `country` | String | De landcode die is beschreven in de internationale norm ISO 3166. De code kan alpha-2 of alpha-3 zijn. |
| [!UICONTROL District] | `district` | String | De naam van het district. |
| [!UICONTROL Line] | `line` | String | De straatnaam, het nummer, de richting, de doos van P.O., of gelijkaardig. |
| [!UICONTROL Postal Code] | `postalCode` | String | De postcode. |
| [!UICONTROL State] | `state` | String | De subeenheid van een land. Afkortingen zijn acceptabel. |
| [!UICONTROL Text] | `text` | String | De tekstrepresentatie van het adres. |
| [!UICONTROL Type] | `type` | String | Het adrestype. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `postal` </li> <li> `physical` </li> <li> `both` </li> |
| [!UICONTROL Use] | `use` | String | Het doel van het adres. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `home` </li> <li> `work` </li> <li> `temp` </li> <li> `old`</li> <li> `billing`</li> |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [ Bevolkt voorbeeld ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.example.1.json)
* [ Volledig schema ](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/datatypes/address.schema.json)
