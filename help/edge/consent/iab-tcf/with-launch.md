---
title: Integreer de Steun van IAB TCF 2.0 gebruikend Platform launch en de Uitbreiding van SDK van het Web van het Platform
description: Leer hoe u IAB TCF 2.0 instelt voor toestemming met Adobe Experience Platform Launch en de Adobe Experience Platform Web SDK-extensie.
translation-type: tm+mt
source-git-commit: b9fb71ac7eca95c65165d6780b681ada3f16325b
workflow-type: tm+mt
source-wordcount: '855'
ht-degree: 0%

---


# Integreer IAB TCF 2.0 steun gebruikend Platform launch en de uitbreiding van SDK van het Web van het Platform

Adobe Experience Platform Web SDK ondersteunt het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont u hoe te opstelling een bezit van Adobe Experience Platform Launch voor het verzenden van IAB TCF 2.0 toestemmingsinformatie aan Adobe gebruikend de uitbreiding van SDK van het Web van Adobe Experience Platform voor Experience Platform Launch.

Als u Experience Platform Launch niet wenst te gebruiken, te verwijzen gelieve naar de gids op [gebruikend IAB TCF 2.0 zonder Experience Platform Launch](./without-launch.md).

## Aan de slag

Om IAB TCF 2.0 met Experience Platform Launch en de uitbreiding van SDK van het Web van het Platform te gebruiken, moet u een beschikbaar schema XDM en dataset hebben.

Bovendien vereist deze handleiding dat u een goed begrip hebt van de SDK van Adobe Experience Platform Web. Lees voor een snelle vernieuwing de [Adobe Experience Platform Web SDK overview](../../home.md) en de [Veelgestelde vragen](../../web-sdk-faq.md) documentatie.

## Standaardtoestemming instellen

Binnen de uitbreidingsconfiguratie, is er een het plaatsen voor standaardtoestemming. Dit beheerst het gedrag van klanten die geen toestemmingskoekje hebben. Als u Experience Events wilt bewaren voor klanten die geen toestemmingskoekje hebben, plaats dit aan `pending`. Als u Experience Events wilt verwijderen voor klanten die geen toestemmingscookie hebben, stelt u deze in op `out`. U kunt ook een gegevenselement gebruiken om de standaardwaarde voor toestemming dynamisch in te stellen.

Voor meer informatie over hoe te om standaardtoestemming te vormen, verwijs naar [standaardtoestemmingssectie](../../fundamentals/configuring-the-sdk.md#default-consent) in de de configuratiegids van SDK.

## Profiel bijwerken met toestemmingsinformatie {#consent-code-1}

Als u de handeling `setConsent` wilt aanroepen wanneer uw klanten hun voorkeuren hebben gewijzigd, moet u een nieuwe regel voor Experience Platforms Launch maken. Begin door een nieuwe gebeurtenis toe te voegen en kies het de gebeurtenistype van de &quot;Code van de Douane&quot;van de uitbreiding van de Kern.

Gebruik het volgende codevoorbeeld voor uw nieuwe gebeurtenis:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Deze aangepaste code doet twee dingen:

* Stelt twee gegevenselementen in, één met de toestemmingstekenreeks en één met de markering `gdprApplies`. Dit is handig als u de handeling &quot;Instemming instellen&quot; later invult.

* De regel wordt geactiveerd wanneer de voorkeuren voor toestemming zijn gewijzigd. De actie &quot;Goedkeuring instellen&quot; moet worden gebruikt wanneer de voorkeuren voor toestemming zijn gewijzigd. Voeg de actie &quot;Goedkeuring instellen&quot; toe aan de extensie en vul het formulier als volgt in:

* Standaard: &quot;IAB TCF&quot;
* Versie: &quot;2.0&quot;
* Waarde: &quot;%IAB TCF toestemming String%&quot;
* GDPR is van toepassing: &quot;%IAB TCF toestemming GDPR%&quot;

![IAB-actie voor toestemming instellen](../../images/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>U kunt deze gegevenselementen niet kiezen met de gegevenselementkiezer omdat ze zijn gemaakt met aangepaste code. U moet in de naam van het gegevenselement met de percentagetekens typen. Deze code werkt het profiel van uw klant bij met de nieuwe voorkeuren voor toestemming wanneer deze worden gewijzigd. Bovendien retourneert de server een cookiewaarde die kan voorkomen dat Adobe Experience Platform Web SDK ervaringsgebeurtenissen opneemt.

## Een XDM-gegevenselement maken voor Experience Events

De toestemmingskoord zou in de Gebeurtenis van de Ervaring moeten worden omvat XDM. Hiervoor gebruikt u het gegevenselement XDM Object. Begin door een nieuw gegevenselement van Objecten te creëren XDM, of anders, gebruik reeds voor het verzenden van gebeurtenissen gecreeerd. Als u de mix van de Privacy van de Gebeurtenis van de Ervaring aan uw schema hebt toegevoegd, zou u een `consentStrings` sleutel in het voorwerp XDM moeten hebben.

1. Selecteer **[!UICONTROL permissionStrings]**.

1. Kies **[!UICONTROL Afzonderlijke items opgeven]** en **[!UICONTROL Item toevoegen]** selecteren.

1. Breid **[!UICONTROL permissionString]** rubriek uit, en breid het eerste punt uit, dan vul de volgende waarden in:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2,0
* `consentStringValue`: %IAB TCF goedkeuring String%
* `gdprApplies`: %IAB TCF toestemming GDPR%

>[!IMPORTANT]
>
>U kunt deze gegevenselementen niet kiezen met de gegevenselementkiezer omdat ze zijn gemaakt met aangepaste code. U moet in de naam van het gegevenselement met de percentagetekens typen.

## Een initiële Experience Event verzenden met IAB TCF 2.0 toestemmingsinformatie

Als de initiële Experience Event op de pagina wordt geactiveerd met een page load-gebeurtenis, is de toestemmingstekenreeks mogelijk nog niet geladen. Deze regel is bedoeld om de huidige gebeurtenis voor het laden van de pagina te vervangen. Om ervoor te zorgen dat de toestemmingsinformatie eerst wordt geladen, creeer een nieuwe regel en voeg de volgende code als gebeurtenis van de douanecode toe:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when there is a consent string
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && (tcData.eventStatus === "useractioncomplete" || tcData.eventStatus === "tcloaded")) {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF GDPR Applies", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn"t defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

Deze code is identiek aan de vorige douanecode, behalve dat zowel `useractioncomplete` als `tcloaded` gebeurtenissen worden behandeld. De [vorige aangepaste code](#consent-code-1) wordt alleen geactiveerd wanneer de klant voor het eerst zijn voorkeuren kiest. Deze code wordt ook geactiveerd wanneer de klant al zijn voorkeuren heeft gekozen. Bijvoorbeeld op de tweede pagina laden.

Voeg een actie &quot;Send Event&quot;van de uitbreiding van SDK van het Web van het Platform toe. Kies in het XDM-veld het XDM-gegevenselement dat u in de vorige sectie hebt gemaakt.

## Andere gebeurtenissen verzenden met IAB TCF 2.0 toestemmingsinformatie

Wanneer gebeurtenissen worden geactiveerd na de initiële Experience Event, zijn de twee gegevenselementen nog steeds gedefinieerd en kunnen deze worden gebruikt om de informatie over de IAB-toestemming te verzenden. Gebruik hetzelfde XDM-gegevenselement om toekomstige gebeurtenissen te verzenden. TCF 2.0-informatie voor IAB is opgenomen.

## Volgende stappen

Nu u hebt geleerd hoe te om IAB TCF 2.0 met de uitbreiding van SDK van het Web van het Platform te gebruiken, kunt u ook verkiezen om met andere Adobe oplossingen zoals Adobe Analytics of platform van de Gegevens van de Klant in real time te integreren. Zie [IAB Transparency &amp; Consent Framework 2.0 overzicht](./overview.md) voor meer informatie.
