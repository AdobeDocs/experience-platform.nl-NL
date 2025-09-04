---
title: pushNotifications
description: Vorm dupberichten voor het Web SDK om browser-gebaseerd dupoverseinen toe te laten.
source-git-commit: 9c3f19cc2b32ab70869584b620f5a55d5b808751
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 1%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> De pushberichten voor het Web SDK zijn momenteel in **bèta**. De functionaliteit en documentatie kunnen veranderen.

Met de eigenschap `pushNotifications` kunt u pushmeldingen configureren voor webtoepassingen. Met deze functie kan uw webtoepassing berichten van een server ontvangen, zelfs als de website momenteel niet in de browser is geladen of zelfs niet als de browser wordt uitgevoerd.

## Vereisten {#prerequisites}

Voordat u pushmeldingen configureert, moet u controleren of u beschikt over:

1. **de toestemming van de Gebruiker**: De gebruikers moeten toestemmingen voor berichten uitdrukkelijk verlenen
2. **de arbeider van de Dienst**: Een geregistreerde de dienstarbeider wordt vereist voor dupberichten aan functie
3. **VAPID sleutels**: produceer VAPID (de Vrijwillige Identificatie van de Server van de Toepassing) sleutels voor veilige mededeling

## VAPID-sleutels genereren {#generate-vapid-keys}

Installeer het `web-push` NPM-pakket en voer de volgende handelingen uit om VAPID-sleutels te genereren:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Dit produceert een openbare en privé zeer belangrijke paar. Gebruik de openbare sleutel in uw configuratie van SDK van het Web en bewaar de privé sleutel binnen het kanaal van de pushberichten van Adobe Journey Optimizer.

## Pushmeldingen configureren met de Web SDK-tagextensie {#configure-push-notifications-tag-extension}

Voer de volgende stappen uit om pushmeldingen in te schakelen en te configureren:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. **laat dupberichten** van de &quot;Douane toe bouwt componenten&quot;sectie.
1. Schuif omlaag om de sectie [!UICONTROL Push Notifications] te zoeken.
1. Voer in het veld **[!UICONTROL VAPID Public Key]** de openbare sleutel voor VAPID in.
1. Klik op **[!UICONTROL Save]** en publiceer de wijzigingen.

>[!NOTE]
>
> Pushmeldingen moeten expliciet zijn ingeschakeld in de configuratie van de tagextensie. De functie is standaard uitgeschakeld.

## Pushmeldingen configureren met de Web SDK JavaScript-bibliotheek {#configure-push-notifications-javascript}

Stel het object `pushNotifications` in wanneer u de opdracht `configure` uitvoert:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey:
      "BEl62iUYgUivElbkzaBgNL3r3vOAhvJyFXjS6FjjRRojYD4NElJkLBJKZvS3xAAh4_gE3WnMaZNu_KGP4jAQlJz",
  },
});
```

## Properties {#properties}

| Eigenschap | Type | Vereist | Beschrijving |
| ------ | ------ | -------- | ----- |
| `vapidPublicKey` | String | Ja | De openbare sleutel van VAPID die voor dupabonnement wordt gebruikt. Moet een Base64-gecodeerde tekenreeks zijn. |

## Belangrijke overwegingen {#important-considerations}

- **Veiligheid**: De pushabonnementen zijn gebonden aan de specifieke openbare sleutel VAPID die tijdens abonnement wordt gebruikt. Als u VAPID-toetsen wijzigt, worden bestaande abonnementen automatisch afgemeld en opnieuw gemaakt met de nieuwe toets.
- **Caching**: Het Web SDK beheert automatisch abonnementsupdates door huidige ECID en abonnementdetails met caching waarden te vergelijken. Abonnementsgegevens worden alleen verzonden wanneer wijzigingen worden gedetecteerd.
- **de arbeiderseis van de Dienst**: De pushberichten vereisen een geregistreerde de dienstarbeider. Zorg ervoor dat de serviceworker correct is geconfigureerd voor de verwerking van pushgebeurtenissen.

## Volgende stappen {#next-steps}

Nadat u pushberichten hebt geconfigureerd, gebruikt u de opdracht [`sendPushSubscription`](../sendPushSubscription.md) om pushabonnementen te registreren bij Adobe Experience Platform.
