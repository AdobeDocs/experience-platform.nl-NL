---
title: Adobe Advertising-configuratie-instellingen
description: De functionaliteit van het platform aan de vraagzijde in- of uitschakelen.
exl-id: 594fd75d-bb13-4146-9105-1398e24c4c16
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 1%

---

# Adobe Advertising-configuratie-instellingen {#advertising}

>[!AVAILABILITY]
>
>Adobe Advertising voor het Web SDK is momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advertising"
>title="Adobe Advertising"
>abstract="Configureer instellingen voor Adobe Advertising-integratie. Er is geen advertentieconfiguratie nodig om doorklikmeting in te schakelen. Zoek-, sociale en Commerce-clients hebben geen verdere actie vereist. Gebruikers van het Demand-Side Platform (DSP) moeten echter in deze sectie adverteerders configureren om doorkijkconversies te meten."

In de sectie **[!UICONTROL Adobe Advertising]** kunt u de functionaliteit van het platform aan de vraagzijde (DSP) in- of uitschakelen als deze wordt gebruikt in uw implementatie. U hoeft dit veld alleen in te stellen als uw implementatie een DSP gebruikt.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
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
