---
title: pushNotifications
description: Vorm dupberichten voor het Web SDK om browser-gebaseerd dupoverseinen toe te laten.
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 1%

---

# `pushNotifications` {#push-notifications}

>[!AVAILABILITY]
>
>De pushberichten voor het Web SDK zijn momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

Met de eigenschap `pushNotifications` kunt u pushmeldingen voor webtoepassingen configureren. Met deze functie kan uw webtoepassing berichten van een server ontvangen, zelfs als de website momenteel niet in de browser is geladen.

## Vereisten {#prerequisites}

Voordat u pushmeldingen configureert, moet u ervoor zorgen dat:

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

Deze actie produceert een openbare en privé zeer belangrijke paar. Gebruik de openbare sleutel in uw configuratie van SDK van het Web en bewaar de privé sleutel binnen het kanaal van de pushberichten van Adobe Journey Optimizer.

## De serviceworker installeren

De code van de de dienstarbeider moet van het zelfde domein zoals de website worden gediend. Download de code van de de dienstarbeider van CDN van Adobe en host het dossier van JavaScript van uw eigen server. De code van de de dienstarbeider van SDK van het Web is beschikbaar gebruikend de volgende structuur URL:

- **Minified**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.min.js`
- **Volledig**: `https://cdn1.adoberesources.net/alloy/[VERSION]/alloyServiceWorker.js`

Hier is een voorbeeld van hoe te om de de dienstarbeider te installeren:

```html
<script>
  navigator.serviceWorker.register("/alloyServiceWorker.js", { scope: "/" });
</script>
```

## Implementatie

Stel het object `pushNotifications` in wanneer u de opdracht `configure` uitvoert:

```js
alloy("configure", {
  datastreamId: "ebebf826-a01f-4458-8cec-ef61de241c93",
  orgId: "ADB3LETTERSANDNUMBERS@AdobeOrg",
  pushNotifications: {
    vapidPublicKey: "BEl62iUYgU[...]KGP4jAQlJz",
    applicationId: "my-app-id",
    trackingDatasetId: "4dc19305cdd27e03dd9a6bbe",
  },
});
```

## Properties {#properties}

| Eigenschap | Type | Vereist | Beschrijving |
|---|---|---|---|
| **`vapidPublicKey`** | String | Ja | De openbare sleutel VAPID die voor pushabonnementen wordt gebruikt. Moet een Base64-gecodeerde tekenreeks zijn. |
| **`applicationId`** | String | Ja | De toepassings-id die is gekoppeld aan de openbare sleutel VAPID. |
| **`trackingDatasetId`** | String | Ja | De id van de systeemgegevensset die wordt gebruikt voor het bijhouden van pushberichten. |

## Belangrijke overwegingen {#important-considerations}

- **Veiligheid**: De pushabonnementen zijn gebonden aan de specifieke openbare sleutel VAPID die tijdens abonnement wordt gebruikt. Als u VAPID-toetsen wijzigt, worden bestaande abonnementen automatisch afgemeld en opnieuw gemaakt met de nieuwe toets.
- **Caching**: Het Web SDK beheert automatisch abonnementsupdates door huidige ECID en abonnementdetails met caching waarden te vergelijken. Abonnementsgegevens worden alleen verzonden wanneer wijzigingen worden gedetecteerd.
- **de arbeiderseis van de Dienst**: De pushberichten vereisen een geregistreerde de dienstarbeider. Zorg ervoor dat de serviceworker correct is geconfigureerd voor de verwerking van pushgebeurtenissen.

## Pushmeldingen configureren met de Web SDK-tagextensie {#configure-push-notifications-tag-extension}

De Web SDK-tagextensie die equivalent is aan deze eigenschap, is de [[!UICONTROL Push notifications]](/help/tags/extensions/client/web-sdk/configure/push-notifications.md) -sectie wanneer u de extensie configureert.

## Volgende stappen {#next-steps}

Na het vormen van duw berichten, gebruik het [ sendPushSubscription ](../sendpushsubscription.md) bevel om dupabonnementen met Adobe Experience Platform te registreren.
