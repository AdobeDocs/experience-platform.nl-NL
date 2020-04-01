---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Overzicht van identiteitsservice

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen. Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

## Identiteitsservice

Elke dag, interactie van klanten met uw zaken en vestigen een onophoudelijk groeiende verhouding met uw merk. Een typische klant kan in om het even welk aantal systemen binnen de gegevensinfrastructuur van uw organisatie, zoals uw eCommerce, loyaliteit, en helpdesksystemen actief zijn. Die zelfde klant kan ook anoniem op om het even welk aantal apparaten in dienst nemen. Met Identity Service kunt u een volledig beeld van uw klant samenstellen, waarbij gerelateerde gegevens worden samengevoegd die anders over verschillende systemen zouden kunnen worden verspreid.

Bekijk een dagelijks voorbeeld van de relatie van een consument met je merk:

Mary heeft een account op je eCommerce-site waar ze in het verleden een paar bestellingen heeft gedaan. Ze gebruikt doorgaans haar persoonlijke laptop om te winkelen, waar ze zich telkens aanmeldt. Tijdens een van haar bezoeken gebruikt ze haar tablet echter om te winkelen op sandalen, maar ze plaatst geen bestelling en meldt zich niet aan.

Op dit punt wordt de activiteit van Mary weergegeven als twee aparte profielen: haar eCommerce-aanmelding en haar tablet-pc, mogelijk geïdentificeerd door apparaat-id.

Mary hervat later haar tabletsessie en stuurt haar e-mailadres wanneer ze zich abonneert op uw nieuwsbrief. Als u dit doet, wordt door streaming opname een nieuwe identiteit toegevoegd als recordgegevens in haar profiel. Dientengevolge, past de Dienst van de Identiteit nu de activiteit van het tabletapparaat van Mary met haar eCommerce rekeningsgeschiedenis.

Met de volgende klik op haar tablet zou uw doelinhoud het volledige profiel en de geschiedenis van Mary kunnen weerspiegelen, in plaats van slechts een tablet die door een onbekende winkelier wordt gebruikt.

De identiteitsrelaties die de Identiteitsservice definieert en onderhoudt, worden gebruikt door het Real-Time Klantprofiel om een volledig beeld van een klant en hun interactie met uw merk te bouwen. Zie het overzicht [van het profiel van de](../profile/home.md)real-time klant voor meer informatie.

### Identiteiten

Een identiteit is gegevens die uniek zijn voor een entiteit, doorgaans een individuele persoon. Een identiteit zoals een login identiteitskaart, ECID, of loyaliteitsidentiteitskaart wordt bedoeld als **bekende identiteit**.

PII, zoals e-mailadres en telefoonnummer, dient om een klant rechtstreeks te identificeren. Als gevolg hiervan wordt PII gebruikt om de verschillende identiteiten van een klant op verschillende systemen af te stemmen.

**Onbekende of anonieme identiteiten** wijzen een apparaat uit zonder de werkelijke persoon te identificeren die het gebruikt. Deze categorie bevat informatie zoals het IP-adres en de cookie-id van een bezoeker. Terwijl gedragsgegevens van een apparaat kunnen worden verzameld gebruikend onbekende identiteiten, associating deze identiteiten over apparaten of media is beperkt tot uw klant PII tijdens hun reis levert.

Zoals in de onderstaande afbeelding wordt getoond, zijn bekende en anonieme identiteiten beide belangrijke componenten van [identiteitsgrafieken](#identity-graphs), die later in dit document worden besproken.

![Identiteitskoppelen op platform](./images/identity-service-stitching.png)

Voorbeelden van implementaties voor identiteitsservices zijn:

- Een telecombedrijf kan zich op de waarde van het &quot;telefoonaantal&quot;baseren, waar een telefoonaantal naar het zelfde individu van belang in zowel off-line als online gegevensreeksen zou verwijzen.
- Een detailhandelsbedrijf kan &quot;e-mailadres&quot; in offlinegegevenssets en ECID in online gegevenssets gebruiken vanwege het hoge percentage anonieme bezoekers.
- Een bank geeft mogelijk de voorkeur aan &quot;rekeningnummer&quot; in offlinegegevenssets, zoals filiaaltransacties. Ze kunnen afhankelijk zijn van de &#39;inlognaam&#39; in online gegevenssets, omdat de meeste bezoekers tijdens hun bezoek zouden worden geverifieerd.
- Uw klanten kunnen unieke merkgebonden IDs, zoals GUID of andere universeel unieke herkenningstekens ook hebben.

### Identiteitsgegevens

Als je iemand vraagt: &quot;Wat is je id?&quot; zonder verdere context zou het voor hen moeilijk zijn een nuttig antwoord te geven . Door dezelfde logica is een tekenreekswaarde die een identiteitswaarde vertegenwoordigt, of het nu een door het systeem gegenereerde id of een e-mailadres is, alleen compleet wanneer deze wordt geleverd met een kwalificatie die de context van de tekenreekswaarde geeft: de naamruimte identity.

## Naamruimten en identiteitsgrafieken

Uw klanten kunnen met uw merk door een combinatie online en off-line kanalen in wisselwerking staan, resulterend in de uitdaging van hoe te om die gefragmenteerde interactie in één enkele klantenidentiteit te verzoenen.

Het Platform van de ervaring richt deze uitdaging door twee concepten: Naamruimten voor [identiteiten](#identity-namespaces) en [identiteitsgrafieken](#identity-graphs).

### Identiteitsnaamruimten

Wanneer uw klant met uw merk op veelvoudige kanalen met inbegrip van Web, mobiele toepassing, callcenter, of een opslag communiceert, kan het moeilijk zijn om hen te begrijpen en te dienen als u hun activiteit over kanalen niet kunt waarnemen en volgen.

Begrijpen van uw klant op meerdere apparaten en kanalen begint door hen in elk kanaal te erkennen. Adobe Experience Platform kan dit bereiken door naamruimten te gebruiken.
Een naamruimte van een identiteit is een id, zoals een apparaat-id of e-mailid, die wordt gebruikt om de context op te geven waaruit gegevens afkomstig zijn. Identiteitsnaamruimten worden gebruikt om individuele identiteiten op te zoeken of te koppelen, en context voor identiteitswaarden te verstrekken om gegevensbotsingen te verhinderen. Id &quot;123456&quot; kan bijvoorbeeld verwijzen naar één persoon in uw eCommerce-systeem en naar een andere persoon in uw helpdesksysteem. Zie het overzicht [van naamruimte voor](./namespaces.md)identiteiten voor meer informatie.

### Identiteitsgrafieken

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteitsnamespaces, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.

Alle grafieken van de klantenidentiteit worden collectief beheerd en door de Dienst van de Identiteit in bijna real time bijgewerkt, in antwoord op klantenactiviteit.

De Dienst van de identiteit beheert een identiteitsgrafiek die door slechts uw organisatie zichtbaar is en die op uw gegevens wordt gebouwd, die als privé grafiek wordt bedoeld. De Dienst van de identiteit vergroot uw privé grafiek wanneer een ingebed gegevensverslag meer dan één identiteit bevat, toevoegend een verhouding tussen de gevonden identiteiten.

Als voorbeeld van de mogelijke typen factoren die in overweging moeten worden genomen bij het leveren en etiketteren van identiteitsgegevens, kan het gebruik van telefoonnummers zoals &quot;werktelefoon&quot; leiden tot meer relaties dan u in de identiteitsgrafiek wilt. Veel werknemers verwijzen naar hetzelfde aantal voor het werk en dat &quot;thuis&quot; en &quot;mobiel&quot; beter geschikt zijn om relaties zo nauwkeurig mogelijk te houden.

## Identiteitsgegevens leveren aan Identity Service

In deze sectie wordt beschreven hoe gegevens die aan het Adobe Experience Platform worden verstrekt, worden verwerkt voordat ze door Identity Service worden gebruikt om een identiteitsgrafiek voor elke klant samen te stellen.

### Beslissen over identiteitsvelden

Afhankelijk van uw strategie van de de gegevensinzameling van ondernemingsgegevens, bepalen de gegevensgebieden u als identiteiten etiketteert welke gegevens in uw identiteitskaart inbegrepen zijn. Als u optimaal wilt profiteren van het Adobe Experience Platform en de meest uitgebreide klantenidentiteiten die mogelijk zijn, moet u zowel online als offline gegevens uploaden.

- Onlinegegevens zijn gegevens die de online aanwezigheid en het gedrag beschrijven, zoals gebruikersnamen en e-mailadressen.

- Offlinegegevens hebben betrekking op gegevens die niet rechtstreeks verband houden met online aanwezigheid, zoals id&#39;s van CRM-systemen. Dit type gegevens maakt uw identiteiten robuuster en steunt gegevenscohesie over uw verschillende systemen.

### Extra naamruimten maken

Terwijl het Platform van de Ervaring een verscheidenheid van standaardnamespaces aanbiedt, kunt u extra namespaces moeten creëren om uw identiteiten behoorlijk te categoriseren. Zie de sectie over het [weergeven en maken van naamruimten voor uw organisatie](./namespaces.md) in het overzicht van naamruimte voor identiteiten voor meer informatie.

>[!NOTE] Naamruimten zijn een kwalificatie voor identiteiten. Als er eenmaal een naamruimte is gemaakt, kan deze daarom niet worden verwijderd.

### Identiteitsgegevens opnemen in XDM (Experience Data Model)

Als gestandaardiseerd kader waardoor Platform klantengegevens organiseert, laat het Model van de Gegevens van de Ervaring (XDM) gegevens toe om over het Platform van de Ervaring en andere diensten worden gedeeld en worden begrepen die met Platform in wisselwerking staan. Zie het [XDM System-overzicht](../xdm/home.md)voor meer informatie.

Zowel de verslagen als de tijdreeksregelingen verstrekken de middelen om identiteitsgegevens te omvatten. Terwijl gegevens worden opgenomen, maakt de identiteitsgrafiek nieuwe relaties tussen gegevensfragmenten van verschillende naamruimten als deze gemeenschappelijke identiteitsgegevens delen.

### XDM-velden als identiteit markeren

Om het even welk gebied van type `string` in schema&#39;s die of verslag of tijdreeks XDM klassen uitvoeren kan als identiteitsgebied worden geëtiketteerd. Als gevolg hiervan worden alle gegevens die in dat veld worden ingevoerd, beschouwd als identiteitsgegevens.

Identiteitsvelden maken het ook mogelijk om identiteiten te koppelen als ze gemeenschappelijke PII-gegevens delen.
Bijvoorbeeld, door de gebieden van het telefoonaantal als identiteitsgebieden te etiketteren, grafiekt de Dienst van de Identiteit automatisch relaties met de andere individuen die worden gevonden om het zelfde telefoonaantal te gebruiken.

>[!NOTE] De naamruimte van resulterende identiteiten wordt opgegeven op het moment dat het veld wordt gelabeld.

### Een dataset voor Identiteitsservice configureren

Tijdens het streamingingingproces extraheert de Identiteitsservice automatisch identiteitsgegevens uit record- en tijdreeksgegevens. Nochtans, alvorens de gegevens kunnen worden opgenomen, moet het voor de Dienst van de Identiteit worden toegelaten. Zie de zelfstudie over het [configureren van een gegevensset voor realtime profiel en identiteitsservice van klanten die API&#39;s](../profile/tutorials/dataset-configuration.md) gebruiken voor meer informatie.

### Gegevens opnemen naar Identity Service

De Dienst van de identiteit verbruikt XDM volgzame gegevens die naar het Platform van de Ervaring worden verzonden door [partijingestitie](../ingestion/batch-ingestion/overview.md) of [streaming opname](../ingestion/streaming-ingestion/overview.md).

## Gegevensbeheer

Het Adobe Experience Platform is gemaakt met het oog op privacy en bevat een raamwerk voor gegevensbeheer ter bescherming van PII-gegevens van uw klanten. Identiteitsgegevens in de naamruimte &quot;email&quot; of &quot;phone&quot; zijn standaard gecodeerd, maar om ervoor te zorgen dat vertrouwelijke gegevens worden gecodeerd voordat deze worden voortgezet, kunnen labels voor gegevensgebruik worden toegepast op gegevens die worden ingevoerd of zodra deze worden ontvangen in Platform. Lees voor meer informatie het [Data Governance-overzicht](../data-governance/home.md).

## Volgende stappen

Nu u de belangrijkste concepten van de Dienst van de Identiteit en zijn rol binnen het Platform van de Ervaring begrijpt, kunt u beginnen te leren hoe te met uw identiteitsgrafiek te werken gebruikend de [Dienst API](./api/getting-started.md)van de Identiteit.