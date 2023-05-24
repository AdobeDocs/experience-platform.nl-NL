---
title: Ondersteuning voor Content Security Policy (CSP)
description: Leer hoe u met CSP-beperkingen (Content Security Policy) omgaat wanneer u uw website integreert met tags in Adobe Experience Platform.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: a8b0282004dd57096dfc63a9adb82ad70d37495d
workflow-type: tm+mt
source-wordcount: '1080'
ht-degree: 0%

---

# Ondersteuning voor Content Security Policy (CSP)

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Een inhoudsbeveiligingsbeleid (CSP) is een beveiligingsfunctie waarmee XSS (cross-site scripting aanvallen) wordt voorkomen. Dit gebeurt wanneer browser in het runnen van kwaadwillige inhoud wordt gesleept die uit een vertrouwde op bron schijnt te komen maar echt van elders komt. CSPs staat browser (namens de gebruiker) toe om te verifiëren dat het manuscript eigenlijk uit een vertrouwde op bron komt.

CSP&#39;s worden geïmplementeerd door een `Content-Security-Policy` HTTP-header naar de reacties van de server of door een geconfigureerde header toe te voegen `<meta>` in het `<head>` van uw HTML-bestanden.

>[!NOTE]
>
> Voor meer gedetailleerde informatie over CDV raadpleegt u de [MDN-webdocumenten](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

Tags in Adobe Experience Platform zijn een systeem voor tagbeheer dat is ontworpen om scripts op uw website dynamisch te laden. Een standaard CSP blokkeert deze dynamisch geladen manuscripten toe te schrijven aan potentiële veiligheidsproblemen. In dit document wordt uitgelegd hoe u uw CSP zo configureert dat dynamisch geladen scripts van tags worden toegestaan.

Als u labels wilt gebruiken voor uw CSP, moeten er twee belangrijke uitdagingen worden overwonnen:

* **De bron voor uw tagbibliotheek moet worden vertrouwd.** Als niet aan deze voorwaarde wordt voldaan, worden de tagbibliotheek en andere vereiste JavaScript-bestanden geblokkeerd door de browser en worden deze niet op de pagina geladen.
* **Inlinescripts moeten zijn toegestaan.** Als niet aan deze voorwaarde wordt voldaan, worden de de regelacties van de Code van de Douane geblokkeerd op de pagina en zullen niet behoorlijk uitvoeren.

De verhoogde veiligheid vereist een verhoogde hoeveelheid werk namens de tevreden schepper. Als u tags wilt gebruiken en een CDV wilt hebben, moet u beide problemen verhelpen zonder andere scripts onjuist als veilig te markeren. In de rest van dit document wordt uitgelegd hoe u dit kunt bereiken.

## Tags toevoegen als vertrouwde bron

Wanneer u een CSP gebruikt, moet u vertrouwde domeinen opnemen in de waarde van de `Content-Security-Policy` header. De waarde die u moet opgeven voor tags, is afhankelijk van het type host dat u gebruikt.

### Zelfhosting

Als u [zelfhosting](../publishing/hosts/self-hosting-libraries.md) uw bibliotheek, dan is de bron voor uw bouwstijl waarschijnlijk uw eigen domein. U kunt specificeren dat het gastheerdomein een veilige bron door de volgende configuratie te gebruiken is:

**HTTP-header**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Door Adobe beheerde hosting

Als u een [Door Adobe beheerde host](../publishing/hosts/managed-by-adobe-host.md), dan blijft uw build behouden op `assets.adobedtm.com`. U moet `self` als een veilig domein zodat breekt u geen manuscripten die u reeds laadt, maar u ook nodig `assets.adobedtm.com` om als veilig te worden vermeld of uw tagbibliotheek wordt niet op de pagina geladen. In dit geval, zou u de volgende configuratie moeten gebruiken:

**HTTP-header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` tag**


Er is een zeer belangrijke voorwaarde: U moet de tagbibliotheek laden [asynchroon](./asynchronous-deployment.md). Dit werkt niet met een synchrone lading van de markeringsbibliotheek (wat in consolefouten en regels resulteert niet behoorlijk).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

U moet `self` als een veilig domein, zodat alle scripts die u al laadt, blijven werken, maar ook `assets.adobedtm.com` om als veilig te worden vermeld of uw bibliotheekbouwstijl zal niet laden op de pagina.

## Inline-scripts

CSP maakt gealigneerde manuscripten door gebrek onbruikbaar, en daarom moet manueel worden gevormd om hen toe te staan. U hebt twee opties om inlinescripts toe te staan:

* [Eenmaal toestaan](#nonce) (goede veiligheid)
* [Alle inline scripts toestaan](#unsafe-inline) (minst veilig)

>[!NOTE]
>
>De CSP-specificatie bevat details voor een derde optie met behulp van hashes, maar deze aanpak is niet mogelijk voor systemen voor tagbeheer zoals tags. Raadpleeg voor meer informatie over de beperkingen van het gebruik van hashes met tags in Platform de klasse [Handleiding Subresource Integrity (SRI)](./sri.md).

### Eenmaal toestaan {#nonce}

Deze methode omvat het genereren van een cryptografische id en het toevoegen ervan aan uw CSP en elk inline script op uw site. Wanneer de browser een instructie ontvangt om een inline script met een nonce te laden, vergelijkt de browser de nonce-waarde met wat zich in de CSP-header bevindt. Als het aanpast, wordt het manuscript geladen. Deze nonce moet worden gewijzigd bij elke nieuwe pagina die wordt geladen.

>[!IMPORTANT]
>
>Als u deze methode wilt gebruiken, moet u de build asynchroon laden. Dit werkt niet wanneer het laden van de bouwstijl synchroon, wat in consolefouten en regels resulteert niet behoorlijk uitvoeren. Zie de handleiding op [asynchrone implementatie](./asynchronous-deployment.md) voor meer informatie .

De voorbeelden tonen hieronder hoe u uw nonce aan de CSP configuratie voor een Adobe-beheerde gastheer kunt toevoegen. Als u zelfhosting gebruikt, kunt u `assets.adobedtm.com`.

**HTTP-header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Nadat u de koptekst- of HTML-tag hebt geconfigureerd, moet u de tag aangeven waar de nonce moet worden gevonden tijdens het laden van een inline-script. Als u wilt dat een tag de nonce gebruikt bij het laden van het script, moet u:

1. Creeer een gegevenselement dat verwijzingen waar nonce binnen uw gegevenslaag wordt gevestigd.
1. Vorm de Uitbreiding van de Kern en specificeer welk gegevenselement u gebruikte.
1. Publiceer uw gegevenselement en de veranderingen van de Uitbreiding van de Kern.

>[!NOTE]
>
>Het bovenstaande proces handelt alleen het laden van uw aangepaste code af, niet wat die aangepaste code doet. Als een inlinescript douanecode bevat die niet volgzaam met uw CSP is, neemt CSP belangrijkheid. Als u bijvoorbeeld aangepaste code gebruikt om een inline-script te laden door het aan de DOM toe te voegen, kan de tag de nonce niet correct toevoegen, zodat bepaalde aangepaste code niet werkt zoals u had verwacht.

### Alle inline scripts toestaan {#unsafe-inline}

Als het gebruiken van nonces niet voor u werkt, kunt u uw CSP vormen om alle gealigneerde manuscripten toe te staan. Dit is de minst veilige optie, maar is ook gemakkelijker uit te voeren en te handhaven.

In de onderstaande voorbeelden ziet u hoe u alle inlinescripts in de CSP-header kunt toestaan.

#### Zelfhosting

Gebruik de volgende configuraties als u zelfhosting gebruikt:

**HTTP-header**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Door Adobe beheerde hosting

Gebruik de volgende configuraties als u Adobe-beheerde hosting gebruikt:

**HTTP-header**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>` tag**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe u de CSP-header zo kunt configureren dat het bibliotheekbestand van de tag en inlinescripts worden geaccepteerd.

Als extra veiligheidsmaatregel, kunt u ook verkiezen om de Integriteit Subresource (SRI) te gebruiken om opgehaalde bibliotheekbouwt te bevestigen. Deze functie heeft echter enkele belangrijke beperkingen bij gebruik in systemen voor tagbeheer, zoals tags. Zie de handleiding op [SRI-compatibiliteit in Platform](./sri.md) voor meer informatie .
