---
keywords: Experience Platform;thuis;populaire onderwerpen;api;API;XDM;XDM systeem;ervaringsgegevensmodel;gegevensmodel;ui;werkruimte;vereist;gebied;
title: Vereiste velden definiëren in de gebruikersinterface
description: Leer hoe u een vereist XDM-veld definieert in de gebruikersinterface van het Experience Platform.
exl-id: 3a5885a0-6f07-42f3-b521-053083d5b556
source-git-commit: 1d04bf56c51506f84c5156e6d2ed6c9f58f15235
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Vereiste velden definiëren in de gebruikersinterface

In het Model van de Gegevens van de Ervaring (XDM), wijst een vereist gebied erop dat het een geldige waarde moet worden verstrekt opdat een bepaalde verslag of een tijd-reeksgebeurtenis tijdens gegevensopname wordt goedgekeurd. Veelvoorkomende gebruiksgevallen voor vereiste velden zijn gebruikersidentiteitsgegevens en tijdstempels.

Wanneer [een nieuw gebied](./overview.md#define) in het gebruikersinterface van Adobe Experience Platform bepaalt, kunt u het als vereist gebied plaatsen door **[!UICONTROL Required]** checkbox in het juiste spoor te selecteren. Selecteer **[!UICONTROL Apply]** om de wijziging op het schema toe te passen.

![Selectievakje vereist](../../images/ui/fields/required/root.png)

Als het veld een kenmerk op hoofdniveau onder het ID-object voor huurders is, wordt het pad direct onder **[!UICONTROL Required fields]** in de linkertrack weergegeven.

![Vereist veld op basisniveau](../../images/ui/fields/required/applied.png)

Als een vereist veld echter is genest binnen een object dat zelf niet is gemarkeerd als vereist, wordt het geneste veld niet weergegeven onder **[!UICONTROL Required fields]** in de linkertrack.

In het onderstaande voorbeeld wordt het veld `loyaltyId` ingesteld als vereist, maar het bovenliggende object `loyalty` niet. In dit geval zouden er geen validatiefouten optreden als `loyalty` was uitgesloten bij het invoeren van gegevens, ook al is het onderliggende veld `loyaltyId` gemarkeerd als vereist. Met andere woorden, terwijl `loyalty` optioneel is, moet het een `loyaltyId` veld bevatten voor het geval dat het wordt opgenomen.

![Genest vereist veld](../../images/ui/fields/required/nested.png)

Als u een genest gebied altijd in een schema wilt worden vereist, moet u alle oudergebieden zoals vereist (met uitzondering van het voorwerp van huurderidentiteitskaart) ook plaatsen.

![Vereiste velden voor bovenliggende en onderliggende elementen](../../images/ui/fields/required/parent-and-child.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u een vereist veld in de gebruikersinterface definieert. Zie het overzicht op [het bepalen van gebieden in UI](./overview.md#special) om te leren hoe te om andere XDM gebiedstypes in [!DNL Schema Editor] te bepalen.
