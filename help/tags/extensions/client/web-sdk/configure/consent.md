---
title: Constante configuratie-instellingen
description: Configureer de standaardinstellingen voor toestemming en privacy voor de tagextensie.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 1%

---

# Constante configuratie-instellingen

In de sectie **[!UICONTROL Consent]** kunt u het standaardniveau van toestemming selecteren dat wordt aangenomen als er geen andere voorkeur voor expliciete toestemming is opgegeven. Het standaard toestemmingsniveau wordt niet bewaard aan gebruikersprofielen.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Consent]** .

![ Beeld dat de privacymontages van de de markeringsuitbreiding van SDK van het Web in de markeringen UI toont ](../assets/web-sdk-ext-privacy.png)

Deze sectie bevat één set keuzerondjes waarmee het standaard toestemmingsniveau wordt bepaald:

* **[!UICONTROL In]**: verzamel gebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft.
* **[!UICONTROL Out]**: neerzetgebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft.
* **[!UICONTROL Pending]**: Wachtrij-gebeurtenissen die plaatsvinden voordat de gebruiker voorkeuren voor toestemming geeft. Wanneer toestemming wordt verleend, worden gebeurtenissen in de wachtrij verzonden naar Adobe. Wanneer toestemming wordt ontkend, worden de een rij gevormde gebeurtenissen verworpen.
* **[!UICONTROL Provide a data element]**: Selecteer een gegevenselement dat een van de bovenstaande configuratie-instellingen bepaalt. Geldige waarden zijn de tekenreeksen `"in"` , `"out"` of `"pending"` .

Als uw organisatie expliciete toestemming van de gebruiker voor het verzamelen van gegevens vereist, raadt Adobe aan om de standaardtoestemming in te stellen op **[!UICONTROL Out]** of **[!UICONTROL Pending]** .
