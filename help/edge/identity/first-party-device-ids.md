---
title: Eerste partij apparaat IDs in het Web SDK van het Platform
description: Leer hoe u FPID's (First-party device ID's) voor de Adobe Experience Platform Web SDK configureert.
source-git-commit: 7a3a89fe92d965a5f5796f7722d3bc2daf6ef178
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 0%

---

# Eerste partij apparaat IDs in het Web SDK van het Platform

De Adobe Experience Platform Web SDK wijst [Adobe Experience Cloud-id&#39;s (ECID&#39;s)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) aan websitebezoekers door middel van cookies, om het gedrag van de gebruiker te volgen. Als u browserbeperkingen voor de levensduur van cookies wilt compenseren, kunt u ervoor kiezen om uw eigen apparaat-id&#39;s in te stellen en te beheren. Deze worden ook wel FPID&#39;s (First-Party Device ID&#39;s) genoemd.

>[!NOTE]
>
>De steun van eerste-partijapparaat identiteitskaart is slechts beschikbaar wanneer het verzenden van gegevens naar het Netwerk van de Rand van het Platform via het Web SDK van het Platform.

Dit document behandelt hoe te om eerste-partijapparaat IDs voor uw implementatie van SDK van het Web van het Platform te vormen.

## Vereisten

Deze gids veronderstelt u vertrouwd met bent hoe de identiteitsgegevens voor het Web SDK van het Platform werken, met inbegrip van de rol van ECIDs en `identityMap`. Zie het overzicht op [identiteitsgegevens in de SDK van het Web](./overview.md) voor meer informatie .

## FPID&#39;s gebruiken

De koekjes van de eerste partij zijn het meest efficiënt wanneer zij gebruikend een klant-bezeten server worden geplaatst die hefboomwerkingen een DNS A-verslag in tegenstelling tot DNS CNAME. Gebruikend eerste-partijapparaat IDs, kunt u uw eigen apparaat IDs in koekjes plaatsen gebruikend DNS A-verslagen. Deze id&#39;s kunnen vervolgens naar Adobe worden verzonden en als zaden worden gebruikt om ECID&#39;s te genereren die de primaire id&#39;s zullen blijven in Adobe Experience Cloud-toepassingen.

Als u een FPID voor een websitebezoeker naar het Edge Network van het Platform wilt verzenden, moet u de FPID opnemen in het dialoogvenster `identityMap` voor die bezoeker. Zie de sectie verderop in dit document op [FPID&#39;s gebruiken in `identityMap`](#identityMap) voor meer informatie .

## Vereisten voor id-opmaak

Het Netwerk van de Rand van het Platform keurt slechts identiteitskaart&#39;s goed die aan het voldoen [UUIDv4-indeling](https://datatracker.ietf.org/doc/html/rfc4122). Apparaat-id&#39;s die niet de UUIDv4-indeling hebben, worden geweigerd.

Het genereren van een UUID zal bijna altijd resulteren in een unieke, willekeurige id, waarbij de kans dat een botsing optreedt verwaarloosbaar is. UUIDv4 kan niet worden verzonden gebruikend IP adressen of een andere persoonlijke identificeerbare informatie (PII). UUID&#39;s zijn alomtegenwoordig en bibliotheken zijn beschikbaar voor vrijwel elke programmeertaal om ze te genereren.

## Een cookie instellen met een DNS A-record

U kunt een cookie op verschillende manieren op een manier instellen die voorkomt dat deze wordt beperkt door het browserbeleid:

* Cookies genereren met scripttalen op de server
* Cookies instellen als reactie op een API-aanvraag die is uitgevoerd naar een subdomein of ander eindpunt op de site
* Cookies genereren met behulp van een CMS
* Cookies genereren met behulp van een CDN

>[!NOTE]
>
>Cookies ingesteld met gebruik van JavaScript `document.cookie` Deze methode wordt bijna nooit beschermd tegen browserbeleid dat de duur van cookies beperkt.

## Wanneer stelt u het cookie in

Het FPID-cookie moet idealiter worden ingesteld voordat u een aanvraag indient bij het Edge-netwerk. In gevallen waarin dat niet mogelijk is, wordt een ECID echter nog steeds gegenereerd met bestaande methoden en fungeert deze als primaire id zolang het cookie bestaat.

Ervan uitgaande dat de ECID uiteindelijk wordt beïnvloed door een beleid voor het verwijderen van de browser, maar de FPID niet, wordt de FPID bij het volgende bezoek de primaire identificator en wordt deze gebruikt om de ECID bij elk volgend bezoek te bezaaien.

## De vervaldatum van de cookie instellen

Het instellen van de vervaldatum van een cookie moet zorgvuldig worden overwogen wanneer u de FPID-functionaliteit implementeert. Bij het nemen van dit besluit moet u rekening houden met de landen of regio&#39;s waarin uw organisatie samen met de wetten en het beleid in elk van die regio&#39;s werkt.

Als onderdeel van dit besluit wilt u mogelijk een beleid voor het instellen van cookies in het hele bedrijf toepassen of een beleid dat varieert voor gebruikers in elke landinstelling waar u werkt.

Ongeacht de instelling die u kiest voor de aanvankelijke vervaldatum van een cookie, moet u logica opnemen die de vervaldatum van de cookie verlengt telkens wanneer een nieuw bezoek aan de site plaatsvindt.

## Gevolgen van cookie-vlaggen

Er zijn verschillende cookievlaggen die van invloed zijn op de manier waarop cookies in verschillende browsers worden verwerkt:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Secure`](#secure)
* [` SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies die zijn ingesteld met de `HTTPOnly` Markering kan niet worden benaderd met clientscripts. Dit betekent dat als u een `HTTPOnly` markering bij het instellen van de FPID, moet u een scripttaal aan serverzijde gebruiken om de cookiewaarde voor opname in de `identityMap`.

Als u ervoor kiest om het Platform Edge Network de waarde van het FPID-cookie te laten lezen, stelt u de optie `HTTPOnly` De markering zorgt ervoor dat de waarde niet toegankelijk is voor clientscripts, maar geen negatieve invloed heeft op de mogelijkheid van het Edge Network van het Platform om de cookie te lezen.

>[!NOTE]
>
>Gebruik van de `HTTPOnly` markering heeft geen invloed op het cookiebeleid dat de levensduur van cookies kan beperken. Het is echter nog steeds iets wat u moet overwegen wanneer u de waarde van de FPID instelt en leest.

### `Secure` {#secure}

Cookies die zijn ingesteld met de `Secure` wordt alleen naar de server verzonden met een gecodeerde aanvraag via het HTTPS-protocol. Met deze markering kunt u ervoor zorgen dat aanvallers van &#39;man-in-the-middle&#39; de waarde van het cookie niet gemakkelijk kunnen benaderen. Het is altijd verstandig om, indien mogelijk, de `Secure` markering.

### `SameSite` {#same-site}

De `SameSite` Met dit kenmerk kunnen servers bepalen of cookies worden verzonden met aanvragen die verwijzen naar andere sites. Het kenmerk biedt enige bescherming tegen valsemunterij op andere locaties. Er zijn drie mogelijke waarden: `Strict`, `Lax` en `None`. Raadpleeg uw interne team om te bepalen welke instelling geschikt is voor uw organisatie.

Indien niet `SameSite` kenmerk is opgegeven. De standaardinstelling voor sommige browsers is nu `SameSite=Lax`.

## FPID&#39;s gebruiken in `identityMap` {#identityMap}

Hieronder ziet u hoe u een FPID als een eigen FPID instelt in de `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Net als bij andere identiteitstypen kunt u de FPID opnemen met andere identiteiten binnen `identityMap`. Hieronder ziet u een voorbeeld van de FPID die is opgenomen in een geautoriseerde CRM-id:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Als FPID in een koekje bevat dat door het Netwerk van de Rand wordt gelezen wanneer de inzameling van de eerste-partijgegevens wordt toegelaten, zou u slechts voor authentiek verklaarde identiteitskaart van CRM moeten vangen:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Het volgende `identityMap` zou resulteren in een foutreactie van het Edge Network, omdat het de `primary` -indicator voor de FPID. Ten minste een van de id&#39;s in `identityMap` moeten worden gemarkeerd als `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

De foutreactie die in dit geval door Experience Edge wordt gegeven, is vergelijkbaar met de volgende:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## ID-hiërarchie

Wanneer zowel een ECID als een FPID aanwezig zijn, krijgt de ECID prioriteit bij het identificeren van de gebruiker. Hierdoor blijft een bestaande ECID in de cookie-winkel van de browser de primaire id en loopt het risico dat het aantal bestaande bezoekers wordt beïnvloed. Voor bestaande gebruikers wordt de FPID pas de primaire identiteit als de ECID verloopt of als gevolg van een browserbeleid of handmatig proces wordt verwijderd.

Identiteiten krijgen prioriteit in de volgende volgorde:

1. ECID opgenomen in de `identityMap`
1. ECID opgeslagen in een cookie
1. FPID opgenomen in de `identityMap`
1. FPID opgeslagen in een cookie

## Migreren naar apparaat-id&#39;s van eerste bedrijven

Als u naar het gebruiken van FPIDs van een vorige implementatie migreert, kan het moeilijk zijn om te visualiseren hoe de overgang op een laag niveau zou kunnen kijken.

Om dit proces te illustreren, overweeg een scenario dat een klant impliceert die eerder uw plaats heeft bezocht en welke invloed een migratie FPID op hoe zou hebben die klant in de oplossingen van Adobe wordt geïdentificeerd.

![Diagram dat toont hoe de waarden van identiteitskaart van een klant tussen bezoeken na het migreren aan FPIDs worden bijgewerkt](../images/identity/tracking/visits.png)

| Bezoek | Beschrijving |
| --- | --- |
| Eerste bezoek | Stel dat u het FPID-cookie nog niet hebt ingesteld. De ECID in de [AMCV cookie](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) wordt gebruikt om de bezoeker te identificeren. |
| Tweede bezoek | De implementatie van de oplossing First-Party Device ID is gestart. De bestaande ECID is nog steeds aanwezig en blijft de primaire identificator voor bezoekersidentificatie. |
| Derde bezoek | Tussen het tweede en het derde bezoek is voldoende tijd verstreken om de ECID te verwijderen vanwege het browserbeleid. Omdat de FPID echter is ingesteld met een DNS A-record, blijft de FPID bestaan. De FPID wordt nu beschouwd als de primaire id en wordt gebruikt om de ECID te verzenden, die naar het apparaat van de eindgebruiker wordt geschreven. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de Adobe Experience Platform en de Experience Cloud. |
| Vierde bezoek | Tussen de derde en de vierde keer is er voldoende tijd verstreken om de ECID te verwijderen vanwege het browserbeleid. Net als bij het vorige bezoek blijft de FPID te wijten aan de wijze waarop zij is ingesteld. Deze keer wordt dezelfde ECID gegenereerd als het vorige bezoek. De gebruiker wordt door het Experience Platform en de oplossingen van de Experience Cloud gezien zoals de zelfde gebruiker zoals het vorige bezoek. |
| Vijfde bezoek | Tussen de vierde en de vijfde keer dat de gebruiker het programma bezoekt, heeft de eindgebruiker alle cookies in zijn browser gewist. Er wordt een nieuwe FPID gegenereerd die wordt gebruikt om het maken van een nieuwe ECID te stimuleren. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de Adobe Experience Platform en de Experience Cloud. |

{style=&quot;table-layout:auto&quot;}

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over apparaat-id&#39;s van andere leveranciers.

### Hoe anders zaait u een id dan eenvoudig een id genereren?

Het begrip zaaien is uniek omdat de FPID die aan Adobe Experience Cloud wordt doorgegeven, wordt omgezet in een ECID met behulp van een deterministisch algoritme. Telkens wanneer dezelfde FPID naar het Adobe Experience Platform Edge Network wordt verzonden, wordt dezelfde ECID van de FPID verzonden.

### Wanneer moet de apparaat-id van de eerste partij worden gegenereerd?

Om potentiële bezoekersinflatie te verminderen, zou FPID moeten worden geproduceerd alvorens uw eerste verzoek te maken gebruikend het Web SDK van het Platform. Als u dit echter niet kunt doen, wordt er nog steeds een ECID gegenereerd voor die gebruiker en wordt deze gebruikt als primaire id. De gegenereerde FPID wordt pas de primaire id als de ECID niet meer aanwezig is.

### Welke methodes van de gegevensinzameling steunen eerste-partij apparaat IDs?

Momenteel slechts steunt het Web SDK van het Platform FPIDs.

### Worden FPIDs opgeslagen op om het even welk Platform of Experience Cloud oplossingen?

Zodra FPID is gebruikt om een ECID te zaaien, wordt het geschrapt van `identityMap` en vervangen door de ECID die is gegenereerd. De FPID wordt niet opgeslagen in Adobe Experience Platform- of Experience Cloud-oplossingen.
