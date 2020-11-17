---
keywords: Experience Platform;home;popular topics;identity;Identity;XDM graphs;identity service;Identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.
translation-type: tm+mt
source-git-commit: af7eab0599b17be55d5a4c129f7ebaeba91333bc
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 0%

---


# [!DNL Identity Service] - overzicht

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen. Adobe Experience Platform [!DNL Identity Service] helpt u om een beter beeld te krijgen van uw klant en van hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

## [!DNL Identity Service] begrijpen

Elke dag, interactie van klanten met uw zaken en vestigen een onophoudelijk groeiende verhouding met uw merk. Een typische klant kan in om het even welk aantal systemen binnen de gegevensinfrastructuur van uw organisatie, zoals uw eCommerce, loyaliteit, en helpdesksystemen actief zijn. Die zelfde klant kan ook anoniem op om het even welk aantal apparaten in dienst nemen. [!DNL Identity Service] kunt u een volledig beeld van uw klant samenstellen, waarbij gerelateerde gegevens worden samengevoegd die anders over verschillende systemen zouden kunnen worden verspreid.

Bekijk een dagelijks voorbeeld van de relatie van een consument met je merk:

Mary heeft een account op je eCommerce-site waar ze in het verleden een paar bestellingen heeft gedaan. Ze gebruikt doorgaans haar persoonlijke laptop om te winkelen, waar ze zich telkens aanmeldt. Tijdens een van haar bezoeken gebruikt ze haar tablet echter om te winkelen op sandalen, maar ze plaatst geen bestelling en meldt zich niet aan.

Op dit punt wordt de activiteit van Mary weergegeven als twee aparte profielen: haar eCommerce-aanmelding en haar tablet-pc, mogelijk geïdentificeerd door apparaat-id.

Mary hervat later haar tabletsessie en stuurt haar e-mailadres wanneer ze zich abonneert op uw nieuwsbrief. Als u dit doet, wordt door streaming opname een nieuwe identiteit toegevoegd als recordgegevens in haar profiel. Dientengevolge, verhoudt [!DNL Identity Service] nu Mary&#39;s tabletapparatenactiviteit met haar eCommerce rekeningsgeschiedenis.

Met de volgende klik op haar tablet zou uw doelinhoud het volledige profiel en de geschiedenis van Mary kunnen weerspiegelen, in plaats van slechts een tablet die door een onbekende winkelier wordt gebruikt.

De identiteitsrelaties die [!DNL Identity Service] definiëren en onderhouden, worden benut door een volledig beeld van een klant en hun interactie met uw merk [!DNL Real-time Customer Profile] te maken. Zie het overzicht [van het profiel van de](../profile/home.md)real-time klant voor meer informatie.

### Identiteiten

Een identiteit is gegevens die uniek zijn voor een entiteit, doorgaans een individuele persoon. Een identiteit zoals een login identiteitskaart, ECID, of loyaliteitsidentiteitskaart wordt bedoeld als bekende identiteit.

PII, zoals e-mailadres en telefoonnummer, dient om een klant rechtstreeks te identificeren. Als gevolg hiervan wordt PII gebruikt om de verschillende identiteiten van een klant op verschillende systemen af te stemmen.

Onbekende of anonieme identiteiten wijzen een apparaat uit zonder de werkelijke persoon te identificeren die het gebruikt. Deze categorie bevat informatie zoals het IP-adres en de cookie-id van een bezoeker. Terwijl gedragsgegevens van een apparaat kunnen worden verzameld gebruikend onbekende identiteiten, associating deze identiteiten over apparaten of media is beperkt tot uw klant PII tijdens hun reis levert.

Zoals in de onderstaande afbeelding wordt getoond, zijn bekende en anonieme identiteiten beide belangrijke componenten van [identiteitsgrafieken](#identity-graphs), die later in dit document worden besproken.

![Identiteitskoppeling op Platform](./images/identity-service-stitching.png)

Voorbeelden van [!DNL Identity Service] implementaties zijn:

- Een telecombedrijf kan zich op de waarde van het &quot;telefoonaantal&quot;baseren, waar een telefoonaantal naar het zelfde individu van belang in zowel off-line als online gegevensreeksen zou verwijzen.
- Een detailhandelsbedrijf kan &quot;e-mailadres&quot; in offlinegegevenssets en ECID in online gegevenssets gebruiken vanwege het hoge percentage anonieme bezoekers.
- Een bank geeft mogelijk de voorkeur aan &quot;rekeningnummer&quot; in offlinegegevenssets, zoals filiaaltransacties. Ze kunnen afhankelijk zijn van de &#39;inlognaam&#39; in online gegevenssets, omdat de meeste bezoekers tijdens hun bezoek zouden worden geverifieerd.
- Uw klanten kunnen unieke merkgebonden IDs, zoals GUID of andere universeel unieke herkenningstekens ook hebben.

### Identiteitsgegevens

Als je iemand vraagt: &quot;Wat is je id?&quot; zonder verdere context zou het voor hen moeilijk zijn een nuttig antwoord te geven . Door dezelfde logica is een tekenreekswaarde die een identiteitswaarde vertegenwoordigt, of het nu een door het systeem gegenereerde id of een e-mailadres is, alleen compleet wanneer deze wordt geleverd met een kwalificatie die de context van de tekenreekswaarde geeft: de naamruimte identity.

## Naamruimten en identiteitsgrafieken

Uw klanten kunnen met uw merk door een combinatie online en off-line kanalen in wisselwerking staan, resulterend in de uitdaging van hoe te om die gefragmenteerde interactie in één enkele klantenidentiteit te verzoenen.

[!DNL Experience Platform] Deze uitdaging wordt aangegaan door twee concepten: [naamruimten](#identity-namespaces) en [identiteitsgrafieken](#identity-graphs).

De volgende video is bedoeld als ondersteuning voor uw begrip van identiteiten en identiteitsgrafieken. De volgende video behandelt de drie mogelijkheden van de Inzameling van de Identiteit, de Grafieken van de Identiteit, en APIs. Het beschrijft ook hoe deterministische en probabilistische algoritmen worden gebruikt om privé identiteitsgrafieken te construeren, en bespreekt de rol van privé identiteitsgrafieken, de CoOp Grafiek van de Dienst van de Identiteit van Adobe Experience Platform, en derdegrafieken.

>[!IMPORTANT]
>
> Probabilistische privégrafieken zijn nog in ontwikkeling en worden later gepubliceerd.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Identiteitsnaamruimten

Wanneer uw klant met uw merk op veelvoudige kanalen met inbegrip van Web, mobiele toepassing, callcenter, of een opslag communiceert, kan het moeilijk zijn om hen te begrijpen en te dienen als u hun activiteit over kanalen niet kunt waarnemen en volgen.

Begrijpen van uw klant op meerdere apparaten en kanalen begint door hen in elk kanaal te erkennen. Adobe Experience Platform bereikt dit door naamruimten te gebruiken.
Een naamruimte van een identiteit is een id, zoals een apparaat-id of e-mailid, die wordt gebruikt om de context op te geven waaruit gegevens afkomstig zijn. Identiteitsnaamruimten worden gebruikt om individuele identiteiten op te zoeken of te koppelen, en context voor identiteitswaarden te verstrekken om gegevensbotsingen te verhinderen. Id &quot;123456&quot; kan bijvoorbeeld verwijzen naar één persoon in uw eCommerce-systeem en naar een andere persoon in uw helpdesksysteem. Zie het overzicht [van naamruimte voor](./namespaces.md)identiteiten voor meer informatie.

### Identiteitsgrafieken

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteitsnamespaces, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.

Alle grafieken van de klantenidentiteit worden collectief beheerd en bijgewerkt door [!DNL Identity Service] in bijna real time, in antwoord op klantenactiviteit.

[!DNL Identity Service] beheert een identiteitsgrafiek zichtbaar door slechts uw organisatie en gebouwd die op uw gegevens wordt gebouwd, die als privé grafiek wordt bedoeld. [!DNL Identity Service] Hiermee vergroot u de persoonlijke grafiek wanneer een opgenomen gegevensrecord meer dan één identiteit bevat, waardoor een relatie tussen de gevonden identiteiten wordt toegevoegd.

Als voorbeeld van de mogelijke typen factoren die in overweging moeten worden genomen bij het leveren en etiketteren van identiteitsgegevens, kan het gebruik van telefoonnummers zoals &quot;werktelefoon&quot; leiden tot meer relaties dan u in de identiteitsgrafiek wilt. Veel werknemers verwijzen naar hetzelfde aantal voor het werk en dat &quot;thuis&quot; en &quot;mobiel&quot; beter geschikt zijn om relaties zo nauwkeurig mogelijk te houden.

Zie de zelfstudie over het [openen van de viewer voor identiteitsgrafieken voor meer informatie](./ui/identity-graph-viewer.md)

## Identiteitsgegevens leveren aan [!DNL Identity Service]

In deze sectie wordt beschreven hoe aan Adobe Experience Platform verstrekte gegevens worden verwerkt voordat ze worden gebruikt om een identiteitsgrafiek voor elke klant [!DNL Identity Service] te maken.

### Beslissen over identiteitsvelden

Afhankelijk van uw strategie van de de gegevensinzameling van ondernemingsgegevens, bepalen de gegevensgebieden u als identiteiten etiketteert welke gegevens in uw identiteitskaart inbegrepen zijn. Als u het maximale voordeel van Adobe Experience Platform en de meest uitgebreide klantidentiteiten wilt benutten, moet u zowel online als offline gegevens uploaden.

- Onlinegegevens zijn gegevens die de online aanwezigheid en het gedrag beschrijven, zoals gebruikersnamen en e-mailadressen.

- Offlinegegevens hebben betrekking op gegevens die niet rechtstreeks verband houden met online aanwezigheid, zoals id&#39;s van CRM-systemen. Dit type gegevens maakt uw identiteiten robuuster en steunt gegevenscohesie over uw verschillende systemen.

### Extra naamruimten maken

Hoewel u verschillende standaardnaamruimten [!DNL Experience Platform] biedt, moet u mogelijk extra naamruimten maken om uw identiteiten correct te categoriseren. Zie de sectie over het [weergeven en maken van naamruimten voor uw organisatie](./namespaces.md) in het overzicht van naamruimte voor identiteiten voor meer informatie.

>[!NOTE]
>
>Naamruimten zijn een kwalificatie voor identiteiten. Als er eenmaal een naamruimte is gemaakt, kan deze daarom niet worden verwijderd.

### Inclusief identiteitsgegevens in [!DNL Experience Data Model] (XDM)

Als gestandaardiseerd kader waardoor [!DNL Platform] klantengegevens worden georganiseerd, [!DNL Experience Data Model] (XDM) staat gegevens toe om over [!DNL Experience Platform] en andere diensten worden gedeeld en worden begrepen die met [!DNL Platform]. Zie het [XDM-systeemoverzicht](../xdm/home.md)voor meer informatie.

Zowel de verslagen als de tijdreeksregelingen verstrekken de middelen om identiteitsgegevens te omvatten. Terwijl gegevens worden opgenomen, maakt de identiteitsgrafiek nieuwe relaties tussen gegevensfragmenten van verschillende naamruimten als deze gemeenschappelijke identiteitsgegevens delen.

### XDM-velden als identiteit markeren

Om het even welk gebied van type `string` in schema&#39;s die of verslag of tijdreeks XDM klassen uitvoeren kan als identiteitsgebied worden geëtiketteerd. Als gevolg hiervan worden alle gegevens die in dat veld worden ingevoerd, beschouwd als identiteitsgegevens.

Identiteitsvelden maken het ook mogelijk om identiteiten te koppelen als ze gemeenschappelijke PII-gegevens delen.
Bijvoorbeeld, door de gebieden van het telefoonaantal als identiteitsgebieden te etiketteren, [!DNL Identity Service] grafiekt automatisch relaties met de andere individuen die worden gevonden om het zelfde telefoonaantal te gebruiken.

>[!NOTE]
>
>De naamruimte van resulterende identiteiten wordt opgegeven op het moment dat het veld wordt gelabeld.

### Een gegevensset configureren voor [!DNL Identity Service]

Tijdens het streamingingingproces extraheert u [!DNL Identity Service ]automatisch identiteitsgegevens uit record- en tijdreeksgegevens. Maar voordat gegevens kunnen worden ingevoerd, moet deze zijn ingeschakeld voor [!DNL Identity Service]. Zie de zelfstudie over het [configureren van een gegevensset voor realtime profiel en identiteitsservice van klanten die API&#39;s](../profile/tutorials/dataset-configuration.md) gebruiken voor meer informatie.

### Gegevens samenvoegen tot [!DNL Identity Service]

[!DNL Identity Service] verbruikt XDM-compatibele gegevens die naar [!DNL Experience Platform] batch-opname [of](../ingestion/batch-ingestion/overview.md) streaming-opname [](../ingestion/streaming-ingestion/overview.md)worden verzonden.

De volgende video is bedoeld om uw begrip van de Dienst van de Identiteit te steunen. In deze video ziet u hoe u gegevensvelden kunt labelen als identiteiten, identiteitsgegevens kunt invoeren en vervolgens kunt controleren of de gegevens zijn omgezet in de persoonlijke grafiek van de Adobe Experience Platform Identity Service.

>[!WARNING]
>
>De [!DNL Platform] UI die in de volgende video wordt getoond is verouderd. Raadpleeg de documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Gegevensbeheer

Adobe Experience Platform is gemaakt met het oog op privacy en bevat een gegevensbeheerframework om PII-gegevens van uw klanten te beschermen. Identiteitsgegevens onder de naamruimte &quot;email&quot; of &quot;phone&quot; worden standaard gecodeerd, maar om ervoor te zorgen dat vertrouwelijke gegevens worden gecodeerd voordat deze worden voortgezet, kunnen labels voor gegevensgebruik worden toegepast op gegevens die worden ingevoerd of zodra deze worden binnengebracht [!DNL Platform]. Lees voor meer informatie het [Data Governance-overzicht](../data-governance/home.md).

## Volgende stappen

Nu u de belangrijkste concepten van [!DNL Identity Service] en zijn rol binnen begrijpt, kunt u beginnen te leren hoe te met uw identiteitsgrafiek te werken gebruikend [!DNL Experience Platform][[!DNL Identity Service API]](./api/getting-started.md).
