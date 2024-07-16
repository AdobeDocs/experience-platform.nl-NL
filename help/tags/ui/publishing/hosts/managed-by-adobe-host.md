---
title: Overzicht van door Adobe beheerde hosts
description: Leer meer over de standaardhostingoptie voor het implementeren van builds van tagbibliotheken in Adobe Experience Platform.
exl-id: 9042c313-b0d3-4f6e-963d-0051d760fd16
source-git-commit: 85b428b3997d53cbf48e4f112e5c09c0f40f7ee1
workflow-type: tm+mt
source-wordcount: '1170'
ht-degree: 0%

---

# Overzicht van door Adobe beheerde hosts

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Gastheren met beheerde Adobe zijn de standaardhostinstelling voor het implementeren van uw tagbibliotheek-builds in Adobe Experience Platform. Wanneer u een nieuw bezit door het gebruikersinterface van de Inzameling van Gegevens creeert, wordt een standaard Adobe-beheerde gastheer gecreeerd voor u.

Met Adobe-beheerde gastheren, worden de bibliotheekbouwstijlen geleverd aan een netwerk van de derdeinhoudslevering (CDN) dat de Adobe met heeft gecontracteerd. Deze CDNs werkt onafhankelijk van Adobe, zodat zelfs wanneer Platform onderhoud ondergaat of anders neer is, zal uw opgestelde code normaal op uw plaatsen en toepassingen blijven functioneren. De insluitcode voor een host met Adobe-beheer verwijst naar het hoofdbibliotheekbestand op de CDN, zodat een clientapparaat de bestanden bij uitvoering kan ophalen.

Dit document verstrekt een overzicht van Adobe-geleide gastheren in Platform en verstrekt stappen op hoe te om een nieuwe Adobe-beheerde gastheer in UI tot stand te brengen.

## Akamai

Momenteel, is de primaire leverancier CDN voor Adobe [ Akamai ](https://www.akamai.com/). De robuuste CDN van Akamai is gebouwd om inhoud aan een globaal, hoog-volume publiek van Webbezoekers te dienen. CDN stelt overtollige netwerken van lading-in evenwicht gebrachte, geo-geoptimaliseerde knopen in werking om inhoud zo snel mogelijk aan bezoekers te dienen die door de wereld worden gevestigd.

Akamai voert meer dan 137.000 servers uit in 87 landen binnen meer dan 1.150 netwerken. In termen van overtolligheid, kan CDN niet alleen routes van één server aan een andere maar ook van één knoop van servers aan een andere knoop van servers leiden zoals nodig. Met andere woorden, elke knoop bestaat uit veelvoudige servers, zodat één server die neer gaat nooit een kwestie wordt aangezien de andere servers op de zelfde knoop kunnen overnemen.

Als een volledige knoop daalt, dient Akamai van de volgende dichtstbijzijnde knoop met de zelfde caching inhoud. Knooppunten worden dynamisch geselecteerd op basis van de locatie van de bezoeker, de verkeerslading en andere factoren, zodat de inhoud consistent wordt aangeboden vanaf het beste lokale knooppunt voor elke bezoeker.

Bestanden die op Akamai worden gehost, hebben het domein `assets.adobedtm.com` . Hiernaar kan veilig worden verwezen of niet (`http://` of `https://`) op basis van hoe het binnen in uw ingesloten `<script>` code wordt geroepen.

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

Wanneer een Edge-knooppunt een aanvraag voor een specifiek bestand ontvangt (zoals de build van de bibliotheek), controleert het knooppunt eerst de vervaltijd van het bestand. Als de tijd niet is verlopen, dient het randknooppunt de versie in de cache. Als de tijd is verlopen, dan verzoekt de randknoop om een nieuw exemplaar van de dichtstbijzijnde oorsprong, dient dat verfriste exemplaar, en beslaat dan het verfriste exemplaar met een nieuwe vervaltijd in het voorgeheugen.

>[!NOTE]
>
>Naast het in cache plaatsen van randknooppunten kunnen er ook tussennetwerken (zoals bedrijfsnetwerken of mobiele netwerken) zijn die hun eigen caching uitvoeren. Als uw bouwstijlen niet zoals verwacht in het voorgeheugen onderbrengen, kunnen deze netwerken de onderliggende oorzaak zijn.

#### Edge cache-validatie {#invalidation}

Wanneer u een nieuwe bibliotheekbuild uploadt, worden de caches op alle relevante randknooppunten ongeldig gemaakt. Dit betekent dat elk knooppunt de versie in de cache als ongeldig beschouwt, ongeacht hoe recent het een nieuwe kopie heeft opgehaald. De volgende keer dat een randknooppunt een aanvraag voor dat bestand ontvangt, haalt het knooppunt een nieuwe kopie op van de oorsprong.

Omdat Akamai meerdere oorspronkelijke servers heeft die bestanden tussen elkaar repliceren en omdat niet kan worden vastgesteld welke oorsprong uw bestand het eerst heeft ontvangen, kunnen deze knooppuntverzoeken een oorsprong bereiken die niet over de nieuwste versie beschikt. Vervolgens wordt de oudere versie opnieuw in de cache opgeslagen. Om dit te verhinderen voor te komen, worden de veelvoudige geheim voorgeheugenbevestigingen uitgevoerd voor elke nieuwe bouwstijl op de volgende intervallen:

* Onmiddellijk na uploaden
* 5 minuten na uploaden
* 60 minuten na uploaden

Deze gefaseerde cachevervalsingen geven de groepen van de oorspronkelijke server tijd om de recentste versie van het dossier tussen zich te herhalen zodat zij allen de recentste versie hebben wanneer het dossier wordt teruggewonnen.

### Browser in cache plaatsen {#browser}

Bibliotheekbuilds worden ook in de cache van de browser opgeslagen via de `cache-control` HTTP-header. Wanneer het gebruiken van Adobe-geleide gastheren, hebt u geen controle over de kopballen die in API reacties worden teruggekeerd, zodat wordt het gebrek van de Adobe voor caching gebruikt. Met andere woorden, kunt u geen douanekopballen voor Adobe-beheerde gastheren gebruiken. Als u een douane `cache-control` kopbal vereist, kunt u [ zelf-ontvangen ](self-hosting-libraries.md) in plaats daarvan willen overwegen.

De vervaltijd voor de in de browser opgeslagen bibliotheekbuild (bepaald door de header `cache-control` ) hangt af van de tagomgeving die u gebruikt:

| Omgeving | `cache-control` value |
| --- | --- |
| Ontwikkeling | `max-age=0, no-cache, no-store` |
| Staging | `max-age=0, no-cache, no-store` |
| Productie | `max-age=3600` |

Zoals in de bovenstaande tabel wordt aangegeven, wordt het in cache plaatsen van browsers niet ondersteund in ontwikkelings- en testomgevingen. Als dusdanig, zou u niet de ontwikkeling of het opvoeren ingebedde codes in hoog-verkeer of productiecontext moeten gebruiken.

De cache-control headers worden alleen toegepast op de hoofdbibliotheek. Eventuele subbronnen onder de hoofdbibliotheek worden altijd als netto-nieuw beschouwd en daarom is het niet nodig deze in de cache op te slaan in de browser.

## Het gebruiken van Adobe-beheerde ontvangen in UI

Wanneer u eerst een bezit in Platform UI of UI van de Inzameling van Gegevens creeert, wordt een Adobe-geleide gastheer automatisch gecreeerd voor u. Alle beschikbare milieu&#39;s die onmiddellijk bruikbare eigenschappen hebben worden ook toegewezen aan Adobe-beheerde gastheer door gebrek.

>[!NOTE]
>
>Als de standaard Adobe-beheerde gastheer van alle milieu&#39;s unassigned, kan de gastheer worden geschrapt. Als u terug naar een Adobe-beheerde gastheer wilt schakelen nadat dit doet, kunt u een nieuwe gastheer door de volgende stappen tot stand brengen:
>
>1. Selecteer de tab **[!UICONTROL Hosts]** op de eigenschap en selecteer vervolgens **[!UICONTROL Add Host]** .
>1. Geef een naam op voor de host, selecteer **[!UICONTROL Managed by Adobe]** als het hosttype en selecteer vervolgens **[!UICONTROL Save]** .
>
>U kunt uw milieu&#39;s aan Adobe-beheerde gastheer dan opnieuw toewijzen zoals gewenst.

## Volgende stappen

Dit document biedt een overzicht van de door Adobe beheerde hosting van tagbibliotheken in Adobe Experience Platform. Raadpleeg de volgende documentatie voor informatie over andere hostingopties:

* [SFTP-hosting](./sftp-host.md)
* [Bibliotheken die zichzelf hosten](./self-hosting-libraries.md)

Voor details op hoe te om gastheren voor uw milieu&#39;s te beheren, zie de [ milieu&#39;s gids ](../environments.md).
