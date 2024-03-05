---
title: setConsent
description: Wordt op elke pagina gebruikt om de toestemming van de gebruiker bij te houden.
source-git-commit: 90493d179e620604337bda96cb3b7f5401ca4a81
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 0%

---

# setConsent

De `setConsent` vertelt de SDK van het Web of het gegevens (opt in) zou moeten verzenden, gegevens (opt out) zou verwerpen, of gebruik [`defaultConsent`](configure/defaultconsent.md) (toestemming onbekend).

De SDK van het Web ondersteunt de volgende standaarden:

* **[Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Zowel 1.0- als 2.0-standaarden worden ondersteund.
* **[IAB-framework voor transparantie en instemming](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Als u deze standaard gebruikt, wordt het Real-Time Klantprofiel van de bezoeker bijgewerkt met de gegevens van de toestemming als uw implementatie correct is geconfigureerd:
   1. Het afzonderlijke XDM-profielschema bevat het [IAB TCF 2.0 Goedgekeurde gebiedsgroep](/help/xdm/field-groups/profile/iab.md).
   1. Het schema Experience Event bevat de [IAB TCF 2.0 Goedgekeurde gebiedsgroep](/help/xdm/field-groups/event/iab.md).
   1. U neemt de informatie van de IAB toestemming in het geval op [XDM-object](sendevent/xdm.md). De Web SDK omvat automatisch niet de toestemmingsinformatie wanneer het verzenden van gebeurtenisgegevens.

Na het gebruiken van dit bevel, schrijft het Web SDK de voorkeur van de gebruiker aan een koekje. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren die nog steeds aanwezig zijn op om te bepalen of gebeurtenissen naar de Adobe kunnen worden verzonden.

Adobe raadt u aan om voorkeuren voor het toestemmingsdialoogvenster los van de toestemming van Web SDK op te slaan. De Web SDK biedt geen manier om toestemming terug te winnen. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de `setConsent` gebruiken bij elke pagina die wordt geladen. SDK van het Web maakt slechts een servervraag wanneer de toestemming verandert.

## Toestemming instellen met de extensie van de Web SDK-tag

Het plaatsen van toestemming wordt uitgevoerd als actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Aanmelden bij [experience.adobe.com](https://experience.adobe.com) je Adobe ID-gebruikersgegevens gebruiken.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeren naar **[!UICONTROL Rules]** Selecteer vervolgens de gewenste regel.
1. Onder [!UICONTROL Actions], selecteert u een bestaande actie of maakt u een actie.
1. Stel de [!UICONTROL Extension] vervolgkeuzeveld naar **[!UICONTROL Adobe Experience Platform Web SDK]** en stelt de [!UICONTROL Action Type] tot **[!UICONTROL Set consent]**.
1. Stel de gewenste velden rechts in, inclusief **[!UICONTROL Standard]** en **[!UICONTROL General consent]**.
1. Klikken **[!UICONTROL Keep Changes]** en voer vervolgens uw publicatieworkflow uit.

U kunt meerdere objecten voor toestemming in deze handeling opnemen.

## Goedkeuring instellen met de Web SDK JavaScript-bibliotheek

Voer de `setConsent` bevel wanneer het roepen van uw gevormde instantie van het Web SDK. U kunt de volgende objecten in deze opdracht opnemen:

* **`consent[]`**: Een array van `consent` objecten. Het bevestigingsobject wordt op een andere manier opgemaakt, afhankelijk van de standaard en versie die u kiest.
* **`identityMap`**: Een object dat bepaalt hoe een ECID wordt gegenereerd en aan welke ID&#39;s toestemmingsinformatie is gekoppeld. Adobe raadt aan dit object op te nemen wanneer `setConsent` wordt uitgevoerd vóór andere opdrachten, zoals [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Een object dat bevat [gegevensstroomconfiguratie overschrijft](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-standaard `consent` object

* **`standard`**: De standaard voor toestemming die u kiest. Deze eigenschap instellen op `"Adobe"` voor de Adobe 2.0-norm.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Deze eigenschap instellen op `"2.0"` voor de Adobe 2.0-norm.
* **`value`**: Een object met toestemmingswaarden.
   * **`value.collect.val`**: De waarde van de toestemming. Geldige waarden zijn `"y"` (opt in) en `"n"` (opt-out).
   * **`value.metadata.time`**: Het tijdstempel dat de gebruiker instelt als waarde voor toestemming.

```js
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "2.0",
    "value": {
      "collect": {
        "val": "y"
      },
      "metadata": {
        "time": "YYYY-03-17T15:48:42-07:00"
      }
    }
  }]
});
```

>[!TAB IAB TCF 2.0]

### IAB TCF 2.0-standaard `consent` object

* **`standard`**: De standaard voor toestemming die u kiest. Deze eigenschap instellen op `"IAB TCF"` voor de IAB TCF 2.0-standaard.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Deze eigenschap instellen op `"2.0"` voor de IAB TCF 2.0-standaard.
* **`value`**: Een tekenreeks die de waarde voor de toestemming bevat.
* **`gdprApplies`**: Een Booleaanse waarde die bepaalt of GDPR op deze toestemmingswaarde van toepassing is. De standaardwaarde is `true`.
* **`gdprContainsPersonalData`**: Een Booleaanse waarde die bepaalt of de gebeurtenisgegevens die aan deze gebruiker zijn gekoppeld, persoonlijke gegevens bevatten. De standaardwaarde is `false`.

```js
alloy("setConsent", {
  consent: [{
    "standard": "IAB TCF",
    "version": "2.0",
    "value": "CO052l-O052l-DGAMBFRACBgAIBAAAAABIYgEawAQEagAAAA",
    "gdprApplies": true,
    "gdprContainsPersonalData": true
  }]
});
```

>[!TAB Adobe 1.0]

### Adobe 1.0 standaard `consent` object

* **`standard`**: De standaard voor toestemming die u kiest. Deze eigenschap instellen op `"Adobe"` voor Adobe 1.0.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Deze eigenschap instellen op `"1.0"` voor Adobe 1.0.
* **`value.general`**: De waarde van de toestemming. Geldige waarden zijn `"in"` (opt in) en `"out"` (opt-out).

```js
// Set consent using the Adobe 1.0 standard
alloy("setConsent", {
  "consent": [{
    "standard": "Adobe",
    "version": "1.0",
    "value": {
      "general": "in"
    }
  }]
});
```

>[!ENDTABS]
