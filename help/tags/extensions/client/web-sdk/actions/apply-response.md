---
title: Antwoord toepassen
description: Voer een actie uit op basis van een reactie van de Edge Network.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 1%

---

# Antwoord toepassen

Met het actietype **[!UICONTROL Apply response]** kunt u verschillende handelingen uitvoeren op basis van een reactie van de Edge Network. Dit actietype wordt typisch gebruikt in hybride plaatsingen waar de server een aanvankelijke vraag aan Edge Network maakt, dan neemt dit actietype de reactie van die vraag en initialiseert het Web SDK in browser. Met dit actietype kan de laadtijd van de client worden verkort voor hybride gebruiksscenario&#39;s voor personalisatie.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel vervolgens de waarde [!UICONTROL Action type] in op **[!UICONTROL Apply response]** .

![&#x200B; Beeld van het gebruikersinterface van Experience Platform die het Apply reactietype tonen.](../assets/apply-response.png)

## Gebruiksscenario’s

* **Hand die tussen gegevensinzameling en verpersoonlijking** wordt gesplitst: U kunt a [&#x200B; verzenden gebeurtenis &#x200B;](send-event.md) actie met teruggeven besluiten teweegbrengen die aan `false` worden geplaatst, dan hebben &quot;verzenden gebeurtenis volledige&quot;regel de belofte. De eerste actie binnen deze regel kan &quot;Apply reactie&quot;zijn. Met deze workflow kunt u DOM-manipulatie uitstellen totdat de eigen code van uw organisatie andere werkzaamheden heeft voltooid.
* **reactie van Edge die van buiten het Web SDK** wordt ontvangen: Als u een andere bibliotheek gebruikt om met Edge Network te communiceren, kunt u SDK van het Web toestaan om nog de reactie van Edge Network te behandelen gebruikend deze actie.

## Beschikbare velden

Dit handelingstype ondersteunt de volgende configuratieopties:

* **[!UICONTROL Instance]**: De SDK-instantie waarop de handeling van toepassing is. Dit vervolgkeuzemenu is uitgeschakeld als uw implementatie één SDK-exemplaar gebruikt.
* **[!UICONTROL Response headers]**: Selecteer het gegevenselement dat een object retourneert dat de headertoetsen en waarden bevat die door de Edge Network-serveraanroep worden geretourneerd.
* **[!UICONTROL Response body]**: selecteer het gegevenselement dat het object retourneert dat de JSON-payload bevat die door het Edge Network-antwoord wordt opgegeven.
* **[!UICONTROL Render visual personalization decisions]**: Schakel deze optie in om automatisch de personalisatie-inhoud van de Edge Network te renderen en de inhoud vooraf te verbergen om flikkering te voorkomen.
