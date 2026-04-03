---
title: Identiteit delen van mobiele apps naar mobiele websites/webweergaven
description: Geef identiteit van een mobiele app door aan mobiele webinhoud of een WebView, zodat rapportage en personalisatie in de webcontext kunnen worden voortgezet.
source-git-commit: bf0bb72777cacd822fd6e887ac3ef71764784214
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 0%

---

# Identiteit delen van mobiele apps naar mobiele websites/webweergaven

Wanneer een bezoeker van een mobiele app naar een webweergave of mobiele webpagina gaat, behouden de app- en webcontext elk hun eigen identiteit. Zonder expliciete overdracht behandelt de webervaring de bezoeker als een nieuwe, onbekende persoon, die fragmenten meldt en verpersoonlijking opnieuw begint.

Mobiel-aan-Web identiteit het delen lost dit door identiteitskaart van Experience Cloud van de bezoeker [ (ECID) over te gaan ](./overview.md) van mobiele toepassing aan de Webbestemming door een `adobe_mc` vraag-koord parameter. De parameter draagt de ECID, uw Experience Cloud-organisatie-id en een tijdstempel. Wanneer de webbestemming wordt geladen met een geldige `adobe_mc` -parameter, leest de Web SDK deze automatisch en past de uitgaande identiteit toe op het eerste Edge Network-verzoek, zodat beide contexten dezelfde bezoeker delen.

Gebruik dit patroon wanneer uw mobiele app een WebView of mobiele webpagina opent die door uw organisatie wordt beheerd en u toepassingsactiviteiten en webactiviteiten aan dezelfde bezoeker wilt koppelen. Als uw doel identiteitscontinuïteit tussen websites op verschillende domeinen is, gebruik [ dwars-domein delend ](cross-domain-sharing.md) in plaats daarvan.

## Vereisten

Voordat u begint, moet u ervoor zorgen dat uw implementatie aan de volgende vereisten voldoet:

* **Mobiele app**: Adobe Experience Platform Mobile SDK met de [ Identiteit voor Edge Network ](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/) uitbreidingsversie **1.1.0 of later** (iOS en Android).
* **bestemming van het Web**: De [ versie van SDK van het Web ](/help/collection/js/js-overview.md) **2.11.0 of later**, of de de markeringsuitbreiding van SDK van het Web.
* **controle URL**: Uw code controleert URL die app tot WebView of browser overgaat zodat u vraag-koordparameters aan het kunt toevoegen.
* **Vergelijkende configuratie**: De zelfde organisatieidentiteitskaart van Experience Cloud wordt gevormd in zowel de mobiele als Webimplementaties.

## Identiteit ophalen van de mobiele app {#retrieve-identity}

Gebruik de [`getUrlVariables` ](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables) API van de uitbreiding van Identiteit voor de uitbreiding van Edge Network om de identiteit van de bezoeker als vraagkoord terug te winnen. Vervolgens kunt u die tekenreeks aan de URL toevoegen voordat u de webweergave of browser opent.

De geretourneerde tekenreeks bevat de volgende URL-gecodeerde parameters:

| Parameter | Beschrijving |
| --- | --- |
| `MCID` | De Experience Cloud-id (ECID). |
| `MCORGID` | Je Experience Cloud-organisatie-id. Deze parameter moet de organisatie aanpassen die in het Web SDK op de bestemmingspagina wordt gevormd. |
| `TS` | Een tijdstempel. De bestemming moet deze waarde binnen **ontvangen vijf minuten** of het afbreken wordt verworpen. |

De volgende codevoorbeelden laten zien hoe een afbreking eruit kan zien in uw mobiele app:

>[!BEGINTABS]

>[!TAB  Swift (iOS) ]

```swift
Identity.getUrlVariables { (urlVariables, error) in
    if let error = error {
        // Handle the error
        return
    }

    guard let urlVariables = urlVariables else { return }

    // Construct the full URL by appending the identity query string
    if let url = URL(string: "https://example.com/webapp?\(urlVariables)") {
        // Open the URL in a WebView or browser
        let request = URLRequest(url: url)
        webView.load(request)
    }
}
```

>[!TAB  Kotlin (Android) ]

```kotlin
Identity.getUrlVariables { urlVariables ->
    if (urlVariables != null) {
        // Construct the full URL by appending the identity query string
        val url = "https://example.com/webapp?$urlVariables"

        // Open the URL in a WebView or browser
        webView.loadUrl(url)
    }
}
```

>[!ENDTABS]

## Identiteit ontvangen op de webzijde {#receive-identity}

Er is geen aanvullende code vereist voor de webbestemming. Wanneer de SDK Web aanwezig is op de pagina en de URL een geldige `adobe_mc` -parameter bevat, extraheert de SDK automatisch de ECID en past deze toe op de identiteitskaart van de bezoeker op de eerste Edge Network-aanvraag.

Als uw Webbestemming de de markeringsuitbreiding van SDK van het Web gebruikt en u de bezoeker aan een andere pagina moet opnieuw richten terwijl het bewaren van identiteit, gebruik [ Redirect met identiteit ](/help/tags/extensions/client/web-sdk/actions/redirect-with-identity.md) actie om de `adobe_mc` parameter aan de volgende pagina door:sturen.

>[!NOTE]
>
>De `adobe_mc` parameter verloopt na **vijf minuten**. Zorg ervoor dat de webbestemming wordt geladen en de eerste Edge Network-aanvraag direct na het openen van de URL verzendt.
