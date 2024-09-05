---
title: Eerste-partij apparaat IDs in Web SDK
description: Leer hoe u FPID's (First-party device ID's) configureert in de Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 1cb38e3eaa83f2ad0e7dffef185d5edaf5e6c38c
workflow-type: tm+mt
source-wordcount: '1900'
ht-degree: 0%

---


# Eerste-partij apparaat IDs in Web SDK

SDK van het Web van Adobe Experience Platform wijst [ Adobe Experience Cloud IDs (ECIDs) ](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html) aan websitebezoekers door koekjes te gebruiken toe, om gebruikersgedrag te volgen. Als u browserbeperkingen voor de levensduur van cookies wilt compenseren, kunt u uw eigen apparaat-id&#39;s instellen en beheren. Deze worden bedoeld als eerste-partij apparaat IDs (`FPIDs`).

>[!NOTE]
>
>De steun van eerste-partijapparaatidentiteitskaart is slechts beschikbaar wanneer het verzenden van gegevens naar de Edge Network van het Experience Platform via het Web SDK.

>[!IMPORTANT]
>
>Eerste-partij apparaat IDs is niet compatibel met de [ functionaliteit van derdekoekjes ](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) in Web SDK.
>U kunt apparaat-id&#39;s van andere leveranciers gebruiken of cookies van andere leveranciers, maar u kunt beide functies niet tegelijkertijd gebruiken.

Dit document verklaart hoe te om eerste-partijapparaat IDs voor uw implementatie van SDK van het Web te vormen.

## Vereisten

Deze gids veronderstelt u vertrouwd met bent hoe de identiteitsgegevens voor het Web SDK van het Platform, met inbegrip van de rol van ECIDs en `identityMap` werken. Zie het overzicht op [ identiteitsgegevens in het Web SDK ](./overview.md) voor meer informatie.

## FPID&#39;s (First-party device ID&#39;s) gebruiken {#using-fpid}

First-party apparaat IDs ([!DNL FPIDs]) houdt bezoekers door eerste-partijkoekjes te gebruiken bij. De koekjes van de eerste partij zijn het meest efficiënt wanneer zij gebruikend een server worden geplaatst die een DNS [ verslag van A ](https://datatracker.ietf.org/doc/html/rfc1035) (voor IPv4) of [ het verslag van AAAA ](https://datatracker.ietf.org/doc/html/rfc3596) (voor IPv6), in tegenstelling tot DNS [!DNL CNAME] of [!DNL JavaScript] code gebruikt.

>[!IMPORTANT]
>
>[!DNL A] - of [!DNL AAAA] -records worden alleen ondersteund voor het instellen en bijhouden van cookies. De belangrijkste methode voor gegevensverzameling is een [!DNL DNS] [!DNL CNAME] . Met andere woorden, [!DNL FPIDs] wordt ingesteld met een [!DNL A] record of [!DNL AAAA] record en wordt vervolgens naar de Adobe verzonden met een [!DNL CNAME] -record.
>
>Het [ Adobe-Beheerde Programma van het Certificaat ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) wordt ook nog gesteund voor de inzameling van eerstepartijgegevens.

Nadat een [!DNL FPID] -cookie is ingesteld, kan de waarde ervan worden opgehaald en naar de Adobe worden verzonden wanneer gebeurtenisgegevens worden verzameld. Verzameld [!DNL FPIDs] wordt gebruikt als zaad om [!DNL ECIDs] te genereren. Dit blijven de primaire id&#39;s in Adobe Experience Cloud-toepassingen.

Als u een [!DNL FPID] voor een websitebezoeker naar de Edge Network wilt verzenden, moet u de [!DNL FPID] in de `identityMap` voor die bezoeker opnemen. Zie de sectie verderop in dit document over [ het gebruiken van FPIDs in `identityMap`](#identityMap) voor meer informatie.

### Opmaakvereisten voor eerste apparaat-id&#39;s {#formatting-requirements}

De Edge Network keurt slechts [!DNL IDs] goed die aan het [ formaat UIDv4 ](https://datatracker.ietf.org/doc/html/rfc4122) voldoen. Apparaat-id&#39;s die niet de [!DNL UUIDv4] -indeling hebben, worden geweigerd.

Het genereren van een [!DNL UUID] resulteert bijna altijd in een unieke, willekeurige id, waarbij de kans dat een botsing optreedt verwaarloosbaar is. [!DNL UUIDv4] kan niet worden verzonden gebruikend IP adressen of een andere persoonlijke identificeerbare informatie ([!DNL PII]). [!DNL UUIDs] zijn alomtegenwoordig en bibliotheken zijn beschikbaar voor vrijwel elke programmeertaal om deze te genereren.

## Het plaatsen van een eerstepartijkoekje van identiteitskaart in de UI van Gegevensstromen {#setting-cookie-datastreams}

U kunt een cookienaam opgeven in de gebruikersinterface van Datastreams, waar [!DNL FPID] kan verblijven, eerder dan het moeten de koekjeswaarde lezen en [!DNL FPID] in de identiteitskaart omvatten.

>[!IMPORTANT]
>
>Deze eigenschap vereist dat u ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) toegelaten de Inzameling van Gegevens van de Eerste Partij [ hebt.

Zie de [ documentatie van gegevensstromen ](../../datastreams/configure.md) voor gedetailleerde informatie over hoe te om een gegevensstroom te vormen.

Schakel de optie **[!UICONTROL First Party ID Cookie]** in wanneer u de gegevensstroom configureert. Dit het plaatsen vertelt de Edge Network om naar een gespecificeerd koekje te verwijzen wanneer het opzoeken van eerste-partijapparaat identiteitskaart, eerder dan het opzoeken van deze waarde in het [ identiteitskaart ](#identityMap).

Zie de documentatie op [ eerste-partijkoekjes ](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html) voor meer details over hoe zij met Adobe Experience Cloud werken.

![ beeld van Platform UI die de configuratie toont die van de gegevensstroom de Eerste het plaatsen van het Koekje van identiteitskaart van de Partij ](../assets/first-party-id-datastreams.png) benadrukt

Als u deze instelling inschakelt, moet u de naam opgeven van het cookie waarop de id moet worden opgeslagen.

Als u id&#39;s van derden gebruikt, kunt u geen syncs voor id&#39;s van derden uitvoeren. Identiteitskaart van de derde baseert syncs zich op de [!DNL Visitor ID] dienst en `UUID` die door die dienst wordt geproduceerd. Wanneer u de functie voor de eerste-id gebruikt, wordt de [!DNL ECID] gegenereerd zonder gebruik te maken van de [!DNL Visitor ID] -service, waardoor syncs van andere id&#39;s niet mogelijk is.

Wanneer u eerste-partij IDs gebruikt, [ Audience Manager ](https://experienceleague.adobe.com/en/docs/audience-manager) mogelijkheden die aan activering in partnerplatforms worden gericht worden niet gesteund, gegeven dat de syncs van identiteitskaart van de Partner van de Audience Manager meestal op `UUIDs` of `DIDs` worden gebaseerd. De [!DNL ECID] die is afgeleid van een id van een eerste partij is niet gekoppeld aan een `UUID` , zodat deze niet-adresseerbaar is.

## Een cookie instellen met uw eigen server {#set-cookie-server}

Wanneer u een cookie instelt met een server die u bezit, kunt u verschillende methoden gebruiken om te voorkomen dat het cookie wordt beperkt door het browserbeleid:

* Cookies genereren met scripttalen op de server
* Cookies instellen als reactie op een API-aanvraag die is uitgevoerd naar een subdomein of ander eindpunt op de site
* Cookies genereren met een [!DNL CMS]
* Cookies genereren met een [!DNL CDN]

>[!IMPORTANT]
>
>Cookies die zijn ingesteld met de methode JavaScript `document.cookie` worden bijna nooit beschermd tegen browserbeleid dat de duur van cookies beperkt.

### Wanneer stelt u het cookie in {#when-to-set-cookie}

Het cookie [!DNL FPID] moet idealiter worden ingesteld voordat aanvragen bij de Edge Network worden ingediend. In situaties waarin dat niet mogelijk is, wordt een [!DNL ECID] echter nog steeds gegenereerd met bestaande methoden en fungeert het als de primaire id zolang het cookie bestaat.

Ervan uitgaande dat [!DNL ECID] uiteindelijk wordt beïnvloed door een beleid voor het verwijderen van browsers, maar [!DNL FPID] niet, wordt [!DNL FPID] de primaire id bij het volgende bezoek en wordt deze gebruikt om [!DNL ECID] bij elk volgend bezoek te begeleiden.

### De vervaldatum van de cookie instellen {#set-expiration}

Het instellen van de vervaldatum van een cookie moet zorgvuldig worden overwogen wanneer u de functie [!DNL FPID] implementeert. Wanneer u hierover beslist, moet u rekening houden met de landen of regio&#39;s waarin uw organisatie werkt, samen met de wetten en het beleid in elk van die regio&#39;s.

Als onderdeel van dit besluit wilt u mogelijk een beleid voor het instellen van cookies in het hele bedrijf toepassen of een beleid dat per landinstelling verschilt.

Ongeacht de instelling die u kiest voor de aanvankelijke vervaldatum van een cookie, moet u logica opnemen die de vervaldatum van de cookie verlengt telkens wanneer een nieuw bezoek aan de site plaatsvindt.

## Gevolgen van cookie-vlaggen {#cookie-flag-impact}

Er zijn verschillende cookiemarkeringen die van invloed zijn op de manier waarop cookies in verschillende browsers worden verwerkt:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Secure`](#secure)
* [` SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies die zijn ingesteld met de markering `HTTPOnly` , zijn niet toegankelijk met clientscripts. Dit betekent dat als u bij het instellen van de [!DNL FPID] -markering een `HTTPOnly` -markering instelt, u een scripttaal aan de serverzijde moet gebruiken om de cookiewaarde te lezen voor opname in de `identityMap` .

Als u ervoor kiest dat de Edge Network de waarde van het cookie [!DNL FPID] leest, zorgt het instellen van de markering `HTTPOnly` ervoor dat de waarde niet toegankelijk is voor clientscripts, maar geen negatieve invloed heeft op de mogelijkheid van de Edge Network om de cookie te lezen.

>[!NOTE]
>
>Het gebruik van de markering `HTTPOnly` heeft geen invloed op het cookiebeleid dat de levensduur van cookies kan beperken. Het is echter nog steeds iets wat u moet overwegen wanneer u de waarde van de [!DNL FPID] instelt en leest.

### `Secure` {#secure}

Cookies die zijn ingesteld met het kenmerk `Secure` worden alleen naar de server verzonden met een gecodeerde aanvraag via het protocol [!DNL HTTPS] . Door deze markering te gebruiken, kunt u ervoor zorgen dat aanvallers van &#39;man in the middle&#39; de waarde van het cookie niet gemakkelijk kunnen benaderen. Het is altijd verstandig om de markering `Secure` in te stellen, als dat mogelijk is.

### `SameSite` {#same-site}

Met het kenmerk `SameSite` kunnen servers bepalen of cookies worden verzonden met aanvragen die verwijzen naar andere sites. Het kenmerk biedt enige bescherming tegen valsemunterij op andere locaties. Er zijn drie mogelijke waarden: `Strict`, `Lax` en `None` . Raadpleeg uw interne team om te bepalen welke instelling geschikt is voor uw organisatie.

Als er geen kenmerk `SameSite` is opgegeven, is de standaardinstelling voor sommige browsers nu `SameSite=Lax` .

## FPID&#39;s gebruiken in `identityMap` {#identityMap}

Hieronder ziet u een voorbeeld van hoe u een [!DNL FPID] -element in de `identityMap` instelt:

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

Net als bij andere identiteitstypen kunt u de [!DNL FPID] opnemen met andere identiteiten in `identityMap` . Hieronder ziet u een voorbeeld van de lus [!DNL FPID] die is opgenomen met een geverifieerde [!DNL CRM ID] :

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

Als [!DNL FPID] in een koekje bevat dat door de Edge Network wordt gelezen wanneer de inzameling van de eerste-partijgegevens wordt toegelaten, zou u slechts authentiek moeten vangen [!DNL CRM ID]:

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

De volgende `identityMap` resulteert in een foutreactie van de Edge Network omdat deze de `primary` -indicator voor de [!DNL FPID] mist. Ten minste een van de id&#39;s in `identityMap` moet zijn gemarkeerd als `primary` .

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

## ID-hiërarchie {#id-hierarchy}

Wanneer zowel een [!DNL ECID] als een [!DNL FPID] aanwezig zijn, krijgt [!DNL ECID] prioriteit bij het identificeren van de gebruiker. Dit zorgt ervoor dat wanneer er een bestaande [!DNL ECID] aanwezig is in de cookie-opslag van de browser, dit de primaire id blijft en dat het aantal bestaande bezoekers niet kan worden beïnvloed. Voor bestaande gebruikers wordt [!DNL FPID] pas de primaire identiteit nadat [!DNL ECID] is verlopen of is verwijderd als gevolg van een browserbeleid of handmatig proces.

Identiteiten krijgen prioriteit in de volgende volgorde:

1. [!DNL ECID] opgenomen in de `identityMap`
1. [!DNL ECID] opgeslagen in een cookie
1. [!DNL FPID] opgenomen in de `identityMap`
1. [!DNL FPID] opgeslagen in een cookie

## Migreren naar apparaat-id&#39;s van eerste bedrijven {#migrating-to-fpid}

Als u van een vorige implementatie naar apparaat-id&#39;s van de eerste partij migreert, kan het moeilijk zijn om te visualiseren hoe de overgang er op een laag niveau uitziet.

Om dit proces te illustreren, kunt u een scenario overwegen waarbij een klant betrokken is die eerder uw site heeft bezocht en welke invloed een [!DNL FPID] -migratie zou hebben op de manier waarop die klant wordt geïdentificeerd in Adobe-oplossingen.

![ Diagram die tonen hoe de waarden van identiteitskaart van een klant tussen bezoeken na het migreren aan FPIDs ](../assets/identity/tracking/visits.png) worden bijgewerkt

>[!IMPORTANT]
>
>Het cookie `ECID` krijgt altijd voorrang boven `FPID` .

| Bezoek | Beschrijving |
| --- | --- |
| Eerste bezoek | Stel dat u nog niet bent begonnen met het instellen van het cookie [!DNL FPID] . [!DNL ECID] bevat in het [ koekje van AMCV ](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) zal het herkenningsteken zijn dat wordt gebruikt om de bezoeker te identificeren. |
| Tweede bezoek | De introductie van de [!DNL FPID] -oplossing is gestart. Het bestaande [!DNL ECID] is nog steeds aanwezig en blijft de primaire id voor bezoekersidentificatie. |
| Derde bezoek | Tussen het tweede en derde bezoek is er voldoende tijd verstreken om [!DNL ECID] te verwijderen vanwege het browserbeleid. Omdat [!DNL FPID] echter is ingesteld met een [!DNL DNS] [!DNL A] -record, blijft [!DNL FPID] bestaan. [!DNL FPID] wordt nu beschouwd als de primaire id en wordt gebruikt om [!DNL ECID] te verzenden, die naar het apparaat van de eindgebruiker wordt geschreven. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de oplossingen Adobe Experience Platform en Experience Cloud. |
| Vierde bezoek | Tussen de derde en vierde keer is er voldoende tijd verstreken om [!DNL ECID] te verwijderen vanwege het browserbeleid. Net als bij het vorige bezoek blijft de [!DNL FPID] afhankelijk van de manier waarop deze is ingesteld. Deze keer wordt dezelfde [!DNL ECID] gegenereerd als het vorige bezoek. De gebruiker wordt gezien door het Experience Platform en de oplossingen van het Experience Cloud zoals de zelfde gebruiker zoals het vorige bezoek. |
| Vijfde bezoek | Tussen de vierde en de vijfde keer dat het programma wordt bezocht, heeft de eindgebruiker alle cookies in de browser gewist. Er wordt een nieuwe [!DNL FPID] gegenereerd en gebruikt om het maken van een nieuwe [!DNL ECID] te versnellen. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de oplossingen Adobe Experience Platform en Experience Cloud. |

{style="table-layout:auto"}

## Veelgestelde vragen {#faq}

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over apparaat-id&#39;s van andere leveranciers.

### Hoe anders zaait u een id dan eenvoudig een id genereren?

Het concept van zaaien is uniek in die zin dat de [!DNL FPID] die aan Adobe Experience Cloud wordt doorgegeven, wordt omgezet in een [!DNL ECID] met behulp van een deterministisch algoritme. Telkens wanneer dezelfde [!DNL FPID] naar de Edge Network wordt verzonden, wordt dezelfde [!DNL ECID] verzonden van de [!DNL FPID] .

### Wanneer moet de apparaat-id van de eerste partij worden gegenereerd?

Om potentiële bezoekersinflatie te verminderen, zou [!DNL FPID] moeten worden geproduceerd alvorens uw eerste verzoek te maken gebruikend SDK van het Web. Als u dit echter niet kunt doen, wordt nog steeds een [!DNL ECID] gegenereerd voor die gebruiker en wordt deze gebruikt als primaire id. De gegenereerde [!DNL FPID] wordt pas de primaire id wanneer [!DNL ECID] niet meer aanwezig is.

### Welke methodes van de gegevensinzameling steunen eerste-partij apparaat IDs?

Momenteel steunt slechts Web SDK eerste-partij apparaat IDs.

### Worden apparaat-id&#39;s van de eerste partij opgeslagen op een platform- of Experience Cloud-oplossing?

Nadat [!DNL FPID] is gebruikt om een [!DNL ECID] te verzenden, wordt het verwijderd uit de `identityMap` en vervangen door de [!DNL ECID] die is gegenereerd. [!DNL FPID] wordt niet opgeslagen in Adobe Experience Platform- of Experience Cloud-oplossingen.
