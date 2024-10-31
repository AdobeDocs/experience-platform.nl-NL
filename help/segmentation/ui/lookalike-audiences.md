---
solution: Experience Platform
title: Soortgelijke soorten publiek
description: Leer hoe je nieuwe waardevolle doelgroepen target in Adobe Experience Platform met behulp van lookalike-doelgroepen.
exl-id: c43dac6c-18a0-482f-803e-b75e1b211e98
source-git-commit: c2f9bcd9aeb0073b8b26413ec29e2dff1ee5c80d
workflow-type: tm+mt
source-wordcount: '2157'
ht-degree: 0%

---

# Gids voor lookalike-doelgroepen

>[!IMPORTANT]
>
>De blik-gelijke inzichten en de blik-alike doelgroepen zijn slechts beschikbaar in de **B2C uitgave**.

In Adobe Experience Platform bieden lookalike-doelgroepen intelligente inzichten in elk van je doelgroepen, waarbij ze gebruikmaken van op machine learning gebaseerde inzichten om waardevolle klanten te identificeren en targeten met je marketingcampagnes.

Met lookalike-doelgroepen kun je uitgebreide doelgroepen maken die klanten targeten, vergelijkbaar met je goed presterende doelgroepen of doelklanten, zoals eerder omgezette doelgroepen.

## Terminologie {#terminology}

Voordat u aan de slag gaat met lookalike-doelgroepen, moet u de volgende concepten begrijpen:

- **het publiek van de Basis**: Het basispubliek is het publiek dat u meer inzichten over wilt weten komen. Dit is het publiek dat het lookalike model **gebaseerd** is.
- **blik-gelijkaardig model**: Een blik-gelijkaardig model is een machine het leren model dat op elk in aanmerking komend basispubliek zonder enige klanteninput wordt getraind. Elk model ziet er hetzelfde uit en creëert de invloedrijke factoren en grafieken van de gelijkenis. Een blik-gelijkaardig model wordt **niet** gescoord.
- **kijkt-als publiek**: Een blik-gelijkaardig publiek is het publiek dat wordt gecreeerd wanneer een blik-gelijkaardig model met een geselecteerde gelijkenisdrempel op het basispubliek wordt toegepast. U kunt veelvoudige blik-alike publiek tot stand brengen gebruikend het zelfde blik-als model. Het publiek ziet er hetzelfde uit: wat wordt er gescoord.
- **Totale adresseerbare publieksgrootte**: De totale adresseerbare publieksgrootte is het totale aantal profielen in de afgelopen 30 dagen minus de populatie van het basispubliek in de afgelopen 30 dagen. Bijvoorbeeld, als een klant 10 miljoen profielen in de afgelopen 30 dagen heeft, en het basispubliek 1 miljoen profielen in de afgelopen 30 dagen heeft, is de totale adresseerbare publieksgrootte 9 miljoen profielen.

## Geschiktheid {#eligibility}

Om blik-gelijke inzichten te gebruiken, moet het basispubliek **** aan de volgende toelatingscriteria voldoen:

- Het basispubliek **moet** binnen Platform worden gecreeerd.
   - Extern-geproduceerd publiek is **niet** geschikt voor blik-gelijke inzichten.
- Het basispubliek **moet** op het standaard fusiebeleid zijn.
- Het basispubliek **moet** geen gebieden gebruiken die door gegevensbeheer worden beperkt.

## Detail van model {#details}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_notEligible"
>title="Niet in aanmerking komend"
>abstract="Dit publiek komt momenteel niet in aanmerking voor dubbelzinnige inzichten, omdat het mogelijk minder profielen heeft dan het minimumaantal profielen dat vereist is voor training of omdat de profielexport nog niet is geactiveerd."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_processing"
>title="Verwerking"
>abstract="Dit publiek wordt momenteel verwerkt. Het kan tot 24 uur duren voordat de verwerking is voltooid. Probeer het later opnieuw."

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_error"
>title="Fout"
>abstract="Er is een fout opgetreden tijdens het verwerken van dit model. Verwijder dit model en maak het opnieuw op of probeer het later opnieuw."

In Adobe Experience Platform gebruikt het lookalike-model drie verschillende typen gegevenspunten:

- Doelgroeplidmaatschap in de afgelopen 30 dagen
- Ervaringsgebeurtenissen van de afgelopen 30 dagen die zijn opgenomen in het Real-Time Customer Profile
- Profielkenmerken die in de afgelopen 30 dagen zijn opgenomen in het realtime profiel van de klant

Al deze gegevenspunten worden omgezet in zeer belangrijke waardeparen die in het blik-gelijkaardige model worden gevoerd. Alleen de sleutelwaardeparen met een significant percentage overeenkomende profielen blijven behouden.

Op dit moment wordt het lookalike-model elke 24 uur uitgevoerd en worden de invloedrijke factoren en gelijksoortige grafieken voor het basispubliek gemaakt en opnieuw gemaakt. Je scores voor het ‘Look-alike’-publiek worden ook regelmatig uitgevoerd.

## Rechten {#entitlements}

De volgende rechten gelden voor het gebruik van look-alike-soorten:

- De eerste klanten van Real-Time CDP hebben recht op **5** actieve blik-alike publiek in productiesanddozen
- Real-Time CDP Ultimate-klanten hebben recht op **20** actieve look-alike-soorten publiek in productiesandboxen
- De zandbakken van de ontwikkeling zijn beperkt tot **5** blik-gelijke publiek voor alle klanten van Real-Time CDP

Pakketten met invoegtoepassingen, die later beschikbaar zullen zijn, verhogen de rechten voor de productie van sandboxen met 20 soorten publiek per verpakking.

Neem contact op met uw Adobe als u wilt controleren of u toegang hebt tot vergelijkbare soorten publiek.

## Bekijk dubbelzinnige inzichten {#view}

Lookalike-inzichten zijn ingebouwd met de pagina met doelgroepdetails. Als u de lookalike-inzichten voor een publiek wilt bekijken, selecteert u **[!UICONTROL Audiences]** in de linkernavigatiebalk, gevolgd door **[!UICONTROL Browse]** , en het publiek voor wie u de inzichten wilt weergeven.

![ de knoop van het publiek wordt benadrukt, evenals het basispubliek dat voor blik-alike modellering wordt gebruikt.](../images/ui/lookalike-audiences/browse.png)

De pagina met de doelgroepdetails wordt weergegeven. Selecteer het tabblad **[!UICONTROL Look-alike insights]** om de kijkgelijke inzichten van het publiek weer te geven. De pagina **[!UICONTROL Look-alike insights]** wordt weergegeven. Deze pagina heeft drie hoofdelementen: de gelijkenis en bereikgrafiek, de lookalike-doelgroepen en de invloedrijke factoren.

![ het blik-gelijke inzichten lusje wordt benadrukt, tonend de blik-gelijke inzichten voor het basispubliek.](../images/ui/lookalike-audiences/look-alike-insights.png)

### Gelijksoortigheid en bereik {#similarity-and-reach}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_similarityAndReach"
>title="Gelijksoortigheid en bereik"
>abstract="Met de gelijkenis en het bereik van de grafiek wordt het verwachte bereik van een publiek dat er uitziet boven een bepaalde score voor gelijkenis weergegeven. U kunt de muisaanwijzer boven een specifiek punt in de grafiek plaatsen om het percentage voor gelijkenis en het verwachte aantal profielen voor het momenteel gemarkeerde punt weer te geven."

De gelijkenis en bereiksectie toont een grafiek die het verwachte bereik van een publiek dat van look-alike bestaat uit profielen boven een bepaalde gelijkenisscore in kaart brengt. De gelijkenisscore vertegenwoordigt de **afstand** van gelijkenis tussen het profiel van het basispubliek en het blik-gelijke profiel van het inzicht.

![ de gelijkenis en bereikgrafiek wordt benadrukt.](../images/ui/lookalike-audiences/similarity-and-reach.png)

In deze grafiek wordt op de x-as het percentage gemeten waarmee een profiel en leden van het geselecteerde publiek op elkaar lijken. De score op basis van de overeenkomst varieert van 0% tot 100%, waarbij een hogere score op basis van gelijkenis aangeeft dat een profiel in termen van invloedrijke factorwaarden dichter bij de leden van het geselecteerde publiek ligt.

Op de y-as wordt het verwachte aantal profielen weergegeven met het percentage voor gelijkenis dat overeenkomt met de overeenkomende waarde van de x-as. Deze verwachte telling van profielen varieert van 0 tot de totale adresseerbare publieksgrootte of 25 miljoen profielen, welke lager is. Deze as wordt gemeten op a **logaritmische schaal** om de leesbaarheid van de grafiek te verbeteren.

Gelieve te merken op dat de grafiek **cumulatief** van rechts naar links is. Dit betekent dat op om het even welk punt in de grafiek, de waarde van de y-as het aantal profielen is die een gelijkenis **boven** de gelijkenisdrempel hebben. Als de x-as bijvoorbeeld op 60% staat en de y-as op 10 miljoen, betekent dit dat er 10 miljoen profielen zijn met een gelijkenis van 60% of meer ten opzichte van het basispubliek.

U kunt de aanwijzer boven een specifiek punt in de grafiek plaatsen om het percentage voor gelijkenis en het verwachte aantal profielen voor het momenteel gemarkeerde punt weer te geven.

### Lookalike doelgroepen {#list}

De blik-gelijke sectie van publiek toont een lijst van alle blik-gelijke publiek dat eerder voor het geselecteerde basispubliek is gecreeerd.

![ de blik-alike sectie van publiek wordt benadrukt.](../images/ui/lookalike-audiences/select-laa.png)

### Influïeve factoren {#influential-factors}

>[!CONTEXTUALHELP]
>id="platform_audiences_lookAlike_influentialFactors"
>title="Influïeve factoren"
>abstract="Influentiële factoren zijn kenmerken, gebeurtenissen en doelgroeplidmaatschappen die belangrijk zijn om de gelijkenis van een profiel met leden van het basispubliek uit te leggen. Met labels en beleidsregels voor datagebruik kunt u bepaalde gegevens uitsluiten van factoren die van invloed zijn op lookalike-modellen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/segmentation/ui/lookalike-audiences.html#exclude" text="Gegevens uitsluiten"

In de sectie met invloedrijke factoren worden de 100 belangrijkste factoren weergegeven die van invloed zijn op het model dat er op lijkt voor het geselecteerde basispubliek. Deze invloedrijke factoren zijn de profielattributen, de ervaringsgebeurtenissen, en de publiekslidmaatschappen die het belangrijkst in het verklaren van gelijkenissen in het basispubliek zijn. Met een goed begrip van de belangrijkste invloedrijke factoren kunt u uw marketinginhoud beter aanpassen aan dit publiek en aan elk publiek dat u eruit maakt. Niet alle invloedrijke factoren die van invloed zijn op het model dat er op lijkt, worden weergegeven.

Voor invloedrijke factoren die numeriek zijn, kunnen de sleutelwaardeparen in emmers worden gezet, afhankelijk van het aantal verschillende waarden die de sleutel heeft. Als u bijvoorbeeld een sleutel van `income` hebt, zijn er waarschijnlijk veel unieke waarden. Dit betekent dat de sleutelwaardeparen in emmers worden geplaatst die er als `income=[0 -> 30000]`, `income=[30000 -> 50000]` en `income=[50000 -> 100000]` kunnen uitzien.

Deze emmers worden regelmatig opnieuw berekend om ervoor te zorgen dat de gegevens worden bijgewerkt.

![ wordt de invloedrijke factorsectie benadrukt.](../images/ui/lookalike-audiences/influential-factors.png)

>[!NOTE]
>
>De invloedrijke factoren worden gesorteerd in volgorde van belangrijkheid en zijn onafhankelijk van elkaar.

| Veld | Beschrijving |
| ----- | ----------- |
| Type | Het type gegevens waaruit de invloedrijke factor wordt afgeleid. Dit kan een profielkenmerk, een ervaringsgebeurtenis of een doelgroeplidmaatschap zijn. |
| Sleutel | De naam van het gegevensveld. Voor sleutels van het type van publiekslidmaatschap, vertegenwoordigt deze waarde **namespace** van het publiek waar de gegevens uit komen. Mogelijke waarden zijn `ups` (Segmentation Service) en `AO` (Audience Orchestration). Voor sleutels van andere types, vertegenwoordigt deze waarde het XDM gebiedspad. Als het bedrijf Luma bijvoorbeeld een aangepast veld met de naam &#39;inkomen&#39; heeft, is de sleutel `_luma.income` |
| Waarde | De waarde varieert afhankelijk van de invloedrijke factor die deze vertegenwoordigt. Voor profielkenmerken of ervaringsgebeurtenissen geeft dit veld de waarde of het waardebereik van het gegevensveld aan dat de gelijkenis met de leden van het basispubliek aangeeft. Het waardebereik wordt geschreven in de vorm `[A -> B]` , waarbij `A` het laagste bereik vertegenwoordigt terwijl `B` het hogere bereik vertegenwoordigt. Voor doelgroeplidmaatschappen is dit veld de naam van de doelgroep. |
| Belang | Het relatieve belang van de invloedrijke factor. Dit kan hoog, gemiddeld of laag zijn. |

## Een publiek met een look-alike maken {#create}

>[!IMPORTANT]
>
>U **kunt niet** een publiek van het blik-gelijkaardig als basispubliek voor een ander publiek van het blik-gelijkaardig gebruiken. Dat wil zeggen, kunt u **niet** geketende publiek-alike tot stand brengen.

Als je een vergelijkbare doelgroep wilt maken, moet je het publiek selecteren waarvan je de lookalike-doelgroep wilt baseren. Selecteer **[!UICONTROL Audiences]** in de linkernavigatiebalk, gevolgd door **[!UICONTROL Browse]** om uw lijst met beschikbare doelgroepen te openen. De lijst met doelgroepen wordt weergegeven. Op deze pagina kunt u het publiek selecteren dat u als uw basisdoelgroep wilt gebruiken.

![ de knoop van het publiek wordt benadrukt, evenals het basispubliek dat voor blik-gelijke modellering wordt gebruikt.](../images/ui/lookalike-audiences/browse.png)

Selecteer **[!UICONTROL Create look-alike audience]** op de pagina met de doelgroepdetails om te beginnen met het maken van een vergelijkbare doelgroep.

![ de [!UICONTROL Create look-alike audience] knoop wordt benadrukt.](../images/ui/lookalike-audiences/create-look-alike-audience.png)

De pop-up **[!UICONTROL Create a look-alike audience]** wordt weergegeven. Op deze pagina kunt u het percentage voor gelijkenis instellen voor het publiek dat er hetzelfde uitziet.

![ popover [!UICONTROL Create a look-alike audience] wordt getoond.](../images/ui/lookalike-audiences/create-audience.png)

U kunt dit percentage voor gelijkenis op drie verschillende manieren instellen:

- Verplaats de schuifregelaar om het percentage voor de gelijkenis in te stellen
- Voer het percentage voor de gelijkenis in het numerieke invoervak naast de schuifregelaar in
- Plaats de muisaanwijzer op de grafiek en selecteer de gewenste locatie om het percentage voor de gelijkenis in te stellen

U kunt ook de details over de lookalike-doelgroep bijwerken, inclusief de naam en beschrijving. Standaard wordt de naam van de lookalike-doelgroep gegenereerd op basis van de naam van de basisdoelgroep en het eerder opgegeven percentage voor gelijkenis.

![ de basisinformatie wordt benadrukt binnen [!UICONTROL Create a look-alike audience] popover.](../images/ui/lookalike-audiences/basic-info.png)

Selecteer **[!UICONTROL Create]** om het maken van een soort publiek te voltooien.

![ creeer knoop wordt benadrukt binnen [!UICONTROL Create a look-alike audience] popover.](../images/ui/lookalike-audiences/create-audience.png)

Het nieuwe publiek van de blik-alike publiek kan in de **[!UICONTROL Look-alike audiences]** sectie van de pagina van de publieksdetails worden betreden, en is ook beschikbaar in het Portaal van de Publiek en voor andere stroomafwaartse gebruik. Houd er rekening mee dat het enige tijd duurt voordat het publiek voor het look-alike wordt gescoord. Totdat een score wordt toegekend, wordt het aantal profielen weergegeven op 0.

## Weergave-gelijke publieksdetails weergeven {#view-details}

Als u de details van een publiek met een look-alike wilt weergeven, selecteert u het publiek voor de look-alike in het gedeelte **[!UICONTROL Look-alike audiences]** van het basispubliek.

![ de blik-alike sectie van het publiek wordt benadrukt.](../images/ui/lookalike-audiences/select-laa.png)

De pagina met publieksdetails wordt weergegeven. Voor meer informatie over deze pagina, te lezen gelieve de [ sectie van publieksdetails van het Poortoverzicht van het Poort van het Publiek ](./audience-portal.md#audience-details).

![ de Details van het publiek worden blik-alike getoond.](../images/ui/lookalike-audiences/laa-details.png)

## Gegevensvelden uitsluiten van lookalike-modellering {#exclude}

>[!IMPORTANT]
>
> **u** bent verantwoordelijk voor het ervoor zorgen dat de gegevens, met inbegrip van gevoelige gegevens, correct geëtiketteerd zijn en dat het beleid van het gegevensgebruik is bepaald en toegelaten om aan de wettelijke en regelgevende verplichtingen te voldoen waaronder u werkt. U zou ook moeten zijn zich ervan bewust dat de gegevensgebieden of segmentlidmaatschappen die **niet** direct met gegevensgebieden verbonden typisch verbonden aan gevoelige of beschermde gegevenstypes een bron van potentiële vooroordelen kunnen zijn. **u** bent verantwoordelijk in het analyseren van uw gegevens om, het aangewezen beleid van het gegevensgebruik op uw gegevens te identificeren, te etiketteren en toe te passen, met inbegrip van om het even welke gegevensgebieden die volmacht voor gevoelige of beschermde gegevenstypes kunnen en van modellering zouden moeten worden uitgesloten.

U kunt lookalike-doelgroepen configureren om gegevensvelden uit te sluiten die zijn beperkt voor de marketingactie &quot;Data Science&quot; door de relevante labels en beleidsregels voor datagebruik toe te passen. Data die zijn gelabeld als beperkt in het gebruik voor datawetenschap, worden uit overweging genomen bij het trainen van een lookalike-doelgroepmodel en bij het genereren van een lookalike-doelgroep uit het getrainde model. 

>[!NOTE]
>
>Het kan tot 48 uur duren voordat wijzigingen in de labels voor gegevensgebruik op het basispubliek van kracht worden.

Het standaard &quot;C9&quot;etiket kan worden gebruikt om gegevens te etiketteren die niet voor gegevenswetenschap zouden moeten worden gebruikt en kunnen worden afgedwongen door het standaardbeleid van de &quot;Beperk datawetenschap&quot;toe te laten. Je kunt ook aanvullende richtlijnen opstellen om data met andere labels, waaronder gevoelige labels, te beperken in het gebruik voor datawetenschap. Voor meer informatie over het beheren van het beleid van het gegevensgebruik, te lezen gelieve de [ gids UI van het het gebruiksbeleid van gegevens ](../../data-governance/policies/user-guide.md). Voor meer informatie over het beheren van de etiketten van het gegevensgebruik, te lezen gelieve de [ gids UI van de etiketten van het gegevensgebruik ](../../data-governance/labels/user-guide.md).

Door gebrek, als een basispubliek geen contractetiketten heeft, zal het modelleringsproces voor blik-alike doelgroepen **om het even welk** gebied, dataset, of publiek uitsluiten dat op het toegelaten privacybeleid voor uw organisatie wordt gebaseerd.

## Volgende stappen

Na het lezen van deze handleiding hebt u geleerd hoe u lookalike-inzichten kunt bekijken en lookalike-doelgroepen kunt maken op basis van deze inzichten. Voor meer informatie over doelgroepen in Adobe Experience Platform UI, te lezen gelieve de [ gids UI van de Dienst van de Segmentatie ](./overview.md).
