---
title: Eerste-partij apparaat IDs in Web SDK
description: Leer hoe u FPID's (First-party device ID's) voor de Adobe Experience Platform Web SDK configureert.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: b35a4316ca4ef82e545a7718f1b986f978003a0e
workflow-type: tm+mt
source-wordcount: '1986'
ht-degree: 0%

---


# Eerste-partij apparaat IDs in Web SDK

SDK van het Web van Adobe Experience Platform wijst [ Adobe Experience Cloud IDs (ECIDs) ](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) aan websitebezoekers door koekjes te gebruiken toe, om gebruikersgedrag te volgen. Als u browserbeperkingen voor de levensduur van cookies wilt compenseren, kunt u ervoor kiezen om uw eigen apparaat-id&#39;s in te stellen en te beheren. Deze worden ook wel FPID&#39;s (First-Party Device ID&#39;s) genoemd.

>[!NOTE]
>
>De steun van eerste-partijapparaatidentiteitskaart is slechts beschikbaar wanneer het verzenden van gegevens naar de Edge Network van het Platform via het Web SDK van het Platform.

>[!IMPORTANT]
>
>Eerste-partij apparaat IDs is niet compatibel met de [ functionaliteit van derdekoekjes ](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) in Web SDK.
>U kunt apparaat-id&#39;s van andere leveranciers gebruiken of cookies van andere leveranciers, maar u kunt beide functies niet tegelijkertijd gebruiken.

Dit document behandelt hoe te om eerste-partijapparaat IDs voor uw implementatie van SDK van het Web van het Platform te vormen.

## Vereisten

Deze gids veronderstelt u vertrouwd met bent hoe de identiteitsgegevens voor het Web SDK van het Platform, met inbegrip van de rol van ECIDs en `identityMap` werken. Zie het overzicht op [ identiteitsgegevens in het Web SDK ](./overview.md) voor meer informatie.

## FPID&#39;s gebruiken

FPID&#39;s volgen bezoekers met behulp van cookies van de eerste partij. De koekjes van de eerste partij zijn het meest efficiënt wanneer zij gebruikend een server worden geplaatst die een DNS [ verslag van A ](https://datatracker.ietf.org/doc/html/rfc1035) (voor IPv4) of [ het verslag van AAAA ](https://datatracker.ietf.org/doc/html/rfc3596) (voor IPv6), in tegenstelling tot een DNS CNAME of code van JavaScript gebruikt.

>[!IMPORTANT]
>
>`A` - of `AAAA` -records worden alleen ondersteund voor het instellen en bijhouden van cookies. De primaire methode voor gegevensinzameling is door DNS CNAME. Met andere woorden, FPID&#39;s worden ingesteld met een A-record of AAAA-record en worden vervolgens naar de Adobe verzonden met een CNAME.
>
>Het [ Adobe-Beheerde Programma van het Certificaat ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) wordt ook nog gesteund voor de inzameling van eerstepartijgegevens.

Nadat een FPID-cookie is ingesteld, kan de waarde ervan worden opgehaald en naar de Adobe worden verzonden wanneer gebeurtenisgegevens worden verzameld. Verzamelde FPID&#39;s worden gebruikt als zaden om ECID&#39;s te genereren, die in Adobe Experience Cloud-toepassingen nog steeds de belangrijkste identificatoren zijn.

Als u een FPID voor een websitebezoeker naar de Edge Network Platform wilt verzenden, moet u de FPID opnemen in de `identityMap` voor die bezoeker. Zie de sectie later in dit document op [ gebruikend FPIDs in `identityMap`](#identityMap) voor meer informatie.

### Vereisten voor id-opmaak

De Edge Network van het Platform keurt slechts IDs goed die aan het [ formaat UIDv4 ](https://datatracker.ietf.org/doc/html/rfc4122) voldoen. Apparaat-id&#39;s die niet de UUIDv4-indeling hebben, worden geweigerd.

Het genereren van een UUID zal bijna altijd resulteren in een unieke, willekeurige id, waarbij de kans dat een botsing optreedt verwaarloosbaar is. UUIDv4 kan niet worden verzonden gebruikend IP adressen of een andere persoonlijke identificeerbare informatie (PII). UUID&#39;s zijn alomtegenwoordig en bibliotheken kunnen voor vrijwel elke programmeertaal worden gevonden om ze te genereren.

## Het plaatsen van een koekje van eerste partijidentiteitskaart in de UI van Gegevensstromen {#setting-cookie-datastreams}

U kunt een cookienaam in de UI van Datastreams specificeren, waar [!DNL FPID] kan verblijven, eerder dan het moeten de koekjeswaarde lezen en FPID in de kaart van de Identiteit omvatten.

>[!IMPORTANT]
>
>Deze eigenschap vereist dat u ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) toegelaten de Inzameling van Gegevens van de Eerste Partij [ hebt.

Zie de [ documentatie van gegevensstromen ](../../datastreams/configure.md) voor gedetailleerde informatie over hoe te om een gegevensstroom te vormen.

Schakel de optie **[!UICONTROL First Party ID Cookie]** in wanneer u de gegevensstroom configureert. Dit het plaatsen vertelt de Edge Network om naar een gespecificeerd koekje te verwijzen wanneer het opzoeken van eerste-partijapparaat identiteitskaart, eerder dan het opzoeken van deze waarde in de [ Kaart van de Identiteit ](#identityMap).

Zie de documentatie op [ eerste-partijkoekjes ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html) voor meer details over hoe zij met Adobe Experience Cloud werken.

![ beeld van Platform UI die de configuratie toont die van de gegevensstroom de Eerste het plaatsen van het Koekje van identiteitskaart van de Partij ](../assets/first-party-id-datastreams.png) benadrukt

Als u deze instelling inschakelt, moet u de naam opgeven van het cookie waarop de id moet worden opgeslagen.

Als u ID&#39;s van eerste partijen gebruikt, kunt u geen synchronisatie van id&#39;s van derden uitvoeren. Identiteitssynces van derden vertrouwen op de [!DNL Visitor ID] -service en de `UUID` die door die service worden gegenereerd. Wanneer u de functie voor de eerste id gebruikt, wordt de ECID gegenereerd zonder gebruik te maken van de [!DNL Visitor ID] -service, waardoor syncs voor andere id&#39;s niet mogelijk is.

Wanneer u eerste partij IDs gebruikt, worden de mogelijkheden van de Audience Manager die op activering in partnerplatforms worden gericht niet gesteund, gegeven dat de syncs van identiteitskaart van de Partner van de Audience Manager meestal gebaseerd op `UUIDs` of `DIDs` zijn. De ECID die is afgeleid van een ID van de eerste partij is niet gekoppeld aan een `UUID`, waardoor deze niet-adresseerbaar is.

## Een cookie instellen met uw eigen server

Wanneer u een cookie instelt met een server die u bezit, kunt u verschillende methoden gebruiken om te voorkomen dat het cookie wordt beperkt door het browserbeleid:

* Cookies genereren met scripttalen op de server
* Cookies instellen als reactie op een API-aanvraag die is uitgevoerd naar een subdomein of ander eindpunt op de site
* Cookies genereren met een CMS
* Cookies genereren met behulp van een CDN

>[!IMPORTANT]
>
>Cookies die zijn ingesteld met de methode JavaScript `document.cookie` worden bijna nooit beschermd tegen browserbeleid dat de duur van cookies beperkt.

### Wanneer stelt u het cookie in

Het FPID-cookie moet idealiter worden ingesteld voordat aanvragen bij de Edge Network worden ingediend. In gevallen waarin dat niet mogelijk is, wordt een ECID echter nog steeds gegenereerd met behulp van bestaande methoden en fungeert deze als primaire id zolang het cookie bestaat.

Ervan uitgaande dat de ECID uiteindelijk wordt beïnvloed door een beleid voor het verwijderen van de browser, maar de FPID niet, wordt de FPID bij het volgende bezoek de primaire identificator en wordt deze gebruikt om de ECID bij elk volgend bezoek te bezaaien.

### De vervaldatum van de cookie instellen

Het instellen van de vervaldatum van een cookie moet zorgvuldig worden overwogen wanneer u de FPID-functionaliteit implementeert. Wanneer u hierover beslist, moet u rekening houden met de landen of regio&#39;s waarin uw organisatie werkt, samen met de wetten en het beleid in elk van die regio&#39;s.

Als onderdeel van dit besluit wilt u mogelijk een beleid voor het instellen van cookies in het hele bedrijf toepassen of een beleid dat per landinstelling verschilt.

Ongeacht de instelling die u kiest voor de aanvankelijke vervaldatum van een cookie, moet u logica opnemen die de vervaldatum van de cookie verlengt telkens wanneer een nieuw bezoek aan de site plaatsvindt.

## Gevolgen van cookie-vlaggen

Er zijn verschillende cookiemarkeringen die van invloed zijn op de manier waarop cookies in verschillende browsers worden verwerkt:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Secure`](#secure)
* [` SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies die zijn ingesteld met de markering `HTTPOnly` , zijn niet toegankelijk met clientscripts. Dit betekent dat als u bij het instellen van de FPID een markering `HTTPOnly` instelt, u een scripttaal aan de serverzijde moet gebruiken om de cookiewaarde voor opname in `identityMap` te lezen.

Als u ervoor kiest om de Edge Network Platform de waarde van het FPID-cookie te laten lezen, zorgt het instellen van de markering `HTTPOnly` ervoor dat de waarde niet toegankelijk is voor clientscripts, maar geen negatieve invloed heeft op de mogelijkheid van de Edge Network van het Platform om de cookie te lezen.

>[!NOTE]
>
>Het gebruik van de markering `HTTPOnly` heeft geen invloed op het cookiebeleid dat de levensduur van cookies kan beperken. Het is echter nog steeds iets wat u moet overwegen wanneer u de waarde van de FPID instelt en leest.

### `Secure` {#secure}

Cookies die zijn ingesteld met het kenmerk `Secure` worden alleen verzonden naar de server met een gecodeerde aanvraag via het HTTPS-protocol. Door deze markering te gebruiken, kunt u ervoor zorgen dat aanvallers van &#39;man in the middle&#39; de waarde van het cookie niet gemakkelijk kunnen benaderen. Het is altijd verstandig om de markering `Secure` in te stellen, als dat mogelijk is.

### `SameSite` {#same-site}

Met het kenmerk `SameSite` kunnen servers bepalen of cookies worden verzonden met aanvragen die verwijzen naar andere sites. Het kenmerk biedt enige bescherming tegen valsemunterij op andere locaties. Er zijn drie mogelijke waarden: `Strict`, `Lax` en `None` . Raadpleeg uw interne team om te bepalen welke instelling geschikt is voor uw organisatie.

Als er geen kenmerk `SameSite` is opgegeven, is de standaardinstelling voor sommige browsers nu `SameSite=Lax` .

## FPID&#39;s gebruiken in `identityMap` {#identityMap}

Hieronder ziet u een voorbeeld van hoe u een FPID instelt in de `identityMap` :

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

Net als bij andere identiteitstypen kunt u de FPID opnemen met andere identiteiten in `identityMap` . Hieronder ziet u een voorbeeld van de FPID die is opgenomen in een geautoriseerde CRM-id:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
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

Als FPID in een koekje bevat dat door de Edge Network wordt gelezen wanneer de inzameling van de eerste-partijgegevens wordt toegelaten, zou u slechts voor authentiek verklaarde identiteitskaart van CRM moeten vangen:

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

De volgende `identityMap` resulteert in een foutreactie van de Edge Network omdat de indicator `primary` voor de FPID ontbreekt. Ten minste een van de id&#39;s in `identityMap` moet zijn gemarkeerd als `primary` .

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

De foutreactie die in dit geval door de Edge Network wordt gegeven, is vergelijkbaar met de volgende:

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

Wanneer zowel een ECID als een FPID aanwezig zijn, krijgt de ECID prioriteit bij het identificeren van de gebruiker. Dit zorgt ervoor dat wanneer een bestaande ECID aanwezig is in de browser cookie store, deze de primaire id blijft en dat het aantal bestaande bezoekers niet kan worden beïnvloed. Voor bestaande gebruikers wordt de FPID pas de primaire identiteit als de ECID verloopt of als gevolg van een browserbeleid of handmatig proces wordt verwijderd.

Identiteiten krijgen prioriteit in de volgende volgorde:

1. ECID opgenomen in de `identityMap`
1. ECID opgeslagen in een cookie
1. FPID opgenomen in de `identityMap`
1. FPID opgeslagen in een cookie

## Migreren naar apparaat-id&#39;s van eerste bedrijven

Als u naar het gebruiken van FPIDs van een vorige implementatie migreert, kan het moeilijk zijn om te visualiseren hoe de overgang op een laag niveau zou kunnen kijken.

Om dit proces te illustreren, overweeg een scenario dat een klant impliceert die eerder uw plaats heeft bezocht en welke invloed een migratie FPID op hoe zou hebben die klant in de oplossingen van de Adobe wordt geïdentificeerd.

![ Diagram die tonen hoe de waarden van identiteitskaart van een klant tussen bezoeken na het migreren aan FPIDs ](../assets/identity/tracking/visits.png) worden bijgewerkt

>[!IMPORTANT]
>
>Het cookie `ECID` krijgt altijd voorrang boven `FPID` .

| Bezoek | Beschrijving |
| --- | --- |
| Eerste bezoek | Stel dat u het FPID-cookie nog niet hebt ingesteld. ECID bevat in het [ koekje van AMCV ](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) zal het herkenningsteken zijn dat wordt gebruikt om de bezoeker te identificeren. |
| Tweede bezoek | De implementatie van de oplossing First-Party Device ID is gestart. De bestaande ECID is nog steeds aanwezig en blijft de primaire identificator voor bezoekersidentificatie. |
| Derde bezoek | Tussen het tweede en derde bezoek is er voldoende tijd verstreken om de ECID te verwijderen vanwege het browserbeleid. Omdat de FPID echter is ingesteld met een DNS A-record, blijft de FPID bestaan. De FPID wordt nu beschouwd als de primaire id en wordt gebruikt om de ECID te verzenden, die naar het apparaat van de eindgebruiker wordt geschreven. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de oplossingen Adobe Experience Platform en Experience Cloud. |
| Vierde bezoek | Tussen de derde en vierde keer is er voldoende tijd verstreken om de ECID te verwijderen vanwege het browserbeleid. Net als bij het vorige bezoek blijft de FPID te wijten aan de wijze waarop zij is ingesteld. Deze keer wordt dezelfde ECID gegenereerd als het vorige bezoek. De gebruiker wordt gezien door het Experience Platform en de oplossingen van het Experience Cloud zoals de zelfde gebruiker zoals het vorige bezoek. |
| Vijfde bezoek | Tussen de vierde en de vijfde keer dat het programma wordt bezocht, heeft de eindgebruiker alle cookies in de browser gewist. Er wordt een nieuwe FPID gegenereerd die wordt gebruikt om het maken van een nieuwe ECID te stimuleren. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de oplossingen Adobe Experience Platform en Experience Cloud. |

{style="table-layout:auto"}

## Veelgestelde vragen

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over apparaat-id&#39;s van andere leveranciers.

### Hoe anders zaait u een id dan eenvoudig een id genereren?

Het begrip zaaien is uniek omdat de FPID die aan Adobe Experience Cloud wordt doorgegeven, wordt omgezet in een ECID met behulp van een deterministisch algoritme. Telkens wanneer dezelfde FPID naar de Adobe Experience Platform-Edge Network wordt verzonden, wordt dezelfde ECID van de FPID verzonden.

### Wanneer moet de apparaat-id van de eerste partij worden gegenereerd?

Om potentiële bezoekersinflatie te verminderen, zou FPID moeten worden geproduceerd alvorens uw eerste verzoek te maken gebruikend SDK van het Web. Als u dit echter niet kunt doen, wordt er nog steeds een ECID gegenereerd voor die gebruiker en wordt deze gebruikt als primaire id. De gegenereerde FPID wordt pas de primaire id als de ECID niet meer aanwezig is.

### Welke methodes van de gegevensinzameling steunen eerste-partij apparaat IDs?

Momenteel steunt slechts Web SDK FPIDs.

### Worden FPIDs opgeslagen op om het even welk platform of Experience Cloud oplossingen?

Nadat de FPID is gebruikt om een ECID te verzenden, wordt deze verwijderd uit de `identityMap` en vervangen door de gegenereerde ECID. De FPID wordt niet opgeslagen in Adobe Experience Platform- of Experience Cloud-oplossingen.
