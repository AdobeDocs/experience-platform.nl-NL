---
title: Apparaat-id's van de eerste partij gebruiken in Web SDK
description: Leer hoe u FPID's (First-Party Device ID's) configureert in de Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: c7be2fff2cd94677b745e6ed095454bc46f8a37b
workflow-type: tm+mt
source-wordcount: '2173'
ht-degree: 0%

---


# Apparaat-id&#39;s van de eerste partij gebruiken in Web SDK

Het Web SDK van Adobe Experience Platform wijst [&#x200B; Adobe Experience Cloud IDs (ECIDs) &#x200B;](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=nl-NL) aan websitebezoekers toe die koekjes gebruiken om gebruikersgedrag te volgen. Als u browserbeperkingen op de levensduur van cookies wilt verhelpen, kunt u uw eigen apparaat-id&#39;s (zogenaamde FPID&#39;s) instellen en beheren.

>[!NOTE]
>
>De ondersteuning voor apparaat-id&#39;s van de eerste partij is alleen beschikbaar wanneer u gegevens naar de Experience Platform Edge Network verzendt via Web SDK.

>[!IMPORTANT]
>
>Het apparaat van de eerste partij IDs is niet compatibel met de [&#x200B; derdekoekjes &#x200B;](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) functionaliteit in SDK van het Web. U kunt apparaat-id&#39;s van de eerste fabrikant of cookies van derden gebruiken, maar niet allebei tegelijk.

## Vereisten {#prerequisites}

Voordat u begint, moet u goed op de hoogte zijn van de werking van identiteitsgegevens in de Web SDK, inclusief ECID&#39;s en `identityMap` . Zie het overzicht op [&#x200B; identiteitsgegevens in het Web SDK &#x200B;](./overview.md) voor meer informatie.

## Opmaakvereisten voor eerste apparaat-id&#39;s {#formatting-requirements}

Edge Network keurt slechts IDs goed die aan het [&#x200B; formaat UIDv4 &#x200B;](https://datatracker.ietf.org/doc/html/rfc4122) voldoen. Apparaat-id&#39;s die niet de UUIDv4-indeling hebben, worden geweigerd.

* [!DNL UUIDs] zijn uniek en willekeurig, met een verwaarloosbare kans op botsing.
* [!DNL UUIDv4] kan niet worden verzonden met IP-adressen of andere persoonlijke identificeerbare gegevens (PII).
* Bibliotheken die [!DNL UUIDs] moeten genereren, zijn beschikbaar voor elke programmeertaal.

## Stel het cookie [!DNL FPID] in met uw eigen server {#set-cookie-server}

Wanneer u een cookie instelt via uw eigen server, kunt u verschillende methoden gebruiken om te voorkomen dat het cookie wordt beperkt door het browserbeleid:

* Cookies genereren met scripttalen op de server
* Cookies instellen als reactie op een API-aanvraag die is uitgevoerd naar een subdomein of ander eindpunt op de site
* Cookies genereren met een [!DNL CMS]
* Cookies genereren met een [!DNL CDN]

Bovendien moet u het FPID-cookie altijd onder de `A` -record van uw domein instellen.

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
* [&quot;Secure&grave;](#secure)
* [` SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies die zijn ingesteld met de markering `HTTPOnly` , zijn niet toegankelijk met clientscripts. Dit betekent dat als u bij het instellen van de [!DNL FPID] -markering een `HTTPOnly` -markering instelt, u een scripttaal aan de serverzijde moet gebruiken om de cookiewaarde te lezen voor opname in de `identityMap` .

Als u ervoor kiest dat de Edge Network de waarde van het cookie [!DNL FPID] laat lezen, zorgt het instellen van de markering `HTTPOnly` ervoor dat de waarde niet toegankelijk is voor clientscripts, maar geen negatieve invloed heeft op de mogelijkheid van de Edge Network om de cookie te lezen.

>[!NOTE]
>
>Het gebruik van de markering `HTTPOnly` heeft geen invloed op het cookiebeleid dat de levensduur van cookies kan beperken. Het is echter nog steeds iets wat u moet overwegen wanneer u de waarde van de [!DNL FPID] instelt en leest.

### `Secure` {#secure}

Cookies die zijn ingesteld met het kenmerk `Secure` worden alleen naar de server verzonden met een gecodeerde aanvraag via het protocol [!DNL HTTPS] . Door deze markering te gebruiken, kunt u ervoor zorgen dat aanvallers van &#39;man in the middle&#39; de waarde van het cookie niet gemakkelijk kunnen benaderen. Het is altijd verstandig om de markering `Secure` in te stellen, als dat mogelijk is.

### `SameSite` {#same-site}

Met het kenmerk `SameSite` kunnen servers bepalen of cookies worden verzonden met aanvragen die verwijzen naar andere sites. Het kenmerk biedt enige bescherming tegen valsemunterij op andere locaties. Er zijn drie mogelijke waarden: `Strict`, `Lax` en `None` . Raadpleeg uw interne team om te bepalen welke instelling geschikt is voor uw organisatie.

Als er geen kenmerk `SameSite` is opgegeven, is de standaardinstelling voor sommige browsers nu `SameSite=Lax` .

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

![&#x200B; Diagram die tonen hoe de waarden van identiteitskaart van een klant tussen bezoeken na het migreren aan FPIDs &#x200B;](../assets/identity/tracking/visits.png) worden bijgewerkt

>[!IMPORTANT]
>
>Het cookie `ECID` krijgt altijd voorrang boven `FPID` .

| Bezoek | Beschrijving |
| --- | --- |
| Eerste bezoek | Stel dat u nog niet bent begonnen met het instellen van het cookie [!DNL FPID] . [!DNL ECID] bevat in het [&#x200B; koekje van AMCV &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=nl-NL#section-c55af54828dc4cce89f6118655d694c8) zal het herkenningsteken zijn dat wordt gebruikt om de bezoeker te identificeren. |
| Tweede bezoek | De introductie van de [!DNL FPID] -oplossing is gestart. Het bestaande [!DNL ECID] is nog steeds aanwezig en blijft de primaire id voor bezoekersidentificatie. |
| Derde bezoek | Tussen het tweede en derde bezoek is er voldoende tijd verstreken om [!DNL ECID] te verwijderen vanwege het browserbeleid. Omdat [!DNL FPID] echter is ingesteld met een [!DNL DNS] [!DNL A] -record, blijft [!DNL FPID] bestaan. [!DNL FPID] wordt nu beschouwd als de primaire id en wordt gebruikt om [!DNL ECID] te verzenden, die naar het apparaat van de eindgebruiker wordt geschreven. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de oplossingen Adobe Experience Platform en Experience Cloud. |
| Vierde bezoek | Tussen de derde en vierde keer is er voldoende tijd verstreken om [!DNL ECID] te verwijderen vanwege het browserbeleid. Net als bij het vorige bezoek blijft de [!DNL FPID] afhankelijk van de manier waarop deze is ingesteld. Deze keer wordt dezelfde [!DNL ECID] gegenereerd als het vorige bezoek. De gebruiker wordt in de Experience Platform- en Experience Cloud-oplossingen gezien als dezelfde gebruiker als het vorige bezoek. |
| Vijfde bezoek | Tussen de vierde en de vijfde keer dat het programma wordt bezocht, heeft de eindgebruiker alle cookies in de browser gewist. Er wordt een nieuwe [!DNL FPID] gegenereerd en gebruikt om het maken van een nieuwe [!DNL ECID] te versnellen. De gebruiker wordt nu beschouwd als een nieuwe bezoeker in de oplossingen Adobe Experience Platform en Experience Cloud. |

{style="table-layout:auto"}

## FPID&#39;s (First-party device ID&#39;s) gebruiken {#using-fpid}

First-party apparaat IDs ([!DNL FPIDs]) houdt bezoekers door eerste-partijkoekjes te gebruiken bij. De koekjes van de eerste partij zijn het meest efficiënt wanneer zij gebruikend een server worden geplaatst die een DNS [&#x200B; verslag van A &#x200B;](https://datatracker.ietf.org/doc/html/rfc1035) (voor IPv4) of [&#x200B; het verslag van AAAA &#x200B;](https://datatracker.ietf.org/doc/html/rfc3596) (voor IPv6), in tegenstelling tot DNS [!DNL CNAME] of [!DNL JavaScript] code gebruikt.

>[!IMPORTANT]
>
>[!DNL A] - of [!DNL AAAA] -records worden alleen ondersteund voor het instellen en bijhouden van cookies. De belangrijkste methode voor gegevensverzameling is een [!DNL DNS CNAME] . [!DNL FPIDs] worden ingesteld met een [!DNL A] - of [!DNL AAAA] -record en worden verzonden naar Adobe met een [!DNL CNAME] -record.
>
>Het [&#x200B; Adobe-Beheerde Programma van het Certificaat &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=nl-NL#adobe-managed-certificate-program) wordt ook gesteund voor de inzameling van eerstepartijgegevens.

Nadat een [!DNL FPID] -cookie is ingesteld, kan de waarde ervan worden opgehaald en naar Adobe worden verzonden wanneer gebeurtenisgegevens worden verzameld. Verzameld [!DNL FPIDs] wordt gebruikt om [!DNL ECIDs] te genereren. Dit zijn de primaire id&#39;s in Adobe Experience Cloud-toepassingen.

U kunt [!DNL FPIDs] op twee manieren gebruiken:

* **[Methode 1](#setting-cookie-datastreams)**: Vorm a [!DNL CNAME] voor uw vraag van SDK van het Web en omvat de naam van uw [!DNL FPID] koekje in uw configuratie van de gegevensstroom.
* **[Methode 2](#identityMap)**: Omvat [!DNL FPID] in de identiteitskaart. Zie de sectie verderop in dit document over [&#x200B; het gebruiken van FPIDs in `identityMap`](#identityMap) voor meer informatie.

### Methode 1: Vorm een CNAME voor uw vraag van SDK van het Web en plaats een Koekje van identiteitskaart van de Eerste Partij in uw gegevensstroom {#setting-cookie-datastreams}

Als u een [!DNL FPID] cookie vanuit uw eigen domein wilt instellen, moet u uw eigen [!DNL CNAME] (Canonical Name) voor uw Web SDK-aanroepen configureren en vervolgens de [!DNL First Party ID Cookie] -functionaliteit in uw datastreamconfiguratie inschakelen.

**Stap 1. Vorm een NAAM voor uw de plaatsingsdomein van SDK van het Web**

Met een [!DNL CNAME] -record in uw DNS kunt u een alias maken van de ene domeinnaam naar de andere. Hierdoor kunnen services van derden er uitzien alsof ze deel uitmaken van uw eigen domein, waardoor hun cookies er zo uitzien als cookies van andere bedrijven.

**Voorbeeld**

Laten we overwegen of u Web SDK wilt implementeren op uw website `mywebsite.com` . Web SDK verzendt gegevens naar de Edge Network naar het `edge.adobedc.net` -domein.

| Zonder [!DNL CNAME] | Met [!DNL CNAME] |
|---------|----------|
| <ul><li>Uw website `mywebsite.com` gebruikt het Web SDK-domein `edge.adobedc.net` om gegevens naar de Edge Network te verzenden.</li><li>Cookies die zijn ingesteld door `edge.adobedc.net` worden beschouwd als cookies van derden, omdat ze niet afkomstig zijn van uw `mywebsite.com` -domein. Afhankelijk van uw gebruikersbrowsers zijn cookies van andere leveranciers mogelijk geblokkeerd en bereiken uw gegevens niet bij de Edge Network.</li></ul> | <ul><li>U maakt een subdomein waarin u Web SDK implementeert, zoals `metrics.mywebsite.com` .</li><li>U stelt een [!DNL CNAME] -record in uw DNS-systeem zo in dat `metrics.mywebsite.com` naar `edge.adobedc.net` wijst.</li><li>Wanneer uw website cookies instelt via `metrics.mywebsite.com` , worden deze vanuit `mywebsite.com` (first-party) in plaats van `edge.adobedc.net` (third-party) naar de browser verzonden. Hierdoor is het minder waarschijnlijk dat de cookie van de eerste-partij-id wordt geblokkeerd, zodat nauwkeuriger gegevens worden verzameld.</li></ul> |

Wanneer de inzameling van de eerste-partijgegevens gebruikend [!DNL CNAME] wordt toegelaten, zullen alle koekjes voor uw domein op verzoeken worden verzonden die aan het eindpunt van de gegevensinzameling worden gemaakt.

Als u deze functionaliteit wilt gebruiken, moet u de cookie [!DNL FPID] op het hoofdniveau van uw domein instellen in plaats van op een specifiek subdomein. Als u de waarde instelt op een subdomein, wordt de waarde van het cookie niet verzonden naar de Edge Network en werkt de oplossing [!DNL FPID] niet naar behoren.

>[!IMPORTANT]
>
>Deze eigenschap vereist dat u [&#128279;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=nl-NL) toegelaten de Inzameling van Gegevens van de Eerste Partij  hebt.

**Stap 2.**&#x200B;[!UICONTROL First Party ID Cookie]&#x200B;**functionaliteit voor uw datastream inschakelen**

Nadat u uw CNAME hebt gevormd, moet u **[!UICONTROL First Party ID Cookie]** optie voor uw gegevensstroom toelaten. Dit het plaatsen vertelt Edge Network om naar een gespecificeerd koekje te verwijzen wanneer het kijken omhoog identiteitskaart van het eerste-partijapparaat, in plaats van het opzoeken van deze waarde in het [&#x200B; identiteitskaart &#x200B;](#identityMap).

Zie de [&#x200B; documentatie van de gegevensstroomconfiguratie &#x200B;](../../datastreams/configure.md#advanced-options) hoe te opstelling uw datastream.

Zie de documentatie op [&#x200B; eerste-partijkoekjes &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=nl-NL) voor meer details over hoe zij met Adobe Experience Cloud werken.

![&#x200B; beeld van Platform UI die de configuratie toont die van de gegevensstroom de Eerste het plaatsen van het Koekje van identiteitskaart van de Partij &#x200B;](../assets/first-party-id-datastreams.png) benadrukt

Wanneer u deze instelling inschakelt, moet u de naam opgeven van het cookie waarop de [!DNL FPID] moet worden opgeslagen.

>[!NOTE]
>
>Als u id&#39;s van derden gebruikt, kunt u geen syncs voor id&#39;s van derden uitvoeren. Identiteitskaart van de derde baseert syncs zich op de [!DNL Visitor ID] dienst en `UUID` die door die dienst wordt geproduceerd. Wanneer u de functie voor de eerste-id gebruikt, wordt de [!DNL ECID] gegenereerd zonder gebruik te maken van de [!DNL Visitor ID] -service, waardoor syncs van andere id&#39;s niet mogelijk is.
><br> Wanneer u eerste-partij IDs gebruikt, [&#x200B; Audience Manager &#x200B;](https://experienceleague.adobe.com/nl/docs/audience-manager) mogelijkheden die aan activering in partnerplatforms worden gericht worden niet gesteund, gegeven dat de syncs van identiteitskaart van de Partner van Audience Manager hoofdzakelijk op `UUIDs` of `DIDs` worden gebaseerd. De [!DNL ECID] die is afgeleid van een id van een eerste partij is niet gekoppeld aan een `UUID` , zodat deze niet-adresseerbaar is.

## Methode 2: FPID&#39;s gebruiken in `identityMap` {#identityMap}

Als alternatief voor het opslaan van de [!DNL FPID] in uw eigen cookie, kunt u de [!DNL FPID] naar de Edge Network verzenden via de identiteitskaart.

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

Als de [!DNL FPID] is opgenomen in een cookie die door de Edge Network wordt gelezen wanneer gegevensverzameling van de eerste partij is ingeschakeld, moet u alleen de geverifieerde [!DNL CRM ID] vastleggen:

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

De door de Edge Network in dit geval geretourneerde foutreactie zou vergelijkbaar zijn met het volgende:

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

## Veelgestelde vragen {#faq}

Hieronder volgt een lijst met antwoorden op veelgestelde vragen over apparaat-id&#39;s van andere leveranciers.

### Hoe anders zaait u een id dan eenvoudig een id genereren?

Het concept van zaaien is uniek in die zin dat de [!DNL FPID] die aan Adobe Experience Cloud wordt doorgegeven, wordt omgezet in een [!DNL ECID] met behulp van een deterministisch algoritme. Telkens wanneer dezelfde [!DNL FPID] naar de Edge Network wordt verzonden, wordt dezelfde [!DNL ECID] verzonden vanuit de [!DNL FPID] .

### Wanneer moet de apparaat-id van de eerste partij worden gegenereerd?

Om potentiële bezoekersinflatie te verminderen, zou [!DNL FPID] moeten worden geproduceerd alvorens uw eerste verzoek te maken gebruikend het Web SDK. Als u dit echter niet kunt doen, wordt nog steeds een [!DNL ECID] gegenereerd voor die gebruiker en wordt deze gebruikt als primaire id. De gegenereerde [!DNL FPID] wordt pas de primaire id wanneer [!DNL ECID] niet meer aanwezig is.

### Welke methodes van de gegevensinzameling steunen eerste-partij apparaat IDs?

Alleen Web SDK biedt momenteel ondersteuning voor apparaat-id&#39;s van andere leveranciers.

### Worden de eerste-partijapparaat IDs opgeslagen op om het even welke oplossing van het Platform of van Experience Cloud?

Nadat [!DNL FPID] is gebruikt om een [!DNL ECID] te verzenden, wordt het verwijderd uit de `identityMap` en vervangen door de [!DNL ECID] die is gegenereerd. [!DNL FPID] wordt niet opgeslagen in Adobe Experience Platform- of Experience Cloud-oplossingen.
