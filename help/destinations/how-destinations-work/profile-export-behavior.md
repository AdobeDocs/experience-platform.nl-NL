---
title: Exportgedrag profiel
description: Leer hoe het gedrag van de profieluitvoer tussen de verschillende integratiepatronen varieert die in de bestemmingen van het Experience Platform worden gesteund.
exl-id: 2be62843-0644-41fa-a860-ccd65472562e
source-git-commit: 223734e2998568f3b9b78933fa5adf740b521f5f
workflow-type: tm+mt
source-wordcount: '2930'
ht-degree: 0%

---

# Profielexportgedrag voor verschillende doeltypen

Er zijn verscheidene bestemmingstypes in Experience Platform, zoals aangetoond in het hieronder diagram. Deze bestemmingen hebben enigszins verschillende uitvoerpatronen wat betreft de vraag wat een export naar een bestemming en wat in een export wordt opgenomen, zoals in de onderstaande secties wordt beschreven.

>[!IMPORTANT]
>
>Op deze documentatiepagina wordt alleen het gedrag voor het exporteren van profielen beschreven voor de verbindingen die onder aan het diagram worden gemarkeerd.

![ Types van bestemmingsdiagram ](/help/destinations/assets/how-destinations-work/types-of-destinations-v4.png)

## Berichtaggregatie in streamingdoelen

Alvorens in specifieke informatie per bestemmingstype te duiken, is het belangrijk om het concept berichtsamenvoeging voor *het stromen bestemmingen* te begrijpen.

De bestemmingen van het Experience Platform voeren gegevens naar op API-Gebaseerde integratie als vraag HTTPS uit. Zodra de bestemmingsdienst door andere stroomopwaartse diensten op de hoogte wordt gebracht dat de profielen als resultaat van partijopname, het stromen ingestie, partijsegmentatie, het stromen segmentatie of de veranderingen van de identiteitsgrafiek zijn bijgewerkt, worden de gegevens uitgevoerd en verzonden naar het stromen bestemmingen.

Profielen worden samengevoegd tot HTTPS-berichten voordat ze naar doel-API-eindpunten worden verzonden.

Neem de [ bestemming van Facebook ](/help/destinations/catalog/social/facebook.md) met a *[configureerbaar samenvoegings](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)* beleid als voorbeeld - het gegeven wordt verzonden op een samengevoegde manier, waar de bestemmingsdienst alle inkomende gegevens van de profieldienst stroomopwaarts neemt en het door één van het volgende samenvoegt, alvorens het aan Facebook te verzenden:

* Aantal records (maximaal 10.000) of
* Tijdlijninterval (300 seconden)

Welke van de bovengenoemde drempels het eerst wordt gehaald, leidt tot een export naar Facebook. In het dashboard van [!DNL Facebook Custom Audiences] zie je publiek dat vanuit Experience Platform komt in recordstappen van 10.000. U ziet misschien 10.000 records elke 2-3 minuten omdat de gegevens sneller worden verwerkt en geaggregeerd dan het exportinterval van 300 seconden en sneller worden verzonden, dus ongeveer om de 2-3 minuten totdat alle records zijn verwerkt. Als er onvoldoende records zijn om een batch van 10.000 samen te stellen, wordt het huidige aantal records verzonden, net als wanneer de drempel voor het tijdvenster is bereikt, zodat u ook kleinere batches naar Facebook kunt zien.

Als een ander voorbeeld, overweeg de [ HTTP API bestemming ](/help/destinations/catalog/streaming/http-destination.md), die het beleid van de a *[beste inspanningssamenvoeging](../destination-sdk/functionality/destination-configuration/aggregation-policy.md)*, met `maxUsersPerRequest: 10` heeft. Dit betekent dat een maximum van tien profielen zal worden bijeengevoegd alvorens een vraag van HTTP aan deze bestemming in brand wordt gestoken, maar het Experience Platform probeert om profielen naar de bestemming te verzenden zodra de bestemmingsdienst bijgewerkte herbeoordelingsinformatie van een stroomopwaartse dienst ontvangt.

Het samenvoegingsbeleid is configureerbaar, en de bestemmingsontwikkelaars kunnen beslissen hoe te om het samenvoegingsbeleid te vormen om aan de tariefbeperkingen van de API eindpunten stroomafwaarts te voldoen. Lees meer over [ samenvoegingsbeleid ](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) in de documentatie van Destination SDK.

## Streaming profiel exporteren (Enterprise) doelen {#streaming-profile-destinations}

>[!IMPORTANT]
>
> De bestemmingen van de onderneming zijn beschikbaar slechts aan [ Adobe Real-time Customer Data Platform Ultimate ](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) klanten.

De [ ondernemingsbestemmingen ](/help/destinations/destination-types.md#advanced-enterprise-destinations) in Experience Platform zijn Amazon Kinesis, Azure Event Hubs, en HTTP API.

Experience Platform optimaliseert het gedrag van de profieluitvoer naar uw ondernemingsbestemming, om gegevens naar uw API eindpunt slechts uit te voeren wanneer de relevante updates aan een profiel na publiekskwalificatie of andere significante gebeurtenissen zijn voorgekomen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een verandering in [ publieksenlidmaatschap ](/help/xdm/field-groups/profile/segmentation.md) voor minstens één van het publiek dat aan de bestemming in kaart wordt gebracht. Het profiel is bijvoorbeeld gekwalificeerd voor een van de soorten publiek die aan de bestemming zijn toegewezen of heeft een van de soorten publiek afgesloten die aan de bestemming zijn toegewezen.
* De profielupdate werd bepaald door een verandering in de [ identiteitskaart ](/help/xdm/field-groups/profile/identitymap.md). Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de soorten publiek dat aan de bestemming is toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een publiek dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export?

Met betrekking tot het gegeven dat voor een bepaald profiel wordt uitgevoerd, is het belangrijk om de twee verschillende concepten *te begrijpen wat een gegevensuitvoer aan uw ondernemingsbestemming* en *bepaalt welke gegevens in de uitvoer* inbegrepen zijn.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en doelgroepen fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als een toegewezen publiek de status wijzigt (van `null` in `realized` of van `realized` in `exiting` ) of dat toegewezen kenmerken worden bijgewerkt, een doelexport wordt uitgeschakeld.</li><li>Aangezien identiteiten momenteel niet aan ondernemingsbestemmingen kunnen worden in kaart gebracht, bepalen de veranderingen in om het even welke identiteit op een bepaald profiel ook bestemmingsuitvoer.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, ongeacht of het dezelfde waarde heeft of niet. Dit houdt in dat een overschrijven van een kenmerk als een wijziging wordt beschouwd, zelfs als de waarde zelf niet is gewijzigd.</li></ul> | <ul><li>Het `segmentMembership` -object bevat het publiek dat is toegewezen in de activeringsgegevensstroom, waarvoor de status van het profiel is gewijzigd na een afsluitgebeurtenis voor kwalificatie of publiek. Merk op dat andere niet in kaart gebrachte publiek waarvoor het profiel dat voor wordt gekwalificeerd deel van de bestemmingsuitvoer kan uitmaken, als deze doelgroepen tot het zelfde [ fusiebeleid ](/help/profile/merge-policies/overview.md) zoals het publiek behoren dat in activeringsdataflow in kaart wordt gebracht. </li><li>Alle identiteiten in het `identityMap` -object worden ook opgenomen (Experience Platform ondersteunt momenteel geen identiteitstoewijzing in de doelmap van de onderneming).</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>De bestemmingen van de onderneming stromen backfill gegevens wanneer het activeren van profielen aan een bestemming. Dit betekent dat de eerste gegevensuitvoer na het vormen van een activeringswerkschema aan een bestemming profielen zal omvatten die voor het geactiveerde publiek voorafgaand aan het publiek die aan de bestemming wordt in kaart gebracht.

>[!BEGINSHADEBOX]

Bijvoorbeeld, overweeg dit dataflow aan een bestemming van HTTP waar drie publiek in dataflow wordt geselecteerd, en vier attributen worden in kaart gebracht aan de bestemming.

![ gegevens van de ondernemingsbestemming ](/help/destinations/assets/catalog/http/profile-export-example-dataflow.png)

Een profieluitvoer naar de bestemming kan door een profiel worden bepaald dat voor of het weggaan van één van *drie in kaart gebrachte segmenten* in aanmerking komt. In de gegevensexport kan in het `segmentMembership` -object echter een ander niet-toegewezen publiek worden weergegeven als dat specifieke profiel lid van dat publiek is en als deze hetzelfde samenvoegbeleid delen als het publiek dat de exportbewerking heeft gestart. Als een profiel voor de **Klant met de Auto&#39;s van DeLorean** maar ook een lid van de **Gecontroleerde &quot;Terug naar de Toekomstige&quot;film** en **de de fictieswaaiers van de Wetenschap** segmenten kwalificeert, dan zullen deze andere twee publiek ook in het `segmentMembership` voorwerp van de gegevensuitvoer aanwezig zijn, alhoewel deze niet in dataflow, als deze het zelfde fusiebeleid delen met de **Klant met het segment van de AutoAuto&#39;s van DeLorean**.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de vier bovenstaande kenmerken de doelexport en zijn alle vier toegewezen kenmerken in het profiel aanwezig in de gegevensexport.

>[!ENDSHADEBOX]

>[!TIP]
>
> U kunt voorbeelden van uitgevoerde gegevens aan diverse ondernemingsbestemmingen in [ Amazon Kinesis ](/help/destinations/catalog/cloud-storage/amazon-kinesis.md#exported-data) zien, [ Azure de Hubs van de Gebeurtenis ](/help/destinations/catalog/cloud-storage/azure-event-hubs.md#exported-data), en [ HTTP API ](/help/destinations/catalog/streaming/http-destination.md#exported-data) bestemmingsdocumentatiepagina&#39;s.

## Streaming op API gebaseerde doelen {#streaming-api-based-destinations}

Het gedrag voor het exporteren van profielen voor streamingdoelen zoals Facebook, Trade Desk en andere op API&#39;s gebaseerde integraties lijkt sterk op het gedrag dat hierboven voor ondernemingsdoelen wordt beschreven.

De voorbeelden van het stromen bestemmingen zijn de bestemmingen die tot de [ sociale en reclamecategorieën ](/help/destinations/destination-types.md#categories) in de catalogus behoren.

Experience Platform optimaliseert het gedrag voor het exporteren van profielen naar uw streamingdoel, zodat gegevens alleen worden geëxporteerd naar op streaming API gebaseerde doelen wanneer relevante updates naar een profiel zijn opgetreden na kwalificatie van het publiek of andere belangrijke gebeurtenissen. In de volgende situaties worden profielen naar uw doel geëxporteerd:

* De profielupdate werd bepaald door een verandering in [ publieksenlidmaatschap ](/help/xdm/field-groups/profile/segmentation.md) voor minstens één van het publiek dat aan de bestemming in kaart wordt gebracht. Het profiel is bijvoorbeeld gekwalificeerd voor een van de soorten publiek die aan de bestemming zijn toegewezen of heeft een van de soorten publiek afgesloten die aan de bestemming zijn toegewezen.
* De profielupdate werd bepaald door een verandering in de [ identiteitstoewijzing ](/help/xdm/field-groups/profile/identitymap.md) voor een identiteit namespace die voor de uitvoer voor deze bestemmingsinstantie duidelijk is. Een profiel dat bijvoorbeeld al was gekwalificeerd voor een van de soorten publiek dat aan de bestemming is toegewezen, is toegevoegd aan een nieuwe identiteit in het kenmerk Naamplaatje.
* De profielupdate is bepaald door een wijziging in kenmerken voor ten minste een van de kenmerken die aan de bestemming zijn toegewezen. Een van de kenmerken die in de toewijzingsstap aan het doel is toegewezen, wordt bijvoorbeeld aan een profiel toegevoegd.
* Wijzigingen in toestemming voor een profiel wanneer automatische handhaving van toestemming is geconfigureerd en een profiel wordt uitgeschakeld. De geautomatiseerde toestemmingshandhaving zal een publiek verlaten gebeurtenis naar de bestemming verzenden zodat het profiel niet inbegrepen in om het even welk richten op de bestemming is.

In alle hierboven beschreven gevallen worden alleen de profielen waarin relevante updates zijn opgetreden, naar uw bestemming geëxporteerd. Bijvoorbeeld, als een publiek dat aan de bestemmingsstroom in kaart wordt gebracht honderd leden heeft, en vijf nieuwe profielen voor het segment kwalificeren, is de uitvoer naar uw bestemming incrementeel en omvat slechts de vijf nieuwe profielen.

Alle toegewezen kenmerken worden geëxporteerd voor een profiel, ongeacht de locatie van de wijzigingen. In het voorbeeld hierboven worden alle toegewezen kenmerken voor deze vijf nieuwe profielen geëxporteerd, zelfs als de kenmerken zelf niet zijn gewijzigd.

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export?

Met betrekking tot de gegevens die voor een bepaald profiel worden geëxporteerd, is het belangrijk dat u de twee verschillende concepten begrijpt van wat een gegevensexport naar uw streaming API-bestemming bepaalt en welke gegevens in de export worden opgenomen.

| Wat bepaalt de doelexport | Wat is inbegrepen in de doelexport |
|---------|----------|
| <ul><li>Toegewezen kenmerken en doelgroepen fungeren als actiepunt voor het exporteren van een bestemming. Dit betekent dat als een toegewezen publiek de status wijzigt (van `null` in `realized` of van `realized` in `exiting` ) of dat toegewezen kenmerken worden bijgewerkt, een doelexport wordt uitgeschakeld.</li><li>Een verandering in de identiteitskaart wordt bepaald als identiteit die wordt toegevoegd/verwijderd voor de [ identiteitsgrafiek ](/help/identity-service/features/identity-graph-viewer.md) van het profiel, voor identiteit namespaces die voor de uitvoer in kaart worden gebracht.</li><li>Een wijziging voor een kenmerk wordt gedefinieerd als een update voor het kenmerk, voor kenmerken die aan het doel zijn toegewezen.</li></ul> | <ul><li>Het publiek dat is toegewezen aan het doel en is gewijzigd, wordt opgenomen in het object `segmentMembership` . In sommige scenario&#39;s zouden zij gebruikend veelvoudige vraag kunnen worden uitgevoerd. Ook, in sommige scenario&#39;s, zouden sommige publiek dat niet is veranderd in de vraag ook kunnen worden omvat. In elk geval worden alleen toegewezen soorten publiek geëxporteerd.</li><li>Alle identiteiten van de naamruimten die zijn toegewezen aan het doel in het `identityMap` -object, worden ook opgenomen.</li><li>Alleen de toegewezen kenmerken worden opgenomen in de doelexport.</li></ul> |

{style="table-layout:fixed"}

>[!IMPORTANT]
>
>Streaming API-doelen streamen backfill-gegevens bij het activeren van profielen op een doel. Dit betekent dat de eerste gegevensuitvoer na het vormen van een activeringswerkschema aan een bestemming profielen zal omvatten die voor het geactiveerde publiek voorafgaand aan het publiek die aan de bestemming wordt in kaart gebracht.

>[!BEGINSHADEBOX]

Neem bijvoorbeeld deze gegevensstroom naar een streamingbestemming waar drie soorten publiek zijn geselecteerd in de gegevensstroom.

![ het stromen bestemmingsdataflow ](/help/destinations/assets/how-destinations-work/streaming-destination-example-dataflow.png)

Een profiel dat naar de bestemming wordt geëxporteerd, kan worden bepaald door een profiel dat in aanmerking komt voor of dat een van de drie toegewezen segmenten verlaat. Als een profiel voor de **Klant met het segment van de Auto&#39;s van DeLorean** wordt gekwalificeerd, zal dit de uitvoer teweegbrengen. Het andere publiek (**Stad - Dallas** en **Basis Actieve Plaats**) zou eveneens kunnen worden uitgevoerd voor het geval dat het profiel dat publiek heeft met één van de mogelijke statussen (`realized` of `exited`) aanwezig is. Het niet in kaart gebrachte publiek (als **de fictiefondsen van de Wetenschap**) zal niet worden uitgevoerd.

Vanuit het oogpunt van profielkenmerken bepalen wijzigingen in de drie bovenstaande kenmerken het exporteren van de bestemming.

>[!ENDSHADEBOX]

## Batchbestemmingen (op basis van bestanden) {#file-based-destinations}

Wanneer het uitvoeren van profielen naar [ op dossier-gebaseerde bestemmingen ](/help/destinations/destination-types.md#file-based) in Experience Platform, zijn er drie soorten programma&#39;s (hieronder vermeld) en twee die dossieruitvoeropties (volledige of stijgende dossiers) worden vermeld die u kunt gebruiken. Al deze montages worden geplaatst op een publieksniveau, zelfs wanneer het veelvoudige publiek aan één enkele bestemmingsdataflow in kaart wordt gebracht.

* Gepland exporteren: configureer een bestemming, voeg een of meer segmenten toe, selecteer of u volledige of incrementele bestanden wilt exporteren en selecteer elke dag of meerdere keren per dag een ingestelde tijd waarop bestanden moeten worden geëxporteerd. Een exporttijd van 5 PM betekent bijvoorbeeld dat de profielen die voor het publiek in aanmerking komen, om 17.00 uur worden geëxporteerd.
* Na segmentevaluatie: de export wordt direct geactiveerd nadat de dagelijkse evaluatietaak voor het publiek is uitgevoerd. Dit betekent dat de geëxporteerde profielnummers in het bestand zo dicht mogelijk bij de meest recente geëvalueerde populatie van het segment liggen.
* Op vraaguitvoer ([ uitvoerdossier nu ](/help/destinations/ui/export-file-now.md)): Gebaseerd op de recentste baan van de publieksevaluatie, wordt een volledig dossier uitgevoerd éénmaal bovenop regelmatig geplande uitvoer.

In alle bovenstaande exportsituaties bevatten de geëxporteerde bestanden de profielen die voor het exporteren zijn gekwalificeerd, naast de kolommen die u hebt geselecteerd als XDM-kenmerken voor het exporteren.

>[!TIP]
>
>Wanneer een streaming publiek wordt toegewezen aan een batchdoel, is het waarschijnlijker dat het aantal profielen in het geëxporteerde bestand dichter bij het aantal gebruikers in het segment ligt. Dit komt doordat er een grotere kans is dat de meest recente publieksevaluatie dichter bij de exporttijd is gekomen.

### Incrementele bestandsuitvoer {#incremental-file-exports}

Niet alle updates op een profiel kwalificeren een profiel dat moet worden opgenomen in incrementele bestandsexport. Als bijvoorbeeld een kenmerk is toegevoegd aan of verwijderd uit een profiel, wordt het profiel niet opgenomen in de exportbewerking.

Wanneer het `segmentMembership` -kenmerk van een profiel echter verandert, wordt het profiel opgenomen in geëxporteerde bestanden. Met andere woorden, als het profiel onderdeel wordt van het publiek of uit het publiek wordt verwijderd, wordt het opgenomen in incrementele exportbewerkingen.

Op dezelfde manier als wordt een nieuwe identiteit (nieuw e-mailadres, telefoonaantal, ECID, etc.) toegevoegd aan een profiel in de [ identiteitsgrafiek ](/help/identity-service/features/identity-graph-viewer.md), die het profiel zal teweegbrengen om in een nieuwe stijgende dossieruitvoer worden omvat.

Als een nieuw publiek aan een bestemmingstoewijzing wordt toegevoegd, beïnvloedt dat geen kwalificaties en de uitvoer voor een ander segment. De programma&#39;s van de uitvoer worden gevormd individueel per publiek en de dossiers worden afzonderlijk uitgevoerd voor elk segment, zelfs als het publiek aan de zelfde bestemmingsdataflow is toegevoegd.

>[!BEGINSHADEBOX]

Als een publiek bijvoorbeeld incrementele bestandsupdates exporteert in de hieronder weergegeven exportinstelling, moet u rekening houden met de volgende omstandigheden waarbij een profiel al dan niet is opgenomen in een incrementele bestandsuitvoer:

![ de Uitvoer die met verscheidene geselecteerde attributen plaatst.](/help/destinations/assets/how-destinations-work/export-selection-batch-destination.png)

* Een profiel *is* inbegrepen in een stijgende dossieruitvoer wanneer het voor het segment kwalificeert of diskwalificeert.
* Een profiel *is* inbegrepen in een stijgende dossieruitvoer wanneer een nieuw telefoonaantal aan de identiteitsgrafiek wordt toegevoegd.
* Een profiel *is niet* inbegrepen in een stijgende dossieruitvoer wanneer de waarde van om het even welke in kaart gebrachte gebieden XDM zoals `xdm: loyalty.points`, `xdm: loyalty.tier`, `xdm: personalEmail.address` op een profiel wordt bijgewerkt.
* Wanneer het `segmentMembership.status` XDM gebied in het werkschema van de bestemmingsactivering in kaart wordt gebracht, zijn de profielen die het publiek *verlaten ook inbegrepen* in uitgevoerde stijgende dossiers, met een `exited` status.

>[!ENDSHADEBOX]

### Wat bepaalt een gegevensexport en wat wordt opgenomen in de export?

Op basis van de informatie in de bovenstaande sectie kan het gedrag voor het exporteren van profielen naar bestandsdoelen worden samengevat zoals hieronder wordt beschreven:

**Volledige dossieruitvoer**

De volledige actieve populatie van het publiek wordt uitgevoerd elke dag.

| Wat bepaalt de doelexport | Wat is opgenomen in het geëxporteerde bestand |
|---------|----------|
| <ul><li>Het de uitvoerprogramma plaatste in UI of API en gebruikersactie (het selecteren van [ dossier van de Uitvoer ](/help/destinations/ui/export-file-now.md) nu in UI of het gebruiken van [ ad-hoc activering API ](/help/destinations/api/ad-hoc-activation-api.md)) bepaalt het begin van een bestemmingsuitvoer.</li></ul> | In de volledige die dossieruitvoer, is de volledige actieve profielbevolking van een segment, op de recentste publieksevaluatie wordt gebaseerd, inbegrepen met elke dossieruitvoer. De meest recente waarden voor elk XDM-kenmerk dat is geselecteerd voor export, worden ook als kolommen opgenomen in elk bestand. Profielen met de status Verlaat worden niet opgenomen in de geëxporteerde bestanden. |

{style="table-layout:fixed"}

**Incrementele dossieruitvoer**

In de eerste bestandsuitvoer na het instellen van de activeringsworkflow wordt de gehele populatie van het publiek geëxporteerd. Bij de volgende exportbewerkingen worden alleen de gewijzigde profielen geëxporteerd.

| Wat bepaalt de doelexport | Wat is opgenomen in het geëxporteerde bestand |
|---------|----------|
| <ul><li>Het exportschema dat is ingesteld in de UI of API bepaalt het begin van een doelexport.</li><li>Wijzigingen in het aantal gebruikers dat deel uitmaakt van een profiel, ongeacht of het om het segment gaat of niet, of wijzigingen in identiteitskaarten, kwalificeren een profiel dat moet worden opgenomen in incrementele exportbewerkingen. De veranderingen in attributen voor een profiel *kwalificeren* geen profiel dat in stijgende uitvoer moet worden omvat.</li></ul> | <p>De profielen waarvoor het publiekslidmaatschap is gewijzigd, samen met de meest recente informatie voor elk XDM-kenmerk dat is geselecteerd voor export.</p><p>Profielen met de verlaten status worden opgenomen in de doelexport als het `segmentMembership.status` XDM-veld is geselecteerd in de toewijzingsstap.</p> |

{style="table-layout:fixed"}

>[!TIP]
>
>Ter herinnering: wijzigingen in kenmerkwaarden of in identiteitskaarten voor een profiel kwalificeren geen profiel dat moet worden opgenomen in een incrementele bestandsuitvoer.

## Volgende stappen {#next-steps}

Nadat u dit document hebt gelezen, weet u nu wat u kunt verwachten in profielexport naar streaming, bedrijven en op bestanden gebaseerde doelen.

Daarna, kunt u over lezen hoe [ identiteiten ](/help/destinations/how-destinations-work/identity-handling.md) in het activeringswerkschema worden behandeld.
