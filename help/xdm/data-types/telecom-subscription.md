---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schemas;telecom;subscription;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Telecom-abonnement
topic-legacy: overview
description: Dit document verstrekt een overzicht van het de gegevenstype van de Gegevens van de Ervaring van Telecom Model (XDM).
source-git-commit: 19675e4042c28061a4b2ed4e68374d5e09216ba1
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 8%

---

# [!UICONTROL Telecom Subscription] gegevenstype

[!UICONTROL Telecom Subscription] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat details voor specifieke types van telecommunicatieabonnement, zoals Internet, mobiel, media, of landline beschrijft.

>[!NOTE]
>
>In dit document wordt het gegevenstype beschreven. Voor de gebiedsgroep van de zelfde naam, verwijs naar [[!UICONTROL Telecom Subscription] de verwijzingsgids van de gebiedsgroep](../field-groups/profile/telecom-subscription.md).
>
>Als u een abonnementstype beschrijft dat niet met de telecommunicatiesector verwant is, gelieve algemeen [[!UICONTROL Subscription] gegevenstype ](./subscription.md) in plaats daarvan te gebruiken.

![Telecom Subscription Structure](../images/data-types/telecom-subscription/structure.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `devices` | Array van objecten | Beschrijft een lijst van apparaten en/of toebehoren verbonden aan het plan. Zie de [sectie hieronder](#devices) voor details over de verwachte structuur van elk seriepunt. |
| `subscriber` | [[!UICONTROL Person]](./person.md) | Beschrijft de eigenaar van het abonnement. |
| `ID` | Tekenreeks | Een unieke id voor het abonnementsexemplaar. |
| `billingPeriod` | Tekenreeks | De duur tussen factureringen. |
| `billingStartDate` | Datum | De datum waarop de factureringsperiode begint. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `chargeMethod` | Tekenreeks | De manier waarop de facturering wordt ingesteld om de klant in rekening te brengen. |
| `contractID` | Tekenreeks | De unieke id voor het contract dat dit abonnement regelt. |
| `country` | Tekenreeks | Het land waarin de contractvoorwaarden voor de inschrijving en de overeenkomst zijn geworteld. |
| `endDate` | Datum | De datum waarop de huidige abonnementsduur afloopt. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `paymentDueDate` | Datum | De datum waarop de abonnementsbetaling verschuldigd is. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `paymentMethod` | Tekenreeks | De betalingsmethode voor terugkerende betalingen. |
| `paymentStatus` | Tekenreeks | De betalingsstatus van de rekening. |
| `planName` | Tekenreeks | De leesbare naam voor het abonnement. |
| `reason` | Tekenreeks | De algemene intentie van het lid voor het gebruik van het abonnement. |
| `renew` | Tekenreeks | De overeengekomen manier waarop het abonnement na de einddatum kan worden voortgezet. |
| `startDate` | Datum | De datum waarop het abonnement begint. De datumnotatie (zonder tijd) moet de [RFC 3339, sectie 5.6](https://tools.ietf.org/html/rfc3339#section-5.6) norm volgen. |
| `status` | Tekenreeks | De huidige status van het abonnement. |
| `subscriptionCategory` | Tekenreeks | De belangrijkste categorisering op hoofdniveau van dit type abonnement. |
| `subscriptionSKU` | Tekenreeks | De voorraadbewaareenheid (SKU) voor het abonnement. |
| `subscriptionSubCategory` | Tekenreeks | De specifieke subcategorisering van het abonnement. |
| `term` | Geheel | De numerieke waarde van de abonnementstermijn. |
| `termUnitOfTime` | Tekenreeks | De tijdseenheid voor de periode. |
| `topUp` | Tekenreeks | Beschrijft de overeengekomen voorwaarden voor hoe de verbruiksaspecten van een abonnement tijdens een factureringsperiode worden teruggekocht. |
| `type` | Tekenreeks | De omvang van het recht in verhouding tot het aantal personen dat onder het abonnement valt. |

{style=&quot;table-layout:auto&quot;}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/industry-verticals/subscription.schema.json)

## `devices` {#devices}

`devices` is een array van objecten, waarbij elk object een apparaat of accessoire beschrijft dat aan het abonnement is gekoppeld.

![Apparaatarraystructuur](../images/data-types/telecom-subscription/devices.png)

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `deviceFees` | Object | Een voorwerp dat om het even welke apparatenkosten voor punten zoals routers, modems, en ontvangers vangt. Verwacht de volgende eigenschappen:<ul><li>`amount`: Het monetaire bedrag zoals vertegenwoordigd door de  `currencyCode`ECB.</li><li>`conversionDate`: De datum waarop de valutaomrekening heeft plaatsgevonden.</li><li>`currencyCode`: De  [ISO 4217](https://www.iso.org/iso-4217-currency-codes.html) valutacode voor de  `amount`.</li></ul> |
| `ID` | Tekenreeks | Een unieke id voor het apparaat. |
| `OS` | Tekenreeks | Het besturingssysteem van het apparaat. |
| `deviceInsurance` | Tekenreeks | Geeft aan of een klant zich heeft aangemeld voor verzekering voor dit apparaat. |
| `manufacturer` | Tekenreeks | De fabrikant van het apparaat. |
| `name` | Tekenreeks | Een naam voor het apparaat. |
| `paymentOptions` | Tekenreeks | Geeft aan of het apparaat in termijnen of tegen de volledige detailhandelsprijs wordt betaald. |
| `serialNumber` | Tekenreeks | Het serienummer van het apparaat. |
| `status` | Tekenreeks | De apparaatstatus. |
| `storageCapacity` | Tekenreeks | De opslagcapaciteit van het apparaat. |
| `type` | Tekenreeks | Het apparaattype. |

{style=&quot;table-layout:auto&quot;}