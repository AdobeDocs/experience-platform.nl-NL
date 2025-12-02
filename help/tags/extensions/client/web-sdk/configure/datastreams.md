---
title: Instellingen voor gegevensstroomconfiguratie
description: Vorm de gegevensstroom om gegevens naar het gebruiken van de de markeringsuitbreiding van SDK van het Web te verzenden.
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 1%

---

# Instellingen voor gegevensstroomconfiguratie

Deze configuratiesectie staat u toe om te bepalen welke [ datastream ](/help/datastreams/overview.md) dat u gegevens wilt verzenden naar. **identiteitskaart van A gegevensstroom wordt vereist voor alle gegevens die naar Edge Network worden verzonden.**

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Datastreams]** .

![ Beeld dat de gegevensstroommontages van de de markeringsuitbreiding van SDK van het Web in de markeringen UI toont ](../assets/web-sdk-ext-datastreams.png)

Wanneer het selecteren van gegevensstromen, kunt u dit voor elk [ milieu ](/help/tags/ui/publishing/environments.md) ([!UICONTROL Development], [!UICONTROL Staging], en [!UICONTROL Production]) doen. Deze gebieden zijn waardevol wanneer u gegevens wilt scheiden die tussen ontwikkeling, het opvoeren, en productiemilieu&#39;s worden verzonden. Het maakt een handige workflow mogelijk waarbij u zich geen zorgen hoeft te maken over het verzenden van gegevens naar de verkeerde gegevensstroom, zolang u de juiste tagloader in elke omgeving installeert.

U kunt gegevensstroom-id&#39;s vullen met een van de volgende methoden:

* **[!UICONTROL Choose from list]**: Elke omgeving bevat twee vervolgkeuzemenu&#39;s waarmee u de sandbox en de gegevensstroom voor de geselecteerde omgeving kunt selecteren. De waarden in elk drop-down menu hangen van uw gevormde [ gegevensstromen ](/help/datastreams/overview.md) binnen elke respectieve [ zandbak ](/help/sandboxes/ui/overview.md) af.

* **[!UICONTROL Enter values]**: als alternatief voor het gebruik van vervolgkeuzemenu&#39;s om de gewenste gegevensstroom te selecteren, kunt u handmatig de gewenste gegevensstroom-id rechtstreeks opgeven. Elk milieu staat u toe om een gegevensstroomidentiteitskaart direct in te voeren, of dit gebied te bevolken gebruikend a [ gegevenselement ](/help/tags/ui/managing-resources/data-elements.md).
