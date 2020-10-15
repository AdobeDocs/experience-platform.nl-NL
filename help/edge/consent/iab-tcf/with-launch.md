---
title: IAB TCF 2.0 gebruiken met Experience Platform Launch
seo-title: IAB TCF 2.0-toestemming instellen met Adobe Experience Platform Launch en de Adobe Experience Platform Web SDK
description: Leer hoe u IAB TCF 2.0-toestemming instelt voor Adobe Experience Platform Launch en Adobe Experience Platform Web SDK
seo-description: Leer hoe u IAB TCF 2.0-toestemming instelt voor Adobe Experience Platform Launch en Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: db742119d8f169817080f1fd4e0dc08a0f0faa47
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%

---


# Het gebruiken van IAB TCF 2.0 met Experience Platform Launch en de uitbreiding van SDK van het Web AEP

De Adobe Experience Platform Web Software Development Kit (Adobe Experience Platform Web SDK) ondersteunt het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont u hoe te opstelling een bezit van Adobe Experience Platform Launch voor het verzenden van IAB TCF 2.0 toestemmingsinformatie aan Adobe gebruikend de uitbreiding van SDK van het Web AEP voor Experience Platform Launch.

Als u geen Experience Platform Launch wilt gebruiken, raadpleeg dan de handleiding over het [gebruik van IAB TCF 2.0 zonder Experience Platform Launch](./without-launch.md).

## Aan de slag

Om IAB TCF 2.0 met Experience Platform Launch en de uitbreiding van SDK van het Web te gebruiken AEP, moet u een beschikbaar schema XDM en dataset hebben. Als u geen van beide hebt ingesteld, begint u met het bekijken van deze handleiding voor snel starten van Adobe Experience Platform Web SDK voordat u verdergaat.

Bovendien, vereist deze gids u een werkend inzicht in de SDK van het Web van Adobe Experience Platform te hebben. Lees voor een snelle vernieuwing het overzicht [van de SDK van het](../../home.md) Adobe Experience Platform-web en de documentatie met [veelgestelde vragen](../../web-sdk-faq.md) .

## Standaardtoestemming instellen

Binnen de uitbreidingsconfiguratie, is er een het plaatsen voor standaardtoestemming. Dit beheerst het gedrag van klanten die geen toestemmingskoekje hebben. Als u de Gebeurtenissen van de Ervaring voor klanten wilt een rij vormen die geen toestemmingskoekje hebben, plaats dit aan `pending`.

>[!NOTE]
>
>Momenteel is het niet mogelijk dit dynamisch in te stellen via de extensie Experience Platform Launch.

Raadpleeg de sectie [over](../../fundamentals/configuring-the-sdk.md#default-consent) standaardtoestemming in de documentatie bij de SDK-configuratie voor meer informatie over standaardtoestemming.

## Profiel bijwerken met toestemmingsinformatie {#consent-code-1}

Om de `setConsent` actie te roepen wanneer uw klanten toestemmingsvoorkeur zijn veranderd, moet u een nieuwe Experience Platform Launch regel tot stand brengen. Begin door een nieuwe gebeurtenis toe te voegen en kies het de gebeurtenistype van de &quot;Code van de Douane&quot;van de uitbreiding van de Kern.

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

* Stelt twee gegevenselementen in, één met de toestemmingstekenreeks en één met de `gdprApplies` markering. Dit is handig als u de handeling &quot;Instemming instellen&quot; later invult.

* De regel wordt geactiveerd wanneer de voorkeuren voor toestemming zijn gewijzigd. De actie &quot;Goedkeuring instellen&quot; moet worden gebruikt wanneer de voorkeuren voor toestemming zijn gewijzigd. Voeg de actie &quot;Goedkeuring instellen&quot; toe aan de extensie en vul het formulier als volgt in:

* Standaard: &quot;IAB TCF&quot;
* Versie: &quot;2.0&quot;
* Waarde: &quot;%IAB TCF toestemming String%&quot;
* GDPR is van toepassing: &quot;%IAB TCF toestemming GDPR%&quot;

![IAB-actie voor toestemming instellen](../../../assets/iab_set_consent_action.png)

>[!IMPORTANT]
>
>U kunt deze gegevenselementen niet kiezen met de gegevenselementkiezer omdat ze zijn gemaakt met aangepaste code. U moet in de naam van het gegevenselement met de percentagetekens typen. Deze code werkt het profiel van uw klant bij met de nieuwe voorkeuren voor toestemming wanneer deze worden gewijzigd. Bovendien retourneert de server een cookie-waarde die kan voorkomen dat de Adobe Experience Platform Web SDK ervaringsgebeurtenissen opneemt.

## Een XDM-gegevenselement maken voor Experience Events

De toestemmingskoord zou in de Gebeurtenis van de Ervaring moeten worden omvat XDM. Hiervoor gebruikt u het gegevenselement XDM Object. Begin door een nieuw gegevenselement van Objecten te creëren XDM, of anders, gebruik reeds voor het verzenden van gebeurtenissen gecreeerd. Als u de mix Experience Event Privacy aan uw schema hebt toegevoegd, moet u een `consentStrings` sleutel in het XDM-object hebben.

1. Selecteer **[!UICONTROL permissionStrings]**.

1. Kies **[!UICONTROL Afzonderlijke items]** opgeven en selecteer Item **** toevoegen.

1. Vouw de kop **[!UICONTROL permissionString]** uit, vouw het eerste item uit en vul vervolgens de volgende waarden in:

* `consentStandard`: IAB TCF
* `consentStandardVersion`: 2.0
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

Voeg de actie &quot;Send Event&quot; toe vanuit de extensie Adobe Experience Platform Web SDK. Kies in het XDM-veld het XDM-gegevenselement dat u in de vorige sectie hebt gemaakt.

## Andere gebeurtenissen verzenden met IAB TCF 2.0 toestemmingsinformatie

Wanneer gebeurtenissen worden geactiveerd na de initiële Experience Event, zijn de twee gegevenselementen nog steeds gedefinieerd en kunnen deze worden gebruikt om de informatie over de IAB-toestemming te verzenden. Gebruik hetzelfde XDM-gegevenselement om toekomstige gebeurtenissen te verzenden. De informatie van IAB TCF 2.0 is inbegrepen.

## Volgende stappen

Nu u hebt geleerd hoe te om IAB TCF 2.0 met de uitbreiding van SDK van het Web van Adobe Experience Platform te gebruiken, kunt u ook verkiezen om met andere oplossingen van de Adobe zoals Adobe Analytics of het platform van de Gegevens van de Klant in real time te integreren. Zie het overzicht [van](./overview.md) IAB Transparency &amp; Consent Framework 2.0 voor meer informatie.
