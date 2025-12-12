---
title: Ondersteuning voor Content Security Policy (CSP)
description: Leer hoe u met CSP-beperkingen (Content Security Policy) omgaat wanneer u uw website integreert met tags in Adobe Experience Platform.
exl-id: 9232961e-bc15-47e1-aa6d-3eb9b865ac23
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1031'
ht-degree: 0%

---

# Ondersteuning voor Content Security Policy (CSP)

Een inhoudsbeveiligingsbeleid (CSP) is een beveiligingsfunctie waarmee XSS (cross-site scripting aanvallen) wordt voorkomen. Dit gebeurt wanneer browser in het runnen van kwaadwillige inhoud wordt gesleept die uit een vertrouwde op bron schijnt te komen maar echt van elders komt. CSPs staat browser (namens de gebruiker) toe om te verifiëren dat het manuscript eigenlijk uit een vertrouwde op bron komt.

CSP&#39;s worden geïmplementeerd door een `Content-Security-Policy` HTTP-header toe te voegen aan uw serverreacties of door een geconfigureerd `<meta>` -element toe te voegen in de sectie `<head>` van uw HTML-bestanden.

>[!NOTE]
>
> Voor meer gedetailleerde informatie over CSP, verwijs naar de [ MDN Webdocumenten ](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP).

Tags in Adobe Experience Platform zijn een systeem voor tagbeheer dat is ontworpen om scripts op uw website dynamisch te laden. Een standaard CSP blokkeert deze dynamisch geladen manuscripten toe te schrijven aan potentiële veiligheidsproblemen. In dit document wordt uitgelegd hoe u uw CSP zo configureert dat dynamisch geladen scripts van tags worden toegestaan.

Als u labels wilt gebruiken voor uw CSP, moeten er twee belangrijke uitdagingen worden overwonnen:

* **de bron voor uw markeringsbibliotheek moet worden vertrouwd.** Als niet aan deze voorwaarde wordt voldaan, worden de tagbibliotheek en andere vereiste JavaScript-bestanden geblokkeerd door de browser en worden deze niet op de pagina geladen.
* **Inline manuscripten moeten worden toegestaan.** Als niet aan deze voorwaarde wordt voldaan, worden de handelingen van de de regelregel van de Code van de Douane geblokkeerd op de pagina en zullen niet behoorlijk uitvoeren.

De verhoogde veiligheid vereist een verhoogde hoeveelheid werk namens de tevreden schepper. Als u tags wilt gebruiken en een CDV wilt hebben, moet u beide problemen verhelpen zonder andere scripts onjuist als veilig te markeren. In de rest van dit document wordt uitgelegd hoe u dit kunt bereiken.

## Tags toevoegen als vertrouwde bron

Wanneer u een CSP gebruikt, moet u vertrouwde domeinen opnemen in de waarde van de header `Content-Security-Policy` . De waarde die u moet opgeven voor tags, is afhankelijk van het type host dat u gebruikt.

### Zelfhosting

Als u [ zelf-gastheer ](../publishing/hosts/self-hosting-libraries.md) uw bibliotheek bent, dan is de bron voor uw bouwstijl waarschijnlijk uw eigen domein. U kunt specificeren dat het gastheerdomein een veilige bron door de volgende configuratie te gebruiken is:

**HTTP- kopbal**

```http
Content-Security-Policy: script-src 'self'
```

**HTML `<meta>` markering**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self'">
```

### Door Adobe beheerde hosting

Als u een [ Adobe-Beheerde gastheer ](../publishing/hosts/managed-by-adobe-host.md) gebruikt, dan wordt uw bouwstijl gehandhaafd op `assets.adobedtm.com`. U moet `self` als een veilig domein opgeven zodat u geen scripts afbreekt die u al laadt, maar u moet `assets.adobedtm.com` ook als veilig weergeven of uw tagbibliotheek wordt niet op de pagina geladen. In dit geval, zou u de volgende configuratie moeten gebruiken:

**HTTP- kopbal**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com
```

**HTML `<meta>` markering**


Er is een zeer belangrijke voorwaarde: U moet de markeringsbibliotheek [ asynchroon ](./asynchronous-deployment.md) laden. Dit werkt niet met een synchrone lading van de markeringsbibliotheek (wat in consolefouten en regels resulteert niet behoorlijk).

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com">
```

U moet `self` opgeven als een veilig domein, zodat alle scripts die u al laadt, blijven werken, maar u moet `assets.adobedtm.com` ook als veilig weergeven of de build van de bibliotheek niet op de pagina laden.

## Inline-scripts

CSP maakt gealigneerde manuscripten door gebrek onbruikbaar, en daarom moet manueel worden gevormd om hen toe te staan. U hebt twee opties om inlinescripts toe te staan:

* [ toestaan door nonce ](#nonce) (goede veiligheid)
* [ staat alle gealigneerde manuscripten ](#unsafe-inline) (minst veilig) toe

>[!NOTE]
>
>De CSP-specificatie bevat details voor een derde optie met behulp van hashes, maar deze aanpak is niet mogelijk voor systemen voor tagbeheer zoals tags. Voor meer informatie over de beperkingen om haken met markeringen in Experience Platform te gebruiken, zie de [ gids van de Integriteit Subresource (SRI) ](./sri.md).

### Eenmaal toestaan {#nonce}

Deze methode omvat het genereren van een cryptografische id en het toevoegen van deze code aan uw CSP en elk inline script op uw site. Wanneer de browser een instructie ontvangt om een inline script met een nonce te laden, vergelijkt de browser de nonce-waarde met wat zich in de CSP-header bevindt. Als het aanpast, wordt het manuscript geladen. Deze nonce moet worden gewijzigd bij elke nieuwe pagina die wordt geladen.

>[!IMPORTANT]
>
>Als u deze methode wilt gebruiken, moet u de build asynchroon laden. Dit werkt niet wanneer het laden van de bouwstijl synchroon, wat in consolefouten en regels resulteert niet behoorlijk uitvoeren. Zie de gids op [ asynchrone plaatsing ](./asynchronous-deployment.md) voor meer informatie.

De voorbeelden tonen hieronder hoe u uw nonce aan de CSP configuratie voor een Adobe-Beheerde gastheer kunt toevoegen. Als u zelfhosting gebruikt, kunt u `assets.adobedtm.com` uitsluiten.

**HTTP- kopbal**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'
```

**HTML `<meta>` markering**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'nonce-2726c7f26c'">
```

Wanneer u de header of HTML-tag hebt geconfigureerd, moet u de tag aangeven waar de nonce moet worden gevonden bij het laden van een inline script. Als u wilt dat een tag de nonce gebruikt bij het laden van het script, moet u:

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

**HTTP- kopbal**

```http
Content-Security-Policy: script-src 'self' 'unsafe-inline'
```

**HTML `<meta>` markering**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' 'unsafe-inline'">
```

#### Door Adobe beheerde hosting

Gebruik de volgende configuraties als u hosting door Adobe gebruikt:

**HTTP- kopbal**

```http
Content-Security-Policy: script-src 'self' assets.adobedtm.com 'unsafe-inline'
```

**HTML `<meta>` markering**

```html
<meta http-equiv="Content-Security-Policy" content="script-src 'self' assets.adobedtm.com 'unsafe-inline'">
```

## Volgende stappen

Door dit document te lezen, moet u nu begrijpen hoe u de CSP-header zo kunt configureren dat het bibliotheekbestand van de tag en inlinescripts worden geaccepteerd.

Als extra veiligheidsmaatregel, kunt u ook verkiezen om de Integriteit Subresource (SRI) te gebruiken om opgehaalde bibliotheekbouwt te bevestigen. Deze functie heeft echter enkele belangrijke beperkingen bij gebruik in systemen voor tagbeheer, zoals tags. Zie de gids op [ verenigbaarheid SRI in Experience Platform ](./sri.md) voor meer informatie.
