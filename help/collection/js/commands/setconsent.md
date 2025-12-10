---
title: setConsent
description: Wordt op elke pagina gebruikt om de voorkeuren voor gebruikersmachtigingen bij te houden.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1117'
ht-degree: 0%

---


# `setConsent`

De opdracht `setConsent` geeft aan de Web SDK door of gegevens moeten worden verzonden (aanmelden), gegevens moeten worden verwijderd (weigeren) of [`defaultConsent`](configure/defaultconsent.md) moeten worden gebruikt (toestemming onbekend).

Web SDK ondersteunt de volgende standaarden:

* **[norm Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Zowel worden 1.0 als 2.0 normen gesteund.
* **[het Kader van de Transparantie &amp; van de Toestemming IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Als u deze norm gebruikt, wordt het Echte Profiel van de Klant van de bezoeker - tijd bijgewerkt met de toestemmingsinformatie als uw implementatie correct wordt gevormd:
   1. Het XDM individuele profielschema bevat [&#x200B; IAB TCF 2.0 de gebiedsgroep van de Toestemming &#x200B;](/help/xdm/field-groups/profile/iab.md).
   1. Het schema van de Gebeurtenis van de Ervaring bevat [&#x200B; IAB TCF 2.0 de gebiedsgroep van de Toestemming &#x200B;](/help/xdm/field-groups/event/iab.md).
   1. U omvat IAB toestemmingsinformatie in het gebeurtenis [&#x200B; voorwerp XDM &#x200B;](sendevent/xdm.md). De SDK van het Web omvat automatisch niet de toestemmingsinformatie wanneer het verzenden van gebeurtenisgegevens.

Wanneer het gebruiken van dit bevel, schrijft het Web SDK de voorkeur van de gebruiker aan het [`kndctr_<orgId>_consent` &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) koekje. Dit cookie wordt ingesteld ongeacht de voorkeuren van de bezoeker voor toestemming, omdat de voorkeuren van de bezoeker voor toestemming worden opgeslagen. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren op om te bepalen of gebeurtenissen naar Adobe kunnen worden verzonden.

Adobe raadt u aan om voorkeuren voor het bevestigingsvenster los van de toestemming van Web SDK op te slaan. De Web SDK biedt geen manier om toestemming terug te winnen. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de opdracht `setConsent` aanroepen bij elke pagina die wordt geladen. Web SDK maakt slechts een servervraag wanneer de toestemming verandert.

## Identiteitssynchronisatieoverwegingen {#identity-considerations}

De opdracht `setConsent` gebruikt alleen de `ECID` van de identiteitskaart, aangezien de opdracht op apparaatniveau werkt. De opdracht `setConsent` houdt geen rekening met andere identiteiten uit het identiteitsoverzicht.

## `defaultConsent` gebruiken in combinatie met `setConsent` {#using-consent}

Web SDK biedt twee aanvullende opdrachten voor de configuratie van toestemmingen:

* [`defaultConsent`](configure/defaultconsent.md): met deze opdracht wordt automatisch de voorkeur voor de standaardtoestemming van de bezoeker ingesteld voordat `setConsent` wordt aangeroepen.
* `setConsent` (huidige pagina): met deze opdracht wordt expliciet de voorkeur voor toestemming van de bezoeker ingesteld.

Wanneer deze instellingen samen worden gebruikt, kunnen ze leiden tot verschillende resultaten voor gegevensverzameling en cookie-instellingen, afhankelijk van de geconfigureerde waarden:

| `defaultConsent` | `setConsent` | Gegevensverzameling vindt plaats | Web SDK stelt browsercookies in |
| --- | --- | --- | --- |
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nee | Ja |
| `in` | Niet ingesteld | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nee | Ja |
| `pending` | Niet ingesteld | Nee | Nee |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nee | Ja |
| `out` | Niet ingesteld | Nee | Nee |

Zie {de koekjes van SDK van het Web van Adobe Experience Platform 1} in de gids van de Diensten van de Kern voor een volledige lijst van koekjes die kunnen worden geplaatst.[&#128279;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)

## De opdracht `setConsent` gebruiken

Voer het `setConsent` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. U kunt de volgende objecten in deze opdracht opnemen:

* **`consent[]`**: een array van `consent` -objecten. Het bevestigingsobject wordt op een andere manier opgemaakt, afhankelijk van de standaard en versie die u kiest. Zie de onderstaande tabbladen voor voorbeelden van elk object permission, afhankelijk van de toestemmingsstandaard.
* **`identityMap`**: Een object dat bepaalt hoe een ECID wordt gegenereerd en aan welke ID&#39;s toestemmingsinformatie is gekoppeld. Adobe raadt aan dit object op te nemen wanneer `setConsent` wordt uitgevoerd vóór andere opdrachten, zoals [`sendEvent`](sendevent/overview.md) .
* **`edgeConfigOverrides`**: Een voorwerp dat [&#x200B; datastreamconfiguratie met voeten treedt &#x200B;](configure/edgeconfigoverrides.md) bevat.

>[!BEGINTABS]

>[!TAB  Adobe 2.0 ]

### Adobe 2.0 standard `consent` -object

Als u gegevens naar Adobe Experience Platform verzendt, wilt u een privacyschemaveldgroep in uw profielschema opnemen. Zie [&#x200B; Bestuur, privacy, en veiligheid in Adobe Experience Platform &#x200B;](/help/landing/governance-privacy-security/overview.md) voor meer informatie over Adobe 2.0 norm. U kunt gegevens in het onderstaande waardeobject toevoegen die overeenkomen met het schema van het veld `consents` van de [!UICONTROL Consents and Preferences] -profielveldgroep.

* **`standard`**: De toestemmingsnorm die u kiest. Stel deze eigenschap in op `"Adobe"` voor de Adobe 2.0-standaard.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Stel deze eigenschap in op `"2.0"` voor de Adobe 2.0-standaard.
* **`value`**: Een object met toestemmingswaarden.
   * **`value.collect.val`**: De waarde van de toestemming. Stel deze in op `"y"` wanneer gebruikers zich aanmelden en op `"n"` wanneer gebruikers weigeren.
   * **`value.metadata.time`**: Het tijdstempel waarin gebruikers hun instellingen voor toestemming voor het laatst hebben bijgewerkt.

```js
// Set consent using the Adobe 2.0 standard
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

>[!TAB  IAB TCF 2.0 ]

### IAB TCF 2.0 standaard `consent` -object

Als u de voorkeuren voor gebruikerstoestemming wilt vastleggen die via de TCF-standaard (Interactive Advertising Bureau Europe) (IAB) Transparency and Consent Framework) zijn opgegeven, stelt u de verbindingstekenreeks in zoals hieronder wordt getoond.

Wanneer de toestemming op deze manier wordt geplaatst, wordt het Real-Time Profiel van de Klant bijgewerkt met de toestemmingsinformatie. Voor dit aan werk, moet het profielXDM schema de [&#x200B; het schemagroep van de Privacy van het Profiel &#x200B;](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md) bevatten. Bij het verzenden van gebeurtenissen moet de informatie over de IAB-toestemming handmatig worden toegevoegd aan het XDM-gebeurtenisobject. De Web SDK neemt automatisch niet de toestemmingsinformatie in de gebeurtenissen op.

Als u toestemmingsinformatie in gebeurtenissen wilt verzenden, moet u de het gebiedsgroep van de Privacy van de Gebeurtenis van de Ervaring aan uw [!DNL Profile] - toegelaten [!DNL XDM ExperienceEvent] schema toevoegen. Zie de sectie op [&#x200B; het bijwerken van het schema ExperienceEvent &#x200B;](/help/landing/governance-privacy-security/consent/iab/dataset.md#event-schema) in de gids van de datasetvoorbereiding voor stappen op hoe te om dit te vormen.

* **`standard`**: De toestemmingsnorm die u kiest. Stel deze eigenschap in op `"IAB TCF"` voor de IAB TCF 2.0-standaard.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Stel deze eigenschap in op `"2.0"` voor de IAB TCF 2.0-standaard.
* **`value`**: Een tekenreeks die de waarde voor toestemming bevat.
* **`gdprApplies`**: Een Booleaanse waarde die bepaalt of GDPR op deze waarde voor toestemming van toepassing is. De standaardwaarde is `true` .
* **`gdprContainsPersonalData`**: Een Booleaanse waarde die bepaalt of de gebeurtenisgegevens die aan deze gebruiker zijn gekoppeld, persoonlijke gegevens bevatten. De standaardwaarde is `false` .

```js
// Set consent using the IAB TCF 2.0 standard
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

De IAB TCF 2.0 API verstrekt een gebeurtenis voor wanneer de toestemming door de klant wordt bijgewerkt. Dit gebeurt wanneer de klant eerst zijn voorkeuren instelt en wanneer de klant zijn voorkeuren bijwerkt. U kunt een gebeurtenislistener toevoegen om de opdracht `setConsent` uit te voeren:

```js
const identityMap = { ... };
window.__tcfapi('addEventListener', 2, function (tcData, success) {
  if (success && tcData.eventStatus === 'useractioncomplete') {
    window.alloy("setConsent", {
      identityMap,
      consent: [
        {
          standard: "IAB TCF",
          version: "2.0",
          value: tcData.tcString,
          gdprApplies: tcData.gdprApplies
        }
      ]
    });
  }
});
```

Het bovenstaande codeblok luistert naar de gebeurtenis `useractioncomplete` en stelt vervolgens de toestemming in, waarbij de toestemmingstekenreeks en de markering `gdprApplies` worden doorgegeven. Als u aangepaste id&#39;s voor uw klanten hebt, moet u de variabele `identityMap` invullen.

>[!TAB  Adobe 1.0 ]

### Adobe 1.0 standard `consent` -object

* **`standard`**: De toestemmingsnorm die u kiest. Stel deze eigenschap in op `"Adobe"` voor de Adobe 1.0-standaard.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Stel deze eigenschap in op `"1.0"` voor de Adobe 1.0-standaard.
* **`value.general`**: De waarde van de toestemming. Stel deze in op `"in"` wanneer gebruikers zich aanmelden en op `"out"` wanneer gebruikers weigeren.

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

### Meerdere standaarden verzenden in één aanvraag {#multiple-standards}

Web SDK steunt ook het verzenden van meer dan één toestemmingsvoorwerp in een verzoek, zoals aangetoond in het hieronder voorbeeld.

```js
alloy("setConsent", {
    consent: [{
        standard: "Adobe",
        version: "2.0",
        value: {
            collect: {
                val: "y"
            },
            metadata: {
                time: "YYYY-03-17T15:48:42-07:00"
            }
        }
    }, {
        standard: "IAB TCF",
        version: "2.0",
        value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
        gdprApplies: true
    }]
});
```

## Voorkeuren voor blijvende toestemming {#persistence}

Nadat u gebruikersvoorkeuren via de opdracht `setConsent` aan de SDK van het web hebt doorgegeven, blijven de gebruikersvoorkeuren van de SDK behouden voor een cookie. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de Web SDK deze voorkeuren op en gebruikt deze om te bepalen of gebeurtenissen naar Adobe kunnen worden verzonden.

Sla de voorkeuren van de gebruiker afzonderlijk op, zodat u het bevestigingsvenster met de huidige voorkeuren kunt weergeven. De gebruikersvoorkeuren kunnen niet worden opgehaald uit de Web SDK. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de opdracht `setConsent` aanroepen bij elke pagina die wordt geladen. De SDK van het Web doet slechts een servervraag als de voorkeur verandert.

## Toestemming instellen met de extensie van de Web SDK-tag

De Web SDK-tagextensie die equivalent is aan deze opdracht, is de [**[!UICONTROL Set consent]**](/help/tags/extensions/client/web-sdk/actions/set-consent.md) -handeling.
