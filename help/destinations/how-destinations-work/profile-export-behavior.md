---
title: Exportgedrag profiel
description: Leer hoe het gedrag van de profieluitvoer tussen de verschillende integratiepatronen varieert die in de bestemmingen van het Experience Platform worden gesteund.
source-git-commit: 372231ab4fc1148c1c2c0c5fdbfd3cd5328b17cc
workflow-type: tm+mt
source-wordcount: '2944'
ht-degree: 0%

---

# Profielexportgedrag voor verschillende doeltypen

Er zijn verscheidene bestemmingstypes in Experience Platform, zoals aangetoond in het hieronder diagram. Deze bestemmingen hebben enigszins verschillende uitvoerpatronen wat betreft de vraag wat een export naar een bestemming en wat in een export wordt opgenomen, zoals in de onderstaande secties wordt beschreven.

>[!IMPORTANT]
>
>Op deze documentatiepagina wordt alleen het gedrag voor het exporteren van profielen beschreven voor de verbindingen die onder aan het diagram worden gemarkeerd.

![Soorten bestemmingsdiagram](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Beleid voor microbatchverwerking en aggregatie

Alvorens in specifieke informatie per bestemmingstype te duiken, is het belangrijk om de concepten microbatching en samenvoegingsbeleid voor te begrijpen *streaming doelen*.

De bestemmingen van het Experience Platform voeren gegevens naar op API-Gebaseerde integratie als vraag HTTPS uit. Zodra de bestemmingsdienst door andere stroomopwaartse diensten op de hoogte wordt gebracht dat de profielen als resultaat van partijopname, het stromen ingestie, partijsegmentatie, het stromen segmentatie of de veranderingen van de identiteitsgrafiek zijn bijgewerkt, worden de gegevens uitgevoerd en verzonden naar het stromen bestemmingen.

Het proces waarmee profielen worden samengevoegd tot HTTPS-berichten voordat ze worden verzonden naar eindpunten van de bestemmings-API wordt aangeroepen *microbatchverwerking*.

Neem de [Facebook-bestemming](/help/destinations/catalog/social/facebook.md) met een *[configureerbare samenvoeging](/help/destinations/destination-sdk/destination-configuration.md#configurable-aggregation)* beleid als voorbeeld - de gegevens worden verzonden op een samengevoegde manier, waar de bestemmingsdienst alle inkomende gegevens van de profieldienst upstream neemt en het door één van het volgende samenvoegt, alvorens het naar Facebook te verzenden:

* Aantal records (maximaal 10.000) of
* Tijdvensterinterval (30 minuten)

Welke van de bovengenoemde drempels het eerst wordt gehaald, leidt tot een export naar Facebook. Dus in de [!DNL Facebook Custom Audiences] in het dashboard ziet u wellicht doelgroepen uit Experience Platform komen in stappen van 10.000 records. Mogelijk ziet u 10.000 records elke 10-15 minuten, omdat de gegevens sneller worden verwerkt en samengevoegd dan het exportinterval van 30 minuten en sneller worden verzonden, dus ongeveer om de 10-15 minuten totdat alle records zijn verwerkt. Als er onvoldoende records zijn om een batch van 10.000 samen te stellen, wordt het huidige aantal records verzonden, net als wanneer de drempel voor het tijdvenster is bereikt, zodat u ook kleinere batches naar Facebook kunt zien.

Als een ander voorbeeld: [HTTP API-bestemming](/help/destinations/catalog/streaming/http-destination.md), die een *[beste inspanningsaggregatie](/help/destinations/destination-sdk/destination-configuration.md#best-effort-aggregation)* beleid, met `maxUsersPerRequest: 10`. Dit betekent dat een maximum van tien profielen zal worden bijeengevoegd alvorens een vraag van HTTP aan deze bestemming in brand wordt gestoken, maar het Experience Platform probeert om profielen naar de bestemming te verzenden zodra de bestemmingsdienst bijgewerkte herbeoordelingsinformatie van een stroomopwaartse dienst ontvangt.

Het samenvoegingsbeleid is configureerbaar, en de bestemmingsontwikkelaars kunnen beslissen hoe te om het samenvoegingsbeleid te vormen om aan de tariefbeperkingen van de API eindpunten stroomafwaarts te voldoen. Meer informatie over [samenvoegingsbeleid](/help/destinations/destination-sdk/destination-configuration.md#aggregation) in de documentatie van Destination SDK.

## Streaming profiel exporteren (Enterprise) doelen {#streaming-profile-destinations}

>[!IMPORTANT]
>
> Enterprise-doelen zijn alleen beschikbaar voor [Adobe Real-time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

De [ondernemingsbestemmingen](/help/destinations/destination-types.md#streaming-profile-export) in Experience Platform zijn Amazon Kinesis, Azure Event Hubs en HTTP API.

Experience Platform optimaliseert het gedrag van de profieluitvoer naar uw ondernemingsbestemming, om gegevens naar uw API eindpunt slechts uit te voeren wanneer de relevante updates aan een profiel na segmentkwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate is bepaald door een wijziging in [segmentlidmaatschap](/help/xdm/field-groups/profile/segmentation.md) voor ten minste één van de segmenten die aan de bestemming worden toegewezen. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export?

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten van *wat bepaalt gegevensexport naar uw ondernemingsbestemming* en *welke gegevens in de uitvoer worden opgenomen*.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als om het even welke in kaart gebrachte segmenten staten (van ongeldig aan gerealiseerd of van gerealiseerde/bestaande aan het weggaan) veranderen of om het even welke in kaart gebrachte attributen worden bijgewerkt, een bestemmingsuitvoer zou worden weggeduwd.</li><li>Aangezien identiteiten momenteel niet aan ondernemingsbestemmingen kunnen worden in kaart gebracht, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>De `segmentMembership` Dit object bevat het segment dat is toegewezen in de activeringsgegevensstroom, waarvoor de status van het profiel is gewijzigd na een afsluitgebeurtenis voor kwalificatie of segment. Merk op dat andere niet in kaart gebrachte segmenten waarvoor het profiel dat voor wordt gekwalificeerd deel van de bestemmingsuitvoer kan uitmaken, als deze segmenten tot het zelfde behoren [samenvoegingsbeleid](/help/profile/merge-policies/overview.md) als het segment dat is toegewezen in de activeringsgegevensstroom. </li><li>Alle identiteiten in de `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de doellocatie van de onderneming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>De bestemmingen van de onderneming stromen backfill gegevens wanneer het activeren van profielen aan een bestemming. Dit betekent dat de eerste gegevensuitvoer na het vormen van een activeringswerkschema aan een bestemming profielen zal omvatten die voor het geactiveerde segment voorafgaand aan het segment die aan de bestemming worden in kaart gebracht.

>[!BEGINSHADEBOX]

Bijvoorbeeld, overweeg dit dataflow aan een bestemming van HTTP waar drie segmenten in dataflow worden geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![doelgegevens onderneming](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de *drie toegewezen segmenten*. Bij de gegevensexport moet u `segmentMembership` objecten, zouden andere niet in kaart gebrachte segmenten kunnen verschijnen, als dat bepaalde profiel een lid van hen is en als deze het zelfde fusiebeleid delen zoals het segment dat de uitvoer teweegbracht. Als een profiel in aanmerking komt voor de opdracht **Klant met DeLorean Auto&#39;s** segment, maar ook lid van **Film &quot;Terug naar de toekomst&quot; bekeken** en **Favorieten voor science fiction** segmenten, dan zullen deze andere twee segmenten ook in de `segmentMembership` -object van de gegevensexport, ook al worden deze niet toegewezen in de gegevensstroom, als deze hetzelfde samenvoegbeleid delen met de **Klant met DeLorean Auto&#39;s** segment.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

>[!ENDSHADEBOX]

>[!TIP]
>
> U kunt voorbeelden van uitgevoerde gegevens aan diverse ondernemingsbestemmingen in zien [Amazon Kinesis](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data), [Azure Event Hubs](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data), en [HTTP-API](/help/destinations/catalog/streaming/http-destination.md#exported-data) doeldocumentatiepagina&#39;s.

## Streaming op API gebaseerde doelen {#streaming-api-based-destinations}

Het gedrag voor het exporteren van profielen voor streamingdoelen zoals Facebook, Trade Desk en andere op API&#39;s gebaseerde integraties lijkt sterk op het gedrag dat hierboven voor ondernemingsdoelen wordt beschreven.

Voorbeelden van streamingdoelen zijn de doelen die bij de [sociale en reclamecategorieën](/help/destinations/destination-types.md#categories) in de catalogus.

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw streamingdoel, zodat gegevens alleen worden geëxporteerd naar op streaming API gebaseerde doelen wanneer relevante updates voor een profiel zijn opgetreden na segmentkwalificatie of andere belangrijke gebeurtenissen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate is bepaald door een wijziging in [segmentlidmaatschap](/help/xdm/field-groups/profile/segmentation.md) voor ten minste één van de segmenten die aan de bestemming worden toegewezen. Het profiel is bijvoorbeeld gekwalificeerd voor een van de segmenten die aan het doel zijn toegewezen of heeft een van de segmenten afgesloten die aan het doel zijn toegewezen.
* De profielupdate is bepaald door een wijziging in het dialoogvenster [identiteitsbewijs](/help/xdm/field-groups/profile/identitymap.md) voor een naamruimte voor identiteit die is gemarkeerd voor exporteren voor deze doelinstantie. Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de segmenten die aan de bestemming zijn toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.
* Wijzigingen in toestemming voor een profiel wanneer automatische handhaving van toestemming is geconfigureerd en een profiel wordt uitgeschakeld. De geautomatiseerde toestemmingshandhaving zal een publiek verlaten gebeurtenis naar de bestemming verzenden zodat het profiel niet inbegrepen in om het even welk richten op de bestemming is.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een segment dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export?

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten begrijpt van wat een gegevensexport naar uw streaming API-bestemming bepaalt en welke gegevens in de export worden opgenomen.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en segmenten fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als om het even welke in kaart gebrachte segmenten staten (van ongeldig aan gerealiseerd of van gerealiseerde/bestaande aan het weggaan) veranderen of om het even welke in kaart gebrachte attributen worden bijgewerkt, een bestemmingsuitvoer zou worden weggeduwd.</li><li>Een wijziging in het identiteitsoverzicht wordt gedefinieerd als een identiteit die wordt toegevoegd/verwijderd voor de [identiteitsgrafiek](/help/identity-service/ui/identity-graph-viewer.md) van het profiel, voor naamruimten die zijn toegewezen voor exporteren.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, voor kenmerken die aan het doel zijn toegewezen.</li></ul> | <ul><li>De segmenten die aan de bestemming in kaart worden gebracht en zijn veranderd zullen in omvatten `segmentMembership` object. In sommige scenario&#39;s zouden zij gebruikend veelvoudige vraag kunnen worden uitgevoerd. Ook, in sommige scenario&#39;s, zouden sommige segmenten die niet zijn veranderd in de vraag ook kunnen worden omvat. In elk geval worden alleen toegewezen segmenten geëxporteerd.</li><li>Alle identiteiten van namespaces die aan de bestemming in in kaart worden gebracht `identityMap` -object wordt ook opgenomen.</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style=&quot;table-layout:fixed&quot;}

>[!IMPORTANT]
>
>Streaming API-doelen streamen backfill-gegevens bij het activeren van profielen op een doel. Dit betekent dat de eerste gegevensuitvoer na het vormen van een activeringswerkschema aan een bestemming profielen zal omvatten die voor het geactiveerde segment voorafgaand aan het segment die aan de bestemming worden in kaart gebracht.

>[!BEGINSHADEBOX]

Neem bijvoorbeeld deze gegevensstroom naar een streamingbestemming waar drie segmenten zijn geselecteerd in de gegevensstroom.

![streaming doelgegevensstroom](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de drie toegewezen segmenten verlaat. Als een profiel gekwalificeerd is voor de **Klant met DeLorean Auto&#39;s** segmenteren, wordt het exporteren geactiveerd. De andere segmenten (**Plaats - Dallas** en **Basissite actief**) kan ook worden geëxporteerd als het profiel dat segment bevat met een van de mogelijke statussen (`realized`, `existing`, `exited`). Niet-toegewezen segmenten (zoals **Favorieten voor science fiction**) wordt niet geëxporteerd.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de drie bovenstaande kenmerken het exporteren van de bestemming.

>[!ENDSHADEBOX]

## Batchbestemmingen (op basis van bestanden) {#file-based-destinations}

Profielen exporteren naar [bestandsgebaseerde doelen](/help/destinations/destination-types.md#file-based) in Experience Platform zijn er drie typen schema&#39;s (hieronder vermeld) en twee exportopties voor bestanden (volledige of incrementele bestanden) die u kunt gebruiken. Al deze montages worden geplaatst op een segmentniveau, zelfs wanneer de veelvoudige segmenten aan één enkele bestemmingsgegeven in kaart worden gebracht.

* Geplande uitvoer: Vorm een bestemming, voeg één of meerdere segmenten toe, selecteer als u volledige of stijgende dossiers wilt uitvoeren en selecteer een vastgestelde tijd elke dag of verscheidene tijden per dag wanneer de dossiers zouden moeten worden uitgevoerd. Een exporttijd van 5 PM betekent bijvoorbeeld dat de profielen die voor het segment zijn gekwalificeerd, worden geëxporteerd om 17.00 uur.
* Na segmentevaluatie: De uitvoer wordt teweeggebracht onmiddellijk nadat de dagelijkse looppas van de segmentevaluatie. Dit betekent dat de geëxporteerde profielnummers in het bestand zo dicht mogelijk bij de meest recente geëvalueerde populatie van het segment liggen.
* Op vraag uitgevoerde goederen ([bestand nu exporteren](/help/destinations/ui/export-file-now.md)): Gebaseerd op de recentste baan van de segmentevaluatie, wordt een volledig dossier één keer uitgevoerd bovenop regelmatig geplande uitvoer.

In alle bovenstaande exportsituaties bevatten de geëxporteerde bestanden de profielen die voor het exporteren zijn gekwalificeerd, naast de kolommen die u hebt geselecteerd als XDM-kenmerken voor het exporteren.

>[!TIP]
>
>Wanneer een streaming segment wordt toegewezen aan een batchdoel, is het waarschijnlijker dat het aantal profielen in het geëxporteerde bestand dichter bij het aantal gebruikers in het segment ligt. Dit is omdat er een grotere kans is dat de recentste segmentevaluatie dichter bij de uitvoertijd is gelopen.

### Incrementele bestandsuitvoer {#incremental-file-exports}

Niet alle updates op een profiel kwalificeren een profiel dat moet worden opgenomen in incrementele bestandsexport. Als bijvoorbeeld een kenmerk is toegevoegd aan of verwijderd uit een profiel, wordt het profiel niet opgenomen in de exportbewerking. Alleen profielen waarvoor de `segmentMembership` Het kenmerk is gewijzigd, wordt opgenomen in geëxporteerde bestanden. Met andere woorden, alleen als het profiel onderdeel wordt van het segment of wordt verwijderd uit het segment, wordt het opgenomen in incrementele exportbewerkingen.

En als een nieuwe identiteit (nieuw e-mailadres, telefoonnummer, ECID enzovoort) wordt toegevoegd aan een profiel in het dialoogvenster [identiteitsgrafiek](/help/identity-service/ui/identity-graph-viewer.md), die geen reden is om het profiel op te nemen in een nieuwe incrementele bestandsuitvoer.

Als een nieuw segment aan een bestemmingstoewijzing wordt toegevoegd, beïnvloedt dat geen kwalificaties en de uitvoer voor een ander segment. De programma&#39;s van de uitvoer worden gevormd individueel per segment en de dossiers worden afzonderlijk uitgevoerd voor elk segment, zelfs als de segmenten aan de zelfde bestemmingsdataflow zijn toegevoegd.

>[!BEGINSHADEBOX]

Als een segment bijvoorbeeld incrementele bestandsupdates exporteert in de hieronder weergegeven exportinstelling, moet u rekening houden met de volgende omstandigheden waarbij een profiel al dan niet is opgenomen in een incrementele exportbewerking:

![Exportinstelling met verschillende geselecteerde kenmerken.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Een profiel wordt opgenomen in een incrementele bestandsuitvoer wanneer het voor het segment in aanmerking komt of niet.
* Een profiel is *niet* opgenomen in een incrementele bestandsuitvoer wanneer een nieuw telefoonnummer wordt toegevoegd aan de identiteitsgrafiek.
* Een profiel is *niet* opgenomen in een incrementele bestandsuitvoer wanneer de waarde van een toegewezen XDM-veld, zoals `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` wordt bijgewerkt in een profiel.
* Wanneer `segmentMembership.status` XDM-veld wordt toegewezen in de workflow voor doelactivering, profielen die het segment verlaten, worden ook opgenomen in geëxporteerde incrementele bestanden, met een `exited` status.

>[!ENDSHADEBOX]

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export?

Op basis van de informatie in de bovenstaande sectie kan het gedrag voor het exporteren van profielen naar bestandsdoelen worden samengevat zoals hieronder wordt beschreven:

**Volledige bestandsuitvoer**

De volledige populatie van het segment wordt elke dag uitgevoerd.

| Wat bepaalt de doelexport | Wat is opgenomen in het geëxporteerde bestand |
|---------|----------|
| <ul><li>Het exportschema dat is ingesteld in de gebruikersinterface of de API en in de actie van de gebruiker (selecteren [Bestand nu exporteren](/help/destinations/ui/export-file-now.md) in de gebruikersinterface of met de [API voor ad-hocactivering](/help/destinations/api/ad-hoc-activation-api.md)) bepaalt u het begin van een doelexport.</li><li>Eventuele wijzigingen in het segmentlidmaatschap van een profiel, ongeacht of deze in aanmerking komen voor of niet in aanmerking komen voor het segment, komen in aanmerking voor een profiel dat wordt opgenomen in incrementele export.</li></ul> | In volledige dossieruitvoer, is de volledige profielbevolking van een segment, die op de recentste segmentevaluatie wordt gebaseerd, inbegrepen met elke dossieruitvoer. De meest recente waarden voor elk XDM-kenmerk dat is geselecteerd voor export, worden ook als kolommen opgenomen in elk bestand. |

{style=&quot;table-layout:fixed&quot;}

**Incrementele bestandsuitvoer**

In de eerste bestandsuitvoer na het instellen van de activeringsworkflow wordt de gehele populatie van het segment geëxporteerd. Bij de volgende exportbewerkingen worden alleen de gewijzigde profielen geëxporteerd.

| Wat bepaalt de doelexport | Wat is opgenomen in het geëxporteerde bestand |
|---------|----------|
| <ul><li>Het exportschema dat is ingesteld in de UI of API bepaalt het begin van een doelexport.</li><li>Eventuele wijzigingen in het segmentlidmaatschap van een profiel, ongeacht of deze in aanmerking komen voor of niet in aanmerking komen voor het segment, komen in aanmerking voor een profiel dat wordt opgenomen in incrementele export. Wijzigingen in kenmerken of in identiteitskaarten voor een profiel *niet* in aanmerking komen voor een profiel dat in incrementele uitvoer moet worden opgenomen.</li></ul> | De profielen waarvoor het segmentlidmaatschap is gewijzigd, samen met de meest recente informatie voor elk XDM-kenmerk dat is geselecteerd voor export. |

{style=&quot;table-layout:fixed&quot;}

>[!TIP]
>
>Ter herinnering: wijzigingen in kenmerkwaarden of in identiteitskaarten voor een profiel kwalificeren geen profiel dat moet worden opgenomen in een incrementele bestandsuitvoer.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu wat u kunt verwachten in profielexport naar streaming, bedrijven en op bestanden gebaseerde doelen.

Vervolgens kunt u lezen over hoe [identiteiten worden verwerkt](/help/destinations/how-destinations-work/identity-handling.md) in de activeringsworkflow.