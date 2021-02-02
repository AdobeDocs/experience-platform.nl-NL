---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;persoon;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Persoon
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Person Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 194b604d4b23f2acfaa4243155b04a6793fb0727
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 3%

---


# [!UICONTROL Het type ] Persondata

 Personeert een standaard het gegevenstype van de Gegevens van de Ervaring Model (XDM) dat een individuele persoon beschrijft. Dit datatype kan een persoon vertegenwoordigen die in diverse rollen, zoals een klant, een contact, of een eigenaar handelt.

<img src="../images/data-types/person.PNG" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `name` | [[!UICONTROL Naam persoon]](./person-name.md) | Beschrijft details over de volledige naam van de persoon. |
| `birthDate` | Datum | De volledige datum waarop een persoon is geboren. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `birthDayAndMonth` | Tekenreeks | De dag en de maand waarin een persoon is geboren, in de notatie MM-DD. Dit veld moet worden gebruikt wanneer de dag en de maand van de geboorte van een persoon bekend is, maar niet het jaar. De opmaak van deze eigenschap moet overeenkomen met deze reguliere expressie `[0-1][0-9]-[0-9][0-9]`. |
| `birthYear` | Geheel | Het jaar waarin een persoon is geboren, inclusief de eeuw (bijvoorbeeld `1983`). Dit veld moet worden gebruikt wanneer alleen de leeftijd van de persoon bekend is en niet de volledige geboortedatum. Deze waarde moet liggen tussen 1 en 32767. |
| `gender` | Tekenreeks | De genderidentiteit van de persoon. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende bekende opsommingswaarden. <li> `female` </li> <li> `male` </li> <li> `not_specified` </li> <li> `non_specific` </li> De standaardwaarde voor deze waarde is `not_specified`. |
| `maritalStatus` | Tekenreeks | Beschrijft de verhouding van een persoon met significante andere. De waarde van deze eigenschap moet gelijk zijn aan een van de volgende opsommingswaarden. <li> `married` </li> <li> `single` </li> <li> `divorced` </li> <li> `widowed` </li> <li> `not_specified` </li> De standaardwaarde voor deze waarde is `not_specified`. |
| `nationality` | Tekenreeks | De juridische relatie tussen een persoon en zijn staat die wordt vertegenwoordigd door middel van de ISO 3166-1 Alpha-2-code. De opmaak van deze eigenschap moet overeenkomen met deze reguliere expressie `^[A-Z]{2}$`. |
| `taxId` | Tekenreeks | De belasting- of fiscale ID van de persoon, zoals het fiscaal identificatienummer (TIN) in de VS of het Certificado de Identificación Fiscal (CIF/NIF) in Spanje. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/person/person.schema.json)