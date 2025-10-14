---
keywords: Experience Platform;home;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;array;field;
solution: Experience Platform
title: Arrayvelden definiëren in de gebruikersinterface
description: Leer hoe u een arrayveld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 0%

---

# Arrayvelden definiëren in de gebruikersinterface

Wanneer u een XDM-veld (Experience Data Model) in de Adobe Experience Platform-gebruikersinterface definieert, kunt u dat veld toewijzen als een array.

De inhoud van de array is afhankelijk van de geselecteerde [!UICONTROL Type] voor dat veld. Als een veld [!UICONTROL Type] bijvoorbeeld is ingesteld op &quot;[!UICONTROL String]&quot;, geeft het instellen van dat veld als een array het veld aan als een array van tekenreeksen. Als het gebied [!UICONTROL Type] aan een multi-gebiedsgegevenstype zoals &quot;[!UICONTROL Postal address]&quot;wordt geplaatst, dan zou het een serie van post-adresvoorwerpen worden die met het gegevenstype in overeenstemming zijn.

Nadat u [&#x200B; een nieuw gebied in UI &#x200B;](./overview.md#define) hebt bepaald, kunt u het als seriegebied plaatsen door **[!UICONTROL Array]** checkbox in het juiste spoor te selecteren.

![](../../images/ui/fields/special/array.png)

Als het selectievakje is ingeschakeld, worden in de rechtertrack extra besturingselementen weergegeven waarmee u de array eventueel verder kunt beperken. Als u een bepaalde beperking niet wilt afdwingen, laat u het veld leeg.

De extra configuratiecontroles voor series zijn als volgt:

| Field, eigenschap | Beschrijving |
| --- | --- |
| [!UICONTROL Minimum length] | Het minimale aantal items dat de array moet bevatten om de opname te laten slagen. |
| [!UICONTROL Maximum length] | Het maximum aantal items dat de array moet bevatten om de opname te laten slagen. |
| [!UICONTROL Unique items only] | Indien ingesteld op &quot;[!UICONTROL True]&quot;, moet elk item in de array uniek zijn om opname te laten slagen. |

{style="table-layout:auto"}

Nadat u het veld hebt geconfigureerd, selecteert u **[!UICONTROL Apply]** om de wijziging toe te passen op het schema.

![](../../images/ui/fields/special/array-config.png)

Het canvas wordt bijgewerkt met de wijzigingen die in het veld zijn aangebracht. Merk op dat het gegevenstype dat naast de gebiedsnaam in het canvas wordt getoond met een paar vierkante haakjes (`[]`) wordt toegevoegd, die op het gebied wijzen een serie van dat gegevenstype vertegenwoordigt.

![](../../images/ui/fields/special/array-applied.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u een arrayveld in de gebruikersinterface definieert. Zie het overzicht op [&#x200B; bepalende gebieden in UI &#x200B;](./overview.md#special) leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.
