---
title: Identiteit van problemen in gegevensverzameling oplossen
description: Diagnose van veelvoorkomende identiteitsproblemen in SDK-implementaties op het web, waaronder bezoekersinflatie, inconsistenties in ECID, cookieconflicten en FPID-problemen.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1034'
ht-degree: 0%

---

# Identiteit van problemen in gegevensverzameling oplossen

Identiteitsproblemen worden vaak beschouwd als symptomen in downstreamrapportage (opgepompte aantallen bezoekers, gefragmenteerde profielen of verbroken personalisatie) in plaats van als fouten in de implementatie zelf. Deze pagina helpt u de gemeenschappelijkste identiteitskwesties in de implementaties van SDK van het Web diagnostiseren en oplossen. Voor achtergrond op hoe de identiteit in de Inzameling van Gegevens werkt, zie het [ identiteitsoverzicht ](./overview.md).

## Identiteitswaarden controleren {#inspect-identity}

Alvorens het oplossen van problemen een specifieke kwestie, wint de huidige identiteitswaarden terug die SDK van het Web gebruikt. Gebruik de opdracht [`getIdentity`](/help/collection/js/commands/getidentity.md) om de ECID en andere identiteitssignalen weer te geven:

```js
alloy("getIdentity", { namespaces: ["ECID", "CORE"] }).then(function(result) {
  console.log("ECID:", result.identity.ECID);
  console.log("CORE ID:", result.identity.CORE);
  console.log("Edge region:", result.edge.regionID);
});
```

U kunt identiteitswaarden in de ontwikkelaarshulpmiddelen van uw browser ook inspecteren:

1. Open het **lusje van de Toepassing** (Chrome/Edge) of **Opslag** tabel (Firefox/Safari).
2. Zoek naar cookies die met `kndctr_` op uw domein zijn voorafgegaan. Het `kndctr_<ORG_ID>_AdobeOrg_identity` -cookie bevat de ECID.
3. Open het **lusje van het Netwerk** en vind een `interact` of `collect` verzoek aan Edge Network. Controleer de lading van de verzoeklading voor `identityMap` en de antwoordlading voor identiteitshandvatten.

## Veelvoorkomende problemen {#common-issues}

+++**de tellingsinflatie van de Bezoeker**

**Symptom**: De rapporten van de Analyse tonen meer unieke bezoekers dan verwacht, of de zelfde persoon verschijnt als veelvoudige bezoekers over zittingen.

**Mogelijke oorzaken**:

| Oorzaak | Hoe te identificeren | Resolutie |
| --- | --- | --- |
| Korte cookie | Controleer of `kndctr_` cookies in de browser verlopen. Als deze over 7 dagen of minder verlopen, wordt de duur van cookies door het browserbeleid mogelijk beperkt. | Voer [ eerste partij apparaat IDs (FPIDs) uit ](./fpid.md) die van een server wordt geplaatst gebruikend een DNS A/AAAA- verslag voor langere koekjespersistentie. |
| FPID ontbreekt bij eerste aanvraag | Controleer het eerste Edge Network-verzoek bij het laden van de pagina. Als er geen FPID-cookie aanwezig is, genereert de Edge Network een nieuwe ECID. Als de FPID na de eerste aanvraag wordt ingesteld, wordt de ECID die op die eerste aanvraag wordt gegenereerd, weesnelheid toegekend. | Stel het FPID-cookie in voordat de Web SDK de eerste aanvraag verzendt. Zie [ wanneer om het koekje ](./fpid.md#when-to-set-cookie) te plaatsen. |
| `orgId` niet overeenkomend in verschillende domeinen | Vergelijk de configuratiewaarde van `orgId` in de verschillende domeinen. Bij niet-overeenkomende waarden ontstaan aparte identiteitsbereiken. | Gebruik hetzelfde [`orgId`](/help/collection/js/commands/configure/orgid.md) op alle domeinen binnen uw organisatie. |
| Constante banner cookies verwijderen | Als in uw toestemmingsimplementatie alle cookies worden gewist voordat toestemming wordt verleend en vervolgens de Web SDK wordt geïnitialiseerd, wordt een nieuwe ECID gegenereerd. | Configureer uw machtigingsbanner om `kndctr_` cookies te behouden of de SDK-initialisatie van het web uit te stellen totdat de toestemming is gegeven. Zie ook [ Toestemming en identiteit ](./consent.md). |
| JavaScript-set FPID-cookies | Voor cookies die zijn ingesteld met `document.cookie` gelden browserbeperkingen (ITP, ETP) die hun levensduur beperken, soms tot 24 uur. | Stel FPID-cookies in vanaf de server met behulp van een DNS A/AAAA-record, niet vanuit JavaScript. |

+++

+++**ECID verandert onverwacht tussen pagina&#39;s**

**Symptom**: ECID is verschillend op verschillende pagina&#39;s van het zelfde domein, of verandert op elke paginading.

**Diagnostische stappen**:

1. Controleer of het `kndctr_` identiteitscookie aanwezig is op beide pagina&#39;s. Als het op één pagina mist, controleer dat het Web SDK op die pagina wordt gevormd.
2. Controleer of het cookiedomein breed genoeg is ingesteld. Een cookie ingesteld op `shop.example.com` is niet beschikbaar op `www.example.com` . Zorg ervoor dat de infrastructuur voor eerste verzameling en cookie-instelling hetzelfde domeinbereik gebruikt.
3. Controleren op JavaScript die cookies op navigatie wist (bijvoorbeeld agressieve cookie-toestemmingsscripts of privacygereedschappen).
4. Als het gebruiken van een enig-paginatoepassing, verifieer dat het Web SDK één keer bij app initialisatie wordt gevormd, niet opnieuw geïnitialiseerd op elke routeverandering. Herinitialisatie kan een nieuwe ECID genereren.

+++

+++**FPID verzendt niet ECID**

**Symptom**: U hebt een koekje FPID geplaatst, maar `getIdentity` keert ECID terug die niet over bezoeken verenigbaar is, of FPID verschijnt niet in de verzoeklading van Edge Network.

**Diagnostische stappen**:

1. **verifieer het FPID koekjesformaat**: FPID moet een geldige [ UUIDv4 ](https://datatracker.ietf.org/doc/html/rfc4122) zijn. Open de ontwikkelaarsgereedschappen van uw browser, zoek het FPID-cookie en bevestig dat de waarde overeenkomt met het patroon `xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx` .
2. **Controle de koekjesnaam in de datastream**: Als u de [ methode van het gegevensstroomkoekje ](./fpid.md#setting-cookie-datastreams) gebruikt, moet de koekjesnaam die in de gegevensstroom wordt gevormd precies de naam van het koekje aanpassen dat uw server plaatst.
3. **Bevestig dat het koekje op het verzoek** wordt verzonden: In het lusje van het Netwerk, inspecteer de `Cookie` kopbal op het verzoek van Edge Network. Het FPID-cookie moet worden opgenomen.
4. **de identiteitsprioriteit van de Controle**: Als bestaande ECID reeds in a `kndctr_` koekje wordt opgeslagen, neemt het belangrijkheid over FPID. De FPID zaait alleen een nieuwe ECID als er geen bestaande ECID aanwezig is. Zie [ hoe FPIDs ](./fpid.md#how-fpids-work) voor de volledige prioritaire orde werkt.
5. **bevestigt CNAME**: Als het gebruiken van de methode van het gegevensstroomkoekje, bevestig dat uw eerste-partijinzameling CNAME correct wordt gevormd en dat de verzoeken door het worden verpletterd.

+++

+++**de identiteit van het dwars-domein werkt niet**

**Symptom**: Een bezoeker die van één van uw domeinen aan een andere klikt wordt behandeld als nieuwe bezoeker op het bestemmingsdomein.

**Diagnostische stappen**:

1. **Controle URL**: Inspecteer bestemmingsURL wanneer de bezoeker de verbinding klikt. Het moet een `adobe_mc` query-string parameter bevatten. Als de parameter ontbreekt, voegt het brondomein het niet toe. Zie [ uitvoeren dwars-domein het delen ](./cross-domain-sharing.md#implement-cross-domain-sharing).
2. **controleer de timing**: De `adobe_mc` parameter verloopt na vijf minuten. Als de bestemmingspagina te lang duurt om te laden (bijvoorbeeld, wegens omleiding of langzaam netwerk), kan de parameter verlopen alvorens het Web SDK het kan lezen.
3. **verifieer `orgId` gelijke**: Beide domeinen moeten het zelfde [`orgId`](/help/collection/js/commands/configure/orgid.md) gebruiken. Verkeerde organisatie-id&#39;s zorgen ervoor dat het doeldomein de identiteit voor de overdracht afwijst.
4. **bevestig SDK van het Web op de bestemming** is: De bestemmingspagina moet het Web SDK hebben geïnstalleerd en gevormd. Zonder deze parameter wordt de parameter `adobe_mc` genegeerd.
5. **Controle voor het strippen URL**: Sommige omleidingsdiensten, CDNs, of server-zij logische strook onbekende vraag-koord parameters. Controleer of `adobe_mc` eventuele tussenliggende omleidingen tussen de bron- en doelpagina&#39;s overleeft.

+++

+++**Mobiel-aan-Web identiteitshandoff ontbreekt**

**Symptom**: Een bezoeker die in mobiele app begint en een WebView of mobiele browser opent wordt behandeld als nieuwe bezoeker op de Webkant.

**Diagnostische stappen**:

1. **verifieer URL**: Logboek URL die tot WebView wordt overgegaan. Het moet een `adobe_mc` parameter bevatten die door [`getUrlVariables` wordt geproduceerd ](https://developer.adobe.com/client-sdks/edge/identity-for-edge-network/api-reference/#geturlvariables).
2. **de versies van SDK van de Controle**: De mobiele Identiteit voor de uitbreiding van Edge Network moet versie 1.1.0 of recenter zijn, en het Web SDK moet versie 2.11.0 of recenter zijn.
3. **controleer de timing**: Als dwars-domein het delen, verloopt de `adobe_mc` parameter na vijf minuten. Zorg ervoor dat de WebView direct wordt geladen nadat de URL is samengesteld.
4. **Bevestig `orgId` gelijke**: De organisatie-identiteitskaart van Experience Cloud moet het zelfde in zowel de mobiele configuraties van SDK als van SDK van het Web zijn.

+++
