---
title: Adobe Advertising-configuratie-instellingen
description: De functionaliteit van het platform aan de vraagzijde in- of uitschakelen.
source-git-commit: 526cb473a6288f367db9cb00c0277cce7543cd57
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 1%

---

# Adobe Advertising-configuratie-instellingen

>[!AVAILABILITY]
>
>Adobe Advertising voor het Web SDK is momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

In de sectie **[!UICONTROL Adobe Advertising]** kunt u de functionaliteit van het platform aan de vraagzijde (DSP) in- of uitschakelen als deze wordt gebruikt in uw implementatie. U hoeft dit veld alleen in te stellen als uw implementatie een DSP gebruikt.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Adobe Advertising]** .

Er is momenteel één optie beschikbaar.

## [!UICONTROL Adobe Advertising DSP]

Een vervolgkeuzemenu waarmee de DSP-functionaliteit voor Adobe Advertising in- en uitgeschakeld wordt.

* **[!UICONTROL Enabled]**: Schakelt weergave via bijhouden in.
* **[!UICONTROL Disabled]**: Schakelt weergave via bijhouden uit.

Wanneer deze optie is ingeschakeld, zijn de volgende instellingen beschikbaar:

* **[!UICONTROL Advertisers]**: De adverteerders waarvoor doorkijktracking moet worden ingeschakeld.
* **[!UICONTROL ID5 partner ID]**: optioneel. ID5-partner van uw organisatie. Met deze instelling kan de Web SDK ID5 universele id&#39;s verzamelen.
* **[!UICONTROL RampID JavaScript path]**: optioneel. Het pad naar de [!DNL LiveRamp RampID] JavaScript-code van uw organisatie (`ats.js` ).  Met deze instelling kan de Web SDK [!DNL RampID] universele id&#39;s verzamelen.
