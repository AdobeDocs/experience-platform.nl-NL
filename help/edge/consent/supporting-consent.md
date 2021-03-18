---
title: Voorkeuren voor toestemming van de klant ondersteunen met de Adobe Experience Platform Web SDK
description: Leer hoe u voorkeuren voor toestemming ondersteunt met de Adobe Experience Platform Web SDK.
keywords: toestemming;defaultConsent;defaultConsent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: dd9101079a1093c109f43b268a78c07770221156
workflow-type: tm+mt
source-wordcount: '977'
ht-degree: 0%

---


# Voorkeuren voor toestemming van klanten ondersteunen

Om de privacy van uw gebruiker te respecteren, zou u om de toestemming van de gebruiker kunnen willen vragen alvorens SDK toe te staan om gebruiker-specifieke gegevens voor bepaalde doeleinden te gebruiken. Momenteel staat SDK gebruikers alleen toe om in of uit alle doeleinden te kiezen, maar in de toekomst hoopt Adobe meer korrelige controle over specifieke doeleinden te verschaffen.

Als de gebruiker voor alle doeleinden inbelt, mag de SDK de volgende taken uitvoeren:

* Gegevens verzenden van en naar Adobe-servers.
* Cookies of webopslagitems lezen en schrijven.

Als de gebruiker uit alle doeleinden kiest, voert de SDK geen van deze taken uit.

## Goedkeuring configureren

De gebruiker is standaard voor alle doeleinden ingeschakeld. Als u wilt voorkomen dat de SDK de bovenstaande taken uitvoert totdat de gebruiker het programma inschakelt, geeft u `"defaultConsent": "pending"` tijdens de SDK-configuratie als volgt door:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Wanneer de standaardtoestemming voor het algemene doel op in behandeling wordt geplaatst, leidt het proberen om het even welke bevelen uit te voeren die van gebruiker opt-in voorkeur (bijvoorbeeld, `sendEvent` bevel) afhangen tot het bevel dat binnen SDK een rij wordt gevormd. Deze opdrachten worden pas verwerkt nadat u de aanmeldingsvoorkeuren van de gebruiker aan de SDK hebt doorgegeven.

>[!NOTE]
>
>Opdrachten worden alleen in het geheugen in de wachtrij geplaatst. Ze worden niet opgeslagen bij het laden van de pagina.

Als u geen gebeurtenissen wilt verzamelen die zijn opgetreden voordat de gebruikersvoorkeuren zijn ingesteld, kunt u `"defaultConsent": "out"` tijdens de SDK-configuratie doorgeven. Het uitvoeren van opdrachten die afhankelijk zijn van de gebruikersaanmeldingsvoorkeuren, heeft pas effect nadat u de aanmeldingsvoorkeuren van de gebruiker aan de SDK hebt doorgegeven.

>[!NOTE]
>
>Momenteel ondersteunt de SDK slechts één doel, alles of niets. Hoewel wij van plan zijn een robuustere reeks doelen of categorieën te ontwikkelen die aan de verschillende mogelijkheden en productaanbiedingen van de Adobe zullen beantwoorden, is de huidige implementatie een alles of niets benadering van opt-in.  Dit geldt alleen voor Adobe Experience Platform [!DNL Web SDK] en NOT other Adobe JavaScript libraries.

Op dit punt wilt u de gebruiker wellicht vragen zich ergens in de gebruikersinterface aan te melden. Nadat de gebruikersvoorkeuren zijn verzameld, geeft u deze door aan de SDK.

## Voorkeuren voor toestemmingen via de Adobe Experience Platform-norm communiceren

De SDK ondersteunt versies 1.0 en 2.0 van de Adobe Experience Platform toestemmingsstandaard. Momenteel ondersteunen de 1.0- en 2.0-normen alleen de automatische handhaving van een voorkeur voor alle of niets toestemming. De 1,0-norm wordt geleidelijk vervangen door de 2,0-norm. Met de 2.0-standaard kunt u aanvullende voorkeuren voor toestemming toevoegen die u kunt gebruiken om de voorkeur voor toestemming handmatig af te dwingen.

### De Adobe-standaardversie 2.0 gebruiken

Als u Adobe Experience Platform gebruikt, moet u een privacymix opnemen in uw profielschema. Zie [Beheer, privacy en beveiliging in Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) voor meer informatie over de standaardversie van Adobe 2.0. U kunt gegevens toevoegen binnen het waardeobject hieronder die overeenkomen met het schema van het veld `consents` van de profielmix van Inhoud en Voorkeuren.

Als de gebruiker binnen kiest, voer `setConsent` bevel met de inzamelingsvoorkeur uit die aan `y` wordt geplaatst als volgt:

```javascript
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
    }]
});
```

In het tijdveld moet worden opgegeven wanneer de gebruiker zijn voorkeuren voor toestemming voor het laatst heeft bijgewerkt. Als de gebruiker ervoor kiest om te weigeren, voert u de opdracht `setConsent` uit met de verzamelvoorkeur ingesteld op `n` als volgt:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

>[!NOTE]
>
>Nadat een gebruiker heeft gekozen, zal SDK u niet toestaan om de gebruikers te plaatsen verzamelen toestemming aan `y`.

### Adobe standaardversie 1.0 gebruiken

Als de gebruiker binnen kiest, voer `setConsent` bevel met de `general` optie uit die aan `in` wordt geplaatst als volgt:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

Als de gebruiker ervoor kiest om te weigeren, voert u de opdracht `setConsent` uit met de optie `general` ingesteld op `out` als volgt:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>Nadat een gebruiker heeft gekozen, zal SDK u niet toestaan om de gebruikers toestemming aan `in` te plaatsen.

## Voorkeuren voor machtigingen verzenden via de IAB TCF-standaard

De SDK ondersteunt het opnemen van voorkeuren voor toestemming van gebruikers via de norm Interactive Advertising Bureau Europe (IAB) Transparency and Consent Framework (TCF). De toestemmingskoord kan door het zelfde `setConsent` bevel zoals hierboven als dit worden geplaatst:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

Wanneer de toestemming op deze manier wordt geplaatst, wordt het Profiel van de Klant in real time bijgewerkt met de toestemmingsinformatie. Dit werkt alleen als het profiel-XDM-schema de [Profile Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md) bevat. Bij het verzenden van gebeurtenissen moet de informatie over de IAB-toestemming handmatig worden toegevoegd aan het XDM-gebeurtenisobject. De SDK neemt niet automatisch de informatie over de toestemming op in de gebeurtenissen. Om de toestemmingsinformatie in gebeurtenissen te verzenden, moet [Experience Event Privacy Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) aan het schema van de Gebeurtenis van de Ervaring worden toegevoegd.

## Meerdere standaarden verzenden in één aanvraag

De SDK biedt ook ondersteuning voor het verzenden van meer dan één bevestigingsobject in een aanvraag.

```javascript
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
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Voorkeuren voor blijvende toestemming

Nadat u gebruikersvoorkeuren aan de SDK hebt doorgegeven met de opdracht `setConsent`, behoudt de SDK de gebruikersvoorkeuren voor een cookie. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren op en gebruikt deze om te bepalen of gebeurtenissen naar Adobe kunnen worden verzonden.

U moet de gebruikersvoorkeuren afzonderlijk opslaan om het bevestigingsvenster met de huidige voorkeuren te kunnen weergeven. U kunt de gebruikersvoorkeuren niet ophalen uit de SDK. Als u er zeker van wilt zijn dat de gebruikersvoorkeuren synchroon blijven met de SDK, kunt u de opdracht `setConsent` aanroepen bij elke laadpagina. De SDK roept alleen een server aan als de voorkeuren zijn gewijzigd.

## Identiteiten synchroniseren tijdens instellen van toestemming

Wanneer de standaardtoestemming hangende of uit is, `setConsent` kan het eerste verzoek zijn dat uit gaat en identiteit vestigt. Daarom kan het belangrijk zijn om identiteiten op het eerste verzoek te synchroniseren. De identiteitskaart kan aan `setConsent` bevel enkel als op &lt;a1 worden toegevoegd/> bevel. `sendEvent` Zie [Experience Cloud-id ophalen](../identity/overview.md)

