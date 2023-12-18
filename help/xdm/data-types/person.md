---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;persoon;datatype;gegeven-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Persoon
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Persoon (XDM).
exl-id: f28a52be-90c7-4ed0-a460-97165bb58046
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# [!UICONTROL Person] gegevenstype

[!UICONTROL Person] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat een individuele persoon beschrijft. Dit datatype kan een persoon vertegenwoordigen die in diverse rollen, zoals een klant, een contact, of een eigenaar handelt.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `name` | [[!UICONTROL Person name]](./person-name.md) | Beschrijft details over de volledige naam van de persoon. |
| `birthDate` | Datum | De volledige datum waarop een persoon is geboren. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `birthDayAndMonth` | String | De dag en de maand waarin een persoon is geboren, in de notatie MM-DD. Dit veld moet worden gebruikt wanneer de dag en de maand van de geboorte van een persoon bekend is, maar niet het jaar. De indeling van deze eigenschap moet overeenkomen met deze reguliere expressie `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Geheel | Het jaar waarin een persoon geboren is, inclusief de eeuw (bijvoorbeeld `1983`). Dit veld moet worden gebruikt wanneer alleen de leeftijd van de persoon bekend is en niet de volledige geboortedatum. Deze waarde moet liggen tussen 1 en 32767. |
| `gender` | String | De genderidentiteit van de persoon. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> De standaardwaarde voor deze waarde is `not_specified`. |
| `maritalStatus` | String | Beschrijft de verhouding van een persoon met significante andere. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende opsommingswaarden. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> De standaardwaarde voor deze waarde is `not_specified`. |
| `nationality` | String | De juridische relatie tussen een persoon en zijn staat die wordt vertegenwoordigd door middel van de ISO 3166-1 Alpha-2 code. De indeling van deze eigenschap moet overeenkomen met deze reguliere expressie `^[A-Z]{2}$`. |
| `taxId` | String | De belasting- of fiscale ID van de persoon, zoals het fiscaal identificatienummer (TIN) in de VS of het Certificado de Identificación Fiscal (CIF/NIF) in Spanje. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)
