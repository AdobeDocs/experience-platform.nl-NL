---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;handel;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Handel
topic-legacy: overview
description: Dit document verstrekt een overzicht van het gegevenstype van het Model van de Gegevens van de Ervaring van de Handel (XDM).
exl-id: c9cc569b-1a91-4a6e-8bfd-7f8ec07d01d4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# [!UICONTROL Commerce] gegevenstype

[!UICONTROL Commerce] is een standaardgegevenstype van het Gegevensmodel van de Ervaring (XDM) dat de verslagen met betrekking tot aankoop en verkoopactiviteit beschrijft.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `order` | [[!UICONTROL Order]](./order.md) | Beschrijft de geplaatste orde voor één of meerdere producten. |
| `cartAbandons` | [[!UICONTROL Measure]](./measure.md) | Wordt gebruikt om te beschrijven wanneer een productlijst is geïdentificeerd als niet meer toegankelijk of te koop door de gebruiker. |
| `checkouts` | [[!UICONTROL Measure]](./measure.md) | Een actie tijdens het afrekenen van een productlijst. Er kunnen meerdere uitcheckgebeurtenissen zijn als er meerdere stappen in een uitcheckproces zijn. Als er meerdere stappen zijn, worden de informatie over de tijd van de gebeurtenis en de pagina waarnaar wordt verwezen of de ervaring gebruikt om de stap en de afzonderlijke gebeurtenissen in volgorde te identificeren. |
| `inStorePurchase` | [[!UICONTROL Measure]](./measure.md) | Beschrijft een waarde verbonden aan een in-store aankoop voor analysegebruik. |
| `productListAdds` | [[!UICONTROL Measure]](./measure.md) | De toevoeging van een product aan de productlijst, zoals een product dat aan een winkelwagentje wordt toegevoegd. |
| `productListOpens` | [[!UICONTROL Measure]](./measure.md) | De initialisaties van een nieuwe productlijst, zoals een winkelwagentje dat wordt gemaakt. |
| `productListRemovals` | [[!UICONTROL Measure]](./measure.md) | Het verwijderen of verwijderen van een product uit een productlijst, zoals een product dat uit een winkelwagentje wordt verwijderd. |
| `productListReopens` | [[!UICONTROL Measure]](./measure.md) | Een productlijst die eerder werd verlaten die door de gebruiker opnieuw is geactiveerd. |
| `productListViews` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een mening of meningen van een productlijst zijn voorgekomen. |
| `productViews` | [[!UICONTROL Measure]](./measure.md) | Beschrijft wanneer een mening of meningen van een individueel product zijn voorgekomen. |
| `purchases` | [[!UICONTROL Measure]](./measure.md) | Wordt gebruikt om bij te houden wanneer een bestelling is geaccepteerd. De aankoopgebeurtenis is de enige vereiste actie bij een commerciële conversie. Er moet naar de aankoopgebeurtenis worden verwezen in een productlijst. |
| `saveForLaters` | [[!UICONTROL Measure]](./measure.md) | Een productlijst wordt opgeslagen voor toekomstig gebruik, zoals een verlanglijst. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)
