---
title: Brand Concierge-configuratie-instellingen
description: Configureer sessieresistentie en streaming time-outs voor Brand Concierge-chat.
source-git-commit: 0a45b688243b17766143b950994f0837dc0d0b48
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 2%

---

# Brand Concierge-configuratie-instellingen

>[!AVAILABILITY]
>
>Brand Concierge voor het Web SDK is momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

Met de sectie **[!UICONTROL Brand Concierge]** kunt u bepalen hoe Brand Concierge-chatsessies zich gedragen in de webextensie voor SDK-tags.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Ga naar **[!UICONTROL Extensions]** en selecteer vervolgens **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schuif omlaag naar de sectie **[!UICONTROL Brand Concierge]** .

De volgende opties zijn beschikbaar:

## [!UICONTROL Sticky conversation session]

Een selectievakje waarmee Brand Concierge-sessies op de pagina worden voortgezet, wordt met een sessiecookie geladen. Deze optie is standaard uitgeschakeld. Zie [`conversation`](/help/collection/js/commands/configure/conversation.md) in de documentatie van de JavaScript-bibliotheek voor hulp bij het instellen van deze waarde.

## [!UICONTROL Stream timeout (seconds)]

De maximumhoeveelheid tijd, in seconden, om op de brokken van de gespreksstroom te wachten alvorens een onderbrekingsfout te teweegbrengen. De standaardwaarde is `10` seconden.
