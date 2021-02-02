---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;Abonnement;datatype;data-type;gegevenstype.
solution: Experience Platform
title: Gegevenstype abonnement
topic: overview
description: Dit document biedt een overzicht van het gegevenstype Subscription Experience Data Model (XDM).
translation-type: tm+mt
source-git-commit: 8ccf0a53f231c9f59cd87735126b180c6b678e51
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 8%

---


# [!UICONTROL Het type ] SubscriptData

 Abonnement is een standaard XDM-gegevenstype (Experience Data Model) waarmee gelicentieerde rechten op software, services of goederen worden beschreven die worden gebruikt op basis van tijd of gebruik.

<img src="../images/data-types/subscription-data-type.png" width="500" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `device` | [[!UICONTROL Apparaat]](./device.md) | Beschrijft details over het apparaat dat met het abonnement verbonden is. |
| `environment` | [[!UICONTROL Omgeving]](./environment.md) | Bevat informatie over de omringende situatie de gebeurtenisobservatie voorkwam, specifiek die voorbijgaande informatie zoals de netwerk of softwareversies specificeert. |
| `subscriber` | [[!UICONTROL Persoon]](./person.md) | Beschrijft een individuele persoon. Dit kan ook een persoon vertegenwoordigen die in diverse rollen, zoals een klant, een contact, of een eigenaar handelt. |
| `SKU` | Tekenreeks | De voorraadeenheid (SKU), een unieke identificatiecode voor een product. |
| `billingPeriod` | Tekenreeks | De duur tussen factureringen. |
| `billingStartDate` | Datum | De datum waarop de eerste rekening verschuldigd is. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `category` | Tekenreeks | De belangrijkste categorisering op hoofdniveau van dit type abonnement. |
| `chargeMethod` | Tekenreeks | De manier waarop de facturering wordt ingesteld om de klant in rekening te brengen. |
| `contractID` | Tekenreeks | De unieke id voor het contract dat dit abonnement regelt. |
| `country` | Tekenreeks | Het land waarin de contractvoorwaarden voor de inschrijving en de overeenkomst zijn geworteld. |
| `endDate` | Datum | De datum waarop de huidige abonnementsduur afloopt. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `paymentMethod` | Tekenreeks | De betalingsmethode voor terugkerende betalingen. |
| `paymentStatus` | Tekenreeks | De betalingsstatus van de rekening. |
| `planName` | Tekenreeks | De leesbare naam voor het abonnement. |
| `reason` | Tekenreeks | De algemene intentie van het lid voor het gebruik van het abonnement. |
| `renew` | Tekenreeks | De overeengekomen manier waarop het abonnement na de einddatum kan worden voortgezet. |
| `revision` | Tekenreeks | De identificatie tussen abonnementen van dezelfde naam en categoriehiërarchie. |
| `startDate` | Datum | De datum waarop het abonnement begint. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `status` | Tekenreeks | De huidige status van het abonnement. |
| `subCategory` | Tekenreeks | De specifieke subcategorisering van het abonnement. |
| `term` | Geheel | De numerieke waarde van de abonnementstermijn. |
| `termUnitOfTime` | Tekenreeks | De tijdseenheid voor de periode. |
| `topUp` | Tekenreeks | Beschrijft de overeengekomen voorwaarden voor hoe de verbruiksaspecten van een abonnement tijdens een factureringsperiode worden teruggekocht. |
| `type` | Tekenreeks | De omvang van het recht in verhouding tot het aantal personen dat onder het abonnement valt. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)