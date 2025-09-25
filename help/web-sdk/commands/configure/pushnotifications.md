---
title: pushNotifications
description: Vorm dupberichten voor het Web SDK om browser-gebaseerd dupoverseinen toe te laten.
source-git-commit: 7c2afd6d823ebb2db0fabb4cc16ef30bcbfeef13
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 1%

---


# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
> De pushberichten voor het Web SDK zijn momenteel in **bèta**. De functionaliteit en documentatie kunnen veranderen.

Met de eigenschap `pushNotifications` kunt u pushmeldingen configureren voor webtoepassingen. Met deze functie kan uw webtoepassing berichten van een server ontvangen, zelfs als de website momenteel niet in de browser is geladen.

## Vereisten {#prerequisites}

Voordat u pushmeldingen configureert, moet u controleren of u beschikt over:

1. **de toestemming van de Gebruiker**: De gebruikers moeten toestemmingen voor berichten uitdrukkelijk verlenen
2. **de arbeider van de Dienst**: Een geregistreerde de dienstarbeider wordt vereist voor dupberichten aan functie
3. **VAPID sleutels**: produceer VAPID (de Vrijwillige Identificatie van de Server van de Toepassing) sleutels voor veilige mededeling
4. **identiteitskaart van de Toepassing**: Toepassings identiteitskaart die wanneer het opslaan van de sleutels VAPID binnen Adobe Journey Optimizer -> Kanalen -> de Montages van de Duw -> de Referenties van de Duw wordt gebruikt
5. **het Volgen dataset identiteitskaart**: Identiteitskaart van de systeemdataset met de naam &quot;de Dataset van de Gebeurtenis van de Ervaring van de Duw van AJO het Volgen&quot;. Haal dit uit Adobe Journey Optimizer -> Datasets

## VAPID-sleutels genereren {#generate-vapid-keys}

Installeer het `web-push` NPM-pakket en voer de volgende handelingen uit om VAPID-sleutels te genereren:

```bash
npm install web-push -g
web-push generate-vapid-keys
```

Dit produceert een openbare en privé zeer belangrijke paar. Gebruik de openbare sleutel in uw configuratie van SDK van het Web en bewaar de privé sleutel binnen het kanaal van de pushberichten van Adobe Journey Optimizer.

## De serviceworker JavaScript installeren

De code van de de arbeider van de dienst moet van het zelfde domein worden gediend zoals de website. Download de code van de de dienstarbeider van CDN van Adobe en host dan het dossier van JavaScript van uw eigen server. De code van de de dienstarbeider van SDK van het Web is beschikbaar gebruikend de volgende structuur URL:

- **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Volledig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Hier is een voorbeeld van hoe te om de de dienstarbeider te installeren:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Pushmeldingen configureren met de Web SDK-tagextensie {#configure-push-notifications-tag-extension}

Voer de volgende stappen uit om pushmeldingen in te schakelen en te configureren:

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Extensions]** en klik vervolgens op **[!UICONTROL Configure]** op de [!UICONTROL Adobe Experience Platform Web SDK] -kaart.
1. Schakel **[!UICONTROL Custom build components]** in vanuit de sectie **[!UICONTROL Push notifications]** .
1. Schuif omlaag om de sectie [!UICONTROL Push Notifications] te zoeken.
1. Voer in het veld **[!UICONTROL VAPID Public Key]** de openbare sleutel voor VAPID in.
1. Voer uw toepassings-id in het veld **[!UICONTROL Application ID]** in.
1. Voer in het veld **[!UICONTROL Tracking Dataset ID]** de id van de volgende gegevensset in.
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
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Properties {#properties}

| Eigenschap | Type | Vereist | Beschrijving |
|---------|----|---------|-----------|
| `vapidPublicKey` | String | Ja | De openbare sleutel van VAPID die voor dupabonnement wordt gebruikt. Moet een Base64-gecodeerde tekenreeks zijn. |
| `applicationId` | String | Ja | De toepassings-id die aan deze openbare sleutel VAPID is gekoppeld. |
| `trackingDatasetId` | String | Ja | De id van de systeemgegevensset die wordt gebruikt voor het bijhouden van pushberichten. |

## Belangrijke overwegingen {#important-considerations}

- **Veiligheid**: De pushabonnementen zijn gebonden aan de specifieke openbare sleutel VAPID die tijdens abonnement wordt gebruikt. Als u VAPID-toetsen wijzigt, worden bestaande abonnementen automatisch afgemeld en opnieuw gemaakt met de nieuwe toets.
- **Caching**: Het Web SDK beheert automatisch abonnementsupdates door huidige ECID en abonnementdetails met caching waarden te vergelijken. Abonnementsgegevens worden alleen verzonden wanneer wijzigingen worden gedetecteerd.
- **de arbeiderseis van de Dienst**: De pushberichten vereisen een geregistreerde de dienstarbeider. Zorg ervoor dat de serviceworker correct is geconfigureerd voor de verwerking van pushgebeurtenissen.

## Volgende stappen {#next-steps}

Nadat u pushberichten hebt geconfigureerd, gebruikt u de opdracht [`sendPushSubscription`](../sendPushSubscription.md) om pushabonnementen te registreren bij Adobe Experience Platform.
