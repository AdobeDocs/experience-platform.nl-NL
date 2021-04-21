---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;array;field;
solution: Experience Platform
title: Arrayvelden definiëren in de gebruikersinterface
description: Leer hoe u een arrayveld definieert in de gebruikersinterface van het Experience Platform.
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# Arrayvelden definiëren in de gebruikersinterface

Wanneer u een XDM-veld (Experience Data Model) in de Adobe Experience Platform-gebruikersinterface definieert, kunt u dat veld toewijzen als een array.

De inhoud van de array is afhankelijk van de [!UICONTROL Type] die voor dat veld is geselecteerd. Als bijvoorbeeld [!UICONTROL Type] van een veld is ingesteld op &quot;[!UICONTROL String]&quot;, geeft het instellen van dat veld als een array het veld aan als een array van tekenreeksen. Als [!UICONTROL Type] van het gebied aan een multi-field gegevenstype zoals &quot;[!UICONTROL Postal address]&quot;wordt geplaatst, dan zou het een serie van post-adresvoorwerpen worden die met het gegevenstype in overeenstemming zijn.

Nadat u [een nieuw gebied in UI](./overview.md#define) hebt bepaald, kunt u het als seriegebied plaatsen door **[!UICONTROL Array]** checkbox in het juiste spoor te selecteren.

![](../../images/ui/fields/special/array.png)

Als het selectievakje is ingeschakeld, worden in de rechtertrack extra besturingselementen weergegeven waarmee u de array eventueel verder kunt beperken. Als u een bepaalde beperking niet wilt afdwingen, laat u het veld leeg.

De extra configuratiecontroles voor series zijn als volgt:

| Field, eigenschap | Beschrijving |
| --- | --- |
| [!UICONTROL Minimum length] | Het minimale aantal items dat de array moet bevatten om de opname te laten slagen. |
| [!UICONTROL Maximum length] | Het maximum aantal items dat de array moet bevatten om de opname te laten slagen. |
| [!UICONTROL Unique items only] | Indien ingesteld op &quot;[!UICONTROL True]&quot;, moet elk item in de array uniek zijn om de opname te laten slagen. |

Wanneer u klaar bent met het configureren van het veld, selecteert u **[!UICONTROL Apply]** om de wijziging toe te passen op het schema.

![](../../images/ui/fields/special/array-config.png)

Het canvas wordt bijgewerkt met de wijzigingen die in het veld zijn aangebracht. Het gegevenstype dat naast de veldnaam op het canvas wordt weergegeven, wordt met twee vierkante haakjes (`[]`) toegevoegd om aan te geven dat het veld een array van dat gegevenstype vertegenwoordigt.

![](../../images/ui/fields/special/array-applied.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u een arrayveld in de gebruikersinterface definieert. Zie het overzicht op [het bepalen van gebieden in UI](./overview.md#special) om te leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.
