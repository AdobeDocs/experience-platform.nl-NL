---
title: Regels evalueren
description: Activeer handmatig een liniaalevaluatie.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 2%

---

# Regels evalueren

Met het actietype **[!UICONTROL Evaluate rulesets]** kunt u handmatig liniaalevaluaties activeren. Regels worden door Adobe Journey Optimizer geretourneerd ter ondersteuning van functies zoals in-browser berichten.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel vervolgens de waarde [!UICONTROL Action type] in op **[!UICONTROL Evaluate rulesets]** .

![ Beeld van het gebruikersinterface van Experience Platform die het Evaluate type van de liniaalreactie toont.](../assets/evaluate-rulesets.png)

## Beschikbare velden

Dit handelingstype ondersteunt de volgende opties:

* **[!UICONTROL Render visual personalization decisions]**: Een selectievakje dat, indien ingeschakeld, visuele aanpassingsbeslissingen rendert voor de liniaalitems die overeenkomen.
* **[!UICONTROL Decision context]**: Een sleutel-waardekaart die wordt gebruikt wanneer het evalueren van de Adobe Journey Optimizer-regels voor het op-apparaat beslissen. U kunt de besluitvormingscontext manueel of door een gegevenselement verstrekken.
