---
title: Overzicht van door Adobe beheerde hosts
description: Leer meer over de standaardhostingoptie voor het implementeren van builds van tagbibliotheken in Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '1166'
ht-degree: 0%

---

# Overzicht van door Adobe beheerde hosts

>[!NOTE]
>
>Adobe Experience Platform Launch wordt omgedoopt tot een reeks technologieën voor gegevensverzameling in Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

Gastheren met Adobe-beheer zijn de standaardhostinstelling voor het implementeren van uw tagbibliotheek-builds in Adobe Experience Platform. Wanneer u een nieuw bezit door het gebruikersinterface van de Inzameling van Gegevens creeert, wordt een standaard Adobe-geleide gastheer gecreeerd voor u.

Met Adobe-beheerde gastheren, worden de bibliotheekbouwstijlen geleverd aan een netwerk van de derdeinhoudslevering (CDN) dat Adobe met heeft gecontracteerd. Deze CDNs werkt onafhankelijk van Adobe, zodat zelfs wanneer het Platform onderhoud ondergaat of anders neer is, zal uw opgestelde code normaal op uw plaatsen en toepassingen blijven functioneren. De insluitcode voor een host met Adobe-beheer verwijst naar het hoofdbibliotheekbestand op de CDN, zodat een clientapparaat de bestanden bij uitvoering kan ophalen.

Dit document verstrekt een overzicht van Adobe-geleide gastheren in Platform en verstrekt stappen op hoe te om een nieuwe Adobe-geleide gastheer in UI tot stand te brengen.

## Akamai

Momenteel is de primaire CDN-provider voor Adobe [Akamai](https://www.akamai.com/). De robuuste CDN van Akamai is gebouwd om inhoud aan een globaal, hoog-volume publiek van Webbezoekers te dienen. CDN stelt overtollige netwerken van lading-in evenwicht gebrachte, geo-geoptimaliseerde knopen in werking om inhoud zo snel mogelijk aan bezoekers te dienen die door de wereld worden gevestigd.

Akamai voert meer dan 137.000 servers uit in 87 landen binnen meer dan 1.150 netwerken. In termen van overtolligheid, kan CDN niet alleen routes van één server aan een andere maar ook van één knoop van servers aan een andere knoop van servers leiden zoals nodig. Met andere woorden, elke knoop bestaat uit veelvoudige servers, zodat één server die neer gaat nooit een kwestie wordt aangezien de andere servers op de zelfde knoop kunnen overnemen.

Als een volledige knoop daalt, dient Akamai van de volgende dichtstbijzijnde knoop met de zelfde caching inhoud. Knooppunten worden dynamisch geselecteerd op basis van de locatie van de bezoeker, de verkeerslading en andere factoren, zodat de inhoud consistent wordt aangeboden vanaf het beste lokale knooppunt voor elke bezoeker.

Bestanden die op Akamai worden gehost, hebben het domein `assets.adobedtm.com`. U kunt hier veilig naar verwijzen (`http://` of `https://`) op basis van de manier waarop deze wordt aangeroepen in uw ingesloten `<script>`-code.

>[!WARNING]
>
>Als uw bibliotheek niet beschikbaar is via het Akamai-netwerk, kan Platform geen fouten voorkomen die zich hierdoor kunnen voordoen.

## Bibliotheek in cache plaatsen

Wanneer het gebruiken van Adobe-beheerde gastheren, worden uw bibliotheekbouwstijlen caching in twee plaatsen:

* [Edge caching](#edge)
* [Browser in cache plaatsen](#browser)

### Edge caching {#edge}

Het primaire doel van een CDN is om inhoud aan servers intelligent te verdelen die geografisch dichter aan eindgebruikers zijn zodat de inhoud sneller door cliëntapparaten kan worden teruggewonnen. CDN&#39;s bereiken dit door kopieën te maken van de inhoud die beschikbaar is op geografisch verspreide servers over de hele wereld (&quot;edge nodes&quot;).

Zodra uw bouwstijl aan de Adobe-beheerde gastheer is opgesteld, verspreidt CDN de bouwstijl op verscheidene gecentraliseerde servers (&quot;oorsprong&quot;), die dan exemplaren van de bouwstijl naar vele verschillende randknopen rond de wereld voor caching verzenden. De cacheversies van de build die op deze Edge-knooppunten zijn opgeslagen, worden dan uiteindelijk op de clientapparaten geplaatst.

![](../images/cdn-diagram.png)

>[!NOTE]
>
>Voor Adobe-beheerde gastheren, kan de zeer eerste gepubliceerde bibliotheek aan om het even welk nieuw milieu tot vijf minuten vergen om uit aan globale CDN te verspreiden.

Wanneer een Edge-knooppunt een aanvraag voor een specifiek bestand ontvangt (zoals de build van de bibliotheek), controleert het knooppunt eerst de waarde time-to-live (TTL) in het bestand. Als de TTL niet is verlopen, dient de randknoop de caching versie. Als TTL is verlopen, dan verzoekt de randknoop om een nieuw exemplaar van de dichtstbijzijnde oorsprong, dat verfrist exemplaar, en dan caches de verfriste exemplaar met nieuwe TTL.

>[!NOTE]
>
>Naast het in cache plaatsen van randknooppunten kunnen er ook tussennetwerken (zoals bedrijfsnetwerken of mobiele netwerken) zijn die hun eigen caching uitvoeren. Als uw bouwstijlen niet zoals verwacht in het voorgeheugen onderbrengen, kunnen deze netwerken de onderliggende oorzaak zijn.

#### Randcache-validatie {#invalidation}

Wanneer u een nieuwe bibliotheekbuild uploadt, worden de caches op alle relevante randknooppunten ongeldig gemaakt. Dit betekent dat elk knooppunt de versie in de cache als ongeldig beschouwt, ongeacht hoe recent het een nieuwe kopie heeft opgehaald. De volgende keer dat een randknooppunt een aanvraag voor dat bestand ontvangt, haalt het knooppunt een nieuwe kopie op van de oorsprong.

Omdat Akamai meerdere oorspronkelijke servers heeft die bestanden tussen elkaar repliceren en omdat niet kan worden vastgesteld welke oorsprong uw bestand het eerst heeft ontvangen, kunnen deze knooppuntverzoeken een oorsprong bereiken die niet over de nieuwste versie beschikt. Vervolgens wordt de oudere versie opnieuw in de cache opgeslagen. Om dit te verhinderen voor te komen, worden de veelvoudige geheim voorgeheugenbevestigingen uitgevoerd voor elke nieuwe bouwstijl op de volgende intervallen:

* Onmiddellijk na uploaden
* 5 minuten na uploaden
* 60 minuten na uploaden

Deze gefaseerde cachevervalsingen geven de groepen van de oorspronkelijke server tijd om de recentste versie van het dossier tussen zich te herhalen zodat zij allen de recentste versie hebben wanneer het dossier wordt teruggewonnen.

### Browser in cache plaatsen {#browser}

Bibliotheekbuilds worden ook in het cachegeheugen van de browser opgeslagen via de HTTP-header `cache-control`. Als u hosts met Adobe-beheer gebruikt, hebt u geen controle over de headers die worden geretourneerd in API-reacties. De standaardinstelling van de Adobe voor caching wordt dus gebruikt. Met andere woorden, u kunt geen douanekopballen voor Adobe-geleide gastheren gebruiken. Als u een aangepaste `cache-control` kopbal vereist, kunt u [self-hosting](self-hosting-libraries.md) in plaats daarvan willen overwegen.

De tijd-aan-levende (TTL) voor uw browser-caching bibliotheek bouwt (die door `cache-control` kopbal wordt bepaald) zal afhankelijk van het markeringsmilieu variëren u gebruikt:

| Omgeving | `cache-control` value |
| --- | --- |
| Ontwikkeling | `max-age=0, no-cache, no-store` |
| Staging | `max-age=0, no-cache, no-store` |
| Productie | `max-age=3600` |

Zoals in de bovenstaande tabel wordt aangegeven, wordt het in cache plaatsen van browsers niet ondersteund in ontwikkelings- en staging-omgevingen. Als dusdanig, zou u niet de ontwikkeling of het opvoeren ingebedde codes in hoog-verkeer of productiecontext moeten gebruiken.

De cache-control headers worden alleen toegepast op de hoofdbibliotheek. Eventuele subbronnen onder de hoofdbibliotheek worden altijd als netto-nieuw beschouwd en daarom is het niet nodig deze in de cache op te slaan in de browser.

## Het gebruiken van Adobe-beheerde ontvangen in de UI van de Inzameling van Gegevens

Wanneer u eerst een bezit in [de Inzameling UI](http://launch.adobe.com/) van Gegevens creeert, wordt een Adobe-geleide gastheer automatisch gecreeerd voor u. Alle beschikbare milieu&#39;s die onmiddellijk bruikbare eigenschappen hebben worden ook toegewezen aan de Adobe-beheerde gastheer door gebrek.

>[!NOTE]
>
>Als de standaard Adobe-beheerde gastheer van alle milieu&#39;s unassigned, kan de gastheer worden geschrapt. Als u terug naar een Adobe-geleide gastheer wilt schakelen nadat dit doet, kunt u een nieuwe gastheer door de volgende stappen tot stand brengen:
>
>1. Selecteer het **[!UICONTROL Hosts]** lusje op uw bezit, dan uitgezocht **[!UICONTROL Add Host]**.
>1. Geef een naam voor de host op en selecteer **[!UICONTROL Managed by Adobe]** als het hosttype en selecteer **[!UICONTROL Save]**.

>
>
Vervolgens kunt u uw omgevingen naar wens opnieuw toewijzen aan de host met Adobe-beheer.

## Volgende stappen

Dit document biedt een overzicht van de door Adobe beheerde hosting van tagbibliotheken in Adobe Experience Platform. Raadpleeg de volgende documentatie voor informatie over andere hostingopties:

* [SFTP-hosting](./sftp-host.md)
* [Bibliotheken die zichzelf hosten](./self-hosting-libraries.md)

Raadpleeg de [handleiding voor omgevingen](../environments.md) voor meer informatie over het beheren van hosts voor uw omgevingen.
