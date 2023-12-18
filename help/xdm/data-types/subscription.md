---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Abonnement;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Gegevenstype abonnement
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Abonnement (XDM).
exl-id: 6fd1e073-441b-45f0-bb4f-54f51ab18694
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 1%

---

# [!UICONTROL Subscription] gegevenstype

[!UICONTROL Subscription] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat vergunning gegeven aanspraken op software, de diensten, of goederen beschrijft die op tijd of gebruik worden gebruikt.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [[!UICONTROL Device]](./device.md) | Beschrijft details over het apparaat dat met het abonnement verbonden is. |
| `environment` | [[!UICONTROL Environment]](./environment.md) | Bevat informatie over de omringende situatie de gebeurtenisobservatie voorkwam, specifiek die voorbijgaande informatie zoals de netwerk of softwareversies specificeert. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschrijft een individuele persoon. Dit kan ook een persoon vertegenwoordigen die in diverse rollen, zoals een klant, een contact, of een eigenaar handelt. |
| `SKU` | String | De voorraadeenheid (SKU), een unieke identificatiecode voor een product. |
| `billingPeriod` | String | De duur tussen factureringen. |
| `billingStartDate` | Datum | De datum waarop de eerste rekening verschuldigd is. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `category` | String | De belangrijkste categorisering op hoofdniveau van dit type abonnement. |
| `chargeMethod` | String | De manier waarop de facturering wordt ingesteld om de klant in rekening te brengen. |
| `contractID` | String | De unieke id voor het contract dat dit abonnement regelt. |
| `country` | String | Het land waarin de contractvoorwaarden voor de inschrijving en de overeenkomst zijn geworteld. |
| `endDate` | Datum | De datum waarop de huidige abonnementsduur afloopt. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `paymentMethod` | String | De betalingsmethode voor terugkerende betalingen. |
| `paymentStatus` | String | De betalingsstatus van de rekening. |
| `planName` | String | De leesbare naam voor het abonnement. |
| `reason` | String | De algemene intentie van het lid voor het gebruik van het abonnement. |
| `renew` | String | De overeengekomen manier waarop het abonnement na de einddatum kan worden voortgezet. |
| `revision` | String | De identificatie tussen abonnementen van dezelfde naam en categoriehiërarchie. |
| `startDate` | Datum | De datum waarop het abonnement begint. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `status` | String | De huidige status van het abonnement. |
| `subCategory` | String | De specifieke subcategorisering van het abonnement. |
| `term` | Geheel | De numerieke waarde van de abonnementstermijn. |
| `termUnitOfTime` | String | De tijdseenheid voor de periode. |
| `topUp` | String | Beschrijft de overeengekomen voorwaarden voor hoe de verbruiksaspecten van een abonnement tijdens een factureringsperiode worden teruggekocht. |
| `type` | String | De omvang van het recht in verhouding tot het aantal personen dat onder het abonnement valt. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)
