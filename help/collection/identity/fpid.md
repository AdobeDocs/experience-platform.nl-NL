---
title: Apparaat-id's van de eerste partij gebruiken in gegevensverzameling
description: Configureer FPID's (First-Party Device ID's) voor een duurzame identiteit in webimplementaties die gegevens naar de Edge Network verzenden.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Apparaat-id&#39;s van de eerste partij gebruiken in gegevensverzameling

De Experience Platform Edge Network gebruikt Experience Cloud-id&#39;s (ECID&#39;s) om websitebezoekers te identificeren. Als u de duurzaamheid van uw identiteit wilt verbeteren voor eigenschapseigenschappen, kunt u uw eigen apparaat-id&#39;s (zogenaamde FPID&#39;s) instellen en beheren. De Edge Network gebruikt de FPID om de ECID die Adobe-oplossingen gebruiken, uit te proberen.

Op deze pagina wordt ervan uitgegaan dat u bekend bent met ECID&#39;s en `identityMap` . Zie [&#x200B; Identiteit in de Inzameling van Gegevens &#x200B;](./overview.md) voor meer informatie.

## Wanneer FPID&#39;s gebruiken {#when-to-use}

Browserbeperkingen kunnen de levensduur van cookies die Adobe gebruikt om terugkerende bezoekers te herkennen, verkorten. Als u duurzamere identiteit op plaatsen nodig hebt die uw organisatie bezit en controleert, laat FPIDs u uw eigen apparatenherkenningsteken beheren en het gebruiken om ECID te zaaien.

FPID&#39;s worden ondersteund voor webimplementaties die de Web SDK gebruiken, inclusief de Web SDK-tagextensie. Zij zijn ideaal wanneer uw belangrijkste doel sterkere identiteitspersistentie op domeinen is uw organisatie bezit, of u wilt betere continuïteit voor rapportering en verpersoonlijking op bezeten Web-eigenschappen. Ze stellen u ook in staat om een cookie van de eerste partij in te stellen en te beheren vanuit de infrastructuur die u beheert.

FPID&#39;s zijn niet het juiste gereedschap als uw belangrijkste doel is het afhandelen van apps naar het web of het onderbrengen van identiteiten in meerdere domeinen. Voor die scenario&#39;s, zie [&#x200B; mobiel-aan-web identiteit het delen &#x200B;](./mobile-to-web.md) en [&#x200B; dwars-domein het delen &#x200B;](./cross-domain-sharing.md).

Tot de voordelen van het gebruik van FPID&#39;s behoren:

* Meer persistentie op eigendommen in eigendom.
* Meer controle over hoe het apparatenherkenningsteken wordt geproduceerd en beheerd.
* Een duurzame basis voor analyses en personalisatie.

Voorbeelden van overgangen naar het gebruik van FPID&#39;s zijn:

* Meer implementatieverantwoordelijkheid dan vertrouwen op standaard identiteitsgedrag.
* Coördinatie van de servercookie-logica en configuratie van gegevensverzameling.
* Aanvullende validatie ter bevestiging van de id wordt gebruikt zoals verwacht.

### Installatiepad op hoog niveau

1. Genereer en beheer een apparaat-id van de eerste partij op de infrastructuur die u beheert.
1. Vorm uw implementatie om die identiteitskaart of van a [&#x200B; eerste-partijkoekje &#x200B;](#setting-cookie-datastreams) of van de [&#x200B; identiteitslading &#x200B;](#identityMap) te lezen.
1. Controleer of bezoekers die de site retourneren, een consistente identiteit behouden op het moment dat ze eigendom zijn van uw eigendommen.

## Hoe FPID&#39;s werken {#how-fpids-work}

De FPID die aan Adobe Experience Cloud wordt doorgegeven, wordt met een deterministisch algoritme omgezet in een ECID. Telkens wanneer dezelfde FPID naar de Edge Network wordt verzonden, wordt dezelfde ECID van de FPID verzonden. Nadat de FPID is gebruikt om een ECID te verzenden, wordt deze verwijderd uit de `identityMap` en vervangen door de gegenereerde ECID. De FPID wordt niet opgeslagen in Adobe Experience Platform- of Experience Cloud-oplossingen.

Wanneer zowel een ECID als een FPID bestaan, wordt de ECID altijd gebruikt om de gebruiker eerst te identificeren. Deze prioritering zorgt ervoor dat wanneer een bestaande ECID aanwezig is in de browser cookie store, deze de primaire id blijft en dat het aantal bestaande bezoekers geen risico op inflatie inhoudt. Voor bestaande gebruikers wordt de FPID pas de primaire identiteit als de ECID verloopt of als gevolg van browserbeleid of handmatige handelingen wordt verwijderd.

Identiteiten krijgen prioriteit in de volgende volgorde:

1. ECID opgenomen in de `identityMap`
1. ECID opgeslagen in een cookie
1. FPID opgenomen in de `identityMap`
1. FPID opgeslagen in een cookie

## FPID-cookie genereren en instellen {#set-fpid-cookie}

Edge Network keurt slechts IDs goed die aan het [&#x200B; formaat UIDv4 &#x200B;](https://datatracker.ietf.org/doc/html/rfc4122) voldoen. Apparaat-id&#39;s die niet de UUIDv4-indeling hebben, worden geweigerd.

* UUIDs is uniek en willekeurig, met een verwaarloosbare waarschijnlijkheid van botsing.
* UUIDv4 kan niet worden verzonden gebruikend IP adressen of een andere persoonlijk identificeerbare informatie (PII).
* De bibliotheken om UUIDs te produceren zijn beschikbaar voor elke programmeertaal.

### Server-side cookie-instelling {#set-cookie-server}

Wanneer u een cookie instelt via uw eigen server, kunt u verschillende methoden gebruiken om te voorkomen dat het cookie wordt beperkt door het browserbeleid:

* Cookies genereren met scripttalen op de server
* Cookies instellen als reactie op een API-aanvraag die is uitgevoerd naar een subdomein of ander eindpunt op de site
* Cookies genereren met behulp van een inhoudsbeheersysteem (CMS)
* Cookies genereren via een CDN (Content Delivery Network)

De koekjes van de eerste partij zijn het meest efficiënt wanneer zij gebruikend een server worden geplaatst die een DNS [&#x200B; verslag van A &#x200B;](https://datatracker.ietf.org/doc/html/rfc1035) (voor IPv4) of [&#x200B; het verslag van AAAA &#x200B;](https://datatracker.ietf.org/doc/html/rfc3596) (voor IPv6), in tegenstelling tot een DNS `CNAME` of code van JavaScript gebruikt.

>[!IMPORTANT]
>
>Cookies die zijn ingesteld met de methode JavaScript `document.cookie` (inclusief de tagmethode [`cookie.set()`](../tags/cookie.md) ) worden bijna nooit beschermd tegen browserbeleid dat de duur van cookies beperkt.

`A` - of `AAAA` -records worden alleen ondersteund voor het instellen en bijhouden van cookies. De primaire methode voor gegevensverzameling is via een DNS `CNAME` . FPID&#39;s worden ingesteld met behulp van een `A` - of `AAAA` -record en verzonden naar Adobe met behulp van een `CNAME` -record. Het [&#x200B; Adobe-Beheerde Programma van het Certificaat &#x200B;](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) staat u toe om a `CNAME` voor gegevensinzameling te vormen.

### Wanneer stelt u het cookie in {#when-to-set-cookie}

Het FPID-cookie wordt idealiter ingesteld voordat gegevens naar de Edge Network worden verzonden. Als uw implementatie toestemming vereist alvorens gegevens te verzamelen, zie [&#x200B; Toestemming met eerste-partij apparaat IDs &#x200B;](./consent.md#consent-with-fpids) voor begeleiding bij het coördineren van het FPID koekje met uw toestemmingsstroom. De inflatie van de bezoeker wordt verminderd wanneer u ervoor zorgt dat FPID beschikbaar is om ECID van het eerste verzoek te zaaien. In scenario&#39;s waar dat niet mogelijk is, wordt een ECID nog geproduceerd gebruikend bestaande methodes en dienst als primaire herkenningsteken zolang het koekje bestaat. De gegenereerde FPID wordt pas de primaire id als de ECID niet meer aanwezig is. Ervan uitgaande dat de ECID uiteindelijk wordt beïnvloed door een beleid voor het verwijderen van de browser, maar de FPID niet, wordt de FPID de primaire id bij het volgende bezoek en wordt deze gebruikt om de ECID bij elk volgend bezoek te bedienen.

### De vervaldatum instellen {#set-expiration}

Adobe raadt u aan de levensduur van uw FPID-cookie zorgvuldig in overweging te nemen. Zorg ervoor dat u rekening houdt met het privacybeleid van uw organisatie en met de wetten en het beleid van de landen of regio&#39;s waarin uw organisatie actief is. Afhankelijk van de opstelling van uw organisatie, kon u een bedrijf-brede koekjesplaatsend beleid of één aannemen dat voor gebruikers in elke scène varieert waar u werkt. Ongeacht de aanvankelijke vervaldatum van het cookie, zorg ervoor dat u logica omvat die de vervaldatum verlengt telkens als een nieuw plaatsbezoek voorkomt.

### Koekjesvlaggen {#cookie-flags}

Er zijn verschillende cookiemarkeringen die van invloed zijn op de manier waarop cookies in verschillende browsers worden verwerkt:

* **`HTTPOnly`**: cookies die zijn ingesteld met de markering `HTTPOnly` , kunnen niet worden benaderd met clientscripts. Dit betekent dat als u bij het instellen van de FPID een markering `HTTPOnly` instelt, u een scripttaal aan de serverzijde moet gebruiken om de cookiewaarde voor opname in `identityMap` te lezen. Als u ervoor kiest dat de Edge Network de waarde van het FPID-cookie leest, zorgt het instellen van de markering `HTTPOnly` ervoor dat de waarde niet toegankelijk is voor clientscripts, maar geen negatief effect heeft op de mogelijkheid van de Edge Network om de cookie te lezen. Het gebruik van de markering `HTTPOnly` heeft geen invloed op het cookiebeleid dat de levensduur van cookies kan beperken. Het is echter nog steeds iets om te overwegen terwijl u de waarde van de FPID instelt en leest.
* **`Secure`**: cookies die zijn ingesteld met het kenmerk `Secure` worden alleen verzonden naar de server met een gecodeerde aanvraag via het HTTPS-protocol. Door deze markering te gebruiken, kunt u ervoor zorgen dat aanvallers van &#39;man-in-the-middle&#39; de cookiewaarde niet gemakkelijk kunnen openen. Het is altijd verstandig om de markering `Secure` in te stellen, als dat mogelijk is.
* **`SameSite`**: Met het kenmerk `SameSite` kunnen servers bepalen of cookies worden verzonden met intersite-aanvragen. Het kenmerk biedt enige bescherming tegen valsemunterij op andere locaties. Er zijn drie mogelijke waarden: `Strict`, `Lax` en `None` . Raadpleeg uw interne team om te bepalen welke instelling geschikt is voor uw organisatie. Als er geen kenmerk `SameSite` is opgegeven, is de standaardinstelling voor sommige browsers `SameSite=Lax` .

## De FPID naar de Edge Network verzenden {#send-fpid}

U kunt FPID&#39;s op twee manieren naar de Edge Network verzenden:

* **[Methode 1](#setting-cookie-datastreams)**: Vorm a `CNAME` voor uw vraag van SDK van het Web en omvat de naam van uw koekje FPID in uw configuratie van de gegevensstroom.
* **[Methode 2](#identityMap)**: Omvat FPID in de identiteitskaart.

### Methode 1: Configureer een `CNAME` en stel een cookie van de eerste-id-id in de gegevensstroom in {#setting-cookie-datastreams}

Om een FPID koekje van uw eigen domein te plaatsen, moet u uw eigen `CNAME` voor uw vraag van SDK van het Web vormen, dan de het koekjesfunctionaliteit van Eerste partij van identiteitskaart in uw datastreamconfiguratie toelaten. Met een `CNAME` -record in uw DNS kunt u een alias maken van de ene domeinnaam naar de andere. Met deze alias kunnen services van derden eruit zien alsof ze deel uitmaken van uw eigen domein, zodat hun cookies eruit zien als cookies van de eerste fabrikant. Wanneer de inzameling van de eerste-partijgegevens gebruikend `CNAME` wordt toegelaten, worden alle koekjes voor uw domein verzonden op verzoeken die aan het eindpunt van de gegevensinzameling worden gemaakt.

1. Werk met Adobe om een `CNAME` -record te maken voor gegevensverzameling in uw organisatie. Zie [&#x200B; Adobe-Beheerde certificaatprogramma &#x200B;](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/adobe-managed-cert) voor het volledige proces.
1. Schakel de optie **[!UICONTROL First Party ID Cookie]** in uw gegevensstroom in. Deze instelling geeft de Edge Network de opdracht om naar het opgegeven cookie te verwijzen wanneer een apparaat-id van de eerste partij wordt opgezocht in plaats van de waarde op te zoeken in het identiteitsoverzicht. Als u deze instelling inschakelt, moet u de naam opgeven van het cookie waarop de FPID moet worden opgeslagen. Zie [&#x200B; gegevensstromen &#x200B;](/help/datastreams/configure.md#advanced-options) voor meer informatie creëren en vormen.

   ![&#x200B; beeld van Platform UI die de configuratie toont die van de gegevensstroom de Eerste het plaatsen van het Koekje van identiteitskaart van de Partij &#x200B;](/help/collection/js/assets/first-party-id-datastreams.png) benadrukt

### Methode 2: FPID&#39;s gebruiken in `identityMap` {#identityMap}

Als alternatief voor het opslaan van de FPID in uw eigen cookie, kunt u de FPID naar de Edge Network verzenden via het identiteitsoverzicht.

Hieronder ziet u hoe u een FPID instelt in het dialoogvenster `identityMap` :

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

Net als bij andere identiteitstypen kunt u de FPID opnemen met andere identiteiten in `identityMap` . In het volgende voorbeeld ziet u de FPID met een geverifieerde CRM-id:

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
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Als FPID in een koekje bevat dat door Edge Network wordt gelezen wanneer de inzameling van de eerste-partijgegevens wordt toegelaten, vang slechts voor authentiek verklaarde identiteitskaart van CRM:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migreren naar FPID&#39;s {#migrating-to-fpid}

Als u van een vorige implementatie naar apparaat-id&#39;s van de eerste partij migreert, kan het moeilijk zijn om te visualiseren hoe de overgang er op een laag niveau zou kunnen uitzien. Om dit proces te illustreren, kunt u een scenario overwegen waarbij een klant betrokken is die eerder uw site heeft bezocht en welke invloed een FPID-migratie zou hebben op de manier waarop die klant wordt geïdentificeerd in Adobe-oplossingen.

![&#x200B; Diagram die tonen hoe de waarden van identiteitskaart van een klant tussen bezoeken na het migreren aan FPIDs &#x200B;](/help/collection/js/assets/identity/tracking/visits.png) worden bijgewerkt

| Bezoek | Beschrijving |
| --- | --- |
| Eerste bezoek | Stel dat u het FPID-cookie nog niet hebt ingesteld. ECID bevat in het [&#x200B; koekje van AMCV &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) is het herkenningsteken dat wordt gebruikt om de bezoeker te identificeren. |
| Tweede bezoek | De implementatie van de FPID-oplossing is gestart. De bestaande ECID is nog steeds aanwezig en blijft de primaire identificator voor bezoekersidentificatie. |
| Derde bezoek | Tussen het tweede en derde bezoek is er voldoende tijd verstreken om de ECID te verwijderen vanwege het browserbeleid. Omdat de FPID echter is ingesteld met een DNS `A` -record, blijft de FPID bestaan. De FPID wordt nu beschouwd als de primaire id en wordt gebruikt om de ECID te verzenden, die naar het apparaat van de eindgebruiker wordt geschreven. De gebruiker wordt nu beschouwd als een nieuwe bezoeker voor Adobe Experience Platform- en Experience Cloud-oplossingen. |
| Vierde bezoek | Tussen de derde en vierde keer is er voldoende tijd verstreken om de ECID te verwijderen vanwege het browserbeleid. Net als bij het vorige bezoek blijft de FPID te wijten aan de wijze waarop zij is ingesteld. Deze keer wordt dezelfde ECID gegenereerd als het vorige bezoek. De gebruiker wordt in Adobe Experience Platform- en Experience Cloud-oplossingen gezien als dezelfde gebruiker als het vorige bezoek. |
| Vijfde bezoek | Tussen de vierde en de vijfde keer dat u de gebruiker bezoekt, wist deze gebruiker alle cookies in de browser. Er wordt een nieuwe FPID gegenereerd die wordt gebruikt om het maken van een nieuwe ECID te stimuleren. De gebruiker wordt nu beschouwd als een nieuwe bezoeker voor Adobe Experience Platform- en Experience Cloud-oplossingen. |
