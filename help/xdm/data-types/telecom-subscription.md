---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;telecom;subscription;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Telecom-abonnement
description: Leer over het gegevenstype van de Gegevens van de Ervaring van Telecom Model (XDM).
exl-id: d67915b6-daaa-489f-81b4-bd3dbe0ffa44
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 1%

---

# [!UICONTROL Telecom Subscription] gegevenstype

[!UICONTROL Telecom Subscription] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details voor specifieke types van telecommunicatieabonnement, zoals Internet, mobiel, media, of landline beschrijft.

>[!NOTE]
>
>In dit document wordt het gegevenstype beschreven. Voor de veldgroep met dezelfde naam raadpleegt u de [[!UICONTROL Telecom Subscription] Referentiehandleiding voor veldgroep](../field-groups/profile/telecom-subscription.md).
>
>Als u een abonnementstype beschrijft dat niet met de telecommunicatiesector verwant is, gelieve te gebruiken generiek [[!UICONTROL Subscription] gegevenstype](./subscription.md) in plaats daarvan.

![Telecom Subscription Structure](../images/data-types/telecom-subscription/structure.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `devices` | Array van objecten | Beschrijft een lijst van apparaten en/of toebehoren verbonden aan het plan. Zie de [sectie hieronder](#devices) voor meer informatie over de verwachte structuur van elk arrayitem. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschrijft de eigenaar van het abonnement. |
| `ID` | String | Een unieke id voor het abonnementsexemplaar. |
| `billingPeriod` | String | De duur tussen factureringen. |
| `billingStartDate` | Datum | De datum waarop de factureringsperiode begint. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `chargeMethod` | String | De manier waarop de facturering wordt ingesteld om de klant in rekening te brengen. |
| `contractID` | String | De unieke id voor het contract dat dit abonnement regelt. |
| `country` | String | Het land waarin de contractvoorwaarden voor de inschrijving en de overeenkomst zijn geworteld. |
| `endDate` | Datum | De datum waarop de huidige abonnementsduur afloopt. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `paymentDueDate` | Datum | De datum waarop de abonnementsbetaling verschuldigd is. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `paymentMethod` | String | De betalingsmethode voor terugkerende betalingen. |
| `paymentStatus` | String | De betalingsstatus van de rekening. |
| `planName` | String | De leesbare naam voor het abonnement. |
| `reason` | String | De algemene intentie van het lid voor het gebruik van het abonnement. |
| `renew` | String | De overeengekomen manier waarop het abonnement na de einddatum kan worden voortgezet. |
| `startDate` | Datum | De datum waarop het abonnement begint. De datumnotatie (zonder tijd) moet de [RFC 3339, punt 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) standaard. |
| `status` | String | De huidige status van het abonnement. |
| `subscriptionCategory` | String | De belangrijkste categorisering op hoofdniveau van dit type abonnement. |
| `subscriptionSKU` | String | De voorraadbewaareenheid (SKU) voor het abonnement. |
| `subscriptionSubCategory` | String | De specifieke subcategorisering van het abonnement. |
| `term` | Geheel | De numerieke waarde van de abonnementstermijn. |
| `termUnitOfTime` | String | De tijdseenheid voor de periode. |
| `topUp` | String | Beschrijft de overeengekomen voorwaarden voor hoe de verbruiksaspecten van een abonnement tijdens een factureringsperiode worden teruggekocht. |
| `type` | String | De omvang van het recht in verhouding tot het aantal personen dat onder het abonnement valt. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` is een array van objecten, waarbij elk object een apparaat of accessoire beschrijft dat aan het abonnement is gekoppeld.

![Apparaatarraystructuur](../images/data-types/telecom-subscription/devices.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `deviceFees` | Object | Een voorwerp dat om het even welke apparatenkosten voor punten zoals routers, modems, en ontvangers vangt. Verwacht de volgende eigenschappen:<ul><li>`amount`: Het bedrag in geld zoals vertegenwoordigd door de `currencyCode`.</li><li>`conversionDate`: De datum waarop de valutaomrekening heeft plaatsgevonden.</li><li>`currencyCode`: De [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) valutacode voor de `amount`.</li></ul> |
| `ID` | String | Een unieke id voor het apparaat. |
| `OS` | String | Het apparaat besturingssysteem. |
| `deviceInsurance` | String | Geeft aan of een klant zich heeft aangemeld voor verzekering voor dit apparaat. |
| `manufacturer` | String | De apparaatfabrikant. |
| `name` | String | Een naam voor het apparaat. |
| `paymentOptions` | String | Geeft aan of het apparaat in termijnen of tegen de volledige detailhandelsprijs wordt betaald. |
| `serialNumber` | String | Het serienummer van het apparaat. |
| `status` | String | De apparaatstatus. |
| `storageCapacity` | String | De opslagcapaciteit van het apparaat. |
| `type` | String | Het apparaattype. |

{style="table-layout:auto"}
