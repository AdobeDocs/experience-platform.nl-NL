---
title: sendPushSubscription
description: Abonnementen voor pushberichten registreren bij Adobe Experience Platform.
source-git-commit: 3abe25a9c538bf4d1b439d48f624d8cad109a99e
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 0%

---


# `sendPushSubscription` {#send-push-subscription}

>[!AVAILABILITY]
>
>De pushberichten voor het Web SDK zijn momenteel in **bèta**. De functionaliteit en documentatie kunnen worden gewijzigd.

Met de opdracht `sendPushSubscription` worden pushberichtabonnementen geregistreerd bij Adobe Experience Platform. Dit bevel behandelt de terugwinning van de details van het dupabonnement van browser en verzendt hen naar uw gevormde datastream. Deze is beschikbaar in SDK 2.29.0 of hoger op het web.

## Vereisten {#prerequisites}

Controleer voordat u `sendPushSubscription` gebruikt of:

1. **Gevormde duw berichten**: Opstelling het [`pushNotifications`](configure/pushnotifications.md) configuratiebezit met uw VAPID openbare sleutel
2. **de toestemming van de Gebruiker**: De gebruikers moeten berichttoestemming hebben verleend (`Notification.permission === "granted"`)
3. **de arbeider van de Dienst**: Een geregistreerde de dienstarbeider moet op uw plaats beschikbaar zijn
4. **de steun van de Manager van de Duw**: Browser moet dupberichten steunen en PushManager beschikbaar hebben API

Voer het `sendPushSubscription` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. Zorg ervoor dat u de opdracht [`configure`](configure/overview.md) aanroept met pushberichten geconfigureerd voordat u de opdracht `sendPushSubscription` aanroept.

```js
alloy("sendPushSubscription")
  .then(() => {
    console.log("Push subscription recorded successfully");
  })
  .catch((error) => {
    console.error("Failed to send push subscription:", error);
  });
```

## Aanbevolen uitvoeringsfrequentie {#recommended-execution-frequency}

Voor optimale functionaliteit van het duw- bericht, adviseert Adobe het `sendPushSubscription` bevel **eens per dag** uit te voeren. Deze frequentie zorgt ervoor dat:

* Abonnementsgegevens blijven geldig in Adobe Experience Platform
* Wijzigingen in de pushtokens of de abonnementsstatus worden vastgelegd
* Het gebruikersprofiel wordt bijgewerkt met de meest recente voorkeuren voor pushmeldingen

U kunt dit implementeren met een aanpak die vergelijkbaar is met de onderstaande aanpak:

```js
// Check if subscription data was sent today
const lastSent = localStorage.getItem("alloy_push_last_sent");
const today = new Date().toDateString();

if (lastSent !== today) {
  alloy("sendPushSubscription").then(() => {
    localStorage.setItem("alloy_push_last_sent", today);
  });
}
```

## Werking {#how-it-works}

De opdracht `sendPushSubscription` voert de volgende handelingen uit:

1. **bevestigt eerste vereisten**: Verifieert dat de duw- berichten worden gevormd en de gebruikerstoestemming wordt verleend
2. **wacht identiteit** af: Wacht op ECID van de gebruiker om beschikbaar te zijn
3. **wint abonnement** terug: Haalt het actieve dupabonnement van de de dienstarbeider gebruikend de gevormde sleutel VAPID
4. **controleert veranderingen**: Vergelijkt huidige abonnementsdetails met caching waarden (ECID + abonnementsdetails). Als de abonnementsdetails niet zijn veranderd, registreert het bevel een informatiebericht en keert zonder een netwerkverzoek terug
5. **verzendt aan datastream**: Als de veranderingen worden ontdekt, brengt de abonnementsgegevens aan uw gevormde datastroom van Adobe Experience Platform over
6. **het geheime voorgeheugen van Updates**: Slaat de nieuwe abonnementsdetails voor toekomstige vergelijking op

## Foutafhandeling {#error-handling}

Algemene foutcondities en de bijbehorende berichten:

| Fout | Oorzaak |
| ------- | ---- |
| `"Push notifications module is not configured. No VAPID public key was provided."` | Configuratie pushNotifications ontbreekt of is ongeldig |
| `"Service workers are not supported in this browser."` | Browser biedt geen ondersteuning voor serviceworkers |
| `"Push notifications are not supported in this browser."` | Browser biedt geen ondersteuning voor pushmeldingen of API voor meldingen |
| `"The user has not given permission to send push notifications."` | Gebruiker heeft geen berichttoestemming verleend (`Notification.permission === "granted"`) |
| `"No service worker registration was found."` | Er is geen serviceworker geregistreerd voor de huidige oorsprong |
| `"No VAPID public key was provided."` | VAPID openbare sleutel ontbreekt in configuratie |

## Gegevenslading {#data-payload}

De opdracht verzendt pushberichtgegevens in de volgende indeling:

```js
{
  pushNotificationDetails: [
    {
      appID: "example.com", // Current domain
      token: "...", // Serialized subscription details + ECID
      platform: "web", // Always "web" for Web SDK
      denylisted: false, // Always false
      identity: {
        namespace: {
          code: "ECID",
        },
        id: "12345678901234567890", // User's ECID
      },
    },
  ],
}
```

## Pushabonnement registreren met de Web SDK-tagextensie {#register-push-subscription-tag-extension}

De Web SDK-tagextensie die equivalent is aan dit veld, gebruikt de handeling [[!UICONTROL Send Push Subscription]](/help/tags/extensions/client/web-sdk/actions/send-push-subscription.md) binnen een tagregel.

>[!MORELIKETHIS]
>
>* [&#x200B; vorm dupberichten &#x200B;](configure/pushnotifications.md)
>* [&#x200B; Push API specificatie van het Web &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Push_API)
>* [&#x200B; de Arbeider API van de Dienst &#x200B;](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
