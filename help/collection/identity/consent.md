---
title: Toestemming en identiteit in gegevensverzameling
description: Begrijp hoe de toestemmingskeuzen identiteitsgedrag in de implementaties van SDK van het Web, met inbegrip van het produceren van ECID, koekjespersistentie, en bezoekerscontinuïteit beïnvloeden.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 0%

---

# Toestemming en identiteit in gegevensverzameling

De toestemming en de identiteit worden nauw verbonden in de implementaties van SDK van het Web. De manier waarop en wanneer u toestemming verzamelt, beïnvloedt rechtstreeks wanneer en of de Web SDK een ECID genereert, identiteitscookies instelt en gegevens naar de Edge Network verzendt. Wanneer de toestemming niet zorgvuldig wordt behandeld, is het resultaat vaak onverwachte bezoekersinflatie, hiaten in identiteitscontinuïteit, of allebei.

Deze pagina verklaart hoe de toestemmingskeuzen met identiteitsgedrag in wisselwerking staan en verstrekt raad voor het vormen van uw implementatie om gemeenschappelijke valkuilen te vermijden. Voor achtergrond op hoe het Web SDK ECIDs, FPIDs, en andere identiteitssignalen behandelt, zie [ Identiteit in de Inzameling van Gegevens ](./overview.md).

## Hoe invloed de toestemming heeft op de identiteit {#how-consent-affects-identity}

Web SDK gebruikt zowel de [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) configuratievariabele als het [`setConsent`](/help/collection/js/commands/setconsent.md) bevel om te controleren als het gegevens naar Edge Network verzendt. De status van toestemming bepaalt rechtstreeks wanneer een ECID wordt gegenereerd en wanneer identiteitscookies worden ingesteld.

In de volgende tabel ziet u het gecombineerde effect van `defaultConsent` en `setConsent` op gegevensverzameling, cookie-instelling en identiteitsgedrag.

| `defaultConsent` | `setConsent` | Gegevensverzameling vindt plaats | Browsercookies set | Identiteitsgedrag |
| --- | --- | --- | --- | --- |
| `in` | Niet ingesteld | Ja | Ja | Er wordt direct een ECID gegenereerd op het eerste verzoek. Identiteitscookies worden ingesteld bij het laden van de pagina. |
| `in` | `in` | Ja | Ja | De bestaande ECID van de bezoeker blijft behouden. Identiteitsgedrag is ongewijzigd. |
| `in` | `out` | Nee | Ja | Gegevensverzameling stopt. De bestaande ECID- en `kndctr_` identiteitscookies blijven in de browser totdat ze verlopen. |
| `pending` | Niet ingesteld | Nee | Nee | Er wordt geen ECID gegenereerd. Er zijn geen cookies ingesteld. Gebeurtenissen worden lokaal in de wachtrij geplaatst totdat `setConsent` wordt aangeroepen. |
| `pending` | `in` | Ja | Ja | Gebeurtenissen in de wachtrij worden verzonden. Er wordt een ECID gegenereerd bij de eerste aanvraag en er worden identieke cookies ingesteld. |
| `pending` | `out` | Nee | Ja | Gebeurtenissen in de wachtrij worden genegeerd. Er wordt geen ECID gegenereerd. In het toestemmingscookie wordt de voorkeur van de bezoeker vastgelegd. |
| `out` | Niet ingesteld | Nee | Nee | Er wordt geen ECID gegenereerd. Er zijn geen cookies ingesteld. Er worden geen gebeurtenissen verzonden. |
| `out` | `in` | Ja | Ja | Er wordt een ECID gegenereerd bij de eerste aanvraag en er worden identieke cookies ingesteld. |
| `out` | `out` | Nee | Ja | Er wordt geen ECID gegenereerd. In het toestemmingscookie wordt de voorkeur van de bezoeker vastgelegd. |

>[!NOTE]
>
>Identiteitscookies en toestemmingscookies worden ingesteld, zelfs als een bezoeker de functie uitschakelt. Deze cookies zijn nodig om de voorkeuren voor gegevensverzameling van de bezoeker te respecteren. Zie {de koekjes van SDK van 0} Web [ voor een volledige lijst van koekjes die SDK van het Web plaatst.](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk)

Wanneer een bezoeker toestemming opnieuw verleent nadat deze eerder is ingetrokken (door `setConsent` met `"general": "in"` after `"general": "out"` aan te roepen), hervat Web SDK het verzenden van gebeurtenissen en gebruikt de bestaande ECID van het cookie als deze nog niet is verlopen. De identiteit van de bezoeker blijft behouden.

Nadat een bezoeker zijn toestemming heeft verleend of geweigerd, houdt de Web SDK zijn voorkeur aan in een `kndctr_` toestemmingscookie. Als de volgende pagina wordt geladen, leest de SDK deze cookie en past de opgeslagen voorkeur automatisch toe. U hoeft `setConsent` niet opnieuw aan te roepen tenzij de voorkeur van de bezoeker verandert. De configuratiewaarde `defaultConsent` blijft niet bestaan tussen paginaladingen, maar de door de bezoeker gekozen toestemming (ingesteld via `setConsent` ) wel.

>[!NOTE]
>
>Gebeurtenissen die in een wachtrij worden geplaatst terwijl toestemming `pending` is, worden in het geheugen opgeslagen en kunnen het opnieuw laden van pagina&#39;s niet overleven. Als een bezoeker naar een nieuwe pagina navigeert voordat de toestemming is omgezet, gaan gebeurtenissen uit de wachtrij van de vorige pagina verloren.

## Implementatiepatronen {#implementation-patterns}

### Inschakelmodel (toestemming vereist voor verzameling) {#opt-in}

Gebruik dit patroon als voorschriften (zoals GDPR) uitdrukkelijke toestemming vereisen voordat u gegevens verzamelt.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Met dit patroon:
* Er wordt geen ECID gegenereerd totdat toestemming is verleend.
* Gebeurtenissen die worden geactiveerd voordat toestemming wordt gegeven (zoals de weergave voor de eerste pagina), worden in de wachtrij geplaatst en verzonden nadat toestemming is verleend.
* Identiteitscookies worden alleen ingesteld na de eerste geslaagde Edge Network-aanvraag.

### Opt-out model (verzameling standaard, stoppen bij ontkennen) {#opt-out}

Gebruik dit patroon als de regelgeving gegevensverzameling standaard toestaat, met de optie Weigeren.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Met dit patroon:
* Er wordt direct een ECID gegenereerd bij het laden van de eerste pagina.
* Alle gebeurtenissen worden verzonden totdat de bezoeker het programma afsluit.
* Na opt-out, houdt het Web SDK op verzendend gebeurtenissen maar bestaande koekjes blijven.

## Goedkeuring met apparaat-id&#39;s van de eerste partij {#consent-with-fpids}

Als uw implementatie [ eerste-partijapparaat IDs (FPIDs) ](./fpid.md) gebruikt, wordt het FPID- koekje geplaatst door uw server onafhankelijk van de de toestemmingsstaat van SDK van het Web. Het FPID-cookie is een id die u beheert op uw eigen infrastructuur. De FPID wordt echter alleen naar de Edge Network verzonden wanneer de Web SDK een aanvraag indient (die met instemming wordt ingediend):

* Met `defaultConsent: "pending"` bestaat de FPID in de browser, maar wordt deze niet gebruikt voor het verzenden van een ECID totdat toestemming is verleend.
* Met `defaultConsent: "in"` wordt de FPID gebruikt op het eerste verzoek en wordt de ECID onmiddellijk zacht.

Als voor de uitvoering van uw toestemming geen id moet worden ingesteld voordat toestemming wordt gegeven, stelt u het FPID-cookie pas in nadat toestemming is gegeven. Alleen de toestemming van SDK Web verhindert niet dat het FPID-cookie wordt ingesteld, omdat dit cookie door uw server wordt beheerd.

## Veelvoorkomende valkuilen {#common-pitfalls}

+++**de toestemmingsbanner ontruimt identiteitskoekjes**

**Probleem**: Sommige platforms van het toestemmingsbeheer (CMPs) ontruimen alle koekjes — met inbegrip van `kndctr_` identiteitskoekjes — wanneer het voorstellen van de toestemmingsbanner, alvorens de bezoeker een keus maakt. Wanneer de bezoeker toestemming geeft, genereert de Web SDK een nieuwe ECID omdat de vorige is verwijderd. De bezoeker wordt in de rapportage weergegeven als een nieuwe persoon.

**Symptomen**:
* Een piek in het aantal unieke bezoekers na het inzetten van een toestemmingsbanner.
* Terugkerende bezoekers worden geteld als nieuwe bezoekers telkens wanneer hun toestemming vervalt en ze weer met de banner communiceren.

**Oplossing**: Vorm uw CMP om `kndctr_` koekjes te bewaren. Deze cookies zijn identiteitscookies, niet cookies volgen — ze identificeren het apparaat en bevatten geen gedragsgegevens. Als de CMP cookies moet wissen, voegt u `kndctr_` vooraf ingestelde cookies toe aan een uitsluitingslijst. U kunt het wissen van cookies ook uitstellen tot nadat de bezoeker uitdrukkelijk zijn toestemming heeft geweigerd in plaats van deze op voorhand te wissen.

+++

+++**Vertraagde toestemming veroorzaakt dubbele identiteit**

**Probleem**: Wanneer `defaultConsent` aan `pending` wordt geplaatst, wacht het Web SDK op toestemming alvorens om het even welke gegevens te verzenden. Als toestemming laat in de paginalopyclus wordt verleend (bijvoorbeeld na een bannerinteractie die een pagina opnieuw laadt), kan de volgende opeenvolging kwesties veroorzaken:

1. Pagina wordt geladen. `defaultConsent: "pending"`. Web SDK verzendt geen verzoeken.
2. De bezoeker verleent toestemming. CMP activeert een pagina opnieuw laden.
3. Pagina wordt opnieuw geladen. Web SDK initialiseert nu met toestemming en genereert een ECID.

Deze stroom is normaal en werkt correct. De kwestie doet zich voor wanneer CMP of uw implementatie per ongeluk koekjes tussen stap 2 en 3 ontruimt, of wanneer het Web SDK verschillend op het herladen wordt gevormd.

**Oplossing**: Zorg ervoor dat de configuratie van SDK van het Web (vooral `orgId` en `defaultConsent`) op elke paginalading identiek is. Als uw CMP na toestemming opnieuw laden activeert, controleert u of de identiteitscookies de herladen overleven.

+++

+++**Gebruikend `defaultConsent: "in"` met een toestemmingsbanner**

**Probleem**: Sommige plaatsingen van implementaties `defaultConsent: "in"` en roepen dan `setConsent` met `"general": "out"` als de bezoeker daalt. Deze benadering produceert een ECID en verzendt minstens één verzoek alvorens de toestemming wordt ontkend. Afhankelijk van uw regelgevende vereisten, zou deze aanvankelijke gegevensinzameling niet met het privacybeleid van uw organisatie kunnen richten.

**Oplossing**: Als uw regelgevend milieu toestemming vóór om het even welke gegevensinzameling of generatie ECID vereist, gebruik `defaultConsent: "pending"` in plaats daarvan. Deze instelling zorgt ervoor dat de Web SDK niet met de Edge Network communiceert totdat expliciet toestemming is verleend.

+++
