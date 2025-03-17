---
title: setConsent
description: Wordt op elke pagina gebruikt om de voorkeuren voor gebruikersmachtigingen bij te houden.
exl-id: d01a6ef1-4fa7-4a60-a3a1-19568b4e0d23
source-git-commit: 83b4745693749c5f50791d6efeb3a7ba02a4cce5
workflow-type: tm+mt
source-wordcount: '1307'
ht-degree: 0%

---


# `setConsent`

De opdracht `setConsent` geeft aan de Web SDK door of gegevens moeten worden verzonden (aanmelden), gegevens moeten worden verwijderd (weigeren) of [`defaultConsent`](configure/defaultconsent.md) moeten worden gebruikt (toestemming onbekend).

Web SDK ondersteunt de volgende standaarden:

* **[norm Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: Zowel worden 1.0 als 2.0 normen gesteund.
* **[het Kader van de Transparantie &amp; van de Toestemming IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: Als u deze norm gebruikt, wordt het Echte Profiel van de Klant van de bezoeker - tijd bijgewerkt met de toestemmingsinformatie als uw implementatie correct wordt gevormd:
   1. Het XDM individuele profielschema bevat [ IAB TCF 2.0 de gebiedsgroep van de Toestemming ](/help/xdm/field-groups/profile/iab.md).
   1. Het schema van de Gebeurtenis van de Ervaring bevat [ IAB TCF 2.0 de gebiedsgroep van de Toestemming ](/help/xdm/field-groups/event/iab.md).
   1. U omvat IAB toestemmingsinformatie in het gebeurtenis [ voorwerp XDM ](sendevent/xdm.md). De SDK van het Web omvat automatisch niet de toestemmingsinformatie wanneer het verzenden van gebeurtenisgegevens.

Nadat u deze opdracht hebt gebruikt, schrijft de Web SDK de gebruikersvoorkeuren naar een cookie. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren op om te bepalen of gebeurtenissen naar Adobe kunnen worden verzonden.

Adobe raadt u aan om voorkeuren voor het bevestigingsvenster los van de toestemming van Web SDK op te slaan. De Web SDK biedt geen manier om toestemming terug te winnen. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de opdracht `setConsent` aanroepen bij elke pagina die wordt geladen. Web SDK maakt slechts een servervraag wanneer de toestemming verandert.

## Identiteitssynchronisatieoverwegingen {#identity-considerations}

De opdracht `setConsent` gebruikt alleen de `ECID` van de identiteitskaart, aangezien de opdracht op apparaatniveau werkt. De opdracht `setConsent` houdt geen rekening met andere identiteiten uit het identiteitsoverzicht.

## `defaultConsent` gebruiken in combinatie met `setConsent` {#using-consent}

Web SDK biedt twee aanvullende opdrachten voor de configuratie van toestemmingen:

* [`defaultConsent`](configure/defaultconsent.md): deze opdracht is bedoeld om de voorkeuren voor toestemming van Adobe-klanten vast te leggen via Web SDK.
* [`setConsent`](setconsent.md): deze opdracht is bedoeld om de voorkeuren voor toestemming van uw sitebezoekers vast te leggen.

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
| **AMCV_##@AdobeOrg** | 34128000 (395 dagen) | Wordt weergegeven wanneer [`idMigrationEnabled`](configure/idmigrationenabled.md) is ingeschakeld. Het helpt bij het overschakelen naar Web SDK terwijl sommige delen van de site nog steeds `visitor.js` gebruiken. |
| **het koekje van de Index** | 15552000 (180 dagen) | Presenteren als id-synchronisatie is ingeschakeld. Audience Manager stelt dit cookie zo in dat een unieke id aan een sitebezoeker wordt toegewezen. Het demdex-cookie helpt Audience Manager basisfuncties uit te voeren, zoals bezoekersidentificatie, id-synchronisatie, segmentatie, modellering, rapportage, enzovoort. |
| **kndctr_orgid_cluster** | 1800 (30 minuten) | Hiermee slaat u het Edge Network-gebied op dat aan de verzoeken van de huidige gebruiker voldoet. Het gebied wordt gebruikt in de weg URL zodat de Edge Network het verzoek aan het correcte gebied kan leiden. Als een gebruiker met een verschillend IP adres of in een verschillende zitting verbindt, wordt het verzoek opnieuw verpletterd aan het dichtstbijzijnde gebied. |
| **kCt_orgid_identity** | 34128000 (395 dagen) | Hiermee slaat u de ECID op, evenals andere informatie over de ECID. |
| **kndctr_orgid_permission** | 15552000 (180 dagen) | Hiermee slaat u de voorkeur van de gebruikers voor toestemming voor de website op. |
| **s_ecid** | 63115200 (2 jaar) | Bevat een kopie van de Experience Cloud-id ([!DNL ECID]) of MID. MID wordt opgeslagen in een sleutelwaardepaar dat deze syntaxis volgt, `s_ecid=MCMID\|<ECID>`. |

## Toestemming instellen met de extensie van de Web SDK-tag

Het plaatsen van toestemming wordt uitgevoerd als actie binnen een regel in de de etiketteninterface van de Inzameling van Gegevens van Adobe Experience Platform.

1. Login aan [ experience.adobe.com ](https://experience.adobe.com) gebruikend uw geloofsbrieven van Adobe ID.
1. Ga naar **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecteer de gewenste eigenschap tag.
1. Navigeer naar **[!UICONTROL Rules]** en selecteer vervolgens de gewenste regel.
1. Selecteer onder [!UICONTROL Actions] een bestaande actie of maak een actie.
1. Stel het vervolgkeuzeveld [!UICONTROL Extension] in op **[!UICONTROL Adobe Experience Platform Web SDK]** en stel de waarde [!UICONTROL Action Type] in op **[!UICONTROL Set consent]** .
1. Stel de gewenste velden rechts in, inclusief **[!UICONTROL Standard]** en **[!UICONTROL General consent]** .
1. Klik op **[!UICONTROL Keep Changes]** en voer vervolgens de publicatieworkflow uit.

U kunt meerdere objecten voor toestemming in deze handeling opnemen.

## Goedkeuring instellen met de Web SDK JavaScript-bibliotheek

Voer het `setConsent` bevel in werking wanneer het roepen van uw gevormde instantie van het Web SDK. U kunt de volgende objecten in deze opdracht opnemen:

* **`consent[]`**: een array van `consent` -objecten. Het bevestigingsobject wordt op een andere manier opgemaakt, afhankelijk van de standaard en versie die u kiest. Zie de onderstaande tabbladen voor voorbeelden van elk object permission, afhankelijk van de toestemmingsstandaard.
* **`identityMap`**: Een object dat bepaalt hoe een ECID wordt gegenereerd en aan welke ID&#39;s toestemmingsinformatie is gekoppeld. Adobe raadt aan dit object op te nemen wanneer `setConsent` wordt uitgevoerd vóór andere opdrachten, zoals [`sendEvent`](sendevent/overview.md) .
* **`edgeConfigOverrides`**: Een voorwerp dat [ datastreamconfiguratie met voeten treedt ](datastream-overrides.md) bevat.

>[!BEGINTABS]

>[!TAB  Adobe 2.0 ]

### Adobe 2.0 standard `consent` -object

Als u Adobe Experience Platform gebruikt, moet u een veldgroep met het privacyschema in uw profielschema opnemen. Zie [ Bestuur, privacy, en veiligheid in Adobe Experience Platform ](../../landing/governance-privacy-security/overview.md) voor meer informatie over Adobe 2.0 norm. U kunt gegevens in het onderstaande waardeobject toevoegen die overeenkomen met het schema van het veld `consents` van de [!UICONTROL Consents and Preferences] -profielveldgroep.

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

Wanneer de toestemming op deze manier wordt geplaatst, wordt het Real-Time Profiel van de Klant bijgewerkt met de toestemmingsinformatie. Voor dit aan werk, moet het profielXDM schema de [ het schemagroep van de Privacy van het Profiel ](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md) bevatten. Bij het verzenden van gebeurtenissen moet de informatie over de IAB-toestemming handmatig worden toegevoegd aan het XDM-gebeurtenisobject. De Web SDK neemt automatisch niet de toestemmingsinformatie in de gebeurtenissen op.

Als u toestemmingsinformatie in gebeurtenissen wilt verzenden, moet u de het gebiedsgroep van de Privacy van de Gebeurtenis van de Ervaring aan uw [!DNL Profile] - toegelaten [!DNL XDM ExperienceEvent] schema toevoegen. Zie de sectie op [ het bijwerken van het schema ExperienceEvent ](../../landing/governance-privacy-security/consent/iab/dataset.md#event-schema) in de gids van de datasetvoorbereiding voor stappen op hoe te om dit te vormen.

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

Nadat u gebruikersvoorkeuren via de opdracht `setConsent` aan de SDK van het web hebt doorgegeven, blijven de gebruikersvoorkeuren van de SDK behouden voor een cookie. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de Web SDK deze voorkeuren op en gebruikt deze om te bepalen of gebeurtenissen naar Adobe kunnen worden verzonden.

U moet de gebruikersvoorkeuren afzonderlijk opslaan om het bevestigingsvenster met de huidige voorkeuren te kunnen weergeven. De gebruikersvoorkeuren kunnen niet worden opgehaald uit de Web SDK. Om ervoor te zorgen dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de opdracht `setConsent` aanroepen bij elke pagina die wordt geladen. Web SDK zal slechts een servervraag maken als de voorkeur is veranderd.
