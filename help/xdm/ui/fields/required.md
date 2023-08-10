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
>Ongeacht of een schemagebied wordt vereist of niet, keurt het Platform niet goed `null` of lege waarden voor een ingesloten veld. Als er geen waarde is voor een bepaald veld in een record of gebeurtenis, moet de sleutel voor dat veld worden uitgesloten van de opname-lading.

Wanneer [een nieuw veld definiëren](./overview.md#define) in de Adobe Experience Platform-gebruikersinterface kunt u deze als een vereist veld instellen door de **[!UICONTROL Required]** selectievakje in de rechterspoorstaaf. Selecteren **[!UICONTROL Apply]** om de wijziging op het schema toe te passen.

![Selectievakje vereist](../../images/ui/fields/required/root.png)

Als het veld een kenmerk op hoofdniveau is onder het ID-object van de huurder, verschijnt het pad onmiddellijk onder **[!UICONTROL Required fields]** in het linkerspoor.

![Vereist veld op basisniveau](../../images/ui/fields/required/applied.png)

Als een vereist veld echter is genest in een object dat zelf niet is gemarkeerd als vereist, wordt het geneste veld niet weergegeven onder **[!UICONTROL Required fields]** in het linkerspoor.

In het onderstaande voorbeeld wordt `internalSKU` veld wordt ingesteld als vereist, maar het bovenliggende object `SKUs` is niet. In dit geval treden er geen validatiefouten op als `SKUs` wordt uitgesloten bij het invoeren van gegevens, ook al wordt het onderliggende veld `internalSKU` is gemarkeerd als vereist. Met andere woorden: `SKUs` is optioneel; bevat een `internalSKU` in het geval dat het wordt opgenomen.

![Genest vereist veld](../../images/ui/fields/required/nested.png)

Als u een genest gebied altijd in een schema wilt worden vereist, moet u alle oudergebieden zoals vereist (met uitzondering van het voorwerp van huurderidentiteitskaart) ook plaatsen.

![Vereiste velden voor bovenliggende en onderliggende elementen](../../images/ui/fields/required/parent-and-child.png)

## Volgende stappen

In deze handleiding wordt beschreven hoe u een vereist veld in de gebruikersinterface definieert. Zie het overzicht op [velden definiëren in de gebruikersinterface](./overview.md#special) leren hoe u andere XDM-veldtypen definieert in het dialoogvenster [!DNL Schema Editor].
