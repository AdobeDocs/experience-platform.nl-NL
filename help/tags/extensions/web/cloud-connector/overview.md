---
title: Overzicht van extensie voor Cloud Connector
description: Meer informatie over de Cloud Connector-gebeurtenis die extensie doorstuurt in Adobe Experience Platform.
source-git-commit: 1d3415146335d3011963c969d5b6aeea1f1a51d0
workflow-type: tm+mt
source-wordcount: '1603'
ht-degree: 0%

---

# Overzicht van de extensie Cloud Connector

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Met de Cloud Connector-gebeurtenis die extensie doorstuurt, kunt u aangepaste HTTP-aanvragen maken om gegevens naar een bestemming te verzenden of gegevens van een bestemming op te halen. De uitbreiding van de Verbinding van de Wolk is als het hebben van Postman op het Netwerk van de Rand van Adobe Experience Platform en kan worden gebruikt om gegevens naar een eindpunt te verzenden dat nog geen specifieke uitbreiding heeft.

Gebruik deze verwijzing voor informatie over de beschikbare opties wanneer het gebruiken van deze uitbreiding om een regel te bouwen.

## Extensietype van Cloud Connector

In deze sectie wordt het actietype Gegevens verzenden beschreven dat beschikbaar is in de extensie Adobe Experience Platform Cloud Connector.

### Type aanvraag

Om het type van verzoek te selecteren dat door het eindpunt wordt vereist, selecteer het aangewezen type onder [!UICONTROL Request Type] dropdown.

| Methode | Beschrijving |
|---|---|
| [GET](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/GET) | Verzoekt een vertegenwoordiging van de gespecificeerde bron. Verzoeken met GET moeten alleen gegevens ophalen. |
| [POST](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/POST) | Verzendt een entiteit naar de opgegeven bron, die vaak een wijziging in status of bijwerkingen op de server veroorzaakt. |
| [PUT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PUT) | Vervangt alle huidige vertegenwoordiging van het doelmiddel met de verzoeklading. |
| [PATCH](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/PATCH) | Past gedeeltelijke wijzigingen op een middel toe. |
| [DELETE](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/DELETE) | Verwijdert de opgegeven bron. |

### URL van eindpunt

Voer in het tekstveld naast het vervolgkeuzemenu Request-type de URL in voor het eindpunt waarnaar u gegevens verzendt.

### De params van de vraag, kopballen, en lichaamconfiguratie

Gebruik elk van deze lusjes (de Params van de Vraag, Kopballen, en Elementen van de Gegevens van het Lichaam) om te controleren welke gegevens naar een bepaald eindpunt worden verzonden.

#### Zoekparameters

Definieer een sleutel en waarde voor elk sleutelwaardepaar dat u als parameter voor een querytekenreeks wilt verzenden. Als u handmatig een gegevenselement wilt invoeren, gebruikt u de samenvoeging van het accolade-gegevenselement voor het doorsturen van gebeurtenissen. Als u wilt verwijzen naar de waarde van een gegevenselement met de naam &quot;siteSection&quot; als een sleutel of waarde, typt u `{{siteSection}}`. Of selecteer het eerder gemaakte gegevenselement door dit in het vervolgkeuzemenu te selecteren.

Als u meer queryparameters wilt toevoegen, selecteert u **[!UICONTROL Add Another]**.

#### Kopteksten

Definieer een sleutel en waarde voor elk sleutelwaardepaar dat u als koptekst wilt verzenden. Als u handmatig een gegevenselement wilt invoeren, gebruikt u de samenvoeging van het accolade-gegevenselement voor het doorsturen van gebeurtenissen. Als u wilt verwijzen naar de waarde van een gegevenselement met de naam &quot;pageName&quot; als een sleutel of waarde, typt u `{{pageName}}`. Of selecteer het eerder gemaakte gegevenselement door dit in het vervolgkeuzemenu te selecteren.

Als u meer kopteksten wilt toevoegen, selecteert u **[!UICONTROL Add Another]**.

In de volgende tabel staan de vooraf gedefinieerde koppen. U bent niet beperkt tot deze kopteksten en kunt uw eigen douanekopballen toevoegen indien nodig, maar zij worden ter beschikking gesteld voor uw gemak.

>[!NOTE]
>
>Voor meer gedetailleerde informatie over deze kopballen, bezoek [https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).

| Koptekst | Beschrijving |
|---|---|
| [A-IM](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) |  |
| [Accepteren](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) |  |
| [Accepteren-tekenset](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Charset) |  |
| [Codering accepteren](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding) |  |
| [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) |  |
| [Accepteren-datumtime](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) | Verzonden door een gebruikersagent om erop te wijzen wil het tot een verleden staat van een originele middel toegang hebben. Te dien einde wordt de `Accept-Datetime` kopbal overgebracht in een HTTP- verzoek dat tegen een TimeGate voor een originele middel wordt uitgegeven, en zijn waarde wijst op de datetime van de gewenste vroegere staat van de originele middel. |
| Access-Control-request-headers | Gebruikt door browsers wanneer het uitgeven van [preflight verzoek](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request), om de server te laten weten welke [HTTP kopballen ](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers) de cliënt zou kunnen verzenden wanneer het daadwerkelijke verzoek wordt gedaan. |
| Access-Control-request-method | Wordt gebruikt door browsers bij het uitgeven van een [preflight-aanvraag](https://developer.mozilla.org/en-US/docs/Glossary/preflight_request), om de server te laten weten welke [HTTP-methode](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods) zal worden gebruikt wanneer het daadwerkelijke verzoek wordt gedaan. Deze kopbal is noodzakelijk omdat het preflight verzoek altijd een [OPTION](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS) is en niet de zelfde methode zoals het daadwerkelijke verzoek gebruikt. |
| Toestemming | Bevat de geloofsbrieven om een gebruiker-agent met een server voor authentiek te verklaren. |
| [Cachebeheer](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control) | Richtlijnen voor caching-mechanismen in zowel verzoeken als antwoorden. |
| [Verbinding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Connection) | Bepaalt of de netwerkverbinding open blijft nadat de huidige transactie is voltooid. |
| [Content-Length](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Length) | De grootte van de bron, in decimaal aantal bytes. |
| [Inhoudstype](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) | Geeft het mediatype van de bron aan. |
| Cookie | Bevat opgeslagen [HTTP-cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies) die eerder door de server zijn verzonden met de header [`Set-Cookie`](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Set-Cookie). |
| Datum | De algemene HTTP-header bevat de datum en tijd waarop het bericht is gestart. |
| [DNT](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/DNT) | Drukt de voorkeur van de gebruiker het volgen uit. |
| Verwacht | Geeft aan dat de server aan de verwachtingen moet voldoen om de aanvraag correct af te handelen. |
| Doorgestuurd | Bevat informatie van [reverse volmachtsservers](https://developer.mozilla.org/en-US/docs/Web/HTTP/Proxy_servers_and_tunneling) die wordt veranderd of verloren wanneer een volmacht in de weg van het verzoek betrokken is. |
| Van | Bevat een e-mailadres van Internet voor een menselijke gebruiker die de het vragen gebruikersagent controleert. |
| Host | Geeft het host- en poortnummer op van de server waarnaar de aanvraag wordt verzonden. |
| If-Match |  |
| If-Modified-Since |  |
| [If-None-Match](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-None-Match) |  |
| [If-Range](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Range) |  |
| [If-Unmodified-Since](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Max-Forwards](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/If-Unmodified-Since) |  |
| [Oorsprong](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Origin) |  |
| [Pragma](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Pragma) | Implementation-specific kopbal die diverse gevolgen overal langs verzoek-reactie keten kan hebben. Wordt gebruikt voor achterwaartse compatibiliteit met HTTP/1.0-caches waarbij de header Cache-Control nog niet aanwezig is. |  |
| [Proxy-autorisatie](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Proxy-Authorization) |
| [Bereik](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Range) | Geeft het deel van een document aan dat de server moet retourneren. |  |
| [Verwijzing](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Referer) | Het adres van de vorige webpagina vanwaar een koppeling naar de momenteel aangevraagde pagina werd gevolgd. |  |
| TE | Specificeert de overdrachtcoderingen de gebruikersagent bereid is te aanvaarden. (U kunt het informeel `Accept-Transfer-Encoding` noemen, wat intuïtiever zou zijn). |
| Upgrade | Het relevante RFC-document voor het koptekstveld [`Upgrade` is RFC 7230, sectie 6.7](https://tools.ietf.org/html/rfc7230#section-6.7). De norm bepaalt regels voor bevordering of het veranderen in een verschillend protocol over de huidige cliënt, de server, de verbinding van het vervoerprotocol. Met deze headerstandaard kan een client bijvoorbeeld van HTTP 1.1 naar HTTP 2.0 gaan, ervan uitgaande dat de server besluit het headerveld `Upgrade` te accepteren en implementeren. Geen van beide partijen is verplicht de voorwaarden te accepteren die zijn opgegeven in het headerveld `Upgrade`. Het kan in zowel cliënt als serverkopballen worden gebruikt. Als het koptekstveld `Upgrade` is opgegeven, MOET de afzender ook het koptekstveld `Connection` met de opgegeven optie `upgrade` verzenden. |  |
| [Gebruikersagent](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/User-Agent) | Bevat een kenmerkende tekenreeks waarmee de gelijken van het netwerkprotocol het toepassingstype, het besturingssysteem, de softwareleverancier of de softwareversie van de verzoekende softwaregebruiker kunnen identificeren. |
| [Via](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Via) | Toegevoegd door volmachten, zowel voorwaartse als omgekeerde volmachten, en kan in de verzoekkopballen en de antwoordkopballen verschijnen. |
| [Waarschuwing](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Warning) | Algemene waarschuwingsinformatie over mogelijke problemen. |
| X-CSRF-token |  |
| x-requested-with |  |

#### Body as JSON

Definieer een sleutel en waarde voor elk sleutelwaardepaar dat u in de hoofdtekst van de aanvraag wilt verzenden. Als u handmatig een gegevenselement wilt invoeren, gebruikt u de samenvoeging van het accolade-gegevenselement voor het doorsturen van gebeurtenissen. Als u wilt verwijzen naar de waarde van een gegevenselement met de naam &quot;appSection&quot; als een sleutel of waarde, typt u `{{appSection}}`. Of selecteer het eerder gemaakte gegevenselement door dit in het vervolgkeuzemenu te selecteren.

Als u extra sleutelwaardeparen wilt toevoegen, selecteert u **[!UICONTROL Add Another]**.

#### Lichaam als onbewerkt

Definieer een sleutel en waarde voor elk sleutelwaardepaar dat u in de hoofdtekst van de aanvraag wilt verzenden. Als u handmatig een gegevenselement wilt invoeren, gebruikt u de samenvoeging van het accolade-gegevenselement voor het doorsturen van gebeurtenissen. Als u wilt verwijzen naar de waarde van een gegevenselement met de naam &quot;appSection&quot; als een sleutel of waarde, typt u `{{appSection}}`. Of selecteer het eerder gemaakte gegevenselement door dit in het vervolgkeuzemenu te selecteren. U kunt een of meer gegevenselementen toevoegen.

### Geavanceerd

Handelingen binnen regels bij het doorsturen van gebeurtenissen worden opeenvolgend uitgevoerd. Er zouden situaties kunnen zijn waar u gegevens van een externe bron wilt terugwinnen die niet op de inkomende gebeurtenis van de cliënt aanwezig is en dan deze reactie nemen en of deze gegevens omzetten of verzenden naar een definitieve bestemming in een verdere actie binnen één enkele regel. Dit wordt mogelijk gemaakt door &quot;De aanvraagreactie opslaan&quot; in de geavanceerde sectie.

Als u de hoofdtekst van de reactie wilt opslaan vanaf een eindpunt, schakelt u het selectievakje **[!UICONTROL Save the request response]** in en definieert u een antwoordsleutel in het tekstveld.

Als u de antwoordsleutel als `productDetails` bepaalde, verwijs deze gegevens in een gegevenselement en verwijs dan dit gegevenselement in een verdere actie binnen de zelfde regel. Als u een gegevenselement wilt maken waarnaar `productDetail` verwijst, maakt u een gegevenselement van het type `path` en voert u het volgende pad in:

```Json
arc.ruleStash.[EXTENSION-NAME-HERE].responses.[RESPONSE-KEY-HERE] 

arc.ruleStash.adobe-cloud-connector.reponses.productDetails 
```
