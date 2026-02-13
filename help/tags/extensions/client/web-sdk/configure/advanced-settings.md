---
title: Geavanceerde configuratie-instellingen
description: Configureer geavanceerde instellingen voor de Web SDK-tagextensie.
exl-id: d830a210-77ab-4823-b5fa-c1194a01bea3
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 2%

---

# Geavanceerde configuratie-instellingen {#advanced}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_advanced"
>title="Geavanceerde instellingen"
>abstract="Geavanceerde configuratie-instellingen. Adobe raadt u aan deze opties ongewijzigd te laten voor de meeste implementaties."

In deze configuratiesectie kunt u geavanceerde instellingen wijzigen. Adobe raadt u aan deze opties ongewijzigd te laten voor de meeste implementaties.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Advanced Settings]** .

![&#x200B; Beeld dat de geavanceerde montages toont gebruikend de de markeringsuitbreidingspagina van SDK van het Web &#x200B;](../assets/advanced-settings.png)

Er is momenteel één optie beschikbaar.

## [!UICONTROL Edge base path]

Met dit veld wijzigt u het basispad dat wordt gebruikt voor interactie met de Edge Network. Adobe kan u verzoeken dit veld te wijzigen als u deelneemt aan bepaalde alfa- of bètatests. Als dit niet het geval is, raadt Adobe aan dit veld de standaardwaarde van `ee` te laten.

Dit veld is het equivalent van de tag [`edgeBasePath`](/help/collection/js/commands/configure/edgebasepath.md) bij het configureren van de JavaScript-bibliotheek.
