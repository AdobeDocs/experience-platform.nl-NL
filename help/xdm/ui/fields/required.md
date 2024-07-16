---
keywords: Experience Platform;thuis;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;vereist;gebied;
title: Vereiste velden definiëren in de gebruikersinterface
description: Leer hoe u een vereist XDM-veld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# Vereiste velden definiëren in de gebruikersinterface

In het Model van de Gegevens van de Ervaring (XDM), wijst een vereist gebied erop dat het een geldige waarde moet worden verstrekt opdat een bepaalde verslag of een tijd-reeksgebeurtenis tijdens gegevensopname wordt goedgekeurd. Veelvoorkomende gebruiksgevallen voor vereiste velden zijn gebruikersidentiteitsgegevens en tijdstempels.

>[!IMPORTANT]
>
>Ongeacht of een schemaveld wordt vereist of niet, accepteert Platform geen `null` of lege waarden voor een ingesloten veld. Als er geen waarde is voor een bepaald veld in een record of gebeurtenis, moet de sleutel voor dat veld worden uitgesloten van de opname-lading.

Wanneer [ het bepalen van een nieuw gebied ](./overview.md#define) in het gebruikersinterface van Adobe Experience Platform, kunt u het als vereist gebied plaatsen door **[!UICONTROL Required]** checkbox in het juiste spoor te selecteren. Selecteer **[!UICONTROL Apply]** om de wijziging op het schema toe te passen.

![ Vereiste checkbox ](../../images/ui/fields/required/root.png)

Als het veld een kenmerk op hoofdniveau onder het ID-object voor huurders is, wordt het pad direct onder **[!UICONTROL Required fields]** in de linkertrack weergegeven.

![ wortel-niveau vereist gebied ](../../images/ui/fields/required/applied.png)

Als een vereist veld echter is genest binnen een object dat zelf niet is gemarkeerd als vereist, wordt het geneste veld niet weergegeven onder **[!UICONTROL Required fields]** in de linkertrack.

In het onderstaande voorbeeld wordt het veld `internalSKU` ingesteld als vereist, maar het bovenliggende object `SKUs` niet. In dit geval treden er geen validatiefouten op als `SKUs` wordt uitgesloten bij het invoeren van gegevens, ook al is het onderliggende veld `internalSKU` gemarkeerd als vereist. Met andere woorden, terwijl `SKUs` optioneel is, moet het een `internalSKU` -veld bevatten voor het geval het wordt opgenomen.

![ Genest vereist gebied ](../../images/ui/fields/required/nested.png)

Als u een genest gebied altijd in een schema wilt worden vereist, moet u alle oudergebieden zoals vereist (met uitzondering van het voorwerp van huurderidentiteitskaart) ook plaatsen.

![ Ouder en kind vereiste gebieden ](../../images/ui/fields/required/parent-and-child.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u een vereist veld in de gebruikersinterface definieert. Zie het overzicht op [ bepalende gebieden in UI ](./overview.md#special) leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.
