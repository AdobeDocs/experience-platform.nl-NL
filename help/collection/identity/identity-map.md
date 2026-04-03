---
title: Identiteitskaart gebruiken in Gegevensverzameling
description: Leer hoe te om payloads te construeren en te verzenden identityMap om bekende bezoekers over namespaces in uw implementatie van SDK van het Web te identificeren.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Identiteitskaart gebruiken in Gegevensverzameling

Het `identityMap` voorwerp van de nuttige lading is hoe u Edge Network vertelt die een bezoeker voorbij hun apparaat-niveau [&#x200B; ECID &#x200B;](./overview.md) is. Wanneer een bezoeker zich aanmeldt, een aankoop voltooit of anderszins bekend wordt, kunt u id&#39;s op persoonlijke niveau (CRM-id, gehashte e-mail, loyalty-id, enz.) naast de ECID verzenden. Deze personen-vlakke herkenningstekens verstrekken waardevolle informatie aan stroomafwaartse diensten zodat zij kunnen:

* **de activiteit van de Sitch aan een persoon over apparaten en kanalen.** [&#x200B; de Dienst van de Identiteit &#x200B;](/help/identity-service/home.md) verbindt de identiteiten u in een [&#x200B; identiteitsgrafiek &#x200B;](/help/identity-service/features/identity-graph-viewer.md) verzendt, verbindend anoniem apparaat-vlakke gedrag met een bekende persoon.
* **bouwt verenigde klantenprofielen.** [&#x200B; Real-Time het Profiel van de Klant &#x200B;](/help/profile/home.md) gebruikt de primaire identiteit die u plaatste om gebeurtenissen en attributen aan één enkel profiel te verankeren, toelatend persoon-vlakke segmentatie en publieksbouw.
* **activeer publiek op stroomafwaartse bestemmingen.** Vele [&#x200B; Doelen &#x200B;](/help/destinations/home.md) vereisen opgehelderde persoon-vlakke identiteiten (gehakte e-mail, telefoonaantallen, enz.) om uw publiek aan hun gebruikersbases aan te passen.
* **Orchestrate dwars-kanaalreizen.** [&#x200B; Journey Optimizer &#x200B;](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html) gebruikt opgeloste identiteiten om reizen over e-mail, duw, en in-app kanalen teweeg te brengen en te personaliseren die op voor authentiek verklaard gedrag van een bezoeker worden gebaseerd.

Op deze pagina wordt uitgelegd hoe u `identityMap` -ladingen kunt samenstellen, de juiste instellingen voor elke identiteit kunt kiezen en algemene implementatiescenario&#39;s kunt afhandelen.

## Payloadstructuur {#structure}

`identityMap` is een JSON-object waarbij elke sleutel op hoofdniveau een naamruimte is en de waarde een array van identiteitsbeschrijvingen is. U kunt een of meer naamruimten opnemen in één lading en elke beschrijver bevat drie gebieden: `id`, `authenticatedState`, en `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Veld | Type | Vereist | Beschrijving |
| --- | --- | --- | --- |
| `id` | String | Ja | De id-waarde (bijvoorbeeld `user@example.com` of `ABC123` ). |
| `authenticatedState` | String | Ja | Hoe vertrouwend weet u dat deze identiteit aan de bezoeker toebehoort. Geldige waarden zijn `ambiguous` , `authenticated` en `loggedOut` . |
| `primary` | Boolean | Ja | Of deze identiteit de primaire id voor de gebeurtenis moet zijn. Precies één identiteit in alle naamruimten moet zijn gemarkeerd als `primary: true` . |

In de onderstaande secties wordt elk deel van de lading in detail beschreven.

### Naamruimtesleutels {#namespace-keys}

Elke top-level sleutel in `identityMap` is een [&#x200B; identiteit namespace &#x200B;](/help/identity-service/features/namespaces.md) — een koord dat het type van herkenningsteken (bijvoorbeeld, `CRMID`, `Email`, `Phone`, of `LoyaltyId`) classificeert. Naamruimten moeten aanwezig zijn in Identiteitsservice voordat u ernaar verwijst in een payload. U kunt meerdere naamruimtetoetsen in dezelfde gebeurtenis opnemen wanneer u meerdere id&#39;s voor de bezoeker hebt.

U hoeft de ECID niet op te nemen als naamruimtesleutel. De Edge Network voegt de ECID automatisch toe aan de identiteitslading. Als u de ECID expliciet opneemt, moet u deze niet markeren als `primary` wanneer er ook een identiteit op persoonniveau aanwezig is.

### `id` {#id}

Het veld `id` is de id-tekenreeks zelf — de waarde die Experience Platform opgeeft welke specifieke persoon of welk apparaat deze identiteit vertegenwoordigt. Elk [&#x200B; identiteit namespace &#x200B;](/help/identity-service/features/namespaces.md) verwacht een specifiek waardeformaat, en het verzenden van een waarde in het verkeerde formaat leidt tot een afzonderlijke identiteit die niet met de correct geformatteerde versie kan worden samengevoegd, resulterend in gefragmenteerde profielen.

Voordat u een waarde opneemt in `identityMap` , moet u deze voorbereiden volgens de indeling die uw doelnaamruimte verwacht:

| Algemene naamruimtetypen | De waarde voorbereiden | Voorbeeld |
| --- | --- | --- |
| **CRM / interne identiteitskaart** | Gebruik de exacte id die uw systeem van recordtoewijzingen toewijst. Houd de indeling consistent voor alle gebeurtenissen (casings, voorvoegsels van nullen en voorvoegsels). | `ABC-12345`, `00098765` |
| **E-mail (onbewerkt)** | Het volledige e-mailadres in kleine letters weergeven en regelafstand en navolgende witruimte bijsnijden. | `user@example.com` |
| **E-mail (gehakt)** | Het e-mailadres wordt eerst in kleine letters bijgesneden en vervolgens bijgesneden met SHA-256. Verzend de resulterende hexadecimale tekenreeks van 64 tekens. Voeg geen salt toe, tenzij uw naamruimtedefinitie dit vereist. | `a1b2c3d4e5f6a7b8c9...` |
| **Telefoon (E.164)** | Formaat het aantal in [&#x200B; E.164 &#x200B;](https://en.wikipedia.org/wiki/E.164): een belangrijke `+`, de landcode, en het abonneeaantal zonder ruimten of punctuatie. | `+15551234567` |
| **FPID** | Produceer a [&#x200B; UUIDv4 &#x200B;](https://datatracker.ietf.org/doc/html/rfc4122) koord. Zie [&#x200B; eerste-partij apparaat IDs &#x200B;](./fpid.md) voor generatievereisten. | `123e4567-e89b-42d3-9456-426614174000` |

Voor de volledige lijst van standaard namespaces en hun definities, zie [&#x200B; Overzicht van identiteitskaart namespace &#x200B;](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>De waarde `id` is hoofdlettergevoelig. `User@Example.com` en `user@example.com` worden behandeld als twee afzonderlijke identiteiten. Normaliseer hoofdletters voordat u de waarde verzendt (meestal door het e-mailadres te verlagen en witruimte in te snijden) om dubbele identiteiten in de grafiek te voorkomen.

#### `id` bij uitvoering verzamelen {#collect-id}

De vereiste id is zelden rechtstreeks beschikbaar op de pagina. De gemeenschappelijke inzamelingsstrategieën omvatten:

* **de laag van Gegevens**: Lees het herkenningsteken van de de gegevenslaag van uw plaats nadat de bezoeker binnen ondertekent. Deze locatie is de meest betrouwbare benadering, omdat de gegevenslaag wordt gevuld door de achterkant van de toepassing en de geverifieerde sessiestatus weerspiegelt.
* **het teken van de Auth of zittingskoekje**: Decode of kijk omhoog het herkenningsteken van een JWT of zittingskoekje dat uw authentificatiesysteem plaatst. Controleer of het token nog steeds actief is voordat u de waarde gebruikt.
* **server-zijverrijking**: De Prep van Gegevens van het gebruik [&#x200B; voor de Inzameling van Gegevens &#x200B;](/help/datastreams/data-prep.md) of een [&#x200B; gebeurtenis die regel &#x200B;](/help/tags/ui/event-forwarding/overview.md) door:sturen om het herkenningsteken bij Edge in kaart te brengen of om te zetten alvorens het stroomafwaartse diensten bereikt. Deze locatie is handig wanneer de client alleen een ondoorzichtig sessietoken heeft dat aan een interne id op de server is toegewezen.

>[!TIP]
>
>Als een bepaalde `id` -waarde wordt omgezet in een lege tekenreeks, `null` of `undefined` , neemt u de naamruimte niet op in de `identityMap` . Als u een lege `id` verzendt, wordt een verbroken identiteitsrecord gemaakt. Bescherm uw implementatie met een controle alvorens de lading te bouwen.

### `authenticatedState` {#authenticated-state}

Het veld `authenticatedState` geeft aan downstream-services door hoeveel vertrouwen een bepaalde identiteit moet krijgen. De volgende waarden zijn geldig voor dit veld:

| Waarde | Wanneer gebruiken |
| --- | --- |
| **`authenticated`** | De bezoeker heeft zijn identiteit tijdens de huidige sessie actief bewezen (bijvoorbeeld door u aan te melden met referenties, een MFA te voltooien of een vergelijkbare verificatie). |
| **`loggedOut`** | De bezoeker is eerder geverifieerd, maar is sindsdien afgemeld. De identiteit is nog steeds gekoppeld aan het apparaat, maar de sessie is niet meer actief. |
| **`ambiguous`** | De identiteit kan niet worden bevestigd als behorend tot de huidige bezoeker. Gebruik deze waarde voor apparaat-vlakke herkenningstekens zoals FPIDs of om het even welke herkenningsteken waar de authentificatie nog niet is gebeurd. |

>[!TIP]
>
>De waarde `authenticatedState` is van invloed op de manier waarop Adobe Experience Platform Identity Service identiteitsgrafieken bouwt en samenvoegt. Als u `authenticated` verzendt voor een identiteit die niet is geverifieerd, kunnen er onjuiste koppelingen naar andere apparaten ontstaan die moeilijk ongedaan kunnen worden gemaakt.

### `primary` {#primary-identity}

Elke `identityMap` -lading moet precies één id hebben die als `primary: true` is gemarkeerd. De primaire identiteit bepaalt welke identiteit wordt gebruikt als anker voor de gebeurtenis in Experience Platform.

Volg deze richtlijnen bij het instellen van de primaire identiteit:

* **wanneer een persoon-vlakke identiteit beschikbaar** is (de bezoeker wordt binnen ondertekend), merk persoon-vlakke namespace als primair en ECID als niet-primair. Dit vertelt Experience Platform om de gebeurtenis aan de persoon eerder dan het apparaat te verankeren.
* **wanneer slechts apparaat-vlakke identiteiten beschikbaar** zijn (de bezoeker is anoniem), wordt ECID automatisch gebruikt als primaire identiteit. U hoeft de ECID niet op te nemen in uw `identityMap` — de Edge Network voegt deze automatisch toe.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Identiteitskaart verzenden in uw implementatie {#send-identity}

>[!BEGINTABS]

>[!TAB  de bibliotheek van JavaScript ]

Geef `identityMap` door in het `xdm` -object van een [`sendEvent`](/help/collection/js/commands/sendevent/overview.md) -aanroep:

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB  de markeringsuitbreiding van SDK van het Web ]

Gebruik het [&#x200B; type van het de kaart van de Identiteit &#x200B;](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) gegevenselement om uw identiteitslading in de Markeringen UI te bouwen:

1. Maak een gegevenselement met de extensie **[!UICONTROL Adobe Experience Platform Web SDK]** en het gegevenstype **[!UICONTROL Identity map]** data-element.
2. Voeg identiteiten toe door namespace, het gegevenselement of de waarde te specificeren die aan het herkenningsteken, en de voor authentiek verklaarde staat wordt opgelost.
3. Eén identiteit als primair markeren.
4. Verwijs naar dit gegevenselement in de handeling **[!UICONTROL Send event]** onder **[!UICONTROL Identity map]** .

>[!ENDTABS]

## Algemene scenario&#39;s {#common-scenarios}

+++**Login**

Wanneer een bezoeker zich aanmeldt, verzendt u de ID op persoonniveau met `authenticatedState: "authenticated"` en `primary: true` . Neem deze identiteit op bij de eerste gebeurtenis na verificatie en bij alle volgende gebeurtenissen in de sessie.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Logout**

Wanneer een bezoeker zich afmeldt, werkt u `authenticatedState` bij naar `loggedOut` terwijl dezelfde id behouden blijft. Dit bewaart de vereniging tussen het apparaat en de persoon terwijl het signaleren dat de zitting niet meer actief is.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Na het uitloggen wordt de ECID weer de effectieve primaire identiteit (de Edge Network past deze automatisch toe). Markeer een andere persoonsidentiteit alleen als primair als de bezoeker zich aanmeldt bij een ander account.

>[!IMPORTANT]
>
>Stop niet volledig met het verzenden van het herkenningsteken na logout. Als u van `authenticated` naar `loggedOut` schakelt, wordt aan de downstream-services doorgegeven dat de sessie is beëindigd. Als u de id weglaat, blijft er in de identiteitsgrafiek een hiaat zitten dat gefragmenteerde profielen kan veroorzaken.

+++

+++**Veelvoudige namespaces**

U kunt meerdere naamruimten verzenden in dezelfde gebeurtenis. Dit scenario is gemeenschappelijk wanneer een bezoeker binnen wordt ondertekend en u verscheidene beschikbare herkenningstekens hebt (bijvoorbeeld, een identiteitskaart van CRM, gehakt e-mail, en loyaliteitsidentiteitskaart). Neem alle bekende id&#39;s op, markeer er slechts één als primair en stel de andere in op `primary: false` .

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>Als u meerdere naamruimten met dezelfde `authenticatedState` -gebeurtenis verzendt, geeft Identiteitsservice het sterkste signaal voor het koppelen van die identiteiten. Alle beschikbare id&#39;s opnemen op het verificatiepunt in plaats van ze te verspreiden over afzonderlijke gebeurtenissen.

+++

+++**Anonieme bezoekers**

Voor anonieme bezoekers hoeft u gewoonlijk helemaal geen `identityMap` te verzenden. De Edge Network wijst automatisch een ECID toe en gebruikt deze als primaire identiteit. Als u [&#x200B; eerste-partij apparaat IDs &#x200B;](./fpid.md) gebruikt, is FPID de enige identiteit u voor anonieme bezoekers moet omvatten.

+++

## Hoe identityMap van invloed is op de identiteitsgrafiek {#identity-graph}

Elke `identityMap` nuttige lading die Experience Platform bereikt wordt verwerkt door [&#x200B; Dienst van de Identiteit &#x200B;](/help/identity-service/home.md), die de identiteiten verbindt u in een [&#x200B; identiteitsgrafiek &#x200B;](/help/identity-service/features/identity-graph-viewer.md) verzendt. Welke naamruimten u opneemt, hoe u `authenticatedState` instelt en welke identiteit u markeert als `primary` , geeft rechtstreeks de vorm hoe Identity Service deze grafieken bouwt en samenvoegt.

Belangrijk gedrag om bewust te zijn van:

* **Identiteiten die op de zelfde gebeurtenis worden verzonden zijn verbonden samen.** Als u een CRMID en een E-mailnaamruimte opneemt in dezelfde `sendEvent` -aanroep, maakt Identity Service een koppeling tussen deze twee identiteiten. Door id&#39;s over verschillende gebeurtenissen te spreiden, worden de koppelingen zwakker en kunnen de grafieken gefragmenteerd raken.
* **de `primary` identiteit verankert de gebeurtenis in het Profiel van de Klant in real time.** Profiel gebruikt de primaire identiteit om te bepalen tot welk profiel de gebeurtenis behoort. Als u de verkeerde identiteit als primair markeert (bijvoorbeeld als u ECID als primair instelt wanneer een id op persoonniveau beschikbaar is), kunnen gebeurtenissen worden opgeslagen op apparaatprofielen in plaats van op persoonniveau.
* **`authenticatedState` beïnvloedt grafiekvertrouwen.** Als u `authenticated` verzendt voor een identiteit die niet echt is geverifieerd, kunnen er onjuiste koppelingen naar andere apparaten ontstaan die moeilijk ongedaan kunnen worden gemaakt. Gebruik `authenticated` alleen als de bezoeker tijdens de huidige sessie actief zijn identiteit heeft bewezen.

Als uw implementatie [&#x200B; identiteitsgrafiek gebruikt die regels &#x200B;](/help/identity-service/identity-graph-linking-rules/overview.md) verbindt (zoals namespaceprioriteit of het algoritme van de identiteitsoptimalisering), herzie de [&#x200B; implementatiegids &#x200B;](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) om te begrijpen hoe die regels met de identiteiten in wisselwerking staan u door `identityMap` verzendt.

>[!NOTE]
>
>`identityMap` wordt alleen verzonden wanneer de Web SDK een aanvraag indient bij de Edge Network, die wordt geblokkeerd door de toestemming van de bezoeker. Als in uw implementatie `defaultConsent: "pending"` wordt gebruikt, worden identiteiten pas verzonden nadat toestemming is verleend. Zie [&#x200B; Toestemming en identiteit &#x200B;](./consent.md) voor details.
