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

De inhoud van de array is afhankelijk van de [!UICONTROL Type] geselecteerd voor dat veld. Als een veld bijvoorbeeld [!UICONTROL Type] is ingesteld op &quot;[!UICONTROL String]&quot;, wordt het veld door het instellen van dat veld als een array aangeduid als een array van tekenreeksen. Als het veld [!UICONTROL Type] wordt ingesteld op een gegevenstype met meerdere velden, zoals &quot;[!UICONTROL Postal address]&quot;, dan zou het een serie van post-adresvoorwerpen worden die met het gegevenstype in overeenstemming zijn.

Nadat u [een nieuw veld in de gebruikersinterface gedefinieerd](./overview.md#define), kunt u het als een matrixveld instellen door de optie **[!UICONTROL Array]** selectievakje in de rechterspoorstaaf.

![](../../images/ui/fields/special/array.png)

Als het selectievakje is ingeschakeld, worden in de rechtertrack extra besturingselementen weergegeven waarmee u de array eventueel verder kunt beperken. Als u een bepaalde beperking niet wilt afdwingen, laat u het veld leeg.

De extra configuratiecontroles voor series zijn als volgt:

| Field, eigenschap | Beschrijving |
| --- | --- |
| [!UICONTROL Minimum length] | Het minimale aantal items dat de array moet bevatten om de opname te laten slagen. |
| [!UICONTROL Maximum length] | Het maximum aantal items dat de array moet bevatten om de opname te laten slagen. |
| [!UICONTROL Unique items only] | Indien ingesteld op &quot;[!UICONTROL True]&quot;, moet elk item in de array uniek zijn om de opname te laten slagen. |

{style="table-layout:auto"}

Als u klaar bent met het configureren van het veld, selecteert u **[!UICONTROL Apply]** om de wijziging op het schema toe te passen.

![](../../images/ui/fields/special/array-config.png)

Het canvas wordt bijgewerkt met de wijzigingen die in het veld zijn aangebracht. Het gegevenstype dat naast de veldnaam op het canvas wordt weergegeven, wordt met twee vierkante haakjes toegevoegd (`[]`), die het veld aangeven, vertegenwoordigt een array van dat gegevenstype.

![](../../images/ui/fields/special/array-applied.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u een arrayveld in de gebruikersinterface definieert. Zie het overzicht op [velden definiëren in de gebruikersinterface](./overview.md#special) leren hoe u andere XDM-veldtypen definieert in het dialoogvenster [!DNL Schema Editor].
