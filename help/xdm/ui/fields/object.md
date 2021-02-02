---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;object;field;
solution: Experience Platform
title: Een objectveld definiëren in de gebruikersinterface
description: Leer hoe u een objecttype-veld definieert in de gebruikersinterface van het Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 2e20403122e65d28f04114af9b7e8d41874f76e2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Een objectveld definiëren in de gebruikersinterface

Met Adobe Experience Platform kunt u de structuur van uw aangepaste Experience Data Model-klassen, -mixen en -gegevenstypen volledig aanpassen. Als u gerelateerde velden wilt ordenen en nesten in aangepaste XDM-bronnen, kunt u objecttype-velden definiëren die aanvullende subvelden kunnen bevatten.

Als [een nieuw veld](./overview.md#define) in de Adobe Experience Platform-gebruikersinterface definieert, gebruikt u het vervolgkeuzemenu **[!UICONTROL Type]** en selecteert u &quot;[!UICONTROL Object]&quot; in de lijst.

![](../../images/ui/fields/special/object.png)

Selecteer **[!UICONTROL Toepassen]** om het object aan het schema toe te voegen. Het canvas wordt bijgewerkt om het nieuwe veld weer te geven met het gegevenstype [!UICONTROL Object] toegepast, inclusief besturingselementen voor het bewerken en toevoegen van subvelden aan het object.

![](../../images/ui/fields/special/object-applied.png)

Als u een subveld wilt toevoegen, selecteert u het pictogram **plus (+)** naast het objectveld op het canvas. Onder het object wordt een nieuw veld weergegeven met besturingselementen voor het configureren van het subveld in het rechterspoor.

![](../../images/ui/fields/special/object-add-field.png)

Nadat u het subveld hebt geconfigureerd en **[!UICONTROL Toepassen]** hebt geselecteerd, kunt u velden aan het object blijven toevoegen met hetzelfde proces. U kunt ook subvelden toevoegen die zelf objecten zijn, zodat u velden zo diep kunt nesten als u wilt.

![](../../images/ui/fields/special/object-nested.png)

Wanneer u klaar bent met het maken van het object, zult u merken dat u de structuur ervan in verschillende klassen en mixen wilt hergebruiken. In dat geval kunt u het object omzetten in een gegevenstype. Zie de sectie over [het omzetten van voorwerpen in gegevenstypes](../resources/data-types.md#convert) in de gids UI van gegevenstypes voor meer informatie.

## Volgende stappen

In deze handleiding wordt beschreven hoe u een objectveld in de gebruikersinterface definieert. Zie het overzicht op [het bepalen van gebieden in UI](./overview.md#special) om te leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.
