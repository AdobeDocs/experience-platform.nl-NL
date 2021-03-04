---
keywords: Experience Platform;home;populaire onderwerpen;identiteit;Identiteit;XDM grafieken;Identiteitsservice;Identiteitsservice
solution: Experience Platform
title: Overzicht van identiteitsservice
topic: ' - overzicht'
description: Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1733'
ht-degree: 0%

---


# [!DNL Identity Service] - overzicht

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen. Met Adobe Experience Platform [!DNL Identity Service] kunt u een beter beeld krijgen van uw klant en zijn gedrag door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

## [!DNL Identity Service] begrijpen

Elke dag, interactie van klanten met uw zaken en vestigen een onophoudelijk groeiende verhouding met uw merk. Een typische klant kan in om het even welk aantal systemen binnen de gegevensinfrastructuur van uw organisatie, zoals uw eCommerce, loyaliteit, en helpdesksystemen actief zijn. Die zelfde klant kan ook anoniem op om het even welk aantal apparaten in dienst nemen. [!DNL Identity Service] kunt u een volledig beeld van uw klant samenstellen, waarbij gerelateerde gegevens worden samengevoegd die anders over verschillende systemen zouden kunnen worden verspreid.

Bekijk een dagelijks voorbeeld van de relatie van een consument met je merk:

Mary heeft een account op je eCommerce-site waar ze in het verleden een paar bestellingen heeft gedaan. Ze gebruikt doorgaans haar persoonlijke laptop om te winkelen, waar ze zich telkens aanmeldt. Tijdens een van haar bezoeken gebruikt ze haar tablet echter om te winkelen op sandalen, maar ze plaatst geen bestelling en meldt zich niet aan.

Op dit punt wordt de activiteit van Mary weergegeven als twee aparte profielen: haar eCommerce-aanmelding en haar tablet-pc, mogelijk geïdentificeerd door apparaat-id.

Mary hervat later haar tabletsessie en stuurt haar e-mailadres wanneer ze zich abonneert op uw nieuwsbrief. Als u dit doet, wordt door streaming opname een nieuwe identiteit toegevoegd als recordgegevens in haar profiel. Als gevolg hiervan koppelt [!DNL Identity Service] nu de tabletapparaatactiviteit van Mary aan haar eCommerce-accountgeschiedenis.

Met de volgende klik op haar tablet zou uw doelinhoud het volledige profiel en de geschiedenis van Mary kunnen weerspiegelen, in plaats van slechts een tablet die door een onbekende winkelier wordt gebruikt.

De identiteitsrelaties die [!DNL Identity Service] definieert en onderhoudt, worden gebruikt door [!DNL Real-time Customer Profile] om een volledig beeld van een klant en hun interactie met uw merk te bouwen. Voor meer informatie, zie [Overzicht van het Profiel van de Klant in real time](../profile/home.md).

### Identiteiten

Een identiteit is gegevens die uniek zijn voor een entiteit, doorgaans een individuele persoon. Een identiteit zoals een login identiteitskaart, ECID, of loyaliteitsidentiteitskaart wordt bedoeld als bekende identiteit.

PII, zoals e-mailadres en telefoonnummer, dient om een klant rechtstreeks te identificeren. Als gevolg hiervan wordt PII gebruikt om de verschillende identiteiten van een klant op verschillende systemen af te stemmen.

Onbekende of anonieme identiteiten wijzen een apparaat uit zonder de werkelijke persoon te identificeren die het gebruikt. Deze categorie bevat informatie zoals het IP-adres en de cookie-id van een bezoeker. Terwijl gedragsgegevens van een apparaat kunnen worden verzameld gebruikend onbekende identiteiten, associating deze identiteiten over apparaten of media is beperkt tot uw klant PII tijdens hun reis levert.

Zoals in de afbeelding hieronder wordt getoond, zijn bekende en anonieme identiteiten beide belangrijke componenten van [identiteitsgrafieken](#identity-graphs), die later in dit document worden besproken.

![Identiteitskoppeling op Platform](./images/identity-service-stitching.png)

Voorbeelden van [!DNL Identity Service]-implementaties zijn:

- Een telecombedrijf kan zich op de waarde van het &quot;telefoonaantal&quot;baseren, waar een telefoonaantal naar het zelfde individu van belang in zowel off-line als online gegevensreeksen zou verwijzen.
- Een detailhandelsbedrijf kan &quot;e-mailadres&quot; in offlinegegevenssets en ECID in online gegevenssets gebruiken vanwege het hoge percentage anonieme bezoekers.
- Een bank geeft mogelijk de voorkeur aan &quot;rekeningnummer&quot; in offlinegegevenssets, zoals filiaaltransacties. Ze kunnen afhankelijk zijn van de &#39;inlognaam&#39; in online gegevenssets, omdat de meeste bezoekers tijdens hun bezoek zouden worden geverifieerd.
- Uw klanten kunnen unieke merkgebonden IDs, zoals GUID of andere universeel unieke herkenningstekens ook hebben.

### Identiteitsgegevens

Als je iemand vraagt: &quot;Wat is je id?&quot; zonder verdere context zou het voor hen moeilijk zijn een nuttig antwoord te geven . Door dezelfde logica is een tekenreekswaarde die een identiteitswaarde vertegenwoordigt, of het nu een door het systeem gegenereerde id of een e-mailadres is, alleen compleet wanneer deze wordt geleverd met een kwalificatie die de context van de tekenreekswaarde geeft: de naamruimte identity.

## Naamruimten en identiteitsgrafieken

Uw klanten kunnen met uw merk door een combinatie online en off-line kanalen in wisselwerking staan, resulterend in de uitdaging van hoe te om die gefragmenteerde interactie in één enkele klantenidentiteit te verzoenen.

[!DNL Experience Platform] Deze uitdaging wordt aangegaan door twee concepten:  [naamruimten ](#identity-namespaces) van identiteiten en  [identiteitsgrafieken](#identity-graphs).

De volgende video is bedoeld als ondersteuning voor uw begrip van identiteiten en identiteitsgrafieken. De volgende video behandelt de drie mogelijkheden van de Inzameling van de Identiteit, de Grafieken van de Identiteit, en APIs. Het beschrijft ook hoe deterministische en probabilistische algoritmen worden gebruikt om privé identiteitsgrafieken te construeren, en bespreekt de rol van privé identiteitsgrafieken, de CoOp Grafiek van de Dienst van de Identiteit van Adobe Experience Platform, en derdegrafieken.

>[!IMPORTANT]
>
> Probabilistische privégrafieken zijn nog in ontwikkeling en worden later gepubliceerd.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Identiteitsnaamruimten

Wanneer uw klant met uw merk op veelvoudige kanalen met inbegrip van Web, mobiele toepassing, callcenter, of een opslag communiceert, kan het moeilijk zijn om hen te begrijpen en te dienen als u hun activiteit over kanalen niet kunt waarnemen en volgen.

Begrijpen van uw klant op meerdere apparaten en kanalen begint door hen in elk kanaal te erkennen. Adobe Experience Platform bereikt dit door naamruimten te gebruiken.
Een naamruimte van een identiteit is een id, zoals een apparaat-id of e-mailid, die wordt gebruikt om de context op te geven waaruit gegevens afkomstig zijn. Identiteitsnaamruimten worden gebruikt om individuele identiteiten op te zoeken of te koppelen, en context voor identiteitswaarden te verstrekken om gegevensbotsingen te verhinderen. Id &quot;123456&quot; kan bijvoorbeeld verwijzen naar één persoon in uw eCommerce-systeem en naar een andere persoon in uw helpdesksysteem. Zie [Naamruimte overzicht](./namespaces.md) voor meer informatie.

### Identiteitsgrafieken

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteitsnamespaces, die u van een visuele vertegenwoordiging van voorziet hoe uw klant met uw merk over verschillende kanalen interactie aangaat.

Alle identiteitsgrafieken van klanten worden gezamenlijk beheerd en bijgewerkt door [!DNL Identity Service] in bijna real-time, als reactie op klantactiviteiten.

[!DNL Identity Service] beheert een identiteitsgrafiek zichtbaar door slechts uw organisatie en gebouwd die op uw gegevens wordt gebouwd, die als privé grafiek wordt bedoeld. [!DNL Identity Service] Hiermee vergroot u de persoonlijke grafiek wanneer een opgenomen gegevensrecord meer dan één identiteit bevat, waardoor een relatie tussen de gevonden identiteiten wordt toegevoegd.

Als voorbeeld van de mogelijke typen factoren die in overweging moeten worden genomen bij het leveren en etiketteren van identiteitsgegevens, kan het gebruik van telefoonnummers zoals &quot;werktelefoon&quot; leiden tot meer relaties dan u in de identiteitsgrafiek wilt. Veel werknemers verwijzen naar hetzelfde aantal voor het werk en dat &quot;thuis&quot; en &quot;mobiel&quot; beter geschikt zijn om relaties zo nauwkeurig mogelijk te houden.

Zie de zelfstudie over [toegang tot de viewer voor identiteitsgrafieken](./ui/identity-graph-viewer.md) voor meer informatie

## Identiteitsgegevens opgeven voor [!DNL Identity Service]

In deze sectie wordt beschreven hoe gegevens die aan Adobe Experience Platform worden verstrekt, worden verwerkt voordat ze door [!DNL Identity Service] worden gebruikt om een identiteitsgrafiek voor elke klant te maken.

### Beslissen over identiteitsvelden

Afhankelijk van uw strategie van de de gegevensinzameling van ondernemingsgegevens, bepalen de gegevensgebieden u als identiteiten etiketteert welke gegevens in uw identiteitskaart inbegrepen zijn. Als u het maximale voordeel van Adobe Experience Platform en de meest uitgebreide klantidentiteiten wilt benutten, moet u zowel online als offline gegevens uploaden.

- Onlinegegevens zijn gegevens die de online aanwezigheid en het gedrag beschrijven, zoals gebruikersnamen en e-mailadressen.

- Offlinegegevens hebben betrekking op gegevens die niet rechtstreeks verband houden met online aanwezigheid, zoals id&#39;s van CRM-systemen. Dit type gegevens maakt uw identiteiten robuuster en steunt gegevenscohesie over uw verschillende systemen.

### Extra naamruimten maken

Hoewel [!DNL Experience Platform] een verscheidenheid van standaardnamespaces aanbiedt, kunt u extra namespaces moeten creëren om uw identiteiten behoorlijk te categoriseren. Zie de sectie over [het weergeven en maken van naamruimten voor uw organisatie](./namespaces.md) in het overzicht van naamruimte voor identiteiten voor meer informatie.

>[!NOTE]
>
>Naamruimten zijn een kwalificatie voor identiteiten. Als er eenmaal een naamruimte is gemaakt, kan deze daarom niet worden verwijderd.

### Inclusief identiteitsgegevens in [!DNL Experience Data Model] (XDM)

Als gestandaardiseerd kader waarmee [!DNL Platform] klantgegevens ordent, [!DNL Experience Data Model] (XDM) staat toe dat gegevens worden gedeeld en begrepen over [!DNL Experience Platform] en andere diensten die met [!DNL Platform] in wisselwerking staan. Zie [XDM System overview](../xdm/home.md) voor meer informatie.

Zowel de verslagen als de tijdreeksregelingen verstrekken de middelen om identiteitsgegevens te omvatten. Terwijl gegevens worden opgenomen, maakt de identiteitsgrafiek nieuwe relaties tussen gegevensfragmenten van verschillende naamruimten als deze gemeenschappelijke identiteitsgegevens delen.

### XDM-velden als identiteit markeren

Om het even welk gebied van type `string` in schema&#39;s die of verslag of tijdreeks XDM klassen uitvoeren kan als identiteitsgebied worden geëtiketteerd. Als gevolg hiervan worden alle gegevens die in dat veld worden ingevoerd, beschouwd als identiteitsgegevens.

Identiteitsvelden maken het ook mogelijk om identiteiten te koppelen als ze gemeenschappelijke PII-gegevens delen.
Bijvoorbeeld, door de gebieden van het telefoonaantal als identiteitsgebieden te etiketteren, [!DNL Identity Service] automatisch verhoudingen met de andere individuen die worden gevonden om het zelfde telefoonaantal te gebruiken.

>[!NOTE]
>
>De naamruimte van resulterende identiteiten wordt opgegeven op het moment dat het veld wordt gelabeld.

### Een gegevensset configureren voor [!DNL Identity Service]

Tijdens het streamingingingproces haalt [!DNL Identity Service ]automatisch identiteitsgegevens uit record- en tijdreeksgegevens. Maar voordat gegevens kunnen worden ingevoerd, moet [!DNL Identity Service] zijn ingeschakeld. Zie de zelfstudie over [het configureren van een gegevensset voor realtime klantprofiel en identiteitsservice met behulp van API&#39;s](../profile/tutorials/dataset-configuration.md) voor meer informatie.

### Gegevens opnemen in [!DNL Identity Service]

[!DNL Identity Service] verbruikt XDM-compatibele gegevens die naar  [!DNL Experience Platform] batch- [ingestionof ](../ingestion/batch-ingestion/overview.md) streaming opname [ ](../ingestion/streaming-ingestion/overview.md) worden verzonden.

De volgende video is bedoeld om uw begrip van de Dienst van de Identiteit te steunen. In deze video ziet u hoe u gegevensvelden kunt labelen als identiteiten, identiteitsgegevens kunt invoeren en vervolgens kunt controleren of de gegevens zijn omgezet in de persoonlijke grafiek van de Adobe Experience Platform Identity Service.

>[!WARNING]
>
>De interface [!DNL Platform] die in de volgende video wordt getoond is verouderd. Raadpleeg de documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Gegevensbeheer

Adobe Experience Platform is gemaakt met het oog op privacy en bevat een gegevensbeheerframework om PII-gegevens van uw klanten te beschermen. Identiteitsgegevens onder de naamruimte &quot;email&quot; of &quot;phone&quot; worden standaard gecodeerd, maar om ervoor te zorgen dat vertrouwelijke gegevens worden gecodeerd voordat deze worden voortgezet, kunnen labels voor gegevensgebruik worden toegepast op gegevens die worden ingevoerd of zodra deze worden ontvangen in [!DNL Platform]. Lees voor meer informatie het [Overzicht van gegevensbeheer](../data-governance/home.md).

## Volgende stappen

Nu u de belangrijkste concepten van [!DNL Identity Service] en zijn rol binnen [!DNL Experience Platform] begrijpt, kunt u beginnen te leren hoe te met uw identiteitsgrafiek te werken gebruikend [[!DNL Identity Service API]](./api/getting-started.md).
