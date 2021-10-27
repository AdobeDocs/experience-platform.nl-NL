---
keywords: Experience Platform;home;populaire onderwerpen;identiteit;Identiteit;XDM grafieken;Identiteitsservice;Identiteitsservice
solution: Experience Platform
title: Overzicht van identiteitsservice
topic-legacy: overview
description: Met de Adobe Experience Platform Identity Service kunt u uw klant en zijn gedrag beter zien door identiteiten tussen apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: eb0fe2267416c5053cb589cc6d147324cc31c985
workflow-type: tm+mt
source-wordcount: '1747'
ht-degree: 0%

---

# [!DNL Identity Service] - overzicht

Voor het aanbieden van relevante digitale ervaringen is een volledig begrip van uw klant vereist. Dit wordt bemoeilijkt wanneer uw klantengegevens over verschillende systemen worden gefragmenteerd, die elke individuele klant ertoe brengen om veelvoudige &quot;identiteiten&quot;te hebben te schijnen.

De Adobe Experience Platform Identity Service biedt u een uitgebreid overzicht van uw klanten en hun gedrag door identiteiten over apparaten en systemen te overbruggen, zodat u in real-time een indrukwekkende, persoonlijke digitale ervaring kunt bieden.

Met [!DNL Identity Service]kunt u:

- Zorg ervoor dat uw klanten door elke interactie een consistente, gepersonaliseerde en relevante ervaring ontvangen.
- U kunt verschillende verschillende identiteiten uit verschillende bronnen samenstellen en een uitgebreide weergave van uw klanten maken.
- Gebruik een identiteitsgrafiek om verschillende naamruimten in kaart te brengen, die u van een visuele vertegenwoordiging van voorziet hoe uw klanten met uw merk over verschillende kanalen interactie aangaan.

## Aan de slag

Voordat u in de details van [!DNL Identity Service]Hier volgt een korte samenvatting van de belangrijkste termen:

| Term | Definitie |
| --- | --- |
| Identiteit | Een identiteit is gegevens die uniek zijn voor een entiteit, doorgaans een individuele persoon. Een identiteit, zoals een login identiteitskaart, ECID, of loyaliteitsidentiteitskaart, wordt ook bedoeld als &quot;bekende identiteit&quot;. |
| ECID | Experience Cloud ID (ECID) is een naamruimte voor gedeelde identiteit die wordt gebruikt in Experience Platform- en Adobe Experience Cloud-toepassingen. ECID verstrekt een stichting voor klantenidentiteit en als primaire identiteitskaart voor apparaten en als basisknoop voor identiteitsgrafieken gebruikt. Zie de [ECID-overzicht](./ecid.md) voor meer informatie . |
| Naamruimte identiteit | Een naamruimte voor identiteiten maakt onderscheid tussen de context of het type van een identiteit. Een identiteit onderscheidt bijvoorbeeld &quot;name&quot;<span>@email.com&quot; als e-mailadres of &quot;443522&quot; als een numerieke CRM-id. Identiteitsnaamruimten worden gebruikt om individuele identiteiten op te zoeken en de context voor identiteitswaarden te verstrekken. Zo kunt u bepalen dat twee [!DNL Profile] fragmenten die verschillende primaire id&#39;s bevatten, maar dezelfde waarde voor de componenten `email` naamruimte van identiteit is in feite hetzelfde individu. Zie de [Overzicht van naamruimte in identiteit](./namespaces.md) voor meer informatie . |
| Identiteitsgrafiek | Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteiten, die u toestaan om te visualiseren en beter te begrijpen welke klantenidentiteiten samen worden vastgemaakt, en hoe. Zie de zelfstudie aan [de viewer voor identiteitsgrafieken gebruiken](./ui/identity-graph-viewer.md) voor meer informatie . |
| Persoonlijk identificeerbare informatie (PII) | PII is informatie die een klant, zoals een e-mailadres of een telefoonaantal direct kan identificeren. PII-waarden worden vaak gebruikt om overeen te komen. de meervoudige identiteit van een klant op verschillende systemen. |
| Onbekende of anonieme identiteiten | Onbekende of anonieme identiteiten zijn indicatoren die apparaten isoleren zonder de werkelijke persoon te identificeren die het apparaat gebruikt. Onbekende en anonieme identiteiten zijn onder andere het IP-adres en de cookie-id van een bezoeker. Hoewel onbekende en anonieme identiteiten gedragsgegevens kunnen verstrekken, zijn zij beperkt tot een klant hun PII levert. |

## Wat is [!DNL Identity Service]?

Elke dag, interactie van klanten met uw zaken en vestigen een onophoudelijk groeiende verhouding met uw merk. Een typische klant kan in om het even welk aantal systemen binnen de gegevensinfrastructuur van uw organisatie, zoals uw e-commerce, loyaliteit, en helpdesksystemen actief zijn. Die zelfde klant kan ook anoniem op om het even welk aantal apparaten in dienst nemen. [!DNL Identity Service] kunt u een volledig beeld van uw klant samenstellen, waarbij gerelateerde gegevens worden samengevoegd die anders over verschillende systemen zouden kunnen worden verspreid.

Bekijk een dagelijks voorbeeld van de relatie van een consument met je merk:

- Mary heeft een account op uw e-commercesite waar ze in het verleden een paar bestellingen heeft gedaan. Ze gebruikt doorgaans haar persoonlijke laptop om te winkelen, waar ze zich telkens aanmeldt. Tijdens een van haar bezoeken gebruikt ze haar tablet echter om te winkelen op sandalen, maar ze plaatst geen bestelling en meldt zich niet aan.
- Op dit punt wordt de activiteit van Mary weergegeven als twee aparte profielen:
   - Haar aanmelding voor e-commerce
   - Haar tabletapparaat, mogelijk geïdentificeerd door apparaat-id
- Mary hervat later haar tabletsessie en stuurt haar e-mailadres wanneer ze zich abonneert op uw nieuwsbrief. Als u dit doet, wordt door streaming opname een nieuwe identiteit toegevoegd als recordgegevens in haar profiel. Dientengevolge [!DNL Identity Service] relateert nu Mary&#39;s tabletapparaatactiviteit met haar e-commerce rekeninggeschiedenis.
- Met de volgende klik op haar tablet zou uw doelinhoud het volledige profiel en de geschiedenis van Mary kunnen weerspiegelen, in plaats van slechts een tablet die door een onbekende winkelier wordt gebruikt.

![Identiteitskoppeling op Platform](./images/identity-service-stitching.png)

Hoofdzakelijk [!DNL Identity Service] kunt u een volledig beeld van uw klant samenstellen, waarbij gerelateerde gegevens worden samengevoegd die anders over verschillende systemen zouden kunnen worden verspreid. De identiteitsrelaties die [!DNL Identity Service] definieert en onderhoudt, worden gebruikt door het Real-time Klantprofiel om een volledig beeld van een klant en hun interactie met uw merk te maken. Zie voor meer informatie de [Overzicht van het realtime klantprofiel](../profile/home.md).

### Gebruiksscenario’s

Voorbeelden van [!DNL Identity Service] de implementatie omvat :

- Een telecombedrijf kan zich op de waarde van het &quot;telefoonaantal&quot;baseren, waar een telefoonaantal naar het zelfde individu van belang in zowel off-line als online gegevensreeksen zou verwijzen.
- Een detailhandelsbedrijf kan &quot;e-mailadres&quot; in offlinegegevenssets en ECID in online gegevenssets gebruiken vanwege het hoge percentage anonieme bezoekers.
- Een bank geeft mogelijk de voorkeur aan &quot;rekeningnummer&quot; in offlinegegevenssets, zoals filiaaltransacties. Ze kunnen afhankelijk zijn van de &#39;inlognaam&#39; in online gegevenssets, omdat de meeste bezoekers tijdens hun bezoek zouden worden geverifieerd.
- Uw klanten kunnen unieke merkgebonden IDs, zoals GUID of andere universeel unieke herkenningstekens ook hebben.

## Identiteitsnaamruimten

Als je iemand vraagt: &quot;Wat is je id?&quot; zonder verdere context zou het voor hen moeilijk zijn een nuttig antwoord te geven . Door dezelfde logica is een tekenreekswaarde die een identiteitswaarde vertegenwoordigt, of het nu een door het systeem gegenereerde id of een e-mailadres is, alleen compleet wanneer deze wordt geleverd met een kwalificatie die de context van de tekenreekswaarde geeft: de naamruimte identity.


Uw klanten kunnen met uw merk door een combinatie online en off-line kanalen in wisselwerking staan, resulterend in de uitdaging van hoe te om die gefragmenteerde interactie in één enkele klantenidentiteit te verzoenen.

Begrijpen van uw klant op meerdere apparaten en kanalen begint door hen in elk kanaal te erkennen. Platform bereikt dit door naamruimten te gebruiken. Een naamruimte voor identiteit is een id, zoals E-mail of Telefoon, die wordt gebruikt om aanvullende context aan de identiteit van de klant te bieden. Identiteitsnaamruimten worden gebruikt om individuele identiteiten op te zoeken of te koppelen en context voor identiteitswaarden te verstrekken. Zie de [Overzicht van naamruimte in identiteit](./namespaces.md) voor meer informatie .

## Identiteitsgrafieken

Een identiteitsgrafiek is een kaart van verhoudingen tussen verschillende identiteitsnamespaces, toestaand u om te visualiseren en beter te begrijpen welke klantenidentiteiten samen, en hoe worden vastgemaakt. Zie de zelfstudie aan [de viewer voor identiteitsgrafieken gebruiken](./ui/identity-graph-viewer.md) voor meer informatie .

De volgende video is bedoeld als ondersteuning voor uw begrip van identiteiten en identiteitsgrafieken.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Identiteitsgegevens leveren aan [!DNL Identity Service]

In deze sectie wordt beschreven hoe aan Adobe Experience Platform verstrekte gegevens worden verwerkt voordat ze door [!DNL Identity Service] om een identiteitsgrafiek voor elke klant te bouwen.

### Beslissen over identiteitsvelden

Afhankelijk van uw strategie van de de gegevensinzameling van ondernemingsgegevens, bepalen de gegevensgebieden u als identiteiten etiketteert welke gegevens in uw identiteitskaart inbegrepen zijn. Als u het maximale voordeel van Adobe Experience Platform en de meest uitgebreide klantidentiteiten wilt benutten, moet u zowel online als offline gegevens uploaden.

- Onlinegegevens zijn gegevens die de online aanwezigheid en het gedrag beschrijven, zoals gebruikersnamen en e-mailadressen.

- Offlinegegevens hebben betrekking op gegevens die niet rechtstreeks verband houden met online aanwezigheid, zoals id&#39;s van CRM-systemen. Dit type gegevens maakt uw identiteiten robuuster en steunt gegevenscohesie over uw verschillende systemen.

### Extra naamruimten maken

Hoewel Experience Platform verschillende standaardnaamruimten biedt, moet u mogelijk extra naamruimten maken om uw identiteiten correct te categoriseren. Zie de sectie over [weergeven en maken van naamruimten voor uw organisatie](./namespaces.md) in het naamruimteoverzicht van de identiteit.

>[!NOTE]
>
>Naamruimten zijn een kwalificatie voor identiteiten. Als er eenmaal een naamruimte is gemaakt, kan deze daarom niet worden verwijderd.

### Identiteitsgegevens opnemen in [!DNL Experience Data Model] (XDM)

Als het gestandaardiseerde kader waardoor [!DNL Platform] klantgegevens ordent; [!DNL Experience Data Model] (XDM) staat gegevens toe om over Experience Platform en andere diensten worden gedeeld en worden begrepen die met interactie [!DNL Platform]. Zie voor meer informatie de [XDM System, overzicht](../xdm/home.md).

Zowel de verslagen als de tijdreeksregelingen verstrekken de middelen om identiteitsgegevens te omvatten. Terwijl gegevens worden opgenomen, maakt de identiteitsgrafiek nieuwe relaties tussen gegevensfragmenten van verschillende naamruimten als deze gemeenschappelijke identiteitsgegevens delen.

### XDM-velden als identiteit markeren

Willekeurig tekstveld `string` in schema&#39;s die of verslag of tijdreeks XDM klassen uitvoeren kunnen als identiteitsgebied worden geëtiketteerd. Als gevolg hiervan worden alle gegevens die in dat veld worden ingevoerd, beschouwd als identiteitsgegevens.

>[!NOTE]
>
>Array- en toewijzingsvelden worden niet ondersteund en kunnen niet worden gemarkeerd en gelabeld als identiteitsvelden.

Identiteitsvelden maken het ook mogelijk om identiteiten te koppelen als ze gemeenschappelijke PII-gegevens delen.
Door bijvoorbeeld velden met telefoonnummers als identiteitsvelden te labelen, [!DNL Identity Service] past automatisch relaties met andere personen toe die hetzelfde telefoonnummer gebruiken.

>[!NOTE]
>
>De naamruimte van resulterende identiteiten wordt opgegeven op het moment dat het veld wordt gelabeld.

### Een gegevensset configureren voor [!DNL Identity Service]

Tijdens het streamingingproces [!DNL Identity Service ]haalt automatisch identiteitsgegevens uit record- en tijdreeksgegevens. Voordat gegevens kunnen worden ingevoerd, moet deze echter zijn ingeschakeld voor [!DNL Identity Service]. Zie de zelfstudie aan  [een Dataset configureren voor realtime gebruikersprofiel en identiteitsservice met behulp van API&#39;s](../profile/tutorials/dataset-configuration.md) voor meer informatie .

### Gegevens samenvoegen tot [!DNL Identity Service]

[!DNL Identity Service] verbruikt XDM volgzame gegevens die naar Experience Platform worden verzonden of door [batch-opname](../ingestion/batch-ingestion/overview.md) of [streaming opname](../ingestion/streaming-ingestion/overview.md).

De volgende video is bedoeld om uw begrip van de Dienst van de Identiteit te steunen. In deze video ziet u hoe u gegevensvelden kunt labelen als identiteiten, identiteitsgegevens kunt invoeren en vervolgens kunt controleren of de gegevens zijn omgezet in de persoonlijke grafiek van de Adobe Experience Platform Identity Service.

>[!WARNING]
>
>De [!DNL Platform] De interface die in de volgende video wordt weergegeven, is verouderd. Raadpleeg de documentatie voor de meest recente schermafbeeldingen en functionaliteit van de gebruikersinterface.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Gegevensbeheer

Adobe Experience Platform is gemaakt met het oog op privacy en bevat een gegevensbeheerframework om PII-gegevens van uw klanten te beschermen. Identiteitsgegevens in de naamruimte &quot;email&quot; of &quot;phone&quot; zijn standaard gecodeerd, maar om ervoor te zorgen dat vertrouwelijke gegevens worden gecodeerd voordat deze worden voortgezet, kunnen labels voor gegevensgebruik worden toegepast op gegevens die worden ingevoerd of zodra deze worden binnengekomen [!DNL Platform]. Lees voor meer informatie de [Overzicht van gegevensbeheer](../data-governance/home.md).

## Volgende stappen

Nu begrijpt u de belangrijkste concepten van [!DNL Identity Service] en zijn rol binnen Experience Platform, kunt u beginnen te leren hoe te met uw identiteitsgrafiek te werken gebruikend [[!DNL Identity Service API]](./api/getting-started.md).
