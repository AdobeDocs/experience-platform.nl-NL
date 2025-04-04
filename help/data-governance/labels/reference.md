---
keywords: Experience Platform;home;populaire onderwerpen;gegevensbeheer;gegevensgebruikslabel api;beleidsservice-api;ondersteunde gegevensgebruikslabels;contractlabels;identiteitslabels;gevoelige labels
solution: Experience Platform
title: Woordenlijst met gegevensverbruikslabels
description: Dit document bevat een overzicht van alle labels voor gegevensgebruik die momenteel door Adobe Experience Platform worden ondersteund.
exl-id: 70d0702d-def7-4ab2-a861-eaf0f0cde1d4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2257'
ht-degree: 0%

---

# Verklarende woordenlijst met gegevensgebruikslabels {#data-usage-labels-glossary}

>[!CONTEXTUALHELP]
>id="platform_policies_labeltype"
>title="Labeltypen"
>abstract="Er zijn verschillende categorieën labels voor gegevensgebruik. Adobe-gedefinieerde labels bevatten contractlabels, identiteitslabels en gevoelige labels. De etiketten die door uw organisatie worden bepaald zijn gecategoriseerd als douanelabels."
>text="See the data usage labels glossary for more information on these label types."

De etiketten van het gebruik van gegevens staan u toe om datasets en gebieden volgens [ governance beleid ](../policies/overview.md) en [ toegangsbeheerbeleid ](../../access-control/abac/overview.md) te categoriseren dat op die gegevens van toepassing is. Adobe Experience Platform biedt verschillende basislabels voor gegevensgebruik die u kunt gebruiken om uw gegevens te categoriseren.

In dit document worden de basislabels voor gegevensgebruik beschreven die momenteel door Experience Platform worden geleverd.

## Contractlabels {#contract}

De etiketten van het contract &quot;C&quot;worden gebruikt om gegevens te categoriseren die contractuele verplichtingen hebben of met het beleid van het gegevensbeheer van uw organisatie verwant zijn.

| Label | Definitie |
| --- | --- |
| [ C1 ](#c1) | Gegevens kunnen alleen uit Adobe Experience Cloud worden geëxporteerd in een geaggregeerde vorm, zonder individuele of apparaat-id&#39;s. |
| [ C2 ](#c2) | Gegevens kunnen niet naar derden worden geëxporteerd. |
| [ C3 ](#c3) | Gegevens kunnen niet met rechtstreeks identificeerbare informatie worden gecombineerd of anderszins worden gebruikt. |
| [ C4 ](#c4) | Gegevens kunnen niet worden gebruikt voor advertenties of inhoud die on-site of intersite zijn. |
| [ C5 ](#c5) | Gegevens kunnen niet worden gebruikt voor op rente gebaseerde, cross-site gerichte adressering van inhoud of advertenties. |
| [ C6 ](#c6) | Gegevens kunnen niet worden gebruikt voor on-site advertenties. |
| [ C7 ](#c7) | Gegevens kunnen niet worden gebruikt voor het on-site maken van inhoud. |
| [ C8 ](#c8) | Gegevens kunnen niet worden gebruikt voor het meten van de websites of apps van uw organisatie. |
| [ C9 ](#c9) | Gegevens kunnen niet worden gebruikt in workflows voor gegevenswetenschap. |
| [ C10 ](#c10) | Gegevens kunnen niet worden gebruikt voor activering van een gestikte identiteit. |
| [ C11 ](#c11) | De gegevens kunnen niet met de partners van de Aanpassing van het Segment worden gedeeld. |
| [ C12 ](#c12) | Gegevens kunnen op geen enkele manier worden geëxporteerd. |

## Identiteitslabels {#identity}

De etiketten van de identiteit &quot;I&quot;worden gebruikt om gegevens te categoriseren die een specifieke persoon kunnen identificeren of contacteren.

| Label | Definitie |
| --- | --- |
| **I1** | Direct identificeerbare gegevens die een specifieke persoon kunnen identificeren of contacteren, eerder dan een apparaat. |
| **I2** | Indirect identificeerbare gegevens die in combinatie met andere gegevens kunnen worden gebruikt om een specifieke persoon te identificeren of contact op te nemen. |

## Gevoelige labels {#sensitive}

De gevoelige etiketten &quot;S&quot;worden gebruikt om gegevens te categoriseren die u, en uw organisatie, gevoelig overwegen.

Eén type gegevens dat u mogelijk als gevoelig beschouwt, kan verschillende typen geografische gegevens zijn. Deze categorie is echter niet beperkt tot geografische gegevens.

| Label | Definitie |
| --- | --- |
| **S1** | Gegevens die breedte- en lengtegraad aangeven die kunnen worden gebruikt om de precieze locatie van een apparaat te bepalen. |
| **S2** | Gegevens die kunnen worden gebruikt om een breed gedefinieerd geofence-gebied te bepalen. |
| **PSPD** | De toegelaten Gevoelige Persoonlijke Gegevens (PSPD) verwijst naar gegevens die u door Adobe contractueel wordt toegelaten om te uploaden die &quot;gevoelig&quot;wordt geacht, &quot;speciale categorie van gegevens&quot;, of een gelijkaardige term die door toepasselijke wetten wordt gebruikt. Dit sluit specifiek beschermde gezondheidsinformatie (PHI) en andere gereglementeerde gezondheidsgegevens uit. |
| **RHD** | Gegevens die verwijzen naar beschermde gezondheidsinformatie (PHI) of informatie over een patiënt die door Adobe contractueel mag worden geüpload. |

## Partnerecosysteemlabels {#partner}

De etiketten van het Ecosysteem van de partner worden gebruikt om gegevens te categoriseren die uit bronnen buiten uw organisatie worden verkregen.

Dit etiket wordt gebruikt om het gebruik van perspectiefgegevens te regelen.

| Label | Definitie |
| --- | --- |
| **Derden** | Gegevens van derden zijn gegevens die u ontvangt van een externe leverancier van gegevens. Een externe leverancier van gegevens is een entiteit die een overeenkomst met uw organisatie heeft gesloten die u machtigt om de gegevens van derden samen met Experience Platform te openen, te gebruiken, weer te geven en te verzenden. |
| **derdeverrijking** | Gegevens verzameld door een externe organisatie die niet rechtstreeks met de betrokkene verband houdt. Het label moet worden toegepast op gegevens van derden die worden gebruikt voor het verrijken van profielen van derden. |
| **derde-partij-Verkennend** | Gegevens verzameld door een externe organisatie die niet rechtstreeks met de betrokkene verband houdt. Het etiket moet worden toegepast op gegevens van derden die worden gebruikt voor de uitbreiding van de trechter naar nieuwe klanten. |

## Bijlage

In de onderstaande secties vindt u aanvullende informatie over beschikbare labels voor gegevensgebruik.

### Details contractlabel

De volgende secties bevatten gedetailleerde informatie over de uitvoering van specifieke &quot;C&quot;-labels voor contracten.

#### C1 {#c1}

Sommige gegevens kunnen alleen uit Adobe Experience Cloud worden geëxporteerd in een geaggregeerd formulier, zonder individuele of apparaat-id&#39;s op te nemen. Bijvoorbeeld, gegevens die uit sociale netwerken voortkwamen.

#### C2 {#c2}

Sommige gegevensleveranciers hebben bedingen in hun contracten die de uitvoer van gegevens van waar het oorspronkelijk werd verzameld verbieden. Sociale netwerkcontracten beperken bijvoorbeeld vaak de overdracht van gegevens die u van hen ontvangt. Het C2 etiket is restrictiever dan [ C1 ](#c1), dat slechts samenvoeging en anonieme gegevens vereist, maar het is minder restrictief dan [ C12 ](#c12), die gegevensuitvoer volledig ongeacht de bestemming verhindert.

#### C3 {#c3}

Sommige gegevensleveranciers hebben bedingen in hun contracten die het combineren of gebruiken van die gegevens met direct identificeerbare informatie verbieden. In contracten voor gegevens die afkomstig zijn van advertentienetwerken, servers en externe gegevensleveranciers zijn bijvoorbeeld vaak specifieke contractuele verbodsbepalingen opgenomen betreffende het gebruik van dergelijke gegevens met rechtstreeks identificeerbare gegevens.

#### C4 {#c4}

C4 omvat etiketten [ C5 ](#c5), [ C6 ](#c6), en [ C7 ](#c7). Het is één van de meest beperkende etiketten, tweede slechts aan [ C12 ](#c12).

#### C5 {#c5}

Op rente-gebaseerd richten, of verpersoonlijking, komt voor als de volgende drie voorwaarden worden vervuld: De gegevens die ter plaatse worden verzameld worden (1) gebruikt om gevolgtrekkingen over de belangen van gebruikers te maken, (2) wordt gebruikt in een andere context, zoals op een andere plaats of een app (off-site) EN (3) wordt gebruikt om te selecteren welke inhoud of advertenties op die gevolgtrekkingen worden gediend.

De combinatie van gegevens van verschillende sites, waaronder een combinatie van gegevens ter plaatse en gegevens buiten de locatie of een combinatie van gegevens van verschillende bronnen buiten de locatie, wordt ook wel gegevens over andere locaties genoemd. De verschillende plaatsen vertegenwoordigen verschillende contexten zodat het gebruik van dwars-plaatgegevens in om het even welke context verschillend is dan origineel. Gegevens over andere sites worden doorgaans verzameld en verwerkt om conclusies te trekken over de belangen van gebruikers. Hierdoor wordt het gebruik van gegevens die naar andere sites verwijzen voor advertenties of inhoud doorgaans gekwalificeerd als doelgerichte advertenties, ongeacht of de advertentie of inhoud op locatie of elders wordt weergegeven. Als on-site gegevens bijvoorbeeld werden gebruikt in combinatie met externe gegevens om te selecteren welke advertentie om een gebruiker op de eigen site van een organisatie te tonen, zou dat gebruik kwalificeren als op rente-gebaseerd richten. Een ander voorbeeld is dat het opnieuw toewijzen van advertenties aan gebruikers buiten de locatie waarschijnlijk ook als een op rente gebaseerde gerichtheid wordt aangemerkt.

Het gebruik van gegevens buiten de locatie alleen voor doelgerichte doeleinden zou waarschijnlijk ook als op rente gebaseerde doelgerichtheid worden aangemerkt, aangezien gegevens buiten de locatie doorgaans worden verzameld en verwerkt om conclusies te trekken over de belangen van de gebruikers.

Het toewijzen van inhoud of advertenties die alleen gegevens ter plaatse gebruiken, zou echter doorgaans niet worden aangemerkt als doelgerichte actie op basis van interesse. Het on-site richten die anders niet als op rente-gebaseerd richten kwalificeert wordt behandeld als twee verschillende etiketten. Specifiek, richt het Etiket C6 de onsite en richt zich en het melden en spreekt specifiek aan de selectie, levering, en het melden van, en Etiket C7 adressen on-site inhoudselectie, levering, en het melden (de inhoud die van de plaats richt zich).

Uiteindelijk is de interpretatie van het label en hoe gegevens met dat label worden gebruikt aan u. Ter referentie worden de IAB- en DAA-frameworks hieronder gegeven:

IAB: Personalization. Het verzamelen en verwerken van informatie over uw gebruik van deze service om reclame en/of inhoud voor u in andere contexten, zoals op andere websites of apps, in de loop van tijd te personaliseren. Doorgaans wordt de inhoud van de site of app gebruikt om conclusies te trekken over uw belangen die de toekomstige selectie van advertenties en/of inhoud van uw website beïnvloeden.

DAA: online gedragsreclame. Gegevens van een bepaalde computer of een bepaald apparaat verzamelen met betrekking tot webweergavegedrag in de loop van de tijd en op niet-gelieerde websites, met als doel deze gegevens te gebruiken om gebruikersvoorkeuren of -belangen te voorspellen voor het aanbieden van reclame op die computer of dat apparaat op basis van voorkeuren of interesses die uit dergelijk webviewergedrag zijn afgeleid.

#### C6 {#c6}

Advertenties zijn berichten of meldingen, met inbegrip van tekst en afbeeldingen, die op een website of app verschijnen en die voornamelijk bedoeld zijn om de verkoop van goederen of diensten te bevorderen. Het is aan u om het doel van dergelijke berichten of berichten te bepalen. Adds zijn gescheiden van inhoud ter plaatse, die door etiket [ C7 ](#c7) wordt behandeld. Gegevens met een C6-label kunnen niet worden gebruikt voor on-site advertenties, zoals de selectie en levering van advertenties op de websites of apps van uw organisatie, of om de levering en doeltreffendheid van dergelijke advertenties te meten. Dit omvat het gebruik van eerder verzamelde onsite gegevens over de belangen van de gebruikers om advertenties te selecteren, gegevens te verwerken over welke advertenties werden getoond, wanneer en waar deze werden getoond en of de gebruikers actie hebben ondernomen in verband met de advertentie, zoals het selecteren van een advertentie of het kopen van een advertentie. Doorgaans zou het maken van conclusies over de voorkeuren van gebruikers op basis van de onsite activiteiten van die gebruikers en het vervolgens gebruiken van deze voorkeuren in on-site advertenties niet worden aangemerkt als een op rente gebaseerde gerichte actie (ook wel personalisatie genoemd), aangezien deze niet voldoet aan alle drie de vereisten die vereist zijn voor op rente gebaseerde doelwitten. *[zie etiket C5 voor deze vereisten.](#c5)*

Uiteindelijk is de interpretatie van het label en hoe gegevens met dat label worden gebruikt aan u. Ter referentie worden de IAB- en DAA-frameworks hieronder gegeven:

IAB: 3. Selectie, levering, rapportage: De verzameling van informatie, en combinatie met eerder verzamelde informatie, om advertenties voor u te selecteren en te leveren, en om de levering en doeltreffendheid van dergelijke advertenties te meten. Hieronder valt het gebruik van eerder verzamelde informatie over uw belangen bij het selecteren van advertenties, het verwerken van gegevens over de getoonde advertenties, hoe vaak deze werden getoond, wanneer en waar ze werden getoond en of u acties hebt ondernomen in verband met de advertentie, zoals het selecteren van een advertentie of het kopen van een advertentie. Dit geldt niet voor Personalization, dat bestaat uit het verzamelen en verwerken van informatie over uw gebruik van deze service om uw reclame en/of inhoud in andere contexten, zoals websites of apps, in de loop der tijd aan te passen.

DAA: Online gedragsreclame omvat niet de activiteiten van Eerste Partijen, Ad Delivery of Ad Reporting, of contextuele reclame (d.w.z. reclame op basis van de inhoud van de te bezoeken webpagina, het huidige bezoek van een consument aan een webpagina of een zoekopdracht).

#### C7 {#c7}

Onsite inhoud is tekst en afbeeldingen die zijn ontworpen om te informeren, te onderwijzen of te vermaken, en die niet zijn gemaakt om de verkoop van goederen of diensten te bevorderen. Het is aan u om het doel van de inhoud te bepalen, met inbegrip van of de inhoud als inheemse reclame zou kwalificeren. Het C7 etiket is niet bedoeld om onsite advertenties te behandelen, die door etiket [ C6 ](#c6) worden behandeld. Gegevens met een C7-label kunnen niet worden gebruikt voor het aanwijzen van inhoud op locatie, zoals de selectie en levering van inhoud op de websites of apps van uw organisatie, of om de levering en doeltreffendheid van dergelijke inhoud te meten. Dit omvat eerder verzamelde informatie over gebruikersbelangen in geselecteerde inhoud, het verwerken van gegevens over welke inhoud werd getoond, hoe vaak of hoe lang het werd getoond, wanneer en waar het werd getoond, en of de gebruikers om het even welke acties met betrekking tot de inhoud, met inbegrip van bijvoorbeeld, het selecteren van inhoud hebben ondernomen. Doorgaans wordt het maken van conclusies over de voorkeuren van gebruikers op basis van de onsite activiteiten van die gebruikers en het vervolgens gebruiken van deze voorkeuren bij het zoeken naar inhoud op locatie niet beschouwd als een op rente gebaseerde keuze (ook wel personalisatie genoemd), omdat het niet voldoet aan alle drie de vereisten die vereist zijn voor het maken van doelwitbestanden. *[zie etiket C5 voor deze vereisten.](#c5)*

Uiteindelijk is de interpretatie van het label en hoe gegevens met dat label worden gebruikt aan u. Ter referentie worden de IAB- en DAA-frameworks hieronder gegeven:

IAB: 4. Selectie, levering, rapportage van inhoud: de verzameling van informatie, en combinatie met eerder verzamelde informatie, om inhoud voor u te selecteren en te leveren, en om de levering en doeltreffendheid van dergelijke inhoud te meten. Dit omvat het gebruik van eerder verzamelde informatie over uw belangen om inhoud te selecteren, het verwerken van gegevens over welke inhoud werd getoond, hoe vaak of hoe lang het werd getoond, wanneer en waar het werd getoond, en of u om het even welke actie met betrekking tot de inhoud, met inbegrip van bijvoorbeeld het selecteren van inhoud nam. Dit geldt niet voor Personalization. Dit is het verzamelen en verwerken van informatie over uw gebruik van deze service om inhoud en/of reclame later in de loop van de tijd voor u te personaliseren in andere contexten, zoals websites of apps.

DAA: Online gedragsreclame omvat niet de activiteiten van Eerste Partijen, Ad Delivery of Ad Reporting, of contextuele reclame (d.w.z. reclame op basis van de inhoud van de webpagina die wordt bezocht, het huidige bezoek van een consument aan een Web-pagina of een zoekopdracht).

#### C8 {#c8}

Gegevens kunnen niet worden gebruikt voor het meten, begrijpen en rapporteren van het gebruik van de sites of apps van uw organisatie door gebruikers. Dit omvat niet op rente-gebaseerde richten (het dwars-plaats richten), die de inzameling van informatie over uw gebruik van deze dienst is om inhoud en/of reclame voor u in andere contexten, d.w.z. op andere diensten, zoals websites of apps, in tijd te personaliseren.

#### C9 {#c9}

Sommige contracten bevatten expliciete verbodsbepalingen voor het gebruik van gegevens voor gegevenswetenschap. Soms worden deze termen gedefinieerd in termen die het gebruik van gegevens voor kunstmatige intelligentie (AI), machinaal leren (ML) of modellering verbieden.

#### C10 {#c10}

Sommige beleidsregels voor gegevensbeheer beperken het gebruik van verankerde identiteitsgegevens voor personalisatie. Het label C10 wordt automatisch toegepast op het publiek als in het samenvoegbeleid de optie &#39;particuliere grafiek&#39; wordt gebruikt.

#### C11 {#c11}

Met Adobe Experience Platform Segment Match kunt u door Experience Platform gegenereerde soorten publiek afstemmen op privacy- en toestemmingsvoorkeuren, zodat beter geprofileerde profielen en downstreaminzichten mogelijk zijn. Het label C11 geeft gegevens aan die niet mogen worden gebruikt in [!DNL Segment Match] -processen. Nadat u hebt bepaald welke datasets en/of gebieden u van de Gelijke van het Segment wilt uitsluiten en dienovereenkomstig het etiket C11 toevoegt, wordt het etiket automatisch afgedwongen door het werkschema van de Gelijke van het Segment.

#### 12 {#c12}

Gegevens met dit label kunnen op geen enkele manier uit Experience Platform worden geëxporteerd. Velden met het label C12 zijn uitgesloten van CSV-downloads, API-verbruik en activeringsworkflows.
