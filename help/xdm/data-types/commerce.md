---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;gebieden;schema's;Schema's;handel;datatype;data-type;gegevenstype;
solution: Experience Platform
title: Gegevenstype Handel
topic: overview
description: Dit document verstrekt een overzicht van het gegevenstype van het Model van de Gegevens van de Ervaring van de Handel (XDM).
translation-type: tm+mt
source-git-commit: 8bbb062df47b6e94630626d0a89a179d759d922d
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# [!UICONTROL Het type ] Commercedata

[!UICONTROL De ] handel is een standaard het gegevenstype van de Gegevens van de Ervaring Model (XDM) dat de verslagen met betrekking tot aankoop en verkoopactiviteit beschrijft.

<img src="../images/data-types/commerce.PNG" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `order` | [[!UICONTROL Volgorde]](./order.md) | Beschrijft de geplaatste orde voor één of meerdere producten. |
| `cartAbandons` | [[!UICONTROL Meetlat]](./measure.md) | Wordt gebruikt om te beschrijven wanneer een productlijst is geïdentificeerd als niet meer toegankelijk of te koop door de gebruiker. |
| `checkouts` | [[!UICONTROL Meetlat]](./measure.md) | Een actie tijdens het afrekenen van een productlijst. Er kunnen meerdere uitcheckgebeurtenissen zijn als er meerdere stappen in een uitcheckproces zijn. Als er meerdere stappen zijn, worden de informatie over de tijd van de gebeurtenis en de pagina waarnaar wordt verwezen of de ervaring gebruikt om de stap en de afzonderlijke gebeurtenissen in volgorde te identificeren. |
| `inStorePurchase` | [[!UICONTROL Meetlat]](./measure.md) | Beschrijft een waarde verbonden aan een in-store aankoop voor analysegebruik. |
| `productListAdds` | [[!UICONTROL Meetlat]](./measure.md) | De toevoeging van een product aan de productlijst, zoals een product dat aan een winkelwagentje wordt toegevoegd. |
| `productListOpens` | [[!UICONTROL Meetlat]](./measure.md) | De initialisaties van een nieuwe productlijst, zoals een winkelwagentje dat wordt gemaakt. |
| `productListRemovals` | [[!UICONTROL Meetlat]](./measure.md) | Het verwijderen of verwijderen van een product uit een productlijst, zoals een product dat uit een winkelwagentje wordt verwijderd. |
| `productListReopens` | [[!UICONTROL Meetlat]](./measure.md) | Een productlijst die eerder werd verlaten die door de gebruiker opnieuw is geactiveerd. |
| `productListViews` | [[!UICONTROL Meetlat]](./measure.md) | Beschrijft wanneer een mening of meningen van een productlijst zijn voorgekomen. |
| `productViews` | [[!UICONTROL Meetlat]](./measure.md) | Beschrijft wanneer een mening of meningen van een individueel product zijn voorgekomen. |
| `purchases` | [[!UICONTROL Meetlat]](./measure.md) | Wordt gebruikt om bij te houden wanneer een bestelling is geaccepteerd. De aankoopgebeurtenis is de enige vereiste actie bij een commerciële conversie. Er moet naar de aankoopgebeurtenis worden verwezen in een productlijst. |
| `saveForLaters` | [[!UICONTROL Meetlat]](./measure.md) | Een productlijst wordt opgeslagen voor toekomstig gebruik, zoals een verlanglijst. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over het gegevenstype:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json)