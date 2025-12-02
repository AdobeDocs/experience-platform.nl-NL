---
title: personalisatie
description: Verschillende inhoud aan verschillende gebruikers renderen, zodat ze een persoonlijke ervaring kunnen opdoen.
exl-id: 4bd370c8-8d8d-469e-9666-b5b6d0e3a660
source-git-commit: 54cd49bc1e6f23e3fb6d539274ea16d36ea21386
workflow-type: tm+mt
source-wordcount: '1244'
ht-degree: 0%

---

# `personalization`

Het `personalization` -object configureert welke verpersoonlijkingsbesluiten (aanbiedingen of voorstellen) worden aangevraagd en hoe deze in de aanvraag en het antwoord worden verwerkt. Deze functie is vooral handig bij Adobe Target- of Adobe Journey Optimizer-implementaties, omdat u hiermee de weergegeven inhoud per gebruiker kunt aanpassen.

```js
alloy("sendEvent", {
  personalization: {
    decisionScopes: ["hero-banner"],
    surfaces: ["web://example.com"],
    schemas: ["https://ns.adobe.com/personalization/dom-action"],
    sendDisplayEvent: true,
    sendDisplayNotifications: true,
    includePendingDisplayNotifications: true,
    defaultPersonalizationEnabled: false
  },
  renderDecisions: true,
  xdm: adobeDataLayer.getState(reference)
});
```

Het `personalization` -object bevat de volgende eigenschappen:

## `personalization.decisionScopes`

De eigenschap `decisionScopes` is een array van tekenreeksen die de Web SDK opdraagt om aanpassingsbeslissingen op te halen en te retourneren. Elk item in de array identificeert een locatie, context of logische plaatsing waar gepersonaliseerde inhoud gewenst is.

Deze eigenschap is handig wanneer u expliciet gepersonaliseerde inhoud wilt ophalen voor specifieke gebieden of componenten van een pagina. Het is vooral waardevol in single-page toepassingen die verschillende reeksen aanbiedingen zouden kunnen vereisen aangezien de navigatie of de mening van de gebruiker verandert. U kunt deze eigenschap ook gebruiken om de prestaties te optimaliseren door alleen aanbiedingen voor de interface-elementen op te halen die relevant zijn voor de gebruiker.

```js
personalization: {
  decisionScopes: ["hero-banner", "cart-offer"]
}
```

In Adobe Target wordt elk beslissingsbereik toegewezen aan een box of activiteit. In Adobe Journey Optimizer wordt elk beslissingsbereik toegewezen aan op beslissingen gebaseerde webinhoud-plaatsingen of -campagnes. In Offer Decisioning wordt een overzicht gegeven van de besluitvormingsgebieden waarop de bezoeker voorstellen of voorstellen kan ontvangen.

>[!TIP]
>
>Als u het algemene bereik wilt aanvragen (of blokkeren), gebruikt u [`defaultPersonalizationEnabled`](#personalizationdefaultpersonalizationenabled) in plaats van het hier in `decisionScopes` op te geven.

## `personalization.surfaces`

Het `surfaces` bezit is een serie van [&#x200B; oppervlakte URI &#x200B;](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/channels/code-based-experience/configure-code-based-channel/code-based-surface#surface-uri) koorden die manueel het kanaal, het apparaat, of de context bepalen waarvan verpersoonlijking wordt gevraagd. Hiermee kunt u onderscheid maken tussen verschillende digitale ervaringen, zoals domeinen, apps of apparaatplatform binnen uw kanaalecosysteem. Standaard wordt het standaardoppervlak van de huidige pagina door de bibliotheek opgehaald. U kunt deze eigenschap gebruiken om het automatisch gegenereerde oppervlak voor de huidige pagina te overschrijven.

Dit bezit is waardevol wanneer u kanaalverpersoonlijking wilt gebruiken en moet onderscheiden hoe de verpersoonlijking tussen afzonderlijke kanalen werkt. Hiermee kunt u verschillende aanbiedingen maken voor verschillende sites onder dezelfde Adobe Experience Platform-organisatie.

```js
personalization: {
  surfaces: ["web://example.com", "web://support.example.com/contact"]
}
```

Deze eigenschap wordt voornamelijk gebruikt bij Adobe Journey Optimizer omdat deze overeenkomt met oppervlakken die zijn ingesteld in Journey Optimizer-campagnes en oppervlakbeheer.

## `personalization.schemas`

De eigenschap `schemas` is een array van schema-URI-tekenreeksen die de typen personalisatie-inhoud filteren die van de Edge Network worden gevraagd. Als u deze eigenschap instelt, wordt het antwoord dat u van Adobe ontvangt, beperkt tot alleen aanbiedingen die overeenkomen met de definities van het inhoudstype die u opgeeft. Als u deze optie weglaat, worden in de bibliotheek alle beschikbare schema&#39;s voor het overeenkomende bereik of de overeenkomende oppervlakken opgevraagd.

Met deze eigenschap kunt u de responsgrootte optimaliseren en ervoor zorgen dat uw website of toepassing alleen aanbiedingstypen ontvangt die deze kan verwerken. Het is ook handig als u toepassingen van één pagina gebruikt die gepersonaliseerde inhoud op een specifieke manier renderen (zoals alleen DOM-handelingen of alleen JSON-objecten).

```js
personalization: {
  schemas: [
    "https://ns.adobe.com/personalization/dom-action",
    "https://ns.adobe.com/personalization/html-content-item"
  ]
}
```

De volgende schema-URI&#39;s worden ondersteund:

* **`https://ns.adobe.com/personalization/dom-action`**: aanbiedingen die directe DOM-handelingen zijn, die doorgaans worden gegenereerd door de Visual Experience Composer in Adobe Target. Ze bevatten instructies voor het automatisch manipuleren van elementen op de pagina zonder extra code. Dit is de standaard voor automatisch gerenderde webpersonalisatie.
* **`https://ns.adobe.com/personalization/html-content-item`**: aanbiedingen die onbewerkte HTML bevatten die als een tekenreeks worden geleverd. Uw implementatie voegt deze inhoud gewoonlijk op de gewenste locatie op de pagina in, zodat u meer controle hebt dan DOM-handelingen. Wordt meestal gebruikt voor banners, fragmenten of modale inhoud.
* **`https://ns.adobe.com/personalization/json-content-item`**: aanbiedingen die zijn opgemaakt als een JSON-object. Meestal gebruikt in API-gebaseerde implementaties of front-ends die gestructureerde gegevens in plaats van HTML- of DOM-wijzigingen verwachten.
* **`https://ns.adobe.com/personalization/redirect-item`**: aanbiedingen die omleiden naar een andere URL. Wordt gebruikt om de gebruiker naar een nieuwe pagina te verplaatsen op basis van logica voor doelframes of beslissingen, zoals pagina&#39;s landen of instapstromen.
* **`https://ns.adobe.com/personalization/ruleset-item`**: levert een blok van bedrijfslogica om een cliënt-zijregelmotor aan te drijven. Bevat een versioned heersenset die logische voorwaarden en gevolgen (als/toen verpersoonlijkingslogica) bepaalt.
* **`https://ns.adobe.com/personalization/message/in-app`**: aanbiedingen die specifiek zijn opgemaakt voor Adobe Journey Optimizer-berichten in de app, die doorgaans worden weergegeven als modules, banners, pop-ups of overlays.
* **`https://ns.adobe.com/personalization/message/content-card`**: aanbiedingen die specifiek zijn opgemaakt voor Adobe Journey Optimizer-inhoudskaarten en die zijn ontworpen voor vaste of inbox-feeds in web- of mobiele apps.
* **`https://ns.adobe.com/personalization/message/native-alert`**: aanbiedingen die specifiek zijn opgemaakt voor eigen Adobe Journey Optimizer-waarschuwingen en die dialoogvensters voor native meldingen via een platform activeren.
* **`https://ns.adobe.com/personalization/measurement`**: gebruikt om kliks en interacties op gepersonaliseerde aanbiedingen te volgen. Bevat geen inhoud die kan worden weergegeven.
* **`https://ns.adobe.com/personalization/eventHistoryOperation`**: schema voor het wijzigen van de gebeurtenisgeschiedenis van een bezoeker in lokale opslag. Wordt intern door SDK&#39;s gebruikt voor het bijhouden van ervaringen die zijn geleverd of geblokkeerd. Bevat geen inhoud die kan worden weergegeven.
* **`https://ns.adobe.com/personalization/default-content-item`**: Fallback- of standaardinhoud, doorgaans wanneer geen gepersonaliseerde aanbieding in aanmerking komt. Hierdoor wordt gegarandeerd dat gebruikers die niet in aanmerking komen nog steeds inhoud ontvangen, waardoor de ervaring consistent blijft.

## `personalization.sendDisplayEvent`

De eigenschap `sendDisplayEvent` is een Booleaanse waarde die bepaalt of een weergavemeldingsgebeurtenis automatisch naar de Edge Network wordt verzonden direct nadat persoonlijke inhoud op de pagina is gerenderd. Als deze waarde wordt weggelaten, is de standaardwaarde `true` . Stel deze variabele in op `false` als u niet wilt aangeven dat gepersonaliseerde inhoud is gerenderd voor het bijhouden van de indruk.

Het meest gebruikte geval voor het instellen van deze variabele op `false` is wanneer u een andere opdracht elders in de implementatie wilt verzenden die een weergavegebeurtenis markeert. Sommige implementaties hebben zowel indruk- als analytische gebeurtenissen. Deze eigenschap geeft u de volledige controle over welke `sendEvent` -opdrachten de increment impressies verhogen.

```js
personalization: {
  sendDisplayEvent: true
}
```

>[!NOTE]
>
>Eerdere versies van de Web SDK (versies 2.12.0 en eerder) gebruiken in plaats daarvan `sendDisplayNotifications` .

## `personalization.includePendingDisplayNotifications`

De eigenschap `includePendingDisplayNotifications` is een Booleaanse waarde die bepaalt of weergavemeldingen die in behandeling zijn, worden gebundeld in de huidige `sendEvent` -aanroep. In afwachting van weergavemeldingen zijn afbeeldingen van gepersonaliseerde inhoud die wel zijn gerenderd, maar nog niet als weergavegebeurtenis aan de Edge Network zijn gerapporteerd. Deze eigenschap is handig bij het gebruik van toepassingen van één pagina, omdat het renderen van gepersonaliseerde inhoud en `sendEvent` -aanroepen asynchroon met elkaar kunnen zijn.

De standaardwaarde voor deze eigenschap is `false` . Stel deze eigenschap in op `true` als u alle weergavemeldingen die in behandeling zijn, wilt batchgewijs en leegmaken, zodat de indrukkingen ervan op de juiste wijze worden opgenomen. Synchrone implementatie, zoals traditionele websites, hoeft deze eigenschap gewoonlijk niet in te stellen.

```js
personalization: {
  includePendingDisplayNotifications: true
}
```

## `personalization.defaultPersonalizationEnabled`

De eigenschap `defaultPersonalizationEnabled` is een Booleaanse waarde die u expliciete controle geeft over de manier waarop de Web SDK het standaardverpersoonlijkingsbereik (`__view__`) voor de hele pagina aanvraagt en het oppervlak voor deze `sendEvent` opdracht. Standaard biedt de Web SDK-aanvraag voor de eerste `sendEvent` -opdracht na het laden van een pagina het standaardverpersoonlijkingsbereik voor de hele pagina en de bijbehorende oppervlakken aan. Volgende `sendEvent` -opdrachten vragen niet om standaardaanpassing. U kunt deze eigenschap gebruiken om dat gedrag te overschrijven. Het is nuttig in toepassingsimplementaties van één pagina waar u standaardverpersoonlijking opnieuw zou kunnen willen vragen aangezien de gebruiker uw plaats navigeert. U kunt dit bezit ook gebruiken wanneer u _slechts_ een vertoningsgebeurtenis wilt verzenden zonder aanbiedingsherwinning te dupliceren.

```js
personalization: {
  defaultPersonalizationEnabled: false
}
```

Deze eigenschap gebruikt de volgende logica, afhankelijk van de manier waarop deze is ingesteld:

* **niet plaats**: De standaardverpersoonlijking van het verzoek wanneer het nog niet is gevraagd. Standaardaanpassing wordt doorgaans aangevraagd op de eerste `sendEvent` na het laden van een pagina, en niet opnieuw aangevraagd bij volgende `sendEvent` -aanroepen op dezelfde pagina. Door deze eigenschap in te stellen, wordt dit gedrag genegeerd.
* **`true`**: vraag expliciet om het paginabereik en het standaardoppervlak, zelfs als deze opdracht `sendEvent` niet de eerste opdracht is na het laden van een pagina. De ideale tijden om deze eigenschap in te stellen op `true` zijn wanneer u een standaardverpersoonlijkingsverzoek moet afdwingen, zoals in toepassingsscenario&#39;s van één pagina.
* **`false`**: onderdruk expliciet de aanvraag voor het paginabereik en het standaardoppervlak, zelfs als deze `sendEvent` -opdracht de eerste opdracht is na het laden van een pagina. De ideale tijd om deze eigenschap in te stellen op `false` is wanneer u wilt dat een bepaalde opdracht van `sendEvent` geen nieuwe aanbiedingen aanvraagt en in plaats daarvan alleen gegevens naar Analytics verzendt of een weergavegebeurtenis verzendt.

## Personalization-componenten die de Web SDK-tagextensie gebruiken

Het equivalent van de de marktextensie van SDK van het Web van dit bezit is de [**[!UICONTROL Personalization]**](/help/tags/extensions/client/web-sdk/actions/send-event.md#personalization-fields) sectie wanneer het vormen van een &quot;[!UICONTROL Send event]&quot;actie.
