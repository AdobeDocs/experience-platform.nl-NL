---
title: De IAB TCF 2.0-ondersteuning integreren met tags en de Experience Platform Web SDK Extension
description: Leer hoe u IAB TCF 2.0-toestemming voor tags en de Adobe Experience Platform Web SDK-extensie instelt.
exl-id: dc0e6b68-8257-4862-9fc4-50b370ef204f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 0%

---

# De IAB TCF 2.0-ondersteuning integreren met tags en de Experience Platform Web SDK-extensie

Adobe Experience Platform Web SDK ondersteunt het Interactive Advertising Bureau Transparency &amp; Consent Framework, versie 2.0 (IAB TCF 2.0). Deze gids toont u hoe te opstelling een markeringsbezit voor het verzenden van IAB TCF 2.0 toestemmingsinformatie naar Adobe gebruikend de de marktextensie van SDK van het Web van Adobe Experience Platform.

Als u niet wenst om markeringen te gebruiken, te verwijzen gelieve naar de gids op [ gebruikend IAB TCF 2.0 zonder markeringen ](./without-tags.md).

## Aan de slag

Om IAB TCF 2.0 met markeringen en de uitbreiding van SDK van het Web van Experience Platform te gebruiken, moet u een beschikbaar schema XDM en dataset hebben.

Bovendien is voor deze handleiding een goed begrip van Adobe Experience Platform Web SDK vereist. Voor een snelle verfrisser, te lezen gelieve het [ overzicht van SDK van het Web van Adobe Experience Platform ](../../home.md) en [ vaak gestelde vragen ](../../faq.md) documentatie.

## Standaardtoestemming instellen

Binnen de uitbreidingsconfiguratie, is er een het plaatsen voor standaardtoestemming. Dit beheerst het gedrag van klanten die geen toestemmingskoekje hebben. Als u Experience Events wilt bewaren voor klanten die geen toestemmingskoekje hebben, plaats dit aan `pending`. Als u Experience Events wilt verwijderen voor klanten die geen toestemmingscookie hebben, stelt u deze in op `out` . U kunt ook een gegevenselement gebruiken om de standaardwaarde voor toestemming dynamisch in te stellen. Zie [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) voor meer informatie.

## Profiel bijwerken met toestemmingsinformatie {#consent-code-1}

Als u de handeling [`setConsent`](/help/web-sdk/commands/setconsent.md) wilt aanroepen wanneer de voorkeuren van uw klanten voor toestemming zijn gewijzigd, maakt u een labelregel. Begin door een nieuwe gebeurtenis toe te voegen en kies het de gebeurtenistype van de &quot;Code van de Douane&quot;van de uitbreiding van de Kern.

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

* Stelt twee gegevenselementen in, één met de toestemmingstekenreeks en één met de markering `gdprApplies` . Dit is handig als u de handeling &quot;Instemming instellen&quot; later invult.

* De regel wordt geactiveerd wanneer de voorkeuren voor toestemming zijn gewijzigd. De actie &quot;Goedkeuring instellen&quot; moet worden gebruikt wanneer de voorkeuren voor toestemming zijn gewijzigd. Voeg de actie &quot;Goedkeuring instellen&quot; toe aan de extensie en vul het formulier als volgt in:

* Standaard: &quot;IAB TCF&quot;
* Versie: &quot;2.0&quot;
* Waarde: &quot;%IAB TCF toestemming String%&quot;
* GDPR is van toepassing: &quot;%IAB TCF Consent GDPR%&quot;

![ IAB plaatste de Actie van de Toestemming ](../../assets/consent/iab-tcf/with-launch/iab-action.png)

>[!IMPORTANT]
>
>U kunt deze gegevenselementen niet kiezen met de gegevenselementkiezer omdat ze zijn gemaakt met aangepaste code. U moet in de naam van het gegevenselement met de percentagetekens typen. Deze code werkt het profiel van uw klant bij met de nieuwe voorkeuren voor toestemming wanneer deze worden gewijzigd. Bovendien retourneert de server een cookiewaarde die kan voorkomen dat Adobe Experience Platform Web SDK Experience Events opneemt.

## Een XDM-gegevenselement maken voor Experience Events

De toestemmingskoord zou in de Gebeurtenis van de Ervaring moeten worden omvat XDM. Hiervoor gebruikt u het gegevenselement XDM Object. Begin door een nieuw gegevenselement van Objecten te creëren XDM, of anders, gebruik reeds voor het verzenden van gebeurtenissen gecreeerd. Als u de het schemagroep van de Privacy van de Gebeurtenis van de Ervaring aan uw schema hebt toegevoegd, zou u een `consentStrings` sleutel in het voorwerp XDM moeten hebben.

1. Selecteer **[!UICONTROL consentStrings]**.

1. Kies **[!UICONTROL Provide individual items]** en selecteer **[!UICONTROL Add Item]** .

1. Vouw de kop **[!UICONTROL consentString]** uit, vouw het eerste item uit en vul vervolgens de volgende waarden in:

* `consentStandard`: IAB TCF
* `consentStandardVersion` : 2.0
* `consentStringValue`: %IAB TCF toestemming String%
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

Deze code is identiek aan de vorige aangepaste code, behalve dat zowel `useractioncomplete` - als `tcloaded` -gebeurtenissen worden afgehandeld. De [ vorige douanecode ](#consent-code-1) brengt slechts teweeg wanneer de klant hun voorkeur voor het eerst kiest. Deze code wordt ook geactiveerd wanneer de klant al zijn voorkeuren heeft gekozen. Bijvoorbeeld op de tweede pagina laden.

Voeg een actie &quot;Send Event&quot; toe vanuit de Experience Platform Web SDK-extensie. Kies in het XDM-veld het XDM-gegevenselement dat u in de vorige sectie hebt gemaakt.

## Andere gebeurtenissen verzenden met IAB TCF 2.0 toestemmingsinformatie

Wanneer gebeurtenissen worden geactiveerd na de initiële Experience Event, zijn de twee gegevenselementen nog steeds gedefinieerd en kunnen deze worden gebruikt om de informatie over de IAB-toestemming te verzenden. Gebruik hetzelfde XDM-gegevenselement om toekomstige gebeurtenissen te verzenden. Informatie over IAB TCF 2.0 is inbegrepen.

## Volgende stappen

Nu u hebt geleerd hoe u IAB TCF 2.0 met de uitbreiding van Experience Platform Web SDK kunt gebruiken, kunt u ook verkiezen om met andere oplossingen van Adobe zoals Adobe Analytics of Adobe Real-Time Customer Data Platform te integreren. Zie het [ IAB overzicht van de Transparantie &amp; van de Toestemming Kader 2.0 ](./overview.md) voor meer informatie.
