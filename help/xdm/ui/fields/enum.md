---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;enum;field;
solution: Experience Platform
title: Enum Fields definiëren in de UI
description: Leer hoe u een opsommingsveld definieert in de gebruikersinterface van het Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Enumvelden definiëren in de gebruikersinterface

In het Model van Gegevens van de Ervaring (XDM), vertegenwoordigt een enumgebied een gebied dat tot een vooraf bepaalde lijst van aanvaardbare waarden wordt beperkt.

Wanneer [een nieuw gebied](./overview.md#define) in het gebruikersinterface van Adobe Experience Platform bepaalt, kunt u het als enum gebied plaatsen door **[!UICONTROL Enum]** checkbox in het juiste spoor te selecteren.

![](../../images/ui/fields/special/enum.png)

Aanvullende besturingselementen worden weergegeven nadat u het selectievakje hebt ingeschakeld, zodat u de waardebeperkingen voor de opsomming kunt opgeven. Onder de **[!UICONTROL Waarde]** kolom, moet u de nauwkeurige waarde verstrekken u het gebied aan wilt beperken. Deze waarde moet voldoen aan [!UICONTROL Type] u voor het enumgebied selecteerde. U kunt optioneel ook een gebruiksvriendelijke **[!UICONTROL Label]** voor de beperking opgeven.

Als u aanvullende beperkingen aan de opsomming wilt toevoegen, selecteert u **[!UICONTROL Rij toevoegen]**.

![](../../images/ui/fields/special/enum-add-row.png)

Ga verder met het toevoegen van de gewenste restricties en optionele labels aan de opsomming. Als u klaar bent, selecteert u **[!UICONTROL Toepassen]** om de wijzigingen toe te passen op het schema.

![](../../images/ui/fields/special/enum-configured.png)

Het canvas wordt bijgewerkt met de wijzigingen. Wanneer u dit schema in de toekomst verkent, kunt u de beperkingen voor het enum gebied binnen het juiste spoor bekijken en uitgeven.

![](../../images/ui/fields/special/enum-applied.png)

## Volgende stappen

Deze handleiding besprak hoe u een opsommingsveld kunt definiëren in de gebruikersinterface. Zie het overzicht op [het bepalen van gebieden in UI](./overview.md#special) om te leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.