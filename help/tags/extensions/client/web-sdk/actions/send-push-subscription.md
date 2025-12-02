---
title: Push-abonnement verzenden
description: Gegevens registreren, verzenden en verzamelen voor push-abonnementen op browsers.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 1%

---

# Push-abonnement verzenden

>[!AVAILABILITY]
>
>De pushberichten voor het Web SDK zijn momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

Met de handeling **[!UICONTROL Send push subscription]** worden pushberichtabonnementen geregistreerd bij Adobe Experience Platform. Het behandelt de terugwinning van de details van het dupabonnement van browser en verzendt hen naar uw gevormde datastream. Het is beschikbaar in de uitbreidingsversies 2.32.0 van SDK van het Web of later.

1. Login aan [&#x200B; experience.adobe.com &#x200B;](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel [!UICONTROL Action Type] in op **[!UICONTROL Send push subscription]** .

De actie heeft geen configuratie-instellingen dan alleen het selecteren van een SDK-instantie.

Zorg ervoor dat u een geldige [&#x200B; VAPID openbare sleutel &#x200B;](../configure/push-notifications.md) plaatst wanneer het vormen van de uitbreiding alvorens u dit bevel gebruikt.

Deze actie is gelijk aan de tagextensie [`sendPushSubscription`](/help/collection/js/commands/sendpushsubscription.md) opdracht. Zie de verbonden pagina voor informatie over eerste vereisten, geadviseerde uitvoeringsfrequentie, hoe het bevel, en fout behandeling werkt.

>[!MORELIKETHIS]
>
>* [&#x200B; vorm dupberichten &#x200B;](../configure/push-notifications.md)
>* [&#x200B; Push API specificatie van het Web &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [&#x200B; de Arbeider API van de Dienst &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
