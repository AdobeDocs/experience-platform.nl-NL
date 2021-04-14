---
title: Typen gegevenselementen in de Adobe Experience Platform Web SDK-extensie
description: Leer over de verschillende types van gegevenselement die door de uitbreiding van SDK van het Web van Adobe Experience Platform in Adobe Experience Platform Launch worden verstrekt.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
translation-type: tm+mt
source-git-commit: 3f7808a08d033c5940d2115006c269b8c4079822
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Gegevenstelelementtypen

Nadat u uw [actietypes](action-types.md) in [de uitbreiding van SDK van het Web van Adobe Experience Platform ](web-sdk-extension.md) voor [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) plaatst, vorm uw types van gegevenselement.

Op deze pagina worden de beschikbare gegevenselemetypen beschreven.

## Samenvoegings-id gebeurtenis

Dit gegevenselement verstrekt een identiteitskaart van de gebeurtenisfusie wanneer gebruikt. Er is geen configuratie nodig voor dit gegevenselement. Het gegevenselement dat wordt opgegeven, blijft hetzelfde totdat de bezoeker de pagina verlaat of totdat het handelingstype &quot;Id van handeling voor samenvoegen van gebeurtenissen opnieuw instellen&quot; wordt gebruikt.

## Identiteitskaart

Met het gegevenselement voor identiteitskaarten kunt u identiteiten maken op basis van andere gegevenselementen of andere waarden die u opgeeft. Alle identiteiten die u maakt, moeten worden gekoppeld aan een bijbehorende naamruimte. Dit gegevenselement bevat een vervolgkeuzelijst met alle standaardnaamruimten en alle gemaakte naamruimten.

![](./assets/identity-map-data-element.png)

## XDM-object {#xdm-object}

Gebruik XDM-indeling om gegevens naar de Adobe Experience Platform Web SDK te verzenden. Het formatteren van uw gegevens is gemakkelijker met het XDM objectelement. Wanneer u dit gegevenselement voor het eerst opent, selecteert u de juiste Adobe Experience Platform-sandbox en -schema. Nadat u het schema hebt geselecteerd, ziet u de structuur van uw schema, dat u gemakkelijk kunt invullen.

![](./assets/XDM-object.png)

Wanneer u bepaalde velden in uw schema opent, zoals `web.webPageDetails.URL`, worden sommige items automatisch verzameld. Hoewel meerdere items automatisch worden verzameld, kunt u indien nodig alle items overschrijven. Alle waarden kunnen handmatig of met andere gegevenselementen worden ingevuld.

>[!NOTE]
>
>Vul alleen de gegevens in die u wilt verzamelen. Alles wat niet is ingevuld, wordt weggelaten wanneer de gegevens naar de oplossingen worden verzonden.
