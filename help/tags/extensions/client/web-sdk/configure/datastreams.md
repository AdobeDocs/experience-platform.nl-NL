---
title: Instellingen voor gegevensstroomconfiguratie
description: Vorm de gegevensstroom om gegevens naar het gebruiken van de de markeringsuitbreiding van SDK van het Web te verzenden.
exl-id: 2d2504c6-b3f9-4e7b-aff4-a8d8d6c4e3dd
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---

# Instellingen voor gegevensstroomconfiguratie {#datastreams}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_datastreams"
>title="Gegevensstromen"
>abstract="Vereist. Hiermee stelt u de gegevensstroom in de Edge Network in waarnaar u gegevens wilt verzenden."

Deze configuratiesectie staat u toe om te bepalen welke [&#x200B; datastream &#x200B;](/help/datastreams/overview.md) dat u gegevens wilt verzenden naar. **identiteitskaart van A gegevensstroom wordt vereist voor alle gegevens die naar Edge Network worden verzonden.**

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Datastreams]** .

![&#x200B; Beeld dat de gegevensstroommontages van de de markeringsuitbreiding van SDK van het Web in de markeringen UI toont &#x200B;](../assets/web-sdk-ext-datastreams.png)

Wanneer het selecteren van gegevensstromen, kunt u dit voor elk [&#x200B; milieu &#x200B;](/help/tags/ui/publishing/environments.md) ([!UICONTROL Development], [!UICONTROL Staging], en [!UICONTROL Production]) doen. Deze gebieden zijn waardevol wanneer u gegevens wilt scheiden die tussen ontwikkeling, het opvoeren, en productiemilieu&#39;s worden verzonden. Het maakt een handige workflow mogelijk waarbij u zich geen zorgen hoeft te maken over het verzenden van gegevens naar de verkeerde gegevensstroom, zolang u de juiste tagloader in elke omgeving installeert.

U kunt gegevensstroom-id&#39;s vullen met een van de volgende methoden:

* **[!UICONTROL Choose from list]**: Elke omgeving bevat twee vervolgkeuzemenu&#39;s waarmee u de sandbox en de gegevensstroom voor de geselecteerde omgeving kunt selecteren. De waarden in elk drop-down menu hangen van uw gevormde [&#x200B; gegevensstromen &#x200B;](/help/datastreams/overview.md) binnen elke respectieve [&#x200B; zandbak &#x200B;](/help/sandboxes/ui/overview.md) af.

* **[!UICONTROL Enter values]**: als alternatief voor het gebruik van vervolgkeuzemenu&#39;s om de gewenste gegevensstroom te selecteren, kunt u handmatig de gewenste gegevensstroom-id rechtstreeks opgeven. Elk milieu staat u toe om een gegevensstroomidentiteitskaart direct in te voeren, of dit gebied te bevolken gebruikend a [&#x200B; gegevenselement &#x200B;](/help/tags/ui/managing-resources/data-elements.md).
