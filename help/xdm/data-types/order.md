---
keywords: Experience Platform;home;populaire onderwerpen;schema;Schema;XDM;velden;schema's;Schema's;order;datatype;data-type;data-type;
solution: Experience Platform
title: Gegevenstype Volgorde
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Orde (XDM).
exl-id: abfc6d53-ffe6-4692-ad65-03d556831fa0
source-git-commit: 09ca510da0819ab38687edadbcc632ccbbe8ef83
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# [!UICONTROL Order] gegevenstype

[!UICONTROL Order] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de orde beschrijft die voor een productlijst wordt geplaatst.

![&#x200B; een diagram van het [!UICONTROL Order] gegevenstype.](../images/data-types/order.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|-------------------------|-------------------------|-----------|------------------------------------------------------------------------------------------------------------------|
| Aankoop-id | `purchaseID` | String | Een unieke id die door de verkoper is toegewezen voor deze aankoop of dit contract. Er is geen garantie dat de id uniek is, omdat de id door de verkoper is gedefinieerd. |
| Inkoopordernummer | `purchaseOrderNumber` | String | Een unieke id die door de koper voor deze aankoop of dit contract is toegewezen. |
| Betalingslijst | `payments` | Array van [[!UICONTROL Payment Items]](./payment-item.md) | De lijst met betalingen voor deze bestelling. Betalingen worden in detail beschreven in de [!UICONTROL Payment Items] -specificatie. |
| Restitutielijst | `refunds` | Array van [[!UICONTROL Refund Items]](./refund-item.md) | De lijst van terugbetalingen voor deze bestelling. Restituties worden beschreven in de [!UICONTROL Refund Items] -specificatie. |
| Retourinformatie | `returns` | [[!UICONTROL Return Info]](./return.md) | De afgegeven RMA (Return Merchandise Authorization). Retourneert u in detail in de [!UICONTROL Return Info] specificatie. |
| Valuta | `currencyCode` | String | De ISO 4217-valutacode die wordt gebruikt voor de totalen van de orders. Voorbeelden zijn `USD` en `EUR` . Alle instanties moeten overeenkomen met het patroon `^[A-Z]{3}$` . |
| Belastingbedrag | `taxAmount` | Getal | Het belastingbedrag dat de koper in het kader van de eindbetaling heeft betaald. |
| Korting | `discountAmount` | Getal | Het verschil tussen de normale prijs en de speciale prijs die van toepassing is op de gehele bestelling en niet op afzonderlijke producten. |
| Prijs totaal | `priceTotal` | Getal | De totale prijs van deze bestelling nadat alle kortingen en belastingen zijn toegepast. |
| Ordertype | `orderType` | String | Het type volgorde dat is geplaatst. Mogelijke waarden zijn `checkout` en `instant_purchase` . |
| Laatst bijgewerkt op | `lastUpdatedDate` | String | Het tijdstip waarop een bepaalde orderrecord voor het laatst is bijgewerkt in het handelssysteem. Indeling: datum en tijd. |
| Aanmaakdatum | `createdDate` | String | De tijd/datum wanneer een nieuwe orde in het handelssysteem wordt gecreeerd. Indeling: datum en tijd. |
| Datum annuleren | `cancelDate` | String | De datum/tijd waarop een orderannulering door de verkoper wordt geïnitieerd. Indeling: datum en tijd. |
| Totaal terugbetaald bedrag | `refundTotal` | Getal | Het totale bedrag dat in deze restitutie op de bestelling is vermeld, waarbij alle terugbetaalde objecten worden gecombineerd, na aftrek van kortingen enz. zijn toegepast. |

{style="table-layout:auto"}

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [&#x200B; Bevolkt voorbeeld &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.example.1.json)
* [&#x200B; Volledig schema &#x200B;](https://github.com/adobe/xdm/blob/master/components/datatypes/data/order.schema.json)
