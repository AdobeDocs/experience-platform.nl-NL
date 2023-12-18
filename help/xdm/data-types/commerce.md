---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;handel;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Handel
description: Leer over het gegevenstype van het Gegevensmodel van de Ervaring van de Handel (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
source-git-commit: f70ca0d8ab0e92cc0e1007021c0778361701dc84
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 0%

---

# [!UICONTROL Commerce] gegevenstype

[!UICONTROL Commerce] is een standaard gegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de verslagen met betrekking tot het kopen en het verkopen beschrijft.

![Een schema van de [!UICONTROL Commerce] gegevenstype.](../images/data-types/commerce.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|------------------------------------------|-----------------------|------------------------------------|----------------------------------------------------------------------------------------------------------|
| [!UICONTROL Order] | `order` | [[!UICONTROL Order]](./order.md) | Beschrijft de geplaatste orde voor één of meerdere producten. |
| [!UICONTROL Promotion ID] | `promotionID` | [!UICONTROL string] | Een promotie-id voor de geplaatste order, indien aanwezig. |
| [!UICONTROL Cart Abandons] | `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een productlijst is geïdentificeerd als niet meer toegankelijk of te kopen door de gebruiker. |
| [!UICONTROL Checkouts] | `checkouts` | [[!UICONTROL Measure]](./measure.md) | Een actie tijdens het afrekenen van een productlijst. Er kunnen meer dan één uitcheckgebeurtenis zijn als er meerdere stappen in een uitcheckproces zijn. Als er meerdere stappen zijn, worden de informatie over de tijd van de gebeurtenis en de pagina waarnaar wordt verwezen of de ervaring gebruikt om de stap en de afzonderlijke gebeurtenissen in volgorde te identificeren. |
| [!UICONTROL Product List (Cart) Adds] | `productListAdds` | [[!UICONTROL Measure]](./measure.md) | De toevoeging van een product aan de productlijst, zoals een product dat aan een winkelwagentje wordt toegevoegd. |
| [!UICONTROL Product List (Cart) Opens] | `productListOpens` | [[!UICONTROL Measure]](./measure.md) | De initialisaties van een nieuwe productlijst, zoals een winkelwagentje dat wordt gemaakt. |
| [!UICONTROL Product List (Cart) Removals] | `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | Het verwijderen of verwijderen van een product uit een productlijst, zoals een product dat uit een winkelwagentje wordt verwijderd. |
| [!UICONTROL Product List (Cart) Reopens] | `productListReopens` | [[!UICONTROL Measure]](./measure.md) | Een productlijst die eerder werd verlaten die door de gebruiker opnieuw is geactiveerd. |
| [!UICONTROL Product List (Cart) Views] | `productListViews` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een mening of meningen van een productlijst is voorgekomen.Mening of meningen van een product-lijst is voorgekomen. |
| [!UICONTROL Product Views] | `productViews` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een mening of meningen van een individueel product zijn voorgekomen. |
| [!UICONTROL Purchases] | `purchases` | [[!UICONTROL Measure]](./measure.md) | Wordt gebruikt om bij te houden wanneer een bestelling is geaccepteerd. De aankoopgebeurtenis is de enige vereiste actie bij een commerciële conversie. Er moet naar de aankoopgebeurtenis worden verwezen in een productlijst. |
| [!UICONTROL Save For Laters] | `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een productlijst voor toekomstig gebruik, zoals een verlanglijst wordt bewaard. |
| [!UICONTROL In Store Purchase] | `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | Hiermee wordt een &#39;inStore&#39;-aankoop aangegeven. Deze informatie wordt opgeslagen voor gebruik in analysemogelijkheden. |
| [!UICONTROL Cart] | `cart` | [[!UICONTROL cart]](./cart.md) | De eigenschappen van de kar die een of meer producten bevat. |
| [!UICONTROL Shipping] | `shipping` | [[!UICONTROL shipping]](./shipping.md) | De verzendgegevens voor een of meer producten. |
| [!UICONTROL Billing] | `billing` | [[!UICONTROL billing]](#billing) | De factureringsgegevens voor een of meer betalingen. |
| [!UICONTROL Instant Purchase] | `instantPurchase` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een product onmiddellijk is gekocht, potentieel overslaat het karretje of de kar. |
| [!UICONTROL Requisition List Opens] | `requisitionListOpens` | [[!UICONTROL Measure]](./measure.md) | Geeft de initialisatie van een nieuwe aanvraaglijst aan. |
| [!UICONTROL Requisition List Deletes] | `requisitionListDeletes` | [[!UICONTROL Measure]](./measure.md) | Geeft de verwijdering van de aanvraaglijst aan. |
| [!UICONTROL Requisition List Adds] | `requisitionListAdds` | [[!UICONTROL Measure]](./measure.md) | Hiermee wordt de toevoeging van een of meer producten aan een aanvraaglijst aangegeven. |
| [!UICONTROL Requisition List Removals] | `requisitionListRemovals` | [[!UICONTROL Measure]](./measure.md) | Geeft aan dat een product of producten uit een productlijst van een aanvraag is verwijderd. |
| [!UICONTROL Requisition List] | `requisitionList` | [[!UICONTROL requisitionlist]](./requisition-list.md) | De eigenschappen van een aanvraaglijst die door de klant is gemaakt. |
| [!UICONTROL Scope] | `commerceScope` | [[!UICONTROL commercescope]](./commerce-scope.md) | De handelingswerkingsgebiedherkenningstekens van waar een gebeurtenis (opslagmening, opslag, website, enz.) voorkwam. |

{style="table-layout:auto"}

## [!UICONTROL billing] gegevenstype {#billing}

[!UICONTROL billing] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat informatie over het factureren details bevat. Specifiek, concentreert het zich op het factureringsadres.

![Een diagram van het gegevenstype voor facturering.](../images/data-types/billing.png)

| Weergavenaam | Eigenschap | Gegevenstype | Beschrijving |
|-------------------------------|-----------------|-----------------|--------------------------|
| [!UICONTROL Billing Address] | `address` | [[!UICONTROL Postal Address]](./postal-address.md) | Het factureringsadres. |

{style="table-layout:auto"}

Voor meer informatie over de [!UICONTROL Commerce] gegevenstype, verwijs naar de openbare bewaarplaats XDM:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
