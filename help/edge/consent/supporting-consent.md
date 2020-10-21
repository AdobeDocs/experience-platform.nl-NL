---
title: Ondersteunende toestemming
seo-title: Voorkeuren voor Adobe Experience Platform Web SDK-toestemming ondersteunen
description: Leer hoe u toestemmingsvoorkeuren met Experience Platform Web SDK kunt ondersteunen
seo-description: Leer hoe u toestemmingsvoorkeuren met Experience Platform Web SDK kunt ondersteunen
keywords: consent;defaultConsent;default consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# Ondersteunende toestemming

Om de privacy van uw gebruiker te respecteren, zou u om de toestemming van de gebruiker kunnen willen vragen alvorens SDK toe te staan om gebruiker-specifieke gegevens voor bepaalde doeleinden te gebruiken. Momenteel staat SDK gebruikers alleen toe om in of uit alle doeleinden te kiezen, maar in de toekomst hoopt Adobe meer korrelige controle over specifieke doeleinden te verschaffen.

Als de gebruiker voor alle doeleinden inbelt, mag de SDK de volgende taken uitvoeren:

* Gegevens verzenden van en naar Adobe-servers.
* Cookies of webopslagitems lezen en schrijven (behalve voor het doorlopen van de aanmeldingsvoorkeuren van de gebruiker).

Als de gebruiker uit alle doeleinden kiest, voert de SDK geen van deze taken uit.

## Goedkeuring configureren

De gebruiker is standaard voor alle doeleinden ingeschakeld. Als u wilt voorkomen dat de SDK de bovenstaande taken uitvoert totdat de gebruiker het programma inschakelt, geeft u als volgt `"defaultConsent": "pending"` tijdens de SDK-configuratie door:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Wanneer de standaardtoestemming voor het algemene doel op in behandeling wordt geplaatst, leidt het proberen om het even welke bevelen uit te voeren die van gebruiker opt-in voorkeur (bijvoorbeeld, het `event` bevel) afhangen tot het bevel dat binnen SDK een rij wordt gevormd. Deze opdrachten worden pas verwerkt nadat u de aanmeldingsvoorkeuren van de gebruiker aan de SDK hebt doorgegeven.

Op dit punt wilt u de gebruiker wellicht vragen zich ergens in de gebruikersinterface aan te melden. Nadat de gebruikersvoorkeuren zijn verzameld, geeft u deze door aan de SDK.

## Voorkeuren voor toestemming via de Adobe-standaard communiceren

Als de gebruiker binnen kiest, voer het `setConsent` bevel met de `general` optie uit die aan `in` als volgt wordt geplaatst:

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

Omdat de gebruiker nu heeft gekozen, voert de SDK alle eerder in de wachtrij geplaatste opdrachten uit. Toekomstige opdrachten die afhankelijk zijn van het inchecken door de gebruiker, worden niet in de wachtrij geplaatst en worden direct uitgevoerd.

Als de gebruiker ervoor kiest om te weigeren, voert u de `setConsent` opdracht uit met de `general` optie ingesteld op `out` als volgt:

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
>Nadat een gebruiker heeft gekozen, zal SDK u niet toestaan om de gebruikers toestemming te plaatsen aan `in`.

Omdat de gebruiker ervoor koos om te weigeren, worden de beloftes die van eerder een rij vormde bevelen zijn teruggekeerd verworpen. Toekomstige opdrachten die afhankelijk zijn van de gebruiker die incheckt, retourneren beloftes die op dezelfde manier worden afgewezen. Raadpleeg Opdrachten [uitvoeren voor meer informatie over het afhandelen of onderdrukken van fouten](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Momenteel ondersteunt de SDK alleen het `general` doel. Hoewel wij van plan zijn een robuustere reeks doelen of categorieën te ontwikkelen die aan de verschillende mogelijkheden en productaanbiedingen van de Adobe zullen beantwoorden, is de huidige implementatie een alles of niets benadering van opt-in.  Dit geldt alleen voor de Adobe Experience Platform [!DNL Web SDK] en NOT other Adobe JavaScript libraries.

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

Wanneer de toestemming op deze manier wordt geplaatst, wordt het Profiel van de Klant in real time bijgewerkt met de toestemmingsinformatie. Dit werkt alleen als het profiel-XDM-schema de [profielprivacymixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md)bevat. Bij het verzenden van gebeurtenissen moet de informatie over de IAB-toestemming handmatig worden toegevoegd aan het XDM-gebeurtenisobject. De SDK neemt niet automatisch de informatie over de toestemming op in de gebeurtenissen. Om de toestemmingsinformatie in gebeurtenissen te verzenden, moet de [Mixin](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) van de Privacy van de Gebeurtenis van de Ervaring aan het schema van de Gebeurtenis van de Ervaring worden toegevoegd.

## Beide standaarden verzenden in één aanvraag

De SDK biedt ook ondersteuning voor het verzenden van meer dan één bevestigingsobject in een aanvraag.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
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

Nadat u gebruikersvoorkeuren aan de SDK hebt doorgegeven met de `setConsent` opdracht, blijft de SDK de gebruikersvoorkeuren voor een cookie gebruiken. De volgende keer dat de gebruiker uw website in de browser laadt, haalt de SDK deze voorkeuren op en gebruikt deze om te bepalen of gebeurtenissen naar Adobe kunnen worden verzonden. U hoeft de `setConsent` opdracht niet opnieuw uit te voeren, behalve om een wijziging in de gebruikersvoorkeuren door te geven, die u op elk gewenst moment kunt doorvoeren.

## Identiteiten synchroniseren tijdens instellen van toestemming

Wanneer de standaardtoestemming hangende is, `setConsent` kan het eerste verzoek zijn dat uit gaat en identiteit vestigt. Daarom kan het belangrijk zijn om identiteiten op het eerste verzoek te synchroniseren. De identiteitskaart kan aan `setConsent` bevel enkel als op het `sendEvent` bevel worden toegevoegd. Zie Experience Cloud-id [ophalen](../identity/overview.md)

