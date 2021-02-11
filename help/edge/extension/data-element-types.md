---
title: Platform Web SDK Extension Data Element Types
description: Adobe Experience Platform Web SDK Extension Data Element Types in Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Typen gegevenselementen

Nadat u uw [actietypes](action-types.md) in [de uitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension.md) voor [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) plaatst, vorm uw types van gegevenselement.

Op deze pagina worden de beschikbare gegevenselemetypen beschreven.

## Samenvoegings-id gebeurtenis

Dit gegevenselement verstrekt een identiteitskaart van de gebeurtenisfusie wanneer gebruikt. Er is geen configuratie nodig voor dit gegevenselement. Het gegevenselement dat wordt opgegeven, blijft hetzelfde totdat de bezoeker de pagina verlaat of totdat het handelingstype &quot;Id van handeling voor samenvoegen van gebeurtenissen opnieuw instellen&quot; wordt gebruikt.

## Identiteitskaart

Met het gegevenselement voor identiteitskaarten kunt u identiteiten maken op basis van andere gegevenselementen of andere waarden die u opgeeft. Alle identiteiten die u maakt, moeten worden gekoppeld aan een bijbehorende naamruimte. Dit gegevenselement bevat een vervolgkeuzelijst met alle standaardnaamruimten en alle ruimten die u hebt gemaakt.

![](./assets/identity-map-data-element.png)

## XDM-object

Alle gegevens die u naar de Adobe Experience Platform Web SDK verzendt, moeten de XDM-indeling hebben. Het formatteren van uw gegevens is gemakkelijker met het XDM objectelement. Wanneer u dit gegevenselement voor het eerst opent, selecteert u de juiste Adobe Experience Platform-sandbox en -schema. Nadat u het schema hebt geselecteerd, ziet u de structuur van het schema, dat u gemakkelijk kunt invullen.

![](./assets/XDM-object.png)

Wanneer u bepaalde velden in uw schema opent, zoals `web.webPageDetails.URL`, worden sommige items automatisch verzameld. Hoewel meerdere items automatisch worden verzameld, kunt u desgewenst alle items overschrijven. Alle waarden kunnen handmatig of met andere gegevenselementen worden ingevuld.

>[!NOTE]
>
>U hoeft alleen de gegevens in te vullen die u wilt verzamelen. Alles wat niet is ingevuld, wordt geactiveerd wanneer de gegevens naar de oplossingen worden verzonden.
