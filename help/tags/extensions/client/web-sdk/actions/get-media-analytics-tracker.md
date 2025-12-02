---
title: Media Analytics-tracker ophalen
description: Exporteert de verouderde media-API naar een vensterobject.
source-git-commit: c55e425f146e4afdb2314b432c9dc48391e02e63
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Media Analytics-beheer ophalen

De handeling **[!UICONTROL Get Media Analytics tracker]** wordt gebruikt om de API voor oude media-analyse op te halen. Wanneer de handeling wordt geconfigureerd en een objectnaam wordt opgegeven, wordt de verouderde Media Analytics-API geëxporteerd naar dat vensterobject. Deze handeling is handig voor de overgang van verouderde media-analysemogelijkheden naar Streaming media-analyse.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel vervolgens de waarde [!UICONTROL Action type] in op **[!UICONTROL Get Media Analytics tracker]** .

![&#x200B; Experience Platform UI beeld dat het Get de actietype van de Traceur van de Analyse van Media toont.](../assets/get-media-analytics-tracker.png)

Deze actie bevat één enkel gebied dat u kunt vormen:

* **[!UICONTROL Export the Media Legacy API to this window object]**: hiermee selecteert u het gewenste object waarnaar de API voor mediaveroudering moet worden geëxporteerd. Als er geen waarde is opgegeven, exporteert de handeling de API naar `window.Media` .
