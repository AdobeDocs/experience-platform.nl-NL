---
title: Instellingen voor pushmeldingen
description: Configureer instellingen voor pushmeldingen voor de Web SDK-tagextensie.
exl-id: 96ab7ea8-7180-46bb-9c15-eecba2009c52
source-git-commit: 6c05d8abde0e4d6b07fe37d6e3eacd5d3dd67ec2
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 2%

---

# Instellingen voor pushmeldingen {#push-notifications}

>[!CONTEXTUALHELP]
>id="platform_tags_websdk_pushnotifications"
>title="Pushmeldingen"
>abstract="Hiermee stelt u een openbare VAPID-sleutel in voor verificatie van pushberichten."

>[!AVAILABILITY]
>
>De pushberichten voor het Web SDK zijn momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

Deze configuratiesectie staat u toe om een openbare sleutel van VAPID voor de authentificatie van de dupmelding te plaatsen.

>[!NOTE]
>
>Deze eigenschap moet eerst worden toegelaten gebruikend [ Douane bouwt componenten ](custom-build-components.md); het wordt onbruikbaar gemaakt door gebrek.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Vouw **[!UICONTROL Custom build components]** uit en schakel **[!UICONTROL Push notifications]** vervolgens in.
1. Blader onder [!UICONTROL SDK instances] omlaag om de sectie [!UICONTROL Push Notifications] te zoeken.
1. Voer in het veld **[!UICONTROL VAPID Public Key]** de openbare sleutel voor VAPID in.

![ Beeld dat duw berichten montages toont gebruikend de de markeringsuitbreiding van SDK van het Web ](../assets/push-notifications.png)

De volgende velden zijn beschikbaar:

## [!UICONTROL VAPID public key]

De openbare sleutel VAPID die voor pushabonnementen wordt gebruikt. Het is een Base64-Gecodeerde koord.

## [!UICONTROL Application ID]

De toepassings-id die is gekoppeld aan de openbare sleutel VAPID.

## [!UICONTROL Tracking dataset ID]

De dataset-id voor het bijhouden en analyseren van pushmeldingen.

## Pushmeldingen met gebruik van de JavaScript-bibliotheek

Deze sectie is het equivalent van de tag [`pushNotifications`](/help/collection/js/commands/configure/pushnotifications.md) bij het configureren van de JavaScript-bibliotheek. De gekoppelde pagina bevat ook informatie over voorwaarden en het genereren van een openbare sleutel voor VAPID.
