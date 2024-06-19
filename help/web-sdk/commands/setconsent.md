---
title: setConsent
description: Wordt op elke pagina gebruikt om de voorkeuren voor gebruikersmachtigingen bij te houden.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 0%

---


# `setConsent`

De `setConsent` vertelt de SDK van het Web of het gegevens (opt in) zou moeten verzenden, gegevens (opt out) zou verwerpen, of gebruik [`defaultConsent`](configure/defaultconsent.md) (toestemming onbekend).

De SDK van het Web ondersteunt de volgende standaarden:

* **[Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Zowel 1.0- als 2.0-standaarden worden ondersteund.
* **[IAB-framework voor transparantie en instemming](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Als u deze standaard gebruikt, wordt het Real-Time Klantprofiel van de bezoeker bijgewerkt met de gegevens van de toestemming als uw implementatie correct is geconfigureerd:
   1. Het afzonderlijke XDM-profielschema bevat het [IAB TCF 2.0 Goedgekeurde gebiedsgroep](/help/xdm/field-groups/profile/iab.md).
   1. Het schema Experience Event bevat de [IAB TCF 2.0 Goedgekeurde gebiedsgroep](/help/xdm/field-groups/event/iab.md).
   1. U neemt de informatie van de IAB toestemming in het geval op [XDM-object](sendevent/xdm.md). De Web SDK omvat automatisch niet de toestemmingsinformatie wanneer het verzenden van gebeurtenisgegevens.

Na het gebruiken van dit bevel, schrijft het Web SDK de voorkeur van de gebruiker aan een koekje. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren die nog steeds aanwezig zijn op om te bepalen of gebeurtenissen naar de Adobe kunnen worden verzonden.

Adobe raadt u aan om voorkeuren voor het toestemmingsdialoogvenster los van de toestemming van Web SDK op te slaan. De Web SDK biedt geen manier om toestemming terug te winnen. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de `setConsent` gebruiken bij elke pagina die wordt geladen. SDK van het Web maakt slechts een servervraag wanneer de toestemming verandert.

## Gebruiken `defaultConsent` samen met `setConsent` {#using-consent}

De Web SDK biedt twee aanvullende opdrachten voor de configuratie van toestemmingen:

* [`defaultConsent`](configure/defaultconsent.md): Dit bevel wordt bedoeld om de toestemmingsvoorkeur van de klanten van de Adobe te vangen gebruikend Web SDK.
* [`setConsent`](setconsent.md): Deze opdracht is bedoeld om de voorkeuren voor toestemming van uw sitebezoekers vast te leggen.

Wanneer deze instellingen samen worden gebruikt, kunnen ze leiden tot verschillende resultaten voor gegevensverzameling en cookie-instellingen, afhankelijk van de geconfigureerde waarden.

Zie de onderstaande tabel om te begrijpen wanneer gegevensverzameling plaatsvindt en wanneer cookies worden ingesteld, op basis van toestemmingsinstellingen.

| defaultConsent | setConsent | Gegevensverzameling vindt plaats | Web SDK stelt browsercookies in |
|---------|----------|---------|---------|
| `in` | `in` | Ja | Ja |
| `in` | `out` | Nee | Ja |
| `in` | Niet ingesteld | Ja | Ja |
| `pending` | `in` | Ja | Ja |
| `pending` | `out` | Nee | Ja |
| `pending` | Niet ingesteld | Nee | Nee |
| `out` | `in` | Ja | Ja |
| `out` | `out` | Nee | Ja |
| `out` | Niet ingesteld | Nee | Nee |

De volgende cookies worden ingesteld wanneer de configuratie van de toestemming dit toestaat:

| Naam | Max. leeftijd | Beschrijving |
|---|---|---|
| **AMCV_##@AdobeOrg** | 34128000 (395 dagen) | Presenteren wanneer [`idMigrationEnabled`](configure/idmigrationenabled.md) is ingeschakeld. Het helpt wanneer het overgaan naar Web SDK terwijl sommige delen van de plaats nog gebruiken `visitor.js`. |
| **Demdex cookie** | 15552000 (180 dagen) | Presenteren als id-synchronisatie is ingeschakeld. Audience Manager stelt dit cookie zo in dat een unieke id wordt toegewezen aan een sitebezoeker. Het demdex-cookie helpt Audience Manager basisfuncties uit te voeren, zoals bezoekersidentificatie, id-synchronisatie, segmentatie, modellering, rapportage, enzovoort. |
| **kndctr_orgid_cluster** | 1800 (30 minuten) | Hiermee slaat u het gebied Edge Network op dat de verzoeken van de huidige gebruiker dient. Het gebied wordt gebruikt in de weg URL zodat de Edge Network het verzoek aan het correcte gebied kan leiden. Als een gebruiker met een verschillend IP adres of in een verschillende zitting verbindt, wordt het verzoek opnieuw verpletterd aan het dichtstbijzijnde gebied. |
| **kndct_orgid_identity** | 34128000 (395 dagen) | Hiermee slaat u de ECID op, evenals andere informatie over de ECID. |
| **kndctr_orgid_permission** | 15552000 (180 dagen) | Hiermee slaat u de voorkeur van de gebruikers voor toestemming voor de website op. |
| **s_ecid** | 63115200 (2 jaar) | Bevat een kopie van de Experience Cloud-id ([!DNL ECID]) of MID. MID wordt opgeslagen in een zeer belangrijk-waardepaar dat deze syntaxis volgt, `s_ecid=MCMID\|<ECID>`. |

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

* **`consent[]`**: Een array van `consent` objecten. Het bevestigingsobject wordt op een andere manier opgemaakt, afhankelijk van de standaard en versie die u kiest. Zie de onderstaande tabbladen voor voorbeelden van elk object permission, afhankelijk van de toestemmingsstandaard.
* **`identityMap`**: Een object dat bepaalt hoe een ECID wordt gegenereerd en aan welke ID&#39;s toestemmingsinformatie is gekoppeld. Adobe raadt aan dit object op te nemen wanneer `setConsent` wordt uitgevoerd vóór andere opdrachten, zoals [`sendEvent`](sendevent/overview.md).
* **`edgeConfigOverrides`**: Een object dat bevat [gegevensstroomconfiguratie overschrijft](datastream-overrides.md).

>[!BEGINTABS]

>[!TAB Adobe 2.0]

### Adobe 2.0-standaard `consent` object

Als u Adobe Experience Platform gebruikt, moet u een veldgroep met het privacyschema in uw profielschema opnemen. Zie [Bestuur, privacy en beveiliging in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) voor meer informatie over de Adobe 2.0 norm. U kunt gegevens toevoegen binnen het waardeobject hieronder die overeenkomen met het schema van het dialoogvenster `consents` van het [!UICONTROL Consents and Preferences] profielveldgroep.

* **`standard`**: De standaard voor toestemming die u kiest. Deze eigenschap instellen op `"Adobe"` voor de Adobe 2.0-norm.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Deze eigenschap instellen op `"2.0"` voor de Adobe 2.0-norm.
* **`value`**: Een object met toestemmingswaarden.
   * **`value.collect.val`**: De waarde van de toestemming. Stel deze in op `"y"` wanneer gebruikers zich aanmelden en naar `"n"` wanneer gebruikers weigeren.
   * **`value.metadata.time`**: De tijdstempel wanneer gebruikers hun instellingen voor toestemming voor het laatst hebben bijgewerkt.

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

>[!TAB IAB TCF 2.0]

### IAB TCF 2.0-standaard `consent` object

Als u de voorkeuren voor gebruikerstoestemming wilt vastleggen die via de TCF-standaard (Interactive Advertising Bureau Europe) worden verschaft, stelt u de tekenreeks voor de toestemming in zoals hieronder wordt getoond.

Wanneer de toestemming op deze manier wordt geplaatst, wordt het Real-Time Profiel van de Klant bijgewerkt met de toestemmingsinformatie. Dit werkt alleen als het XDM-profielschema het volgende bevat: [Veld groep profielprivacyschema](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Bij het verzenden van gebeurtenissen moet de informatie over de IAB-toestemming handmatig worden toegevoegd aan het XDM-gebeurtenisobject. De SDK van het Web neemt automatisch niet de toestemmingsinformatie in de gebeurtenissen op.

Als u toestemmingsinformatie in gebeurtenissen wilt verzenden, moet u de het gebiedsgroep van de Privacy van de Gebeurtenis van de Ervaring aan uw toevoegen [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schema. Zie de sectie over [het bijwerken van het schema ExperienceEvent](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) in de de voorbereidingsgids van de dataset voor stappen op hoe te om dit te vormen.

* **`standard`**: De standaard voor toestemming die u kiest. Deze eigenschap instellen op `"IAB TCF"` voor de IAB TCF 2.0-standaard.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Deze eigenschap instellen op `"2.0"` voor de IAB TCF 2.0-standaard.
* **`value`**: Een tekenreeks die de waarde voor de toestemming bevat.
* **`gdprApplies`**: Een Booleaanse waarde die bepaalt of GDPR op deze toestemmingswaarde van toepassing is. De standaardwaarde is `true`.
* **`gdprContainsPersonalData`**: Een Booleaanse waarde die bepaalt of de gebeurtenisgegevens die aan deze gebruiker zijn gekoppeld, persoonlijke gegevens bevatten. De standaardwaarde is `false`.

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

>[!TAB Adobe 1.0]

### Adobe 1.0 standaard `consent` object

* **`standard`**: De standaard voor toestemming die u kiest. Deze eigenschap instellen op `"Adobe"` voor Adobe 1.0.
* **`version`**: Een tekenreeks die de versie van de toestemmingsstandaard vertegenwoordigt. Deze eigenschap instellen op `"1.0"` voor Adobe 1.0.
* **`value.general`**: De waarde van de toestemming. Stel deze in op `"in"` wanneer gebruikers zich aanmelden en naar `"out"` wanneer gebruikers weigeren.

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

De SDK van het Web steunt ook het verzenden van meer dan één toestemmingsvoorwerp in een verzoek, zoals aangetoond in het hieronder voorbeeld.

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
                time: "2021-03-17T15:48:42-07:00"
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

Nadat u gebruikersvoorkeur aan het Web SDK gebruikend hebt gecommuniceerd `setConsent` de SDK behoudt de gebruikersvoorkeuren voor een cookie. De volgende keer dat de gebruiker uw website in browser laadt, zal SDK van het Web deze persisted voorkeur terugwinnen en gebruiken om te bepalen of de gebeurtenissen naar Adobe kunnen worden verzonden of niet.

U moet de gebruikersvoorkeuren afzonderlijk opslaan om het bevestigingsvenster met de huidige voorkeuren te kunnen weergeven. Er is geen manier om de gebruikersvoorkeur van SDK van het Web terug te winnen. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de `setConsent` gebruiken bij elke pagina die wordt geladen. De SDK van het Web zal slechts een servervraag maken als de voorkeur is veranderd.

## Identiteiten synchroniseren tijdens instellen van toestemming {#sync-identities}

Wanneer de standaardtoestemming (ingesteld door de [defaultConsent](configure/defaultconsent.md) parameter) is ingesteld op `pending` of `out`de `setConsent` het bepalen kan het eerste verzoek zijn dat uit gaat en identiteit vestigt. Daarom kan het belangrijk zijn om identiteiten op het eerste verzoek te synchroniseren. U kunt het identiteitsoverzicht toevoegen aan de `setConsent` op dezelfde manier als op de `sendEvent` gebruiken. Zie [gebruiken van identityMap](../identity/overview.md#using-identitymap) voor een voorbeeld van hoe te om de identiteitskaart op uw bevel te omvatten.
